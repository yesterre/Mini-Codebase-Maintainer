### LLM_Client

解决问题：
Agent 需要一个大脑即“LLM”，其封装应该要考虑到LLM的配置和兼容问题，以及LLM的正确调用和回答返回。

核心结构：
__init__ + think + invoke

项目用法：
在 Mini Codebase Maintainer Agent 中，用它封装一个LLM客户端。

注意点：
think和invoke的选择