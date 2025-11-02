# Deep Research API - Zeabur 部署模板

<p align="center">
  <strong>基于 Gemini 的深度研究引擎</strong>
</p>

<p align="center">
  AI 驱动的深度研究工具，支持异步任务执行、实时进度追踪、Webhook 回调<br>
  提供 REST API 和 Web 界面，完美集成 n8n 等自动化工具
</p>

<p align="center">
  🌐 <a href="https://xiangyugongzuoliu.com/">官网</a> |
  📦 <a href="https://github.com/xiangyugongzuoliu/deep-research-zeabur">GitHub 仓库</a> |
  🐳 <a href="https://hub.docker.com/r/xiangyugongzuoliu/deep-research">Docker Hub</a> |
  🎬 <a href="https://www.youtube.com/@xiangyugongzuoliu">YouTube</a>
</p>

---

## 🚀 一键部署

[![Deploy on Zeabur](https://zeabur.com/button.svg)](https://zeabur.com/templates/RW99XV?referralCode=xiangyugongzuoliu)

点击上方按钮，一键部署到 Zeabur。

> **注意：** 部署前请准备好 Gemini API Key，并设置安全的 API 访问密钥！

---

## ⚙️ 环境变量配置

部署时需要配置以下环境变量：

| 变量名 | 说明 | 默认值 | 必填 |
|--------|------|--------|------|
| `GOOGLE_GENERATIVE_AI_API_KEY` | Gemini API Key（[获取地址](https://aistudio.google.com/app/apikey)） | 无 | ✅ |
| `ACCESS_PASSWORD` | 访问密码（用于前端代理模式和 REST API 认证） | 无 | ✅ |
| `TAVILY_API_KEY` | Tavily API Key（[获取地址](https://tavily.com)）<br>配置后将使用 Tavily 搜索服务，自动获取图片和完整引用来源 | 空 | ❌ |
| `TASK_RETENTION_HOURS` | 任务保留时间（小时） | `24` | ❌ |

**安全提示：**
- Gemini API Key 和 ACCESS_PASSWORD 务必妥善保管
- 建议使用 `openssl rand -base64 32` 生成 ACCESS_PASSWORD

**关于搜索服务：**
- 默认使用 **Gemini 内置搜索**（完全免费）
- 配置 `TAVILY_API_KEY` 后自动切换到 **Tavily 搜索服务**
- Tavily 优势：
  - 提供相关图片（Gemini 内置搜索不支持）
  - 提供完整的引用来源链接
  - 搜索结果更丰富
- Tavily 限制：
  - 需要注册获取 API Key（有免费额度）
  - [注册地址](https://tavily.com)

---

## 📖 使用说明

### API 端点

#### 创建研究任务
```
POST /api/research
```

#### 查询任务状态
```
GET /api/research/:taskId
```

### 请求示例

```bash
# 创建研究任务
curl -X POST https://your-domain.zeabur.app/api/research \
  -H "Content-Type: application/json" \
  -H "x-api-key: YOUR_API_KEY" \
  -d '{
    "query": "2024年人工智能发展趋势",
    "language": "zh-CN",
    "maxSearchTasks": 8
  }'

# 查询任务状态
curl https://your-domain.zeabur.app/api/research/task_xxx \
  -H "x-api-key: YOUR_API_KEY"
```

### 请求参数

**创建任务参数：**

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `query` | string | ✅ | 研究主题 |
| `language` | string | ❌ | 语言（默认：自动检测） |
| `maxSearchTasks` | number | ❌ | 最大搜索任务数（默认：8） |
| `includeImages` | boolean | ❌ | 是否包含图片（默认：true） |
| `includeReferences` | boolean | ❌ | 是否包含参考文献（默认：true） |
| `searchMaxResults` | number | ❌ | 每次搜索最大结果数（默认：5） |
| `webhookUrl` | string | ❌ | Webhook 回调地址 |

---

## ✨ 核心功能

- ✅ **AI 深度思考** - 基于 Gemini 模型
- ✅ **智能搜索** - 自动规划多维度搜索任务，支持 Gemini 内置搜索和 Tavily 外部搜索
- ✅ **长文本报告** - 生成 3000+ 字的结构化 Markdown 报告
- ✅ **图片和引用** - 配置 Tavily API 后自动获取相关图片和完整引用来源
- ✅ **异步执行** - 支持轮询和 Webhook 两种模式
- ✅ **实时进度** - 0-100% 进度追踪
- ✅ **API 认证** - x-api-key 保护
- ✅ **n8n 集成** - 完美适配自动化工具
- ✅ **Web 界面** - 现代化 Web UI
- ✅ **100% 免费** - 使用 Gemini 免费额度（Tavily 可选）

---

## 🔧 访问你的服务

部署完成后，你将获得一个 Zeabur 提供的域名：

```
https://your-app-name.zeabur.app
```

- **Web 界面**：`https://your-app-name.zeabur.app`
- **API 文档**：`https://your-app-name.zeabur.app/api-docs`
- **API 端点**：`https://your-app-name.zeabur.app/api/research`

---

## 🌐 n8n 集成示例

### 轮询模式

1. **HTTP Request** - 创建任务，记录 taskId
2. **Wait** - 等待 10 秒
3. **HTTP Request** - 查询状态
4. **IF** - 如果 status === "running" 返回步骤 2

### Webhook 模式（推荐）

1. **Webhook** - 创建 Webhook URL
2. **HTTP Request** - 创建任务（包含 webhookUrl）
3. 等待 Webhook 自动回调，接收结果

---

## 💰 成本说明

- **Zeabur 免费计划**：足够个人和小型项目使用
- **Gemini API 免费额度**：
  - 每分钟 15 次请求
  - 每天 1500 次请求
  - 完全免费

**预估成本**：$0/月（在免费额度内）

---

## 🙏 技术栈

- **框架**：Next.js 15 + React 19
- **AI 模型**：Gemini
- **语言**：TypeScript
- **样式**：Tailwind CSS
- **API**：REST API + SSE
- **运行时**：Node.js 18+
- **容器**：Docker（支持 amd64/arm64）
- **部署**：Zeabur Cloud

---

## 📚 相关链接

- **官网**：https://xiangyugongzuoliu.com/
- **YouTube**：https://www.youtube.com/@xiangyugongzuoliu
- **GitHub**：https://github.com/xiangyugongzuoliu
- **Docker Hub**：https://hub.docker.com/r/xiangyugongzuoliu/deep-research
- **Gemini API**：https://aistudio.google.com/app/apikey

---

## 📝 说明

本项目修改自开源项目 [u14app/deep-research](https://github.com/u14app/deep-research)，添加了 REST API 功能、异步任务执行、Webhook 回调等特性，仅供自用。

**新增功能**：
- REST API 接口（POST /api/research, GET /api/research/:taskId）
- 异步任务执行和轮询机制
- Webhook 回调支持
- 实时进度追踪（0-100%）
- x-api-key 认证保护
- Docker 部署优化
- API 文档页面
- Zeabur 一键部署
