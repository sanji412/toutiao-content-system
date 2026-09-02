# Articles 字段指南

`articles.csv` 是文章计划与发布后表现的统一台账。每一行对应一个稳定的 `article_id`，并通过 `card_ids` 记录使用过的观点卡（多个 ID 用分号分隔）。

## 字段含义与允许值

- `article_id`：稳定文章标识，格式建议为 `ARTICLE-001`；创建后不要复用。
- `publish_date`：实际发布日期，使用 `YYYY-MM-DD`；未发布留空。
- `category`：沿用总纲四类：`money_life`、`family_relationships`、`human_social`、`career_wealth`。
- `core_conflict`：文章要解决的核心生活矛盾，用一句话写清。
- `card_ids`：关联的观点卡 ID；没有关联时留空。
- `title`：最终标题。
- `title_type`：只能是 `story`（故事型）、`counterintuitive`（反常识型）、`question`（问题型）、`benefit`（利益型）或 `restrained`（克制型）。其中：`story` 是已核验案例或明确标识的普遍场景的陈述句，不是问句，也绝不虚构个人；`counterintuitive` 是有边界的对比或纠偏，不作普遍断言；`question` 是明确问句；`benefit` 说明读者可获得的具体收获，不承诺结果；`restrained` 是不煽动的低强度观察或判断。
- `opening_type`：只能是 `verified_case`（已核实案例）、`public_data`（公开数据）或 `common_situation`（普遍生活处境）。
- `character_count`：只计算 `## 正文` 与 `## 备选标题` 之间的非空白正文文本，不计文章标题、元数据、Markdown 标记或来源包／文件说明；未完成时留空。
- `status`：只能是 `planned`（已计划）、`drafted`（已写草稿）、`published`（已发布）或 `retired`（退役）。
- `source_count`：文章使用的可追溯来源数量。
- `impressions_24h`、`reads_24h`、`reads_72h`、`click_rate_24h`、`avg_read_time_24h`、`completion_rate_24h`、`comments_24h`、`follows_24h`：发布后的平台表现。当前表记录完整可得的 24 小时指标集，以及 `reads_72h` 一项；它不声称记录完整的 72 小时指标集。头条没有等价指标时保持空白，不要用猜测值替代。
- `diagnosis`：根据数据做出的简短判断。
- `next_action`：下一轮标题、开头、选题或分发动作。

## 诊断规则

- 强曝光加弱阅读：检查标题与选题 framing。
- 强阅读加弱阅读时长：检查开头与内容交付。
- 阅读表现扎实加评论偏弱：内容有用，但可能情绪关联度偏低。
- 很多读者分享个人经历：说明真实生活共鸣强。
- 阅读量中等加关注强：说明账号定位匹配度强。

对应的英文速记规则：

- Strong impressions plus weak reads: inspect title and topic framing.
- Strong reads plus weak reading time: inspect opening and content delivery.
- Solid reading plus weak comments: useful but possibly low emotional relevance.
- Many readers sharing personal experiences: strong lived-life resonance.
- Moderate reads plus strong follows: strong account-positioning fit.

记录诊断时只根据实际平台数据，不将单篇表现外推成稳定规律。平台未暴露的性能字段保持空白。

## 30天汇总与决策

- 只在某个主栏目累计至少 5 篇文章后，才判断该栏目的表现；不足 5 篇时标记为样本不足，不作栏目优劣结论。
- 30 天结束时，使用平台实际可提供的指标，汇总并记录：表现最好的 2 个栏目、最有效的 3 种标题结构、最有效的 1 种文章结构，以及评论区反复出现的 3 个讨论问题。
- 决策前逐项核对：素材表中至少有 30 张未使用观点卡；每篇已发布文章都记录完整可得的 24 小时指标及可得的 `reads_72h`，而非假定存在完整 72 小时指标集；没有虚构案例；所有关键数据均可追溯到来源。
- 不设置固定的阅读量、曝光量或关注量阈值；判断必须结合可获得的平台指标、文章样本和评论质量。
- 如果没有清晰赢家，但选题、核验、写作和复盘流程稳定，延长测试 15 天后再决策。
- 只有在多个栏目持续偏弱，且评论显示读者与账号定位不匹配时，才重新考虑定位；单篇表现或单一指标不足以触发改定位。
- 只使用平台实际提供的指标；平台没有等价指标的字段保持空白，不用猜测值补齐。
