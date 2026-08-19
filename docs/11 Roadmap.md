# Roadmap

> 状态：Draft

## MVP

以“一个中文小说项目从导入到 9:16 成片”为验收主线。

1. 小说导入与结构化小说圣经，支持人物和关系可视化编辑。
2. 分集规划与分镜编辑，支持局部重生成。
3. 角色、场景资产库与跨镜头状态引用。
4. 一个 OpenAI-compatible LLM、两个图像 Provider、两个视频 Provider 和一个语音 Provider。
5. 异步任务队列、状态与成本展示、单镜头重做。
6. 自动质检和 FFmpeg 自动成片。

## 推荐技术路线

采用自有统一系统并复用底层组件。对外产品、项目数据、Story State、任务状态与用户体验由 Director OS 控制；ComfyUI 和 Provider 仅作为后台执行器。

调研建议的首版技术为 Next.js、FastAPI、PostgreSQL、MinIO/S3、Redis + Celery、ComfyUI API、Provider Adapter、FFmpeg 与 pgvector。复杂跨日的人工工作流出现后，再评估 Temporal。

Toonflow、ViMax、Wind Comic 可作为体验和实现参考，或在完成许可证与实际部署评估后成为局部代码来源；不能构成用户需要来回操作的多个软件。特别是 Toonflow 的当前 LICENSE 含附加商业授权条件，任何对外产品 fork 或分发前必须单独确认授权。

可行性、证据与风险的完整推演不在本仓库。
