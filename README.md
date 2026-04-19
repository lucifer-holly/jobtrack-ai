# 🎯 JobTrack AI · 校招求职管理看板

> AI 原生的校招投递管理工具 · 作品集 by [@lucifer-holly](https://github.com/lucifer-holly)

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-blue?style=flat-square&logo=github)](https://lucifer-holly.github.io/jobtrack-ai/)
[![Tech](https://img.shields.io/badge/Stack-React%20%2B%20Tailwind-38b2ac?style=flat-square&logo=react)](#)
[![AI](https://img.shields.io/badge/AI-GLM%2BGemini-10b981?style=flat-square)](#)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](#)

## 📖 背景

2026 校招季,我手头同时在投 20+ 家公司,用 Excel 管理 Offer、截止日期、面试时间已经不够用了。
所以花了 48 小时从零做了这个——**第一个用户就是我自己**。

这也是我在准备 AI 产品经理岗位时的思考练习:**不是把 AI 塞进一个已有产品,而是找到用户真实痛点后,识别哪里能用 AI 带来 10 倍效率提升**。

## ✨ 核心功能

### 🗂️ 三视图工作流
- **看板视图**:拖拽式 Kanban,6 个投递状态(待投/已投/笔试/面试/Offer/已截止),支持赛道与紧急度多维度筛选
- **日历视图**:可视化截止日期,再也不会错过任何 DDL
- **数据分析**:4 个 KPI + 投递漏斗 + 赛道分布 + 城市/状态分析

### 🤖 双引擎 AI Copilot
基于真实投递场景设计的 3 个 AI 助手:

| 功能 | 描述 |
|-----|------|
| **JD 智能解析** | 粘贴岗位 JD,自动提取公司/薪资/核心要求/关键词 |
| **简历匹配度评分** | 基于你的简历和岗位要求,输出匹配分数 + 优势 + 缺口分析 |
| **面试题预测** | 根据 JD 生成 10 道高频面试题及回答思路 |

**双 AI 引擎架构**:默认 **智谱 GLM-4-Flash**(国内稳定免费),可切换 **Google Gemini 2.5 Flash**(需代理网络)。
网络异常时会自动提示切换引擎,体现**产品视角的错误处理**。

### 📬 邮箱智能归类(Beta)
交互式原型:OAuth 授权流程 → 同步动画 → AI 自动识别招聘邮件并关联到对应岗位。
**诚实的边界标注**:这是交互原型,不是真接入。**这本身就是一个产品决策**。

### 🎨 设计亮点
- **加载骨架屏**:首屏立即展示 Logo 和加载进度,把"白屏焦虑"转化为"有序等待"
- **Linear / Notion 风格**:翡翠绿 + 亮蓝渐变,克制的阴影,现代化圆角
- **流畅动画**:Fade-in 卡片、呼吸 FAB、shimmer 按钮、拖拽高亮

## 🏗️ 技术栈

```
Frontend : React 18 + Tailwind CSS (单文件零构建)
AI       : 智谱 GLM-4-Flash + Google Gemini 2.5 Flash
Storage  : LocalStorage (用户数据不出浏览器)
Host     : GitHub Pages / Cloudflare Pages
```

**关键技术决策**:
- **单 HTML 文件架构**:零构建、零后端、一键分享,符合"48 小时 MVP"约束
- **统一 AI Dispatcher** (`callAI(provider, ...)`):上层业务不感知模型差异,这是**适配器模式**在 AI 产品里的应用
- **LocalStorage 隐私优先**:API Key 和简历只存在用户本地,不上传任何服务器

## 🚀 在线体验

**Live Demo**: [https://lucifer-holly.github.io/jobtrack-ai/](https://lucifer-holly.github.io/jobtrack-ai/)

> ⚠️ **AI 功能体验须知**:由于安全原因,GitHub Pages 版本**不预置 API Key**。想完整体验 AI 功能:
> 1. 打开右上角 ⚙ **设置**
> 2. 填入 GLM API Key(免费申请:[智谱 AI 开放平台](https://open.bigmodel.cn/))
> 3. 保存后即可使用所有 AI 功能
>
> 所有输入仅存储在你的浏览器本地,不上传任何服务器。

## 🧠 产品思考过程

### 为什么做看板而不是列表?
校招投递是强状态流转的业务——每个岗位都在 `待投 → 已投 → 笔试 → 面试 → Offer` 之间动。
**Kanban 是表达流转的最佳 UI 范式**,一眼看出瓶颈(比如"已投" 列堆了 20 个说明简历筛选通过率低)。

### 为什么做双 AI 引擎?
我是真实用户,我知道 Gemini 在国内网络不稳定。
但 Gemini 在某些推理任务上更强。所以我做了切换 + 自动降级提示——
**这不是把模型列表曝露给用户那么简单,而是基于对用户网络环境的真实理解**。

### 为什么邮箱只做 UI 不做后端?
这是有意的产品决策,展示四个维度:
1. **用户洞察**——求职邮件散落 300 封里是真痛点
2. **产品完整度**——完整的用户旅程,不是加个登录框了事
3. **工程可行性**——OAuth/IMAP/分类模型都想清楚了
4. **职业诚信**——每一屏都明确标注"Beta / 演示数据",不伪装可用

## 💡 可以聊的细节(欢迎面试官提问)

- [ ] 为什么选 GLM-4-Flash 作为默认?国内直连 + 免费 + OpenAI 兼容格式
- [ ] 错误处理如何做产品化?检测 CORS/网络错误 → 一键切引擎按钮
- [ ] 为什么用 LocalStorage 不用后端?48 小时约束 + 隐私优先,但加载时间 <100ms
- [ ] Tailwind CDN 为什么不换国内镜像?`cdnjs` 的 Tailwind 是静态版,不支持我的 `tailwind.config` 自定义主题
- [ ] 如果做成生产级产品,会怎么改?SSR(Next.js) + 国内云服务 + 后端数据同步 + 接入真实邮箱 OAuth

## 📂 文件结构

```
jobtrack-ai/
├── index.html          # 单文件应用 (3300+ 行, React + Tailwind)
└── README.md           # 你正在看的这个
```

## 📝 License

MIT License — 欢迎自用、改造、借鉴。
