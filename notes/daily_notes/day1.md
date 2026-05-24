## 任务

- 看 HelloAgents LLM 调用方式
- 总结输入/输出/错误处理
- 用 vibe coding 写简化版 invoke()

## 总结

关于LLM的封装，关键在于LLM的配置，以及LLM如何输出回答（流式响应think和非流式响应invoke）。

invoke() 和 think() 的区别：

- think()：流式调用，stream=True，模型边生成边输出，适合观察 LLM “实时回答”的过程。
- invoke()：非流式调用，一次性等模型完整返回后，再取 response.choices[0].message.content，适合普通工具调用、Agent loop 里拿完整结果。

利用try…except进行错误处理，告知用户调用出错。

- 输入：messages 是消息列表，每条消息是包含 role 和 content 的字典，其中 content 是字符串；
- 输出：成功时返回模型响应内容string；
- 错误：异常时返回 None ，并打印异常说明；

## 机制卡片

### LLM_Client

解决问题：
Agent 需要一个大脑即“LLM”，其封装应该要考虑到LLM的配置和兼容问题，以及LLM的正确调用和回答返回。

核心结构：
__init__ + think + invoke

项目用法：
在 Mini Codebase Maintainer Agent 中，用它封装一个LLM客户端。

注意点：
think和invoke的选择