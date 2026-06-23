# 📦 OpenClaw 技能库

一个 OpenClaw 技能库，记录学习过程中的技能积累。

## 技能列表

### 🐳 DevOps
- **docker-deploy** — Docker 部署助手，生成 Dockerfile、docker-compose、检查配置

### 🎯 面试准备
- **interview-tutor** — 面试辅导，分析考察点、多角度回答、实战案例

### 🐍 教学辅导
- **python-tutor** — Python 作业辅导，调试报错、写代码、讲知识点、检查作业

## 安装指南

1. 下载本仓库：`git clone https://github.com/Jimnir/open-claw-skill.git`
2. 把需要的技能文件夹（如 `skills/devops/docker-deploy/`）复制到你的 `~/.openclaw/workspace/skills/` 对应的分类目录下
3. 重启 OpenClaw 或在聊天窗口输入 `/reset`，技能即可生效

## 贡献指南

加一个新技能的步骤：

1. **写 SKILL.md** — 定义触发条件和操作步骤
2. **创建提案 → 检查 → 应用生效** — 通过 `openclaw skills workshop` 流程
3. **写 README 说明** — 让人一看就知道这个技能是干什么的
4. **放入对应的分类文件夹** — 按业务场景归类
5. **更新复习手册** — 在技能列表中加入新技能
6. **提交到 GitHub** — `git add / commit / push`

## 命名规范

- **文件夹名**：全小写英文、短横线连接（如 `docker-deploy`）
- **描述**：用中文写清楚触发场景
- **格式**：每个技能包含 `SKILL.md`（AI 操作手册）和 `README.md`（使用说明）
