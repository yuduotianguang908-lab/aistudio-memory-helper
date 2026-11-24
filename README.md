# AI Studio Memory Helper

![Userscript](https://img.shields.io/badge/Tampermonkey-Userscript-00485B?style=flat-square&logo=tampermonkey)
![Version](https://img.shields.io/badge/Version-v1.3-blue?style=flat-square)
![Platform](https://img.shields.io/badge/Google%20AI%20Studio-Compatible-4285F4?style=flat-square&logo=google)

[English](#-english) | [简体中文](#-简体中文)

---

## 📖 English

A lightweight Tampermonkey userscript that brings **persistent, cross-session memory** to Google AI Studio (`aistudio.google.com` & `ai.dev`).

Instead of repeating your background, tech stack, and preferences in every new chat, this tool maintains a local memory store and seamlessly injects selected context into the prompt input—with optional LLM-powered extraction and merging.

### ✨ Key Features

- **Framework-Safe DOM Injection**: Isolated UI built with **Shadow DOM**; dispatches native input events compatible with Angular's reactive form state and `TrustedHTML` policies.
- **Granular Context Grouping**: Organize memories using Markdown `##` headings and toggle specific sections per conversation to save tokens and keep context focused.
- **LLM-Assisted Memory Distillation**:
  - **Incremental Extract**: Extracts new facts from the current chat with timestamps.
  - **Smart Merge**: Resolves conflicts and updates outdated entries based on recent conversation context.
  - **Deduplicate & Prune**: Cleans up redundant or expired records.
  - *Powered by Gemini API over **SSE streaming** with preview-before-write confirmation.*
- **Local-First Privacy & Rollback**: All memory data and API keys reside strictly in local Tampermonkey storage (`GM_setValue`). Includes **5-version undo history** and JSON backup/restore.

### 🚀 Quick Start

1. Install the [Tampermonkey](https://www.tampermonkey.net/) browser extension.
2. Open [`aistudio-memory-helper.user.js`](./aistudio-memory-helper.user.js) in this repository and click **Raw** to trigger one-click installation.
3. Open [Google AI Studio](https://aistudio.google.com/), click the floating memory panel on the left, and enter your Gemini API Key under **Settings** *(only required for AI distillation; manual editing & auto-injection work without a key)*.

### 📌 Transparency & Maintenance

- **Privacy**: Zero external backend. No user prompts, memories, or API keys ever leave your browser except direct calls to Google's Gemini API when you trigger distillation.
- **Authorship**: Product requirements, edge-case debugging, and end-to-end verification were driven by the author; source code was generated with AI assistance (Claude & Gemini).
- **Maintenance**: Provided on a best-effort basis. Upstream UI updates to Google AI Studio may break DOM selectors—PRs and forks are welcome.

---

## 📖 简体中文

一个面向 Google AI Studio（`aistudio.google.com` / `ai.dev`）的轻量级油猴脚本，用于实现**跨对话持久化共享记忆**。

无需在每次开启新对话时重复交代个人背景、技术栈与交互偏好，脚本会在本地维护一份结构化记忆库，并在发送对话时按需无感注入；同时支持调用 Gemini API 对当前对话进行增量提炼与智能合并。

### ✨ 核心特性

- **低侵入界面与状态同步**：悬浮面板采用 **Shadow DOM** 样式隔离，通过原生事件模拟实现与 Angular 响应式输入框的状态同步，兼容 `TrustedHTML` 安全策略。
- **按分组按需注入**：支持使用 Markdown `## 标题` 划分记忆模块，不同对话可自由勾选需要注入的上下文分组，减少无关 Token 消耗。
- **AI 驱动的记忆整理**：
  - **提炼增量**：从当前对话中提取带日期的新增事实并追加；
  - **智能合并**：结合本轮上下文自动更新、覆盖矛盾的旧条目；
  - **整理去重**：清理重复或过时信息。
  - *采用 **SSE 流式输出** 实时预览结果，所有修改均需人工确认后才写入。*
- **本地隐私与防误操作**：记忆库与 API Key 均仅保存在本地油猴沙盒存储（`GM_setValue`）中，不经过任何第三方服务器；内置 **5 版本历史回滚** 与 JSON 导入导出备份。

### 🚀 快速安装与使用

1. 确保浏览器已安装 [Tampermonkey（篡改猴）](https://www.tampermonkey.net/) 扩展。
2. 点击本仓库中的 [`aistudio-memory-helper.user.js`](./aistudio-memory-helper.user.js)，再点击右上角 **Raw** 按钮即可一键安装。
3. 打开 [Google AI Studio](https://aistudio.google.com/)，点击页面左侧悬浮记忆按钮，在 **「设置」** 中填入你自己的 Gemini API Key 并保存即可。*（若仅使用“手动维护 + 自动注入”，无需填写 Key。）*

### 📌 说明与声明

- **数据隐私**：纯前端本地运行，除你主动点击“提炼/合并”时直连 Google Gemini API 外，不会向任何外部服务器上传数据。
- **开发方式**：本项目由个人提出需求、排查边界问题并完成实测调通，代码部分由 AI（Claude & Gemini）辅助生成。
- **维护说明**：由于 Google AI Studio 前端改版较快，不保证长期同步跟进维护；如遇页面改版导致失效，欢迎自行 Fork 修改。