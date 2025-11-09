# AI 半定制化课件生成器 - MVP 骨架

简介
- 这是一个 MVP 骨架：Node.js (TypeScript) API + BullMQ 队列 + Node worker + Python FastAPI 处理服务。
- Python 服务负责文档解析、Embeddings（占位，可用 Qwen3-Embedding-4B）、调用硅基流动 GLM（GLM-4.6）生成 slides JSON 并渲染 PPTX（python-pptx）。
- 支持 seedream / qwan 图片生成的钩子（需填 API keys）。

目录结构（示例）
- docker-compose.yml
- .env.example
- prompt_templates.yaml
- api/ (Node TypeScript API)
- node-worker/ (Node BullMQ worker)
- python-worker/ (Python FastAPI 服务：解析 + pptx 渲染)

快速开始（本地开发）
1. 复制 repo 文件到本地
2. 在项目根目录创建 `.env`，参考 `.env.example` 填入你的 keys（或占位）
3. 启动（本地开发）
   - 安装 Docker & Docker Compose
   - 运行: `docker-compose up --build`
4. 调用 API（示例）
   POST http://localhost:3000/api/v1/generate_course
   Body:
   {
     "client_name":"Acme Corp",
     "audience":"产品经理",
     "audience_level":"intermediate",
     "course_duration_hrs": 2,
     "language":"zh",
     "outcomes":["掌握需求拆解","构建用户故事"],
     "modules_count": 4
   }
5. 查询 job 状态:
   GET http://localhost:3000/api/v1/jobs/{jobId}

注意
- GLM、Embeddings、seedream/qwan 需你填入真实 API keys 与 endpoints。
- Qdrant 作为向量 DB 为可选服务，未在 docker-compose 默认启用（注释提供配置）。
- 本仓库为开发级骨架，生产需考虑安全、认证、多租户、审计、监控、错误重试等.
