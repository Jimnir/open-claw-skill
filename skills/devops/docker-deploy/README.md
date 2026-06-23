# Docker 部署助手 🐳

> Docker 部署配置生成和检查工具，自动生成 Dockerfile、docker-compose.yml，或审查现有配置。

## 技能简介

**docker-deploy** 是一个专注于 Docker 容器化部署的 AI 技能。当你需要将一个项目容器化、编排多服务部署、或者检查现有的 Docker 配置时，调用这个技能即可获得专业的配置模板和审查意见。

## 使用场景

| 场景 | 说明 |
|------|------|
| 🆕 项目容器化 | 给新项目写 Dockerfile，自动选择合适的基础镜像和构建策略 |
| 🏗️ 多服务编排 | 生成 docker-compose.yml，配置数据库、缓存等依赖服务 |
| 🔍 配置审查 | 检查已有的 Dockerfile 或 docker-compose.yml，发现潜在问题 |

## 触发方式

直接在对话中提及以下关键词即可触发：

- **Dockerfile 生成**：「帮我写 Dockerfile」「容器化这个项目」
- **docker-compose 生成**：「帮我写 docker-compose.yml」「需要数据库一起部署」
- **配置检查**：「检查我的 Dockerfile」「看看这个配置有问题吗」

## 工作模式

### 模式 1：docker-init — 生成 Dockerfile

自动分析项目类型（Python / Node / Go / Java / 静态网站等），生成优化过的 Dockerfile：

- 选择官方 slim/alpine 基础镜像
- 利用 Docker 层缓存优化构建速度
- 支持多阶段构建
- 非 root 用户运行（安全性）
- 附带每段代码的说明

### 模式 2：docker-compose — 生成编排配置

生成多服务 docker-compose.yml：

- 主服务 + 依赖服务（MySQL / PostgreSQL / Redis / Nginx 等）
- 端口映射、数据卷（volumes）配置
- 健康检查
- 环境变量与 .env 文件支持
- 启动顺序控制（depends_on）

### 模式 3：docker-check — 配置审查

对现有配置逐项检查，找出如下问题：

- ✅ 基础镜像是否过大
- ✅ 是否充分利用缓存
- ✅ 是否有过多的镜像层
- ✅ 端口暴露是否正确
- ✅ 是否以非 root 用户运行
- ✅ CMD/ENTRYPOINT 是否合理
- ✅ docker-compose 中的 depends_on 是否足够
- ✅ volumes 路径是否正确
- ✅ 是否有硬编码的敏感信息

## 使用示例

```
你：帮我写一个 Python Flask 项目的 Dockerfile，用多阶段构建
→ 助手开始执行 docker-init 模式，生成完整的 Dockerfile

你：帮我写 docker-compose，我要 Flask + Redis + PostgreSQL
→ 助手开始执行 docker-compose 模式，生成编排配置

你：检查一下这个 Dockerfile 哪里可以优化（贴出内容）
→ 助手开始执行 docker-check 模式，逐项审查并给出建议
```

## 最佳实践

1. **提供完整的项目信息**：项目类型、运行时版本、依赖管理方式，越详细生成的配置越准确
2. **利用多阶段构建**：对于编译型语言（Go、Java）和前端项目，多阶段构建能大幅减小最终镜像体积
3. **敏感信息用环境变量**：密码、密钥等不要硬编码在配置中，使用 .env 文件或 Docker Secrets

## 依赖

- Docker（建议 20.10+）
- docker-compose（建议 v2+）
