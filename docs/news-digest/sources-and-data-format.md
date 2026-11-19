# 每日资讯摘要：资讯源清单与统一数据格式约定

> 本文档是「每日资讯摘要」功能的**第一份交付物**，供后续「抓取」与「渲染」任务直接读取。它回答两件事：
> 1. 从哪里抓（资讯源清单）；
> 2. 抓下来的数据长什么样（统一数据格式约定）。
>
> 后续任务应以此为准，不要再各自重新调研或发明格式。

---

## 一、背景与目标

用户想要一个**每日资讯摘要页**：抓取两个话题的最新资讯，生成一个**排版好的单文件 HTML 日报**，能在项目文件页直接阅读，之后可设成每天自动重跑。

固定约束（用户已确认）：

| 约束 | 说明 |
| --- | --- |
| 话题 | **AI / 大模型**、**财经商业**，共两个话题 |
| 数量 | 每话题约 **8–10 条** |
| 单条字段 | 标题、摘要、来源、时间、链接 |
| 语言呈现 | 日报**中文呈现**；资讯来源中英均可 |
| 来源限制 | 只用**免费公开的订阅源（RSS/Atom）**，不引入任何 API 密钥 |

本文档只约定「资讯源 + 数据格式」。抓取脚本、HTML 渲染、定时调度属于后续任务。

---

## 二、资讯源清单

### 2.1 话题一：AI / 大模型

| # | 来源 | RSS 地址 | 格式 | 语言 | 验证状态 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Hacker News（AI 搜索） | `https://hnrss.org/newest?q=AI` | RSS 2.0 | en | ✅ 已验证 | 社区投稿聚合，更新极快，适合发现热点 |
| 2 | MIT Technology Review（AI） | `https://www.technologyreview.com/topic/artificial-intelligence/feed` | RSS 2.0 | en | ✅ 已验证 | 深度科技报道 |
| 3 | The Verge（AI） | `https://www.theverge.com/rss/ai-artificial-intelligence/index.xml` | Atom | en | ✅ 已验证 | 科技媒体 AI 专区 |
| 4 | Google（AI 博客） | `https://blog.google/technology/ai/rss/` | RSS 2.0 | en | ✅ 已验证 | 官方产品与研究成果 |
| 5 | OpenAI（News） | `https://openai.com/news/rss.xml` | RSS 2.0 | en | ✅ 已验证 | 官方公告 |
| 6 | Hugging Face（Blog） | `https://huggingface.co/blog/feed.xml` | RSS 2.0 | en | ✅ 已验证 | 开源模型生态 |
| 7 | arXiv（cs.AI） | `https://export.arxiv.org/rss/cs.AI` | RSS 2.0 | en | ✅ 已验证 | 论文预印本，偏学术 |
| 8 | TechCrunch（AI） | `https://techcrunch.com/category/artificial-intelligence/feed/` | RSS 2.0 | en | ✅ 已验证 | 创投视角 AI 新闻 |
| 9 | 机器之心 | `https://www.jiqizhixin.com/rss` | RSS 2.0 | zh | ⚠️ 本机未验证 | 中文 AI 头部媒体，见 2.4 说明 |
| 10 | 量子位 | `https://www.qbitai.com/feed` | RSS 2.0 | zh | ⚠️ 本机未验证 | 中文 AI 媒体，见 2.4 说明 |
| 11 | 爱范儿 ifanr | `https://www.ifanr.com/feed` | RSS 2.0 | zh | ✅ 已验证 | 中文科技媒体，含 AI 内容 |
| 12 | IT之家 | `https://www.ithome.com/rss/` | RSS 2.0 | zh | ✅ 已验证 | 中文科技媒体，更新快 |

### 2.2 话题二：财经商业

| # | 来源 | RSS 地址 | 格式 | 语言 | 验证状态 | 备注 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | MarketWatch（Dow Jones） | `https://feeds.content.dowjones.io/public/rss/mw_topstories` | RSS 2.0 | en | ✅ 已验证 | 综合财经要闻 |
| 2 | Dow Jones（Markets） | `https://feeds.a.dj.com/rss/RSSMarketsMain.xml` | RSS 2.0 | en | ✅ 已验证 | 市场动态 |
| 3 | Business Insider | `https://www.businessinsider.com/rss` | Atom | en | ✅ 已验证 | 商业与科技报道 |
| 4 | BBC（Business） | `http://feeds.bbci.co.uk/news/business/rss.xml` | RSS 2.0 | en | ✅ 已验证 | 国际商业新闻 |
| 5 | The Guardian（Business） | `https://www.theguardian.com/uk/business/rss` | RSS 2.0 | en | ✅ 已验证 | 商业报道 |
| 6 | Forbes（Business） | `https://www.forbes.com/business/feed/` | RSS 2.0 | en | ✅ 已验证 | 商业财经 |
| 7 | Fortune | `https://fortune.com/feed/` | RSS 2.0 | en | ✅ 已验证 | 商业财经 |
| 8 | The Economist（Business） | `https://www.economist.com/business/rss.xml` | RSS 2.0 | en | ✅ 已验证 | 深度商业分析 |
| 9 | CNBC（Top News） | `https://www.cnbc.com/id/10001147/device/rss/rss.html` | RSS 2.0 | en | ✅ 已验证 | 财经要闻 |
| 10 | 36氪 | `https://36kr.com/feed` | RSS 2.0 | zh | ⚠️ 本机未验证 | 中文创投财经，见 2.4 说明 |
| 11 | 虎嗅 | `https://www.huxiu.com/rss/0.xml` | RSS 2.0 | zh | ⚠️ 本机未验证 | 中文商业科技，见 2.4 说明 |

### 2.3 源分级（抓取时的取用顺序）

每个话题都提供远超 8–10 条的候选。抓取任务按以下优先级取用，凑满每话题 8–10 条即止（去重后）：

- **首选源**（稳定、更新及时，优先抓取）：上表中 ✅ 已验证的英文源 + 已验证中文源（AI：爱范儿、IT之家；财经：无已验证中文源）。
- **补充源**（备选，用于凑数或补中文）：机器之心、量子位、36氪、虎嗅。这些源在本机构建机上因 TLS 阻断无法验证（见 2.4），需在抓取机上先验证再启用。
- **话题匹配**：验证过的中文源（爱范儿、IT之家）是「科技综合」而非纯 AI/财经，抓取时需按关键词过滤（见 4.2）。

### 2.4 验证与选择说明

- 上表所有 ✅ 源均在构建机实测：HTTP 200 且返回合法 XML（RSS 2.0 或 Atom）。
- ⚠️ 源（机器之心、量子位、36氪、虎嗅、以及少数派、极客公园、InfoQ 中文等）在本机构建机返回 TLS 握手失败（`unexpected eof`），判断为地理/TLS 限制，**并非源失效**。它们仍是中文内容的重要候选，抓取任务应在目标运行机上先验证再启用。
- 已确认失效、不采用的源：Yahoo Finance 旧 RSS（`rssindex` 返回 404，已下线）、Bloomberg / FT / WSJ（无免费公开 RSS，均需订阅）。
- 全部来源均为**免费公开订阅源**，无需任何 API 密钥。

---

## 三、统一数据格式约定

抓取任务产出一份 JSON，渲染任务消费同一份 JSON。格式版本为 `1.0`。

### 3.1 顶层结构：日报 `DailyDigest`

```jsonc
{
  "version": "1.0",              // 固定，格式版本号
  "date": "2026-11-19",          // 日报日期，YYYY-MM-DD
  "generatedAt": "2026-11-19T08:00:00Z", // 生成时间，ISO 8601（UTC）
  "topics": [
    {
      "key": "ai",               // 话题键：ai | finance
      "label": "AI / 大模型",     // 中文话题名，用于页面标题
      "items": [ /* NewsItem，8–10 条 */ ]
    },
    {
      "key": "finance",
      "label": "财经商业",
      "items": [ /* NewsItem，8–10 条 */ ]
    }
  ]
}
```

### 3.2 单条资讯 `NewsItem`

| 字段 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `id` | string | ✅ | 稳定唯一标识，全日报内唯一。建议 `source + guid` 的哈希（见 4.3） |
| `topic` | `"ai" \| "finance"` | ✅ | 所属话题键 |
| `title` | string | ✅ | 原始标题，保留源语言 |
| `titleZh` | string | ⬜ | 中文标题。源为英文时，翻译后的中文标题 |
| `summary` | string | ✅ | **中文摘要**，纯文本、无 HTML，约 80–160 字。英文源需翻译/改写为中文 |
| `source` | string | ✅ | 来源名称，用上表「来源」列的固定名称（如 `The Verge`、`机器之心`） |
| `sourceUrl` | string(URL) | ⬜ | 来源主页，便于页面加来源链接 |
| `url` | string(URL) | ✅ | 原文链接，用户点击跳转 |
| `publishedAt` | string(ISO 8601) | ✅ | 发布时间，含时区或 UTC，如 `2026-11-18T18:18:35-05:00` |
| `fetchedAt` | string(ISO 8601) | ✅ | 抓取时间，UTC，如 `2026-11-19T08:00:00Z` |
| `language` | `"zh" \| "en"` | ✅ | 原文语言 |
| `author` | string | ⬜ | 作者（源提供时保留） |
| `imageUrl` | string(URL) | ⬜ | 封面图（源提供时保留，渲染可选用） |

约定：

- `title` 始终保留**原文**；`titleZh` 是英文源的翻译，中文源可省略。
- `summary` **统一为中文**——这是「日报中文呈现」的落点。英文源的摘要由抓取任务翻译或改写，不得直接粘贴英文原文。
- 时间一律用 **ISO 8601**，优先带时区；排序、去重时内部统一折算成 UTC 比较。
- `summary` 必须是**纯文本**，抓取时要剥掉 RSS `description` 里可能夹带的 HTML 标签与实体。

### 3.3 zod Schema（权威定义）

以下 zod 定义是字段与类型的**权威来源**，与上表一致；后续任务若在本仓库内实现，直接复用此 schema。

```ts
import { z } from "zod";

export const TopicKey = z.enum(["ai", "finance"]);

export const NewsItemSchema = z.object({
  id: z.string(),
  topic: TopicKey,
  title: z.string(),
  titleZh: z.string().optional(),
  summary: z.string(),
  source: z.string(),
  sourceUrl: z.string().url().optional(),
  url: z.string().url(),
  publishedAt: z.string().datetime({ offset: true }),
  fetchedAt: z.string().datetime({ offset: true }),
  language: z.enum(["zh", "en"]),
  author: z.string().optional(),
  imageUrl: z.string().url().optional(),
});

export const DailyDigestSchema = z.object({
  version: z.literal("1.0"),
  date: z.string(), // YYYY-MM-DD
  generatedAt: z.string().datetime({ offset: true }),
  topics: z.array(
    z.object({
      key: TopicKey,
      label: z.string(),
      items: z.array(NewsItemSchema).min(8).max(10),
    }),
  ),
});

export type NewsItem = z.infer<typeof NewsItemSchema>;
export type DailyDigest = z.infer<typeof DailyDigestSchema>;
```

### 3.4 示例 JSON

```json
{
  "version": "1.0",
  "date": "2026-11-19",
  "generatedAt": "2026-11-19T08:00:00Z",
  "topics": [
    {
      "key": "ai",
      "label": "AI / 大模型",
      "items": [
        {
          "id": "a1b2c3d4e5",
          "topic": "ai",
          "title": "The nation's largest school districts consider ditching Google Search",
          "titleZh": "美国最大几个学区考虑弃用谷歌搜索",
          "summary": "据 The Verge 报道，美国多个大型学区正在评估停止在课堂上使用谷歌搜索，转向其他方案。",
          "source": "The Verge",
          "sourceUrl": "https://www.theverge.com",
          "url": "https://www.theverge.com/ai-artificial-intelligence/1037151/school-districts-ditching-google",
          "publishedAt": "2026-11-18T18:18:35-05:00",
          "fetchedAt": "2026-11-19T08:00:00Z",
          "language": "en",
          "author": "Terrence O'Brien",
          "imageUrl": "https://platform.theverge.com/wp-content/uploads/sites/2/2025/01/verge-rss-large_80b47e.png"
        }
      ]
    },
    {
      "key": "finance",
      "label": "财经商业",
      "items": [
        {
          "id": "f6e7d8c9b0",
          "topic": "finance",
          "title": "Global markets rally as inflation cools",
          "titleZh": "通胀降温，全球市场反弹",
          "summary": "最新通胀数据低于预期，全球主要股指普遍上涨，市场对降息的预期升温。",
          "source": "BBC",
          "sourceUrl": "https://www.bbc.com",
          "url": "https://www.bbc.com/news/business-example",
          "publishedAt": "2026-11-19T02:00:00Z",
          "fetchedAt": "2026-11-19T08:00:00Z",
          "language": "en"
        }
      ]
    }
  ]
}
```

---

## 四、抓取与清洗约定

### 4.1 抓取

- 按 2.3 的源分级抓取，每话题目标 **8–10 条**（去重后）。
- 抓取全部首选源通常即足够；不足时启用补充源。
- 每源抓取最近约 1–2 天的条目即可，避免旧闻。
- 请求带常见的浏览器 `User-Agent`；个别源（如 VentureBeat）会限流，失败重试一次、间隔数秒。

### 4.2 话题匹配与过滤（针对「科技综合」中文源）

爱范儿、IT之家等综合源需按关键词过滤后归类：

- **AI / 大模型**：`AI`、`人工智能`、`大模型`、`LLM`、`GPT`、`OpenAI`、`ChatGPT`、`机器学习`、`深度学习`、`生成式` 等。
- **财经商业**：`财经`、`商业`、`公司`、`市场`、`股价`、`融资`、`上市`、`财报`、`经济`、`央行`、`利率` 等。

关键词不匹配的条目丢弃，不进入该话题。

### 4.3 去重

- 优先用源提供的 `guid`/`id`；无则用 `url` 归一化（去 `utm_*` 参数、去尾部 `#`、统一 https）后作唯一键。
- 同一链接被多个源报道时，保留 `publishedAt` 最新或来源优先级最高的一条，其余丢弃。
- `id` 取 `来源名 + 唯一键` 的稳定哈希（如 SHA-1 前 10 位），保证日报内唯一且跨日稳定。

### 4.4 排序与截断

- 每话题内按 `publishedAt` 降序（最新在前）。
- 去重后若超过 10 条，截断到 10 条；若不足 8 条，按优先级扩源补齐。

### 4.5 中文呈现与翻译约定

- 页面骨架、话题标题、来源标签一律中文。
- 英文源条目：`titleZh`（翻译标题）+ 中文 `summary` 必填；`title` 保留原文。
- 中文源条目：`titleZh` 省略，`summary` 可直接沿用原文或缩写。

---

## 五、给后续任务的接口约定

本功能拆成两个后续任务，本文档是它们的共同契约：

1. **抓取任务**：读取本文档第二、三、四节，抓取各源并产出 JSON 文件，建议路径 `daily-digest/<date>.json`，内容符合 `DailyDigestSchema`。
2. **渲染任务**：读取本文档第三节，消费该 JSON，生成**单文件 HTML** 日报（建议路径 `daily-digest/<date>.html`），样式内联或随页自包含，满足在项目文件页直接阅读、可直接交给浏览器打开。

定时自动重跑（每天定时触发抓取 + 渲染）在二者完成后另行接入调度。
