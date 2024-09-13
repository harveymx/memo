## 2024-09-13 将langchain和tools调用结合来，并实现tagging（标签）和Extract(信息提取)
主要知识点:
* 利用JS的zod机制，实现tools的(约束)知识机制.可以添加多个function,并管控调用
const getCurrentWeatherSchema = z.object({
    location: z.string().describe("the city and state e.g. San Francisco, CA"),
    unit: z.enum(["celsius", "fahrenheit"]).describe("the unit of temperature"),
})
......
const modelWithTools = model.bind({
    tools:[
        {
            type:"function",
            function:{
                name:"getCurrentWeather",
                description: "Get the current weather in a given location",
                parameters: zodToJsonSchema(getCurrentWeatherSchema),
            }
        }
    ]
});

* 利用上述机制实现tagging
const taggingSchema = z.object({
    emotion:z.enum(["pos","neg","neutral"]).describe("文本的情感"),
    language:z.string().describe("文本的核心语言(应为ISO 639-1代码)"),
});
......
const modelTagging = model.bind({
    tools: [
        {
            type: "function",
            function: {
                name: "tagging",
                description: "为特定的文本片段打上标签",
                parameters: zodToJsonSchema(taggingSchema)
            }
        }
    ],
    tool_choice: {
        type: "function",
        function: {
            name: "tagging"
        }
    }
});
const prompt = ChatPromptTemplate.fromMessages([
    ["system","仔细思考，你有充足的时间进行严谨的思考，然后按照指示对文本进行标记"],
    ["human","{input}"],
]);

const chain = prompt.pipe(modelTagging).pipe(new JsonOutputToolsParser());
await chain.invoke({input:"我非常喜欢 AI，特别是 LLM，因为它非常 powerful"}); 

* 利用上述机制实现Extract

const personExtractionSchema = z.object({
    name:z.string().describe("人的名字"),
    age: z.number().optional().describe("人的年龄"),
}).describe("提取关于一个人的信息");

const relationExtractionSchema = z.object({
    people: z.array(personExtractionSchema).describe("提取所有人"),
    relation: z.string().describe("人之间的关系，尽量简洁"),
});

const schema = zodToJsonSchema(relationExtractionSchema);
...........
const modelExtract = model.bind({
  tools: [
    {
      type: "function",
      function: {
        name: "relationExtract",
        description: "提取数据中人的信息和人的关系",
        parameters: zodToJsonSchema(relationExtractionSchema),
      },
    },
  ],
  tool_choice: { type: "function", function: { name: "relationExtract" } },
});

const prompt = ChatPromptTemplate.fromMessages([
  ["system","仔细思考，你有充足的时间进行严谨的思考，然后提取文中的相关信息，如果没有明确提供，请不要猜测，可以仅提取部分信息。"],
  ["human", "{input}"],
]);
const chain = prompt.pipe(modelExtract).pipe(new JsonOutputToolsParser());
await chain.invoke({input: "我是小明，现在18岁了，我和小A、小B是好朋友，都一样大"})
