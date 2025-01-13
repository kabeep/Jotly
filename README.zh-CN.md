<div align="center">

<h1>Jotly</h1>

一款跨平台的计划与笔记管理工具，运用 AI 技术提供清晰且可执行的步骤，助力实现目标导向的进展。

[English][en-us-url] | 简体中文

<pre>进行中的工作</pre>

</div>

## 🟡 为什么

曾经我没有记录宏观目标与 TODO 的习惯，总是想到什么就去做，脑海里漂浮的想法让我保持兴奋，我想立刻开始或实现它，

对我的健康而言，更像是一种诅咒。所以我的睡眠习惯一直不好，有时会保持无睡眠 36 h，有时只在两天之间休息 1-2h。

---

随着时间变化，任务复杂度逐渐上升，完成一项工作的区间变得很长，我不得不将它们拆解成一份份清晰明确的任务列表，

提醒我下一步该做什么，我还有多少时间可以煮咖啡。当一些想法出现，我需要立刻将它记录下来，以免它消失。

有许多商业软件和开源程序可以实现这些目标，记事本、白板、思维导图、知识图谱、大语言模型...。 

无论如何，我会：

- 发消息给 微信文件传输助手 记录今天应该买衣服和酱油
- 使用 iOS 提醒事项 / Microsoft TODO 记录要去给轮胎打气
- 深夜在某人的 微信聊天窗 写下明早要发的消息草稿
- 在 VSCode / Webstorm 中写 TODO 代码注释
- 使用 Obsidian / Blogs 记录学习笔记和调研报告
- 通过 Notion / 语雀 管理小组或团队的协作文档
- 使用 Writerside 写项目或 API 文档
- 使用 Excalidraw 画一个 GUI 的草图
- 打开 备忘录 / Sublime / Typora 记录即时的灵感
- 通过 AFFiNE / Project-Graph 来串联灵感
- 总结 prompt 让 ChatGPT 为我规划任务

为了更快、更丰富、更可关联、更可视化的需求，我不得不在某一时刻使用不同的程序，

我习惯了这些复杂的工作流，即使它们可能被遗忘，即使它们之间无法同步。

---

直到有天我发现：

- iOS 提醒事项 搁置了一年的 TODO
- 一份记录灵感的 Markdown 文件
- Excalidraw 被遗忘的超棒草图
- 微信聊天窗 未发送的消息，导致了没有帮朋友挽回 5 位数的投资亏损

我突然厌倦了辗转程序间的过程、广告、更新推送、订阅提示窗，还有为留存用户在 UI 中添加的各种 “霓虹招牌”，

我希望有个程序能更快、更纯粹，至少能解决深入我个人每一日的工作需求。

于是我找到了这个: [klaudiosinani/taskbook][taskbook-url]，并使用了一个月， 
刚开始一切都很完美，至少计划一个小目标、一个小程序时是这样。

但我很快便不满于现状：

- 无法同步数据，无法跨平台使用
- 无法复制任务模板，无法将任务列表聚焦于当日
- 不能创建多个 store
- 无法和 AI 很好的配合，无法快速查找某条任务或便签
- 每个 task 只有标题没有描述，编辑命令只能替换而无法使用原内容修改
- 只是一份串行的列表，我希望它可以 step by step 亦或是一个 tree 结构
- ...

这是当前仓库的目标，它的开发进度可能很慢，因为即使没有它，我们也能很好的完成***真正重要的工作***。

## 🟣 怎么做

### 核心目标 / 愿景

这个项目无法满足全部场景，我们反对商业化的超级 App 和围墙花园，从用户角度来讲它们根本没有必要存在，

但尽可能应该替代文本操作的部分。

---

### Packages

这应该是一个 monorepo 仓库，包含以下 packages：

- docs
- core
- cli
- web
- client
- app
- server
- locale

#### docs

**Option A**

Writerside 是快速实现很好的选择。

**Option B**

Vuepress 有很丰富的社区生态。

**Option C**

Rspress 有很好的工具链。

#### core

核心是数据结构与 Error Handler，GitHub 托管版本应该包含 FileSystem 操作和 Git 的功能组件。

#### cli

这是命令行程序。

需要编写许多 middleware (adapter) 来支持更多 AI Api，设计成 plugins 形式能有效减少 Installed Size。

比起 taskbook，还需要：

- GitHub 同步和文件托管 (Inspired by gopass)
- 多 jotter / book / store
- today 模式
- AI 拆解目标生成 steps / tasks / notes
- 渐进式的目标和当前任务的 AI 建议
- 数据结构 goal -> plan -> tree -> step
- 标题 / 标题 & 内容 多模式
- 使用默认编辑器修改项
- 快速复制
- 交互式文件管理组件
- 双向链接
- 截止日期 | Deadline
- 优先级排序
- 钉 | Pin
- 标签 | Label
- encrypt & decrypt 组件
- stream read & write 组件
- terminal timeline & calendar 组件
- i18n 组件

#### web

这不是必需的，File System Access API 可用受限，存在兼容性问题，无法复用 package:cli 代码，需要 API 上云。

Fallback 方案：Storage & IndexedDB

React / NextJS, Tailwind

部署：GitHub Page，考虑大陆网络还需要 Cloudflare 来代替 CDN 的部分。

#### client

这是 Desktop APP 的存储库。

**Option A**

Pake 可以利用 webview 复用 package:web 代码。

**Option B**

Tauri & NodeJS 可以利用 webview 和 cli 代码。

与高度使用 Storage 和 IndexedDB 的 Web 冲突，无法复用。

Fallback：上云

~~**Option C**~~

使用 Electron 逆向构建 Web，但可执行文件体积过大且 Web 支持有限...

#### app

这不是必需的，iOS, Android & WeApp

需要上云，地区政策，隐私协议，数字签名。

**Option A**

Flutter 的 Canvas 渲染能很好的支持各种机型，并且有很好的渲染性能，但不支持构建 WeApp。

**Option B**

TaroJS 是一个不错的选择，可以逆向构建 Web，和 H5 离线包的 WeApp，
但 App 端内置 ReactNative 多机型兼容性和渲染性能堪忧。

~~**Option C**~~

ReactNative，一旦有用户就会有一堆麻烦...

#### server

这不是必需的，但托管版本和同步功能版本是必不可少的。

K8s, Redis, NginxJS, NodeJS

**Option A**

NestJS GraphQL, PostgreSQL

**Option B**

Fastify, Prisma, SQLite

#### locale

这个包用来存储国际化文件，独立出来是为了更好的新增和维护，以及用户反馈和社区贡献。

由于 monorepo 的特性，Issues 会稍微难以管理，需要设置 Issue 分类和社区守则并提供相应模板。

---

### Flow

core -> cli -> docs -> locale ->

    Option A: Web -> Client -> Server -> App

    Option B: Server -> TaroJS (App / WeApp) -> Web -> Client

---

### CI / CD

这是一个开源项目，使用 GitHub Action。

## 🔵 是什么

TODO: 草图

[taskbook-url]: https://github.com/klaudiosinani/taskbook

[en-us-url]: README.md
[zh-cn-url]: README.zh-CN.md
