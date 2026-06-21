# 🛠️ OpenClaw 技能编写完整指南

## 技能是什么？
一个技能 = 一份给AI的操作手册（SKILL.md）。告诉AI：什么场景触发、按什么步骤干活、输出什么格式。

---

## 完整流程（6步）

### 第一步：构思
回答3个问题：
1. 这个技能**什么时候触发**？（用户说什么话时调用它）
2. AI**具体要做什么**？（列步骤）
3. 输出**长什么样**？（如果有特定格式要求）

### 第二步：写技能内容（SKILL.md）
文件结构：
```yaml
---
name: 技能名字
description: "告诉AI什么场景触发这个技能"
---

# 技能标题

技能说明或触发条件。

## 模式1：XXX
步骤1...
步骤2...

## 模式2：XXX
步骤1...
步骤2...
```

### 第三步：保存文件
```bash
cat > /tmp/技能名字.md << 'EOF'
这里放你写的内容
EOF
```

### 第四步：创建提案
```bash
# --name: 技能名字
# --description: 技能描述（AI触发条件）
# --proposal: 刚才保存的文件路径
openclaw skills workshop propose-create \
  --name "技能名字" \
  --description "技能描述" \
  --proposal /tmp/技能名字.md
```

### 第五步：检查提案
```bash
# 把返回的ID替换进去
openclaw skills workshop inspect 提案ID
```

### 第六步：应用生效
```bash
openclaw skills workshop apply 提案ID
```
生效后技能在 `~/.openclaw/workspace/skills/技能名字/SKILL.md`

---

## 关键命令速查

| 你想做什么 | 命令 |
|-----------|------|
| 看所有命令 | `openclaw --help` |
| 看技能相关命令 | `openclaw skills --help` |
| 看技能工作区命令 | `openclaw skills workshop --help` |
| 创建技能提案 | `openclaw skills workshop propose-create --name "名字" --description "描述" --proposal 文件路径` |
| 查看提案 | `openclaw skills workshop inspect 提案ID` |
| 让技能生效 | `openclaw skills workshop apply 提案ID` |
| 列出所有技能 | `openclaw skills list` |

---

## 文件存储位置

| 阶段 | 位置 |
|------|------|
| 提案阶段（草稿） | `~/.openclaw/skill-workshop/proposals/提案ID/PROPOSAL.md` |
| 生效后（活技能） | `~/.openclaw/workspace/skills/技能名字/SKILL.md` |

---

## 面试常问

| 问题 | 参考回答 |
|------|---------|
| 你怎么理解OpenClaw的技能系统？ | Skill是YAML frontmatter + Markdown的结构化操作手册，定义AI在什么场景触发、按什么步骤执行 |
| description字段有什么用？ | 告诉AI什么时候该触发这个技能，比如"Python期末作业辅导"就对应调试报错、写代码、讲知识点、检查作业 |
| 怎么把一个想法变成活的技能？ | 写SKILL.md → propose-create创建提案 → inspect检查 → apply应用生效 |
| 技能和普通提示词有什么区别？ | 技能是结构化的、可复用的、多模式的操作手册，不是一次性对话；更稳定、可迭代 |
