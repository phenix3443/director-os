# Story State

> 状态：Draft
> 来源：长篇叙事、视觉记忆与连续性的生态调研。

## 定义

Story State 是在任意叙事位置对故事事实、角色状态、场景状态、镜头连续性和已生产资产的持久化描述。

系统保存 Story State，而不是只保存 Prompt。Prompt 是根据当前状态、镜头规格和目标 Provider 编译出的可再生中间产物。

## 必须解决的问题

角色在后续集数中的发型、服装、伤势、情绪和所持道具必须与剧情事件一致；后续镜头也可能需要继承上一镜头的结尾帧或关键视觉记忆。系统不得将第一集的默认角色设定误用于已发生变化后的镜头。

## 状态范围

    叙事结构：Novel → Season → Episode → Scene → Shot
    角色状态：Character、CharacterVersion、Costume、Expression、Voice
    世界状态：Location、Prop、StoryEvent
    连续性状态：ContinuityState、上一镜头结尾帧、关联视觉记忆
    生产状态：ImageAsset、VideoAsset、AudioAsset、GenerationJob、QualityReport

## 核心原则

- 状态必须绑定叙事位置，例如某角色在某个 Scene 或 Shot 生效的服装、伤势和情绪。
- `Character` 表示角色身份；`CharacterVersion` 表示该身份在特定叙事状态下可被生产系统引用的版本。
- `ContinuityState` 记录跨镜头约束与继承来源，包括应延续的状态和视觉锚点。
- 已生成资产必须可追溯至生成它时使用的状态版本、镜头规格和生成任务。
- 修改状态或资产后，应只使依赖该变化的下游结果失效，而不是重做整集。

## 状态快照示例

以下示例描述角色“林夏”在第 8 集第 12 场的可生产状态。它比“女主、25 岁、长发、漂亮”这类静态角色 Prompt 额外包含当前外观、情绪和角色已知信息；正式 Schema 将进一步明确其与 `CharacterVersion`、`ContinuityState` 和剧情事件的关系。

```json
{
  "episode": 8,
  "scene": 12,
  "character": "林夏",
  "appearance": {
    "hair": "短发",
    "costume": "蓝色病号服",
    "injury": "右手包扎"
  },
  "emotion": "警惕、疲惫",
  "known_information": [
    "已经知道陈默撒谎",
    "尚不知道父亲仍然活着"
  ]
}
```

## 与其他层的关系

- Director Layer 读取并更新 Story State，输出分集、场次和镜头决策。
- Prompt Compiler 读取 State 与镜头规格，生成可替换的 Provider Prompt。
- Production Layer 使用冻结的状态快照创建生成任务。
- Quality Layer 根据 State 核验成片，并把质量报告回写到对应资产和镜头。

## 待细化

- 状态版本、有效时间范围与冲突处理规则。
- 视觉记忆和标准资产的存储、检索与淘汰机制。
- 状态变更对下游镜头、资产和任务的影响图。
