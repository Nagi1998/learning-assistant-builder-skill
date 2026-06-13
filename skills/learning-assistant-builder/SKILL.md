---
name: learning-assistant-builder
description: Build student-friendly learning assistant web projects through a required Chinese Q&A workflow. Use when the user says "我想创造一个学习助手" or asks to create a learning assistant, AI tutor, study helper, homework coach, quiz practice app, mistake notebook, learning planner, or similar educational web app. The workflow must ask questions first, confirm before generating a design document, confirm again before implementing, and strictly apply Vite auto-port startup requirements.
---

# Learning Assistant Builder

Use Chinese by default.

For reuse outside Codex, use `references/portable-agent-prompt.md` as the self-contained portable prompt. It can be pasted into another Agent tool's system prompt, custom instruction, workflow node, or role definition.

## 必须保留的触发与流程

- 该 skill 接收到“我想创造一个学习助手”后开启调用，调用后按照以下提示词的流程进行问答交流，全部问答结束后请求用户确认后生成设计文档，再请求用户确认后开始执行生成项目，项目生成严格按照提示词中的要求进行，最终明确指明如何进行项目展示，例如启动文件的名称和网址，越直接明了越好。
- 在问答交流环节，如若收到“停止”指令，则自动按照主流设计理念直接补充剩下的部分，不占用多余时间。

## 执行顺序

1. 当用户说“我想创造一个学习助手”或表达同等需求时，先进入问答交流。
2. 问答交流结束后，必须新增一个提问，确认这个应用的使用逻辑。
3. 使用逻辑确认后，必须请求用户确认是否生成设计文档。
4. 只有用户确认后，才生成设计文档。
5. 设计文档生成后，必须再次请求用户确认是否开始执行生成项目。
6. 只有用户确认后，才开始创建或修改项目文件。
7. 生成项目时，必须严格执行下面“端口自动适配与一次启动成功要求”。
8. 最终回复必须明确指明如何展示项目，包括启动文件名称和网址说明；启动命令和网址说明必须放在整个回复最后。

## 问答交流要求

- 问答交流必须是引导式、开放式、自然对话，不是问卷、表格、选择题或需求清单。
- 每一轮优先只问 1 个核心问题；确实必要时最多问 2 个，不要一次性把多个方向全部抛给用户。
- 不要给具体选项让用户选择，例如不要写“A/B/C”、不要写“你可以选择……”、不要列出一串可选功能、年级、学科、风格或页面。
- 不要用“请选择”“以下选项”“你更偏向哪一种方案”这类话术，除非用户主动要求你给选项。
- 开启问答后的第一轮必须围绕“学科方向”提问，并且只问一个开放问题。
- 第一轮推荐使用：“为了先把学习方向定下来，我们先从学科聊起：你希望这个学习助手主要陪学生学习哪一门或哪一类内容？可以用一句话描述你心里的学习场景。”
- 不要把第一轮问题写成学科选项列表；让用户自由描述学科、课程或跨学科方向。
- 每次必须先提问获取用户回答，再基于用户回答给出理解、建议或推荐；不要在用户回答前主动推荐方案。
- 用户回答后，先用一句话确认理解；如果需要推荐，只能推荐与该回答直接相关的内容，然后继续问下一个自然问题。
- 不要在信息不足时直接生成设计文档或项目。
- 如果用户回复“停止”，立刻停止追问，按照主流设计理念补齐剩余需求，并进入“请求用户确认是否生成设计文档”的步骤。

## 问答覆盖范围

问答交流结束前，必须尽量确认以下内容。不要把这些内容一次性列给用户；应按照自然对话逐轮提问：

1. 学科方向：学习助手主要服务哪门学科、课程或跨学科内容。
2. 实际问题：学生当前最需要解决的具体学习痛点、卡点或任务。
3. 使用对象：学生年龄、年级、基础水平、学习习惯，以及是否面向老师或家长辅助使用。
4. 使用场景：课堂演示、课后练习、作业辅导、考试复习、自主学习、社团项目或其他真实场景。
5. 功能范围：围绕用户回答提炼必要功能，不要提前塞功能清单；必须区分核心功能和可后置功能。
6. 页面布局：根据已确认的学习流程讨论页面组织方式，例如主界面、练习区、记录区、计划区等，但不要先给模板式选项。
7. 设计风格：根据使用对象和场景引导确认视觉气质、信息密度、互动感和课堂展示效果。
8. MVP 实现部分：确认第一版必须完成的最小可用范围，保证能运行、能展示、能体现学习助手核心价值。
9. 迭代部分：确认后续可以增强的方向，例如真实 AI 接口、上传资料、个性化学习档案、教师端、数据统计等。

推荐顺序：

1. 先问学科方向。
2. 再问实际问题。
3. 再问使用对象。
4. 再问使用场景。
5. 基于前四项回答，再引导功能范围、页面布局、设计风格、MVP 和迭代部分。

在功能、布局、风格、MVP、迭代部分，必须先让用户描述想法或约束，再根据回答做推荐。推荐时用“基于你刚才说的……”开头，避免凭空给方案。

## 使用逻辑确认

问答交流结束后、请求生成设计文档前，必须单独确认应用的使用逻辑。

这一轮提问必须帮助用户确认：

- 用户打开应用后第一步做什么
- 用户如何输入或选择学习任务
- 学习助手如何给出讲解、练习或反馈
- 用户如何查看结果、记录或下一步学习建议
- 一次完整学习流程如何结束

不要直接替用户定稿。先用一句话概括你根据前面问答理解到的使用逻辑，再用开放式问题请用户确认或修正。

推荐问法：

```text
在生成设计文档前，我想先确认一下这个应用的使用逻辑：我理解的是，学生进入应用后先说明自己要学习的问题，系统再引导讲解和练习，最后沉淀记录或下一步建议。这个流程符合你的想法吗？你希望学生实际使用时还有哪些关键步骤？
```

## 设计文档要求

用户确认后，生成一份清晰、可执行的设计文档，至少包含：

- 项目名称和定位
- 学科方向
- 实际问题
- 目标用户
- 使用场景
- 核心功能
- 页面结构
- 设计风格
- 交互流程
- 应用使用逻辑
- MVP 实现范围
- 后续迭代方向
- 技术方案
- 端口与启动方案
- 项目验收标准

设计文档完成后，必须请求用户确认是否开始执行生成项目。

## 端口自动适配与一次启动成功要求

为了尽量保证学生一次启动成功，项目不能强行固定死端口。

项目必须采用：

* 优先尝试 3000 端口
* 如果 3000 被占用，自动切换到下一个可用端口
* 启动后自动打开浏览器
* 不手动写死打开 [http://localhost:3000](http://localhost:3000/)
* 不使用 strictPort
* 不要求学生自己判断端口
* 不要求学生手动复制终端里的新端口

---

## package.json 要求

package.json 中必须这样设置：

```json
{
  "scripts": {
    "dev": "vite --host 0.0.0.0 --port 3000 --open",
    "build": "tsc && vite build",
    "preview": "vite preview --host 0.0.0.0 --port 3000 --open"
  }
}
```

注意：

* 必须使用 `--open`
* 必须使用 `--port 3000`
* 禁止使用 `--strictPort`
* 禁止在启动脚本中写死打开 `http://localhost:3000`
* 如果 3000 被占用，Vite 会自动使用新的可用端口
* 浏览器应由 Vite 自动打开正确地址

---

## Windows 快速启动要求

项目根目录必须生成：

```text
start.bat
```

内容如下：

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

说明：

* Windows 学生优先双击 `start.bat`
* 不要求学生使用 bash
* 不要求学生手动输入多行命令
* 不要在 bat 中使用 `start http://localhost:3000`
* 浏览器打开交给 Vite 的 `--open` 自动完成
* 这样可以避免端口切换后仍然打开错误网址

---

## Windows PowerShell 启动要求

项目根目录必须生成：

```text
start.ps1
```

内容如下：

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

说明：

如果 Windows 阻止运行 PowerShell 脚本，优先使用 `start.bat`。

---

## Mac 快速启动要求

项目根目录必须生成：

```text
start.command
```

内容如下：

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

同时生成：

```text
start.sh
```

内容如下：

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

说明：

* Mac 学生优先双击 `start.command`
* 不要在脚本中写死 `open http://localhost:3000`
* 浏览器打开交给 Vite 的 `--open` 自动完成
* 如果无法双击运行，可以在终端执行：

```bash
chmod +x start.command && ./start.command
```

---

## 启动方式输出要求

项目完成后，最后必须根据系统分别输出启动方式。

启动方式必须放在整个回复最后。

最终输出格式必须是：

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
* 启动命令和网址说明必须放在整个回复最后
````
