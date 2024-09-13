## 2024-09-12 RAG模块终章-支持LLM改写prompt和本地数据库的chat history功能。
* 主要实现的函数，创建一个能够根据用户问题检索相关文本片段，并使用这些信息生成回答的对话系统，同时能够记录和管理聊天历史：
    export async function getRagChain(): Promise<Runnable> {
        const vectorStore = await loadVectorStore();
        const retriever = vectorStore.asRetriever(2);

        const convertDocToString = (documents: Document[]):string => {
            return documents.map((document) => document.pageContent).join("\n");
        }
        
        const contextRetrieverChain = RunnableSequence.from([
            (input) => input.standalone_question,
            retriever,
            convertDocToString,
        ]);

        const SYSTEM_TEMPLATE = '\
            你是一个熟读刘慈欣的《球状闪电》的终极原著党，精通根据作品原文详细解释和回答问题，但你在回答时会引用作品原文。\
            并且回答时仅根据原文，尽可能回答用户问题，如果原文中没有回答用户问题的答案，则回答"原文中没有相关内容"。\
            \
            以下是原文中跟用户回答相关的内容：\
            {context}\
            \
            以下是用户的问题：\
            {question}\
        ';
        const prompt = ChatPromptTemplate.fromMessages([
            ["system", SYSTEM_TEMPLATE],
            new MessagesPlaceholder("history"),
            ["human", "现在，你需要基于原文，回答以下问题：\n {standalone_question}"],
        ]);

        const model = new ChatAlibabaTongyi({ model:"qwen-max",verbose: true});
        const rephraseChain = await getRephraseChain();

        const ragChain = RunnableSequence.from([
            RunnablePassthrough.assign({
                standalone_question:rephraseChain,
            }),
            RunnablePassthrough.assign({
                context: contextRetrieverChain,
            }),
            prompt,
            model,
            new StringOutputParser(),
        ]);

        const chatHistoryDir = path.join(__dirname, "../../chat_data");

        const ragChainWithHistory = new RunnableWithMessageHistory({
            runnable: ragChain,
            getMessageHistory: (sessionId) => new JSONChatHistory({sessionId,dir: chatHistoryDir}) as BaseListChatMessageHistory,
            historyMessagesKey: "history",
            inputMessagesKey: "question",
        });    

        return ragChainWithHistory;
    }

    * 将上述的RAG函数可以开放形成WebAPI，供Web端调用使用，web sever端代码如下：
    import express from "express";
    import { getRagChain } from ".";

    const app = express();
    const port = 8080;

    app.use(express.json());

    app.post("/", async (req, res) => {
    const ragChain = await getRagChain();
    const body = req.body;

    const result = await ragChain.stream(
        { 
        question: body.question,
        },
        {
            configurable:{sessionId: body.sessionId}
        },
    );
    
    res.set("Content-type","text/plain");
    for await (const chunk of result) {
        res.write(chunk);
    }
    res.end();
    });

    app.listen(port, () => {
    console.log(`Server is running on port ${port}`);
    });