# Data Model

> 状态：Draft
> 范围：核心对象目录。字段、关系基数、索引与持久化技术待后续 Schema 设计确认。

## 设计目标

数据模型必须表达从小说到成片的结构、角色和世界的动态状态、资产版本、生成任务与质量反馈。它不能只保存 Prompt 或最终文件路径。

## 核心对象

### 叙事结构

- `Novel`
- `Season`
- `Episode`
- `Scene`
- `Shot`

### 角色与表演

- `Character`
- `CharacterVersion`
- `Costume`
- `Expression`
- `Voice`

### 世界与剧情

- `Location`
- `Prop`
- `StoryEvent`
- `ContinuityState`

### 生产资产与反馈

- `ImageAsset`
- `VideoAsset`
- `AudioAsset`
- `QualityReport`
- `GenerationJob`

## 关键对象

### CharacterVersion

`CharacterVersion` 是同一角色在特定叙事状态下可用于生成和核验的版本。它连接角色身份与服装、表情、伤势等当前外观或表演状态，避免生成过程只引用静态角色模板。

### ContinuityState

`ContinuityState` 保存镜头间必须延续的事实和视觉约束，例如人物状态、场景与道具状态、上一镜头结尾帧以及连续性检查结果。它是跨镜头生成和局部返工的关键对象。

### GenerationJob

`GenerationJob` 表示一次可追踪的异步生产任务。它应关联输入状态快照、镜头、Provider 工作流、输出资产、运行状态、成本、失败原因与重试或回退关系。

### QualityReport

`QualityReport` 记录对指定资产或镜头的检查结果，例如人物身份、构图、连续性、视频技术指标、字幕和口型。报告必须支持将问题定位到可重做的最小生产单元。

## 待细化

- 各对象的唯一标识、版本和审计字段。
- 叙事对象、状态对象、资产对象与任务对象之间的关系图。
- 资产存储、元数据索引、软删除与重新生成的保留策略。
- 成本、预算与 Provider 调用记录的归属方式。
