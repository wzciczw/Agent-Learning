# Agent Learning

> 可视化重要的 Agent 文章 —— 每篇文章配一份**中文精译**与**可视化理解图**（自包含 HTML，样式与 SVG 全部内联，可直接用浏览器打开）。

站点首页：https://wzciczw.github.io/Agent-Learning/

## 文章清单

| # | 文章 | 作者 | 日期 | 主题 | 可视化理解图 | 原文 |
| :-: | --- | --- | :-: | --- | :-: | :-: |
| 1 | Loop Engineering（循环工程） | Addy Osmani | 2026-06-07 | 循环工程 · Agent 编排 | [仓库文件](./loop-engineering-zh.html) · [在线预览](https://wzciczw.github.io/Agent-Learning/loop-engineering-zh.html) | [原文](https://addyosmani.com/blog/loop-engineering/) |
| 2 | Redesigning Source Control（在 Anthropic 重新设计源代码管理） | Anthropic 源代码管理团队 | 2026-10-13 | 源代码管理 · Scion · Monorepo 扩展 | [仓库文件](./redesigning-source-control-zh.html) · [在线预览](https://wzciczw.github.io/Agent-Learning/redesigning-source-control-zh.html) | [原文](https://www.anthropic.com/engineering/redesigning-source-control) |

> 后续每新增一篇，在上表追加一行，并把对应的 `*.html` 放在仓库根目录。

## 文章摘要

### 1. Loop Engineering（循环工程）· Addy Osmani

**一句话**：把「给智能体写提示的人」这个角色从你身上拿掉，改为由你设计那套替你写提示的系统。

**核心内容**：循环由五个部件 —— **自动化**（定时发现与分诊）、**工作树**（隔离并行任务）、**技能**（固化项目知识）、**插件与连接器**（接入真实工具）、**子智能体**（制造者与检查者分离）—— 外加一个落在磁盘上的**状态文件**组成。循环替代的只是「你逐步提示」这个动作；验证、理解债、认知投降这三件事仍然由人承担。

**可视化理解图包含**：
1. 全景理解图 —— 「你只设计一次 → 发现 / 分派 / 执行 / 校验 / 记录 → 回到起点」，以及底部的产出；
2. 五部件在 **Codex** 与 **Claude Code** 中的能力对照表；
3. 关键概念卡片 —— 意图债、理解债、认知投降、编排税。

### 2. Redesigning Source Control（在 Anthropic 重新设计源代码管理）· Anthropic 源代码管理团队

**一句话**：写代码不再是 Anthropic 的瓶颈——为「人类规模」设计的源代码管理、构建和 CI 才是。

**核心内容**：每日合并的代码变更从 2026 年 5 月的约 2,500 个涨到 9 月的 30,000 个以上；主分支历史接近 100 GB，压缩工作副本超过 25 GB，CI 每天要检出约 2,500 万次。团队自研版本控制系统 **Scion**，五个月内把 monorepo 从 git 完整迁走，基础设施占用（CPU + 内存）降到原先几百个内部 git 镜像方案的 **1/200**，检出快了两个数量级（分钟级 → 秒级），仅 CI 就释放出 25% 的 CPU 容量。文章给出四条核心设计原则 —— **客户端始终在线**、**客户端／服务端不对称**、**一切必须能水平扩展**、**提交必须便宜／增量／无锁**、**工作副本可有可无且天生稀疏** —— 以及 changeset + 派生数据的数据结构、分层缓存的检出架构，和四条可以搬回 git 的经验。

**可视化理解图包含**：
1. 全景理解图 —— 负载压力（100 GB 历史 / 25 GB 工作副本 / 2,500 万次检出 / 600 PB 流量）→ git 四个设计前提被逐个替换 → 五个月换来的结果；
2. 检出链路分层缓存图 —— `scn` 客户端 / `scion-daemon` / `scion-cache` / `scion-server` 四层与 Spanner、云存储的关系；
3. 原文 6 张图表按原文顺序保留。

**为什么重要**：这是目前少见的、把「AI agent 规模化写代码之后，开发基础设施会在哪里先断」讲清楚的工程复盘，并且明确指出了哪些部分可以搬回 git。

## 新增一篇文章的流程

1. **翻译**：用本地 `baoyu-translate` 技能产出中文精译，并过一遍 `markup_fidelity.py` 标记保真门禁（超链接、图片、加粗、脚注标记不得静默丢失）。
2. **判断重要性**：翻译完成后先判断这篇文章是否值得收录（是否触及 agent 工程的关键议题、是否有一手工程细节、是否会被反复引用）。
3. **征询同意**：若判断为重要，先向用户询问，获得同意后再上传；不擅自发布。
4. **独立检查与润色**：正式上传前，单独做一遍逐段对照原文的复核 —— 术语一致性、错别字、标点与空格、长句可读性、标题层级与图注质量。
5. **打包**：按仓库约定生成自包含 HTML 放在仓库**根目录**，补 1–2 张手写内联 SVG 理解图，并同步更新上表、文章摘要与下方目录树。
6. **发布**：推送到 `main` 分支，触发 GitHub Pages 重新构建，并回访线上页面确认排版正常。

## 目录结构

```
.
├── index.html                              # Pages 站点首页（文章画廊）
├── loop-engineering-zh.html                # 《Loop Engineering》中文精译 + 可视化理解图
├── redesigning-source-control-zh.html      # 《Redesigning Source Control》中文精译 + 可视化理解图
├── README.md                               # 本文件
└── .gitignore
```

## 阅读方式

- **仓库内**：点击上表「仓库文件」链接查看源码，或下载后双击用浏览器打开。
- **在线预览**：点击「在线预览」链接，由 GitHub Pages 渲染，排版与图更完整（GitHub 页面本身只会把 `.html` 当源码显示）。

## 出处与版权

各篇文章的著作权归原作者所有，本仓库仅提供中文翻译与可视化整理，供学习参考。每篇文章页面底部均标注了原文标题、作者、日期与原文链接。
