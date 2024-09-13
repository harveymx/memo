## 2024-09-13 通过proxy，langchain和openai gpt的调用
主要知识点：
* baseURL的设置藏的比较深，通过阅读官方文档解决问题
https://v02.api.js.langchain.com/classes/_langchain_openai.ChatOpenAI.html

import { ChatOpenAI } from "@langchain/openai";

const model = new ChatOpenAI({
    configuration: {baseURL:env.OPENAI_API_BASE},
    apiKey: env.Open_API_KEY,
    model:"gpt-4o-mini",
    verbose:true
}); 