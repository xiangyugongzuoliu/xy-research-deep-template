# Deep Research API

<div align="center">

[![Deploy on Zeabur](https://zeabur.com/button.svg)](https://zeabur.com/templates/TEMPLATE_CODE?referralCode=xiangyugongzuoliu)

**基于 Gemini 2.0 Flash Thinking 的深度研究引擎 REST API**

[官网](https://xiangyugongzuoliu.com/) · [YouTube](https://www.youtube.com/@xiangyugongzuoliu) · [GitHub](https://github.com/xiangyugongzuoliu)

</div>

---

## ✨ 功能特点

- 🤖 **AI 深度思考** - 基于 Gemini 2.0 Flash Thinking 模型，提供深度推理能力
- 🔍 **智能搜索** - 自动规划搜索任务，多维度收集信息
- 📝 **长文本报告** - 生成结构化 Markdown 报告，字数可达 3000+ 字
- 🔄 **异步执行** - 支持异步任务执行，轮询和 Webhook 两种模式
- 🔐 **API 认证** - 使用 x-api-key 认证，保护 API 端点
- 🌐 **n8n 集成** - 完美适配 n8n 等自动化工具
- 💯 **100% 免费** - 使用 Gemini 免费额度

## 🚀 快速部署

### 方式 1：一键部署到 Zeabur（推荐）

点击上方按钮或访问：[部署链接](https://zeabur.com/templates/TEMPLATE_CODE?referralCode=xiangyugongzuoliu)

配置以下环境变量：
- `GOOGLE_GENERATIVE_AI_API_KEY` - [获取 Gemini API Key](https://aistudio.google.com/app/apikey)
- `X_API_KEY` - API 访问密钥（建议使用 32 位随机字符串）

### 方式 2：Docker 部署

```bash
# 拉取镜像
docker pull xiangyugongzuoliu/deep-research:latest

# 运行容器
docker run -d \
  --name deep-research \
  -p 3000:3000 \
  -e GOOGLE_GENERATIVE_AI_API_KEY=your_gemini_key \
  -e X_API_KEY=your_api_key \
  xiangyugongzuoliu/deep-research:latest
```

### 方式 3：Docker Compose

```yaml
version: "3.9"
services:
  deep-research:
    image: xiangyugongzuoliu/deep-research:latest
    container_name: deep-research
    ports:
      - "3000:3000"
    environment:
      - GOOGLE_GENERATIVE_AI_API_KEY=your_gemini_key
      - X_API_KEY=your_api_key
      - TASK_RETENTION_HOURS=24
    restart: unless-stopped
```

## 📖 API 使用

### 创建研究任务

```bash
curl -X POST https://your-domain/api/research \
  -H "Content-Type: application/json" \
  -H "x-api-key: YOUR_API_KEY" \
  -d '{
    "query": "2024年人工智能发展趋势",
    "language": "zh-CN"
  }'
```

**响应**：
```json
{
  "success": true,
  "taskId": "task_abc123",
  "status": "pending",
  "pollUrl": "/api/research/task_abc123"
}
```

### 查询任务状态

```bash
curl https://your-domain/api/research/task_abc123 \
  -H "x-api-key: YOUR_API_KEY"
```

**响应（进行中）**：
```json
{
  "success": false,
  "taskId": "task_abc123",
  "status": "running",
  "progress": {
    "percentage": 45,
    "currentStep": "search-task",
    "stepDescription": "正在执行搜索任务 (3/8)"
  }
}
```

**响应（已完成）**：
```json
{
  "success": true,
  "taskId": "task_abc123",
  "status": "completed",
  "result": {
    "report": "# 标题\n\n完整的研究报告...",
    "title": "2024年人工智能发展趋势",
    "wordCount": 3500
  }
}
```

## 🔌 n8n 集成示例

### 轮询模式

1. **HTTP Request** - 创建任务
2. **Wait** - 等待 10 秒
3. **HTTP Request** - 查询状态
4. **IF** - 检查状态，如果 `running` 则返回步骤 2

### Webhook 模式（推荐）

1. **Webhook** - 创建 Webhook URL
2. **HTTP Request** - 创建任务（包含 webhookUrl）
3. 等待 Webhook 回调，自动接收结果

## 📊 技术栈

- **框架**: Next.js 15 + React 19
- **AI 模型**: Gemini 2.0 Flash Thinking + Gemini 2.0 Flash Exp
- **运行时**: Node.js 18+
- **容器**: Docker + Multi-platform (amd64/arm64)
- **部署**: Zeabur Cloud

## 💰 成本说明

- **Zeabur 免费计划**: 足够个人和小型项目使用
- **Gemini API 免费额度**:
  - 每分钟 15 次请求
  - 每天 1500 次请求
  - 完全免费

**预估成本**: $0/月（在免费额度内）

## 📝 环境变量

| 变量名 | 必填 | 默认值 | 说明 |
|--------|------|--------|------|
| `GOOGLE_GENERATIVE_AI_API_KEY` | ✅ | - | Gemini API Key |
| `X_API_KEY` | ✅ | - | API 访问密钥 |
| `TASK_RETENTION_HOURS` | ❌ | 24 | 任务保留时间（小时） |
| `GOOGLE_GENERATIVE_AI_API_BASE_URL` | ❌ | - | Gemini API Base URL |

## 🔗 相关链接

- **官网**: https://xiangyugongzuoliu.com/
- **YouTube**: https://www.youtube.com/@xiangyugongzuoliu
- **GitHub**: https://github.com/xiangyugongzuoliu
- **Docker Hub**: https://hub.docker.com/r/xiangyugongzuoliu/deep-research
- **Gemini API**: https://aistudio.google.com/app/apikey

## 📄 许可证

本项目基于私有源码，Docker 镜像公开发布供免费使用。

---

**作者**: 翔宇工作流
**年份**: 2025
