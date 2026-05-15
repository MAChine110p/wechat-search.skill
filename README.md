# wechat-search

**[English](#english) | [中文](#中文)**

---

<a name="english"></a>

# wechat-search (English)

> A Claude skill that automatically searches WeChat public accounts (微信公众号) alongside regular web searches for Chinese-language queries.

## What it does

When you ask Claude something in Chinese — or mention topics related to China — this skill kicks in automatically and runs **two searches in parallel**:

1. A regular web search
2. A WeChat public account search (`site:mp.weixin.qq.com`)

The results are presented in two separate sections, so you get both broad web coverage and the rich, in-depth content that WeChat public accounts are known for.

**Example output:**

```
### 网页搜索结果
...（普通搜索结果）

---

### 📱 微信公众号相关文章
- 文章标题 — 一句话摘要
- 文章标题 — 一句话摘要
- 文章标题 — 一句话摘要
```

## Why WeChat public accounts?

WeChat public accounts are a uniquely important source of Chinese-language content. Unlike open blogs or news sites, they host:

- Deep technical write-ups from practitioners
- Industry analysis and commentary not found elsewhere
- Chinese academic and professional discourse

Standard web searches often miss this content. This skill surfaces it automatically.

## Trigger conditions

The skill activates when **any** of the following is true:

| Condition | Example |
|---|---|
| Query contains Chinese characters | `大模型推理优化` |
| User mentions WeChat / public accounts | `微信上有没有相关文章` |
| Topic is China-related (even in English) | `latest news on Baidu AI` |

It does **not** trigger for pure English queries (e.g. searching GitHub, Stack Overflow, or English documentation).

## Installation

This skill is packaged as a `.skill` file for use with Claude's Skills system.

1. Download `wechat-search.skill` from the [Releases](../../releases) page
2. Open Claude (claude.ai or the Claude app)
3. Go to **Settings → Skills** and upload the `.skill` file
4. Claude will now automatically search WeChat public accounts for Chinese queries

## How it works under the hood

The implementation is intentionally simple — no external APIs or third-party dependencies required.

The skill instructs Claude to append `site:mp.weixin.qq.com` to the original query and fire it as a second `web_search` call in parallel with the regular search. The `site:` operator restricts results to WeChat's article domain (`mp.weixin.qq.com`), reliably returning real public account articles.

This approach was chosen over alternatives like Sogou WeChat Search because:
- It uses Claude's existing `web_search` tool directly — no extra integrations
- Results link directly to original articles on `mp.weixin.qq.com`
- No dependency on third-party platform availability

## File structure

```
wechat-search/
├── SKILL.md        # Skill definition and instructions for Claude
└── README.md       # This file
```

## License

MIT

---

<a name="中文"></a>

# wechat-search（中文）

> 一个 Claude Skill，在搜索中文内容时自动附加微信公众号文章搜索，将公众号结果作为独立区块呈现。

## 功能介绍

当你用中文向 Claude 提问，或涉及中国相关话题时，这个 skill 会自动触发，**并行执行两次搜索**：

1. 常规网页搜索
2. 微信公众号专项搜索（`site:mp.weixin.qq.com`）

两类结果分区块展示，让你同时获得广度覆盖的网页内容，以及公众号独有的深度专业内容。

**输出示例：**

```
### 网页搜索结果
...（普通搜索结果）

---

### 📱 微信公众号相关文章
- 文章标题 — 一句话摘要
- 文章标题 — 一句话摘要
- 文章标题 — 一句话摘要
```

## 为什么需要搜公众号？

微信公众号是中文互联网独树一帜的内容生态，与普通博客或新闻站点不同，它汇聚了大量：

- 来自一线从业者的深度技术文章
- 在其他平台难以找到的行业分析与评论
- 中文学术与职业圈的专业讨论

常规网页搜索往往触达不到这些内容，这个 skill 让 Claude 自动帮你补上这一环。

## 触发条件

满足以下**任意一个**条件即触发：

| 条件 | 示例 |
|---|---|
| 查询包含中文字符 | `大模型推理优化` |
| 用户明确提到微信 / 公众号 | `微信上有没有相关文章` |
| 话题涉及中国（即使用英文提问） | `latest news on Baidu AI` |

纯英文查询（如搜索 GitHub、Stack Overflow、英文文档等）**不触发**。

## 安装方法

本 skill 以 `.skill` 文件格式打包，适用于 Claude 的 Skills 系统。

1. 从 [Releases](../../releases) 页面下载 `wechat-search.skill`
2. 打开 Claude（claude.ai 或 Claude 客户端）
3. 进入 **设置 → Skills**，上传 `.skill` 文件
4. 完成！此后 Claude 在处理中文查询时会自动搜索微信公众号

## 实现原理

实现方式故意保持极简——无需任何外部 API 或第三方依赖。

skill 指示 Claude 在原始查询词后追加 `site:mp.weixin.qq.com`，与常规搜索并行发起第二次 `web_search` 调用。`site:` 限定符将结果限制在微信文章域名（`mp.weixin.qq.com`），可靠地返回真实公众号文章。

之所以选择这种方式而非搜狗微信搜索等方案，原因如下：
- 直接复用 Claude 现有的 `web_search` 工具，无需额外集成
- 结果直链指向 `mp.weixin.qq.com` 上的原文
- 不依赖第三方平台的可用性

## 文件结构

```
wechat-search/
├── SKILL.md        # Skill 定义文件，包含对 Claude 的指令
└── README.md       # 本文件
```

## 开源协议

MIT
