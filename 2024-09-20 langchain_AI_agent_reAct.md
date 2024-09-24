## 2024-09-20 AI agent with langchain reAct
使用langchain的reAct模式来实现agent
* ReAct框架
ReAct 框架是非常流行的 agent 框架，其结合了推理（reasoning）和行动（acting），其流程大概是让 llm 推理完成任务需要的步骤，然后根据环境和提供的工具进行调用，观察工具的结果，推理下一步任务。 就这样 推理-调用-观察 交错调用，直到模型认为完成推理，输出结果。

ReAct 的意义是在于，这个框架将 llm 的推理能力、调用工具能力、观察能力结合在一起，让 llm 能适应更多的任务和动态的环境，并且强化了推理和行动的协同作用。因为 agents 在执行过程中，会把思考和推理过程记录下来，所以具有很好的透明度和可解释性，提高了用户对输出结果的可信度。
code：
    //使用 SERP API 密钥和环境变量创建 SerpAPI 实例
    const tools = [new SerpAPI(process.env.SERP_KEY), new Calculator()];

    //从langchain hub拉取reAc(Reasoning + Acting)的prompt
    const prompt = await pull<PromptTemplate>("hwchase17/react");

    //创建模型实例，由于creatReactAgent报type错误，这里使用了类型as
    const llm = new ChatOpenAI({
        configuration: {baseURL: process.env.OPENAI_API_BASE},
        model: process.env.OPENAI_API_MODEL,
        temperature: 0
    }) as BaseLanguageModelInterface;

    //创建React模式的agent
    const agent = await createReactAgent({
        llm,
        tools,
        prompt,
      });

    //创建agent执行器
    const agentExecutor = new AgentExecutor({
        agent,
        tools
    });

    const result = await agentExecutor.invoke({
        input:"我有17美元，现在相当于多少人民币？",
    });
    console.log(result);
prompt(最后的step):

    HUMAN:
        Answer the following questions as best you can. You have access to the following tools:

        search: a search engine. useful for when you need to answer questions about current events. input should be a search query.
        calculator: Useful for getting the result of a math expression. The input to this tool should be a valid mathematical expression that could be executed by a simple calculator.

        Use the following format:

        Question: the input question you must answer
        Thought: you should always think about what to do
        Action: the action to take, should be one of [search, calculator]
        Action Input: the input to the action
        Observation: the result of the action
        ... (this Thought/Action/Action Input/Observation can repeat N times)
        Thought: I now know the final answer
        Final Answer: the final answer to the original input question

        Begin!

        Question: 我有17美元，现在相当于多少人民币？
        Thought:I need to find the current exchange rate between USD and RMB.
        Action: search
        Action Input: USD to RMB exchange rate

        Observation: 7.05 Chinese Yuan
        Thought: Now I can calculate how much 17 USD is in RMB.
        Action: calculator
        Action Input: 17 * 7.05

        Observation: 119.85
        Thought: 

    AI：
        I now know the final answer
        Final Answer: 17 USD is equivalent to 119.85 RMB.
* LLM跟踪调试工具：langsmith
    安装：yarn add langsmith
    环境变量：(env) :
      LANGCHAIN_TRACING_V2=true
      LANGCHAIN_API_KEY=XXXX
    运行跟踪分析工具：https://smith.langchain.com/ （免费版 5000 monthly traces）
