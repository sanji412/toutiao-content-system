# 今日头条内容工具包

这是一个围绕“用真实故事讲清金钱背后的人性，帮助普通人做出更清醒的生活选择”的30天内容工作台。四个栏目分别是：钱与普通人的生活、家庭与人情、人性与社会生活、职场与财富规律。

## 第一次使用

1. 阅读 [editorial-brief.md](editorial-brief.md)。
2. 打开 [topics/week-1-board.md](topics/week-1-board.md)。
3. 把一个选题复制到 [templates/prompts.md](templates/prompts.md) 的四个提示词阶段。
4. 按“素材卡生命周期”选择已有卡或录入新来源，并更新 [data/materials.csv](data/materials.csv)。
5. 应用 [templates/daily-release-checklist.md](templates/daily-release-checklist.md)。
6. 发布后，在 [data/articles.csv](data/articles.csv) 记录完整可得的24小时指标，以及仅有的72小时阅读量。
7. 每周完成一次 [templates/weekly-review.md](templates/weekly-review.md)。

## 每日20～30分钟
1. 准备3个候选，确定1个；候选可以是 `materials.csv` 中已有的 `unused` 卡，也可以是尚未入库的新来源。
2. 按来源分支处理：
   - 已有卡：直接使用现有卡，不再生成重复观点卡。
   - 新来源：先打开直接来源，再用观点蒸馏提示词制作卡片；分配下一个连续的 `CARD-NNN`，并同时录入 [cards/seed-cards.md](cards/seed-cards.md)（或后续卡片文件）与 [data/materials.csv](data/materials.csv)。
3. 用中国化研究提示词查找2～4个来源。
4. 人工打开并核对关键来源。
5. 用写作提示词生成初稿和5个标题。
6. 用独立审稿提示词审查。
7. 人工执行发布检查表。
8. 发布后记录24小时和72小时表现。

## 素材卡生命周期

`materials.csv` 是素材卡状态和文章关联的唯一基准。卡片可复用于真正不同的文章，但已使用过的卡不再计入“未使用”库存。

### 路径一：使用已有卡

从 `materials.csv` 选择一张状态为 `unused` 的现有卡，不生成重复卡；随写作推进将状态依次更新为 `unused → planned → drafted → published`，并在 `used_article_id` 填入关联的文章 ID。若一张已使用卡确实用于多篇不同文章，用 `|` 分隔多个文章 ID；它可以复用，但不再算作 `unused`。

### 路径二：录入新来源

先人工打开直接来源并完成核验；使用下一个连续的 `CARD-NNN` 编号，在 [cards/seed-cards.md](cards/seed-cards.md)（或后续卡片文件）追加一张 Markdown 卡，并在 `materials.csv` 新增一行。随后进入同一条 `unused → planned → drafted → published` 生命周期。

前四周每周至少补充 9 张新卡（已核验或部分核验均可，但状态与核验边界必须如实记录）。试点后仍有 19 张未使用卡，这一节奏足以支撑首轮运行，并在第 30 天复盘时仍以至少 30 张未使用卡为目标；文章不要求一篇只消耗一张卡。

## 每周15分钟
1. 找出最好2篇和最差2篇。
2. 分别诊断选题、标题、开头和正文。
3. 从高共鸣评论中选择下周问题。
4. 每次只改变一个变量。

## 发布前整理净稿

确定一个最终标题后，只复制文章正文用于发布；不要复制内部元数据、备选标题、Markdown 反引号包住的文件引用或审稿备注。保留的证据标记须在人工重新打开来源后，改写为读者可理解的自然来源说明；来源包和审计记录仍保留在工具包内，用于追溯。

## 指标记录范围

当前追踪表记录完整可得的 24 小时指标集，并只记录 `reads_72h`；这不表示拥有完整的 72 小时指标集。头条未提供等价指标时，对应字段保持空白。

## 文件索引

### 开始与编辑规则

- [README：开始页](README.md)
- [编辑总纲](editorial-brief.md)

### 模板与提示词

- [观点卡模板](templates/idea-card.md)
- [AI提示词库：四阶段流程](templates/prompts.md)
- [每日发布检查表：绿／黄／红灯](templates/daily-release-checklist.md)
- [每周复盘模板](templates/weekly-review.md)

### 数据表与字段说明

- [素材追踪表](data/materials.csv)
- [素材追踪表字段说明](data/materials-field-guide.md)
- [文章表现追踪表](data/articles.csv)
- [文章表现追踪表字段说明](data/articles-field-guide.md)

### 来源卡与选题

- [20张来源观点卡](cards/seed-cards.md)
- [30天选题库：24个主选题＋12个备用选题](topics/30-day-topic-bank.md)
- [第一周执行板](topics/week-1-board.md)

### 端到端试点示例

- [试点来源包](examples/pilot-source-pack.md)
- [试点六段式提纲](examples/pilot-outline.md)
- [试点文章与五种标题](examples/pilot-article.md)
- [试点审稿与发布审计](examples/pilot-audit.md)
- [ARTICLE-001 v2 成品](examples/pilot-article-v2.md) 与 [v2 审稿记录](examples/pilot-audit-v2.md)

### 生产文章草稿（按篇归档）

- [ARTICLE-002：全家一起休息先排进周末](articles/ARTICLE-002/article.md)，含[来源包](articles/ARTICLE-002/source-pack.md)、[提纲](articles/ARTICLE-002/outline.md)与[审稿记录](articles/ARTICLE-002/audit.md)。
- [ARTICLE-003：成绩出来那天，谈话不只围着分数](articles/ARTICLE-003/article.md)，含[来源包](articles/ARTICLE-003/source-pack.md)、[提纲](articles/ARTICLE-003/outline.md)与[审稿记录](articles/ARTICLE-003/audit.md)。
- 后续文章沿用 `articles/ARTICLE-NNN/` 目录结构。
