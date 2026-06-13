# Learning Assistant Builder Skill

这是一个可通过 GitHub 链接安装的 Codex Skill，同时包含可复制到其他 Agent 工具中的通用提示词版本。

## GitHub 安装链接格式

把本仓库上传到 GitHub 后，Skill 安装链接应使用下面这种格式：

```text
https://github.com/<你的GitHub用户名>/learning-assistant-builder-skill/tree/main/skills/learning-assistant-builder
```

例如：

```text
https://github.com/your-name/learning-assistant-builder-skill/tree/main/skills/learning-assistant-builder
```

## 在 Codex 中安装

在 Codex 中可以让 Agent 使用 skill-installer 安装上面的 GitHub 链接。

也可以在终端执行：

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py --url https://github.com/<你的GitHub用户名>/learning-assistant-builder-skill/tree/main/skills/learning-assistant-builder
```

安装后重启 Codex，让新 skill 生效。

## 其他 Agent 工具复用

如果目标工具不支持 Codex Skill 机制，可以直接复制这个文件内容到其他 Agent 的 System Prompt、Custom Instructions、角色设定或工作流节点中：

```text
skills/learning-assistant-builder/references/portable-agent-prompt.md
```

## Skill 内容

- `skills/learning-assistant-builder/SKILL.md`：Codex Skill 主文件
- `skills/learning-assistant-builder/agents/openai.yaml`：Codex UI 元数据
- `skills/learning-assistant-builder/references/portable-agent-prompt.md`：跨 Agent 通用提示词
