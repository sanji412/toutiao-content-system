# Materials 字段指南

`materials.csv` 是观点卡的规范台账和结构化索引。每一行代表一个可追溯的外部材料，`card_id` 是稳定主键，供选题、文章和复盘表关联；Markdown 卡仅作可读详情，状态和关联以本表为准。

## 字段含义

- `card_id`：观点卡稳定标识，格式建议为 `CARD-001`；创建后不要复用。
- `source_author`：来源作者。初始种子批次只允许 `Morgan Housel` 或 `Sahil Bloom`。
- `source_title`：原文标题；未完成核验时可明确写“作者公开文章入口”，不要猜测标题。
- `source_url`：可回溯的原文或作者公开入口链接。
- `source_date`：原文发布日期；查不到就留空，不用推定日期。
- `collected_date`：团队实际收集日期，使用 `YYYY-MM-DD`。
- `core_claim`：用自己的话概括核心观点，不写未经核验的引语。
- `mechanism`：解释观点如何发生、通过什么因果链影响生活。
- `evidence_summary`：案例、数据或研究的简短出处摘要；关键证据必须可追溯。
- `fact_vs_opinion`：区分已核实事实与作者判断。
- `counterexample_boundary`：反例、限制条件和不适用场景。
- `china_context`：可落到中国普通人生活的具体场景，不能把海外经验直接当作中国事实；这里只能写用于选题的示例性映射，不能冒充已核验的真实生活案例。
- `verification_status`：只能是 `unreviewed`（尚未核验）、`partial`（部分核验）或 `verified`（关键来源与事实已核验）。
- `category`：只能是 `money_life`（钱与普通人的生活）、`family_relationships`（家庭与人情）、`human_social`（人性与社会生活）或 `career_wealth`（职场与财富规律）。
- `status`：只能是 `unused`（未使用）、`planned`（已计划）、`drafted`（已写草稿）、`published`（已发布）或 `retired`（退役）。
- `used_article_id`：若已用于文章，填对应的 `article_id`；一张卡用于多篇真正不同的文章时，用 `|` 分隔多个 ID；否则留空。
- `notes`：核验记录、缺口和后续动作。

## 录入规则

先记录来源，再提炼观点；重要事实在 `verification_status` 变为 `verified` 前不得作为确定结论发布。CSV 文本不得包含虚构的引号或无依据的精确数字；无法确认的内容留空并在 `notes` 标明待核实。

## 操作生命周期

**使用已有卡：**只从状态为 `unused` 的已有卡开始，不生成重复卡；写作推进时更新为 `unused → planned → drafted → published`，并链接文章 ID。已使用卡仍可用于真正不同的文章，但不再计入未使用库存。

**录入新来源：**先打开直接来源，使用下一个连续 `CARD-NNN`，在 `cards/seed-cards.md`（或后续卡片文件）追加一张 Markdown 卡，并在本 CSV 新增一行；然后再进入相同生命周期。

首四周每周至少补充 9 张 `verified` 或 `partial` 的新卡。`partial` 卡不得把未核验事实作为确定结论发布；补卡目标用于维持来源库存，并不要求每篇文章消耗一张不同的卡。
