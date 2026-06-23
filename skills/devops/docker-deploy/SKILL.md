---
name: "docker-deploy"
description: "Docker部署助手：生成Dockerfile / docker-compose.yml / 检查部署配置"
---

# Docker 部署助手

当用户提到 Docker、容器化部署、Dockerfile、docker-compose、镜像构建等话题时触发这个技能。

## 模式1：生成 Dockerfile（docker-init）

当用户说"帮我写 Dockerfile""容器化这个项目"时：

1. **了解项目信息**
   - 问清楚项目类型（Python/Node/Go/Java/静态网站等）
   - 确认运行时版本（Python 3.x / Node 18 / Go 1.x 等）
   - 了解依赖管理方式（requirements.txt / package.json / go.mod 等）
   - 确认是否需要多阶段构建

2. **生成 Dockerfile**
   - 选择合适的基础镜像（官方 slim/alpine 优先）
   - 设置工作目录
   - 复制依赖文件 → 安装依赖（利用缓存）
   - 复制源码
   - 暴露端口
   - 设置启动命令（CMD / ENTRYPOINT）
   - 多阶段构建时注意产物复制路径

3. **输出完整 Dockerfile**
   - 用代码块输出，附带简要说明每段的作用
   - 标注需要用户替换的变量（如有）

## 模式2：生成 docker-compose（docker-compose）

当用户说"帮我写 docker-compose.yml""需要数据库一起部署"时：

1. **了解服务构成**
   - 确认主服务是什么
   - 确认需要哪些依赖服务（MySQL / PostgreSQL / Redis / Nginx 等）
   - 确认端口映射需求
   - 确认需要持久化数据（volumes）
   - 确认环境变量配置方式（直接写还是 .env 文件）

2. **生成 docker-compose.yml**
   - 定义 services 结构
   - 配置网络
   - 配置 volumes
   - 配置依赖顺序（depends_on）
   - 配置健康检查（如有必要）
   - 配置环境变量

3. **输出完整 docker-compose.yml**
   - 附带启动命令说明
   - 标注注意事项（首次启动顺序、数据持久化路径等）

## 模式3：检查部署配置（docker-check）

当用户说"检查我的 Dockerfile""看看这个配置有问题吗"时：

1. **要求用户贴出配置**
   - 让用户贴出 Dockerfile 或 docker-compose.yml 内容

2. **逐项检查**
   - 基础镜像是否过大（建议用 slim/alpine）
   - 是否利用缓存（依赖先复制再安装，最后复制源码）
   - 是否有多余层（合并 RUN 命令）
   - 端口是否正确暴露
   - 是否以非 root 用户运行（USER 指令）
   - CMD/ENTRYPOINT 是否合理
   - docker-compose 中 depends_on 是否足够
   - volumes 路径是否正确
   - 环境变量是否硬编码敏感信息

3. **输出检查结果**
   - 列出问题项 ⚠️
   - 给出改进建议 ✅
   - 提供修正后的完整配置（如有必要）
