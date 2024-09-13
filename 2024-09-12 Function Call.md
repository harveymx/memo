## 2024-09-12 LLM调用外界函数的能力 Function Call, 这是开展Agent探索的基础
主要知识点:
* 控制LLM调用外部函数的通过Tool工具来实现
function getCurrentWeather({location, unit = "fahrenheit"}) {
    const weather_info = {
        "location": location,
        "temperature": "72",
        "unit": unit,
        "forecast": ["sunny", "windy"],
    }
    return JSON.stringify(weather_info);
}
..........
//openai的Tool机制，用来描述外部调用函数，按照openAI官方指定的格式，定义了一个工具类, 用来描述上面的外部调用函数
const tools = [
    {
        type:"function",
        function:{
            name:"getCurrentWeather",
            description:"get the curent weather in a given location and unit",
            parameters:{
                type:"object",
                properties:{
                    location:{
                        type:"string",
                        description:"the city and state, e.g. San Francisco, CA"
                    },
                    unit:{
                        type:"string",
                        enum:["celsius","fahrenheit"]
                    },
                    description: "The unit of temperature, either celsius or fahrenheit"
                },
                required:["location","unit"],
            },
        },
    },
]
......
const messages = [
    {
        "role": "user",
        "content": "What's the weather like in Redmond?"
    }
];
.....
const result = await openai.chat.completions.create({
    messages,
    tools
});
* 链的思路
可以将messages和tools作为链，不断"迭代"进一步提升回答质量
。。。。。
const messages = [{role: "user",content: "北京市的天气怎么样?"}];

const result = await openai.chat.completions.create({
    messages,
    tools,
    tool_choice: "auto",
});
......

messages.push(result.choices[0].message);

const functions = {"getCurrentWeather": getCurrentWeather};

const cell = result.choices[0].message.tool_calls[0];
const functionInfo = cell.function;
const functionName = functionInfo.name;
const functionParams = functionInfo.arguments;
const functionResult = functions[functionName](functionParams);

messages.push({
    tool_call_id: cell.id,
    role: "tool",
    name: functionName,
    content: functionResult,
});


const response = await openai.chat.completions.create({
    messages
});

