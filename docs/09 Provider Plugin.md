# Provider Plugin

> 状态：Draft

## 目标

Provider 是后台能力，不是用户工作流。用户在统一工作台中操作项目；系统根据镜头类型、质量、成本、并发限制和失败情况，通过 Adapter 调用 Provider。

## 路由参考

| 任务 | 候选能力 |
| --- | --- |
| 角色设计 | GPT Image、Flux、Nano Banana |
| 普通分镜生图 | Flux、即梦、可灵图片 |
| 对白视频 | Seedance、可灵 |
| 动作视频 | 可灵、海螺 |
| 低成本过渡镜头 | 本地模型 |
| 配音 | 火山语音、MiniMax Speech、ElevenLabs |
| 音乐音效 | 本地素材库或外部 API |

上述候选能力不是固定选型，须根据实际 API、授权、价格与质量验证。

## 接口边界

- LLM Provider 可优先支持 OpenAI-compatible API：URL、API Key、模型名、上下文长度和并发限制。
- Image、Video、Voice Provider 必须通过各自 Adapter 接入，不能假设它们拥有一致的 API 或任务参数。
- Adapter 负责转换参考图、首尾帧、角色一致性、任务轮询、成本信息和 Provider 特有错误。
- Provider 配置应记录价格、并发限制、能力标签和可用状态，供 Router 与预算器使用。

## MVP

支持一个 OpenAI-compatible LLM、两个图像 Provider、两个视频 Provider 和一个语音 Provider。替换 Provider 不得改变小说解析、导演流程或用户数据。
