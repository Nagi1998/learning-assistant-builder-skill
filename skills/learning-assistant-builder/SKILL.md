---
name: learning-assistant-builder
description: Build student-friendly learning assistant web projects through a guided Chinese workflow. Use when the user says or implies "我想创造一个学习助手", wants to create a learning assistant, AI tutor, study helper, homework coach, quiz practice app, mistake notebook, learning planner, or similar educational web app, especially when the project must include Vite auto-port startup scripts for Windows and Mac.
---

# Learning Assistant Builder

## Core Workflow

Use Chinese by default unless the user requests another language.

For reuse outside Codex, use `references/portable-agent-prompt.md` as the self-contained portable prompt. It avoids Codex-specific skill assumptions and can be pasted into another Agent tool's system prompt, custom instruction, workflow node, or role definition.

Follow this workflow exactly:

1. Start a guided Q&A when the user says "我想创造一个学习助手" or asks to create a learning assistant.
2. Ask concise questions in batches. Keep each batch to the fewest questions needed to define the product.
3. If the user replies "停止" at any point during Q&A, stop asking questions and fill all remaining choices with mainstream, beginner-friendly education product defaults.
4. After Q&A is complete, ask for confirmation before generating the design document.
5. Generate a design document only after the user confirms.
6. After presenting the design document, ask for confirmation before implementing the project.
7. Implement only after the user confirms.
8. Verify the project files, startup scripts, and package scripts.
9. Put the required startup instructions at the very end of the final response.

Do not skip the two confirmation gates unless the user explicitly says to proceed through both design and implementation without stopping.

## Q&A Guide

Collect enough information to design a useful learning assistant. Prefer these question groups:

- Learner: age/grade, subject, learning goal, difficulty level.
- Scenarios: homework help, concept explanation, quiz generation, mistake review, study planning, reading support, exam prep.
- Interaction: chat-first, dashboard-first, practice-first, voice-free/text-only, teacher/parent view if needed.
- Content: whether the app uses built-in sample content, user-entered content, uploaded files, or future API integration.
- Style: calm academic, playful, minimal, classroom-friendly, or user-specified.
- Delivery: local-only demo, mock AI behavior, or real API integration if credentials are available.

If the user says "停止", use these defaults:

- Target: middle-school students.
- Subject: general learning assistant with math, English, science examples.
- Core flow: chat explanation, practice quiz, mistake notebook, study plan.
- AI mode: local mock tutor behavior unless the user provides API details.
- Style: clear, warm, focused, modern, classroom-friendly.
- Tech: Vite app with responsive UI and simple local state.
- Startup: strict compliance with the auto-port requirements below.

## Design Document Requirements

After the first confirmation, generate a design document with these sections:

- Project name and one-sentence positioning.
- Target users and learning scenarios.
- Core features and non-goals.
- Main screens and user flow.
- Data/state model.
- Tutor interaction rules, including how the assistant explains, quizzes, corrects mistakes, and avoids pretending to know unavailable personal data.
- Visual style and accessibility notes.
- Technical plan, dependencies, and project structure.
- Startup and port behavior plan.
- Acceptance checklist.

Keep the design document direct and implementation-ready. After showing it, ask the user to confirm whether to start generating the project.

## Project Implementation Rules

When implementation starts:

- Inspect the existing workspace before editing.
- Use existing project conventions if a project already exists.
- If creating a new frontend project, prefer Vite and the current ecosystem already present in the workspace.
- Build a usable first screen, not a marketing landing page.
- Include realistic educational workflows, sample prompts/content, empty states, and responsive behavior.
- Use local/mock AI behavior unless the user has explicitly requested and provided enough detail for a real API integration.
- Do not require students to inspect terminal output to decide the port.

## Mandatory Port And Startup Requirements

The project must prefer port 3000, automatically fall back to the next available port if 3000 is occupied, and let Vite open the correct browser URL.

In `package.json`, set scripts exactly as:

```json
{
  "scripts": {
    "dev": "vite --host 0.0.0.0 --port 3000 --open",
    "build": "tsc && vite build",
    "preview": "vite preview --host 0.0.0.0 --port 3000 --open"
  }
}
```

Hard rules:

- Use `--open`.
- Use `--port 3000`.
- Do not use `--strictPort`.
- Do not hardcode `http://localhost:3000` in startup scripts.
- Do not use `start http://localhost:3000`, `open http://localhost:3000`, or similar manual browser-open commands.
- Let Vite open the correct URL after it chooses the actual available port.

## Required Startup Files

Create these files in the project root with exactly these contents.

`start.bat`:

```bat
@echo off
chcp 65001
cd /d "%~dp0"

echo 正在检查项目依赖...

if not exist node_modules (
  echo 第一次启动需要安装依赖，请稍等...
  npm install
)

echo 正在启动本地服务...
echo 如果 3000 端口被占用，系统会自动切换到可用端口并打开浏览器。
npm run dev

pause
```

`start.ps1`:

```powershell
Set-Location -Path $PSScriptRoot

Write-Host "正在检查项目依赖..."

if (!(Test-Path "node_modules")) {
  Write-Host "第一次启动需要安装依赖，请稍等..."
  npm install
}

Write-Host "正在启动本地服务..."
Write-Host "如果 3000 端口被占用，系统会自动切换到可用端口并打开浏览器。"
npm run dev
```

`start.command`:

```bash
#!/bin/bash

cd "$(dirname "$0")"

echo "正在检查项目依赖..."

if [ ! -d "node_modules" ]; then
  echo "第一次启动需要安装依赖，请稍等..."
  npm install
fi

echo "正在启动本地服务..."
echo "如果 3000 端口被占用，系统会自动切换到可用端口并打开浏览器。"
npm run dev
```

`start.sh`:

```bash
#!/bin/bash

cd "$(dirname "$0")"

echo "正在检查项目依赖..."

if [ ! -d "node_modules" ]; then
  echo "第一次启动需要安装依赖，请稍等..."
  npm install
fi

echo "正在启动本地服务..."
echo "如果 3000 端口被占用，系统会自动切换到可用端口并打开浏览器。"
npm run dev
```

Make `start.command` and `start.sh` executable on Unix-like systems when possible:

```bash
chmod +x start.command start.sh
```

## Verification Checklist

Before final response, verify:

- `package.json` contains the required `dev`, `build`, and `preview` scripts.
- No startup script hardcodes `localhost:3000`.
- No script uses `strictPort`.
- `start.bat`, `start.ps1`, `start.command`, and `start.sh` exist at project root.
- `start.command` and `start.sh` are executable where the filesystem supports it.
- The app builds or the best available validation command passes.
- If validation cannot run, explain the reason briefly.

## Required Final Response Ending

The final response must end with the following startup section. Put it at the very end of the whole reply, after any summary, test results, or file notes.

````markdown
---

## 启动项目

### Windows 推荐方式

双击项目文件夹中的：

```text
start.bat
```

如果不能双击启动，可使用命令行：

```bash
cd 项目文件夹路径 && npm install && npm run dev
```

---

### Mac 推荐方式

双击项目文件夹中的：

```text
start.command
```

如果 Mac 提示没有执行权限，请在终端执行：

```bash
cd 项目文件夹路径 && chmod +x start.command && ./start.command
```

也可以使用通用命令：

```bash
cd 项目文件夹路径 && npm install && npm run dev
```

---

## 打开网址

正常情况下，浏览器会自动打开项目页面。

如果浏览器没有自动打开，请查看终端中显示的 Local 地址。

通常是：

```text
http://localhost:3000
```

如果 3000 被占用，可能会自动变成：

```text
http://localhost:3001
```

或其他可用端口。

注意：

* 不要承诺端口绝对不会被占用
* 要承诺项目会优先使用 3000
* 如果 3000 被占用，会自动寻找可用端口
* 浏览器由 Vite 自动打开正确地址
````
