# Toutiao AI Content System Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a ready-to-use, 30-day content operating kit for a Toutiao account about wealth, human nature, and everyday social life.

**Architecture:** The system is deliberately file-based and lightweight: one editorial brief controls positioning, CSV files track source cards and published articles, reusable Markdown prompts drive four separate AI stages, and a topic bank plus pilot article prove the workflow end to end. X posts and essays are treated only as idea seeds; every publishable article requires independent Chinese context, verifiable evidence, and a human release decision.

**Tech Stack:** Markdown, UTF-8 CSV, one web-enabled AI assistant, a browser for source verification, X bookmarks/lists, and Toutiao creator analytics. No API, database, paid automation, or custom application is required for the first 30 days.

## Global Constraints

- Core audience: Chinese readers aged 30–55; secondary audiences are working adults aged 25–40 and readers aged 35–60 interested in wealth principles.
- Positioning: “用真实故事讲清金钱背后的人性，帮助普通人做出更清醒的生活选择。”
- Voice: calm, restrained, plainspoken, insightful, and non-preachy.
- Publishing cadence: one article per day, five to six articles per week, for an initial 30-day test.
- Human time budget: 20–30 minutes per daily article.
- Article length: approximately 1,600–2,200 Chinese characters.
- Content mix for the first 24 articles: 10 money/everyday-life, 6 family/relationships, 6 human-nature/social-life, and 2 career/wealth-principles.
- Never fabricate first-person experiences, friends, colleagues, named characters, statistics, studies, or quotations.
- Never translate, paraphrase line by line, combine, or imitate the distinctive wording and full narrative structure of Morgan Housel or Sahil Bloom.
- Exclude political commentary, stock recommendations, market predictions, guaranteed returns, and unqualified medical or legal advice.
- Every consequential factual claim must have a traceable source; unsupported material is removed rather than completed by AI.
- Every publishable article includes Chinese lived context and at least one limitation, counterexample, or boundary condition.
- The current workspace is not a Git repository. Do not initialize one without explicit user authorization; use file-level checkpoints and verification output instead of commits.

---

## Deliverable Map

All user-facing files will live under `outputs/toutiao-content-kit/`.

- `README.md`: start-here guide and daily operating sequence.
- `editorial-brief.md`: audience, positioning, voice, columns, exclusions, and article structure.
- `templates/idea-card.md`: one reusable source-distillation card.
- `templates/prompts.md`: fixed project instruction plus four stage prompts.
- `templates/daily-release-checklist.md`: green/yellow/red release gate.
- `templates/weekly-review.md`: 15-minute weekly diagnosis and decision form.
- `data/materials.csv`: source-card and usage tracker.
- `data/materials-field-guide.md`: allowed values and field definitions.
- `data/articles.csv`: publishing and performance tracker.
- `data/articles-field-guide.md`: metric definitions and diagnostic rules.
- `cards/seed-cards.md`: first 20 source-linked idea cards, split evenly between the two seed authors.
- `topics/30-day-topic-bank.md`: 24 primary topics and 12 backups.
- `topics/week-1-board.md`: first six production-ready assignments.
- `examples/pilot-source-pack.md`: sources and claim-to-source mapping for one pilot.
- `examples/pilot-outline.md`: approved six-part outline.
- `examples/pilot-article.md`: one complete 1,600–2,200-character sample.
- `examples/pilot-audit.md`: factual, originality, tone, and release audit.

---

### Task 1: Build the Editorial Foundation

**Files:**
- Create: `outputs/toutiao-content-kit/README.md`
- Create: `outputs/toutiao-content-kit/editorial-brief.md`

**Interfaces:**
- Consumes: the approved design in `outputs/toutiao-ai-content-system-design.md`.
- Produces: the canonical audience, voice, category, structure, and exclusion rules used by every later task.

- [ ] **Step 1: Create the kit directory and editorial brief**

Create `editorial-brief.md` with these exact sections:

```markdown
# 编辑总纲

## 一句话定位
用真实故事讲清金钱背后的人性，帮助普通人做出更清醒的生活选择。

## 核心读者
- 主读者：30～55岁普通中文读者。
- 补充读者：25～40岁职场人，以及35～60岁关注财富规律的人。

## 作者角色
冷静的生活观察者：冷静、克制、通俗、有洞察，不卖弄概念，不居高临下，不制造焦虑。

## 内容比例
- 钱与普通人的生活：40%。
- 家庭与人情：25%。
- 人性与社会生活：25%。
- 职场与财富规律：10%。

## 标准结构
1. 真实案例、公开数据或普遍生活处境。
2. 300字内提出核心矛盾。
3. 解释人性或财富机制。
4. 加入反例或适用边界。
5. 回到中国普通人的现实选择。
6. 用克制的判断结尾。

## 不可触碰
- 不讨论政治。
- 不荐股、不预测行情、不承诺收益。
- 不虚构第一人称、朋友、同事或具名人物。
- 不逐段翻译、拼接或模仿原作者标志性表达。
- 不发布无法追溯的关键数据、研究和人物故事。
- 不用医疗、法律或投资结论填补证据缺口。
```

- [ ] **Step 2: Create the start-here guide**

Create `README.md` with this operating order:

```markdown
# 今日头条内容工具包

## 每日20～30分钟
1. 从素材表选择3个候选，确定1个。
2. 用观点蒸馏提示词生成观点卡。
3. 用中国化研究提示词查找2～4个来源。
4. 人工打开并核对关键来源。
5. 用写作提示词生成初稿和5个标题。
6. 用独立审稿提示词审查。
7. 人工执行发布检查表。
8. 发布后记录24小时和72小时表现。

## 每周15分钟
1. 找出最好2篇和最差2篇。
2. 分别诊断选题、标题、开头和正文。
3. 从高共鸣评论中选择下周问题。
4. 每次只改变一个变量。
```

Add links to every file in the Deliverable Map after those files exist.

- [ ] **Step 3: Verify the foundation**

Run:

```bash
rg -n "一句话定位|核心读者|作者角色|内容比例|标准结构|不可触碰" outputs/toutiao-content-kit/editorial-brief.md
rg -n "每日20～30分钟|每周15分钟" outputs/toutiao-content-kit/README.md
```

Expected: all eight required headings or phrases appear exactly once in their intended files.

- [ ] **Step 4: Record checkpoint**

List the two created files and the verification result in the execution summary. Do not initialize Git.

---

### Task 2: Build the Material and Performance Trackers

**Files:**
- Create: `outputs/toutiao-content-kit/templates/idea-card.md`
- Create: `outputs/toutiao-content-kit/data/materials.csv`
- Create: `outputs/toutiao-content-kit/data/materials-field-guide.md`
- Create: `outputs/toutiao-content-kit/data/articles.csv`
- Create: `outputs/toutiao-content-kit/data/articles-field-guide.md`

**Interfaces:**
- Consumes: category names and source rules from `editorial-brief.md`.
- Produces: stable identifiers `card_id` and `article_id`, which Tasks 4–7 use to connect sources, topics, articles, and results.

- [ ] **Step 1: Create the reusable idea-card template**

Use these exact fields:

```markdown
# 观点卡：CARD-000

- 原作者：
- 原文标题：
- 原文链接：
- 原文日期：
- 收集日期：
- 一句话核心观点：
- 作者试图解释的问题：
- 因果机制：
- 原文案例与证据：
- 已证实事实与作者判断：
- 反例或适用边界：
- 中国生活场景：
- 待核实事实：
- 所属栏目：
- 3个原创选题方向：
- 使用状态：未使用
```

- [ ] **Step 2: Create the materials tracker**

The first line of `materials.csv` must be:

```csv
card_id,source_author,source_title,source_url,source_date,collected_date,core_claim,mechanism,evidence_summary,fact_vs_opinion,counterexample_boundary,china_context,verification_status,category,status,used_article_id,notes
```

Allowed values:

- `source_author`: `Morgan Housel` or `Sahil Bloom` for the initial seed batch.
- `verification_status`: `unreviewed`, `partial`, or `verified`.
- `category`: `money_life`, `family_relationships`, `human_social`, or `career_wealth`.
- `status`: `unused`, `planned`, `drafted`, `published`, or `retired`.

Document those meanings in `materials-field-guide.md`. State that CSV text must not contain fabricated quotation marks or unsupported exact figures.

- [ ] **Step 3: Create the article tracker**

The first line of `articles.csv` must be:

```csv
article_id,publish_date,category,core_conflict,card_ids,title,title_type,opening_type,character_count,status,source_count,impressions_24h,reads_24h,reads_72h,click_rate_24h,avg_read_time_24h,completion_rate_24h,comments_24h,follows_24h,diagnosis,next_action
```

Allowed values:

- `title_type`: `story`, `counterintuitive`, `question`, `benefit`, or `restrained`.
- `opening_type`: `verified_case`, `public_data`, or `common_situation`.
- `status`: `planned`, `drafted`, `published`, or `retired`.
- Performance fields remain blank when Toutiao does not expose an equivalent metric.

In `articles-field-guide.md`, include these diagnostic rules:

- Strong impressions plus weak reads: inspect title and topic framing.
- Strong reads plus weak reading time: inspect opening and content delivery.
- Solid reading plus weak comments: useful but possibly low emotional relevance.
- Many readers sharing personal experiences: strong lived-life resonance.
- Moderate reads plus strong follows: strong account-positioning fit.

- [ ] **Step 4: Verify CSV schemas**

Run:

```bash
python3 - <<'PY'
import csv
from pathlib import Path
base = Path('outputs/toutiao-content-kit/data')
expected = {
    'materials.csv': 17,
    'articles.csv': 21,
}
for name, count in expected.items():
    with (base / name).open(encoding='utf-8', newline='') as f:
        header = next(csv.reader(f))
    assert len(header) == count, (name, len(header), count)
    assert len(header) == len(set(header)), (name, 'duplicate column')
print('CSV schemas valid')
PY
```

Expected: `CSV schemas valid`.

- [ ] **Step 5: Record checkpoint**

List all five files and the schema-verification output in the execution summary.

---

### Task 3: Build the Prompt and Release-Control Library

**Files:**
- Create: `outputs/toutiao-content-kit/templates/prompts.md`
- Create: `outputs/toutiao-content-kit/templates/daily-release-checklist.md`
- Create: `outputs/toutiao-content-kit/templates/weekly-review.md`

**Interfaces:**
- Consumes: `editorial-brief.md` and `idea-card.md`.
- Produces: four named prompt stages and two human gates used in Tasks 4–7.

- [ ] **Step 1: Create the prompt library**

Copy the approved instruction and prompt content from Sections 7 and 8 of `outputs/toutiao-ai-content-system-design.md` into these exact sections:

```markdown
# AI提示词库
## 0. 固定项目指令
## 1. 观点蒸馏
## 2. 中国化研究
## 3. 文章写作
## 4. 独立审稿
```

Preserve all ten hard rules. Preserve the explicit instruction that the first stage must not translate, rewrite, or generate a Chinese article. Preserve the requirement for two to four research sources, source names, dates, and links. Preserve the five headline types and the final release verdict.

- [ ] **Step 2: Create the daily release checklist**

Include three sections with checkbox items:

- Green: independent claim, one real case/study/dataset, Chinese context, boundary condition, no invented characters, independent structure, concrete reader takeaway.
- Yellow: unsupported abstraction, suspiciously fictional opening, remote foreign context, absolute language, generic numbered headings, motivational ending, source-structure similarity.
- Red: unverifiable key fact, unverifiable story, medical/legal/investment dependency, attraction requiring exaggeration, synonym-only rewrite, or no independent conclusion.

End with this mandatory test:

> 删除原博主的文章后，这篇中文文章是否仍然拥有独立的案例、资料、结构和结论？

The release decision must be one of `可以发布`, `修改后发布`, or `不建议发布`.

- [ ] **Step 3: Create the weekly-review template**

Use these fields:

```markdown
# 周复盘：第__周
- 最好两篇：
- 最差两篇：
- 选题诊断：
- 标题诊断：
- 开头诊断：
- 正文诊断：
- 评论区反复出现的问题：
- 下周继续研究的问题：
- 下周唯一要调整的变量：
- 周末重点稿方向：
```

- [ ] **Step 4: Verify prompt and gate coverage**

Run:

```bash
rg -n '^## [0-4]\.' outputs/toutiao-content-kit/templates/prompts.md
rg -n '不要翻译|2～4个可靠来源|5个标题|可以发布／修改后发布／不建议发布' outputs/toutiao-content-kit/templates/prompts.md
rg -n '绿灯|黄灯|红灯|删除原博主' outputs/toutiao-content-kit/templates/daily-release-checklist.md
```

Expected: five numbered prompt sections; all four prompt safeguards; all three gate colors; and the independence test.

- [ ] **Step 5: Record checkpoint**

List the three files and note any wording differences from the approved design. Any difference requires user approval before Task 4.

---

### Task 4: Produce the First 20 Source-Linked Idea Cards

**Files:**
- Create: `outputs/toutiao-content-kit/cards/seed-cards.md`
- Modify: `outputs/toutiao-content-kit/data/materials.csv`

**Interfaces:**
- Consumes: `idea-card.md`, `materials.csv`, `prompts.md`, and public source pages from Morgan Housel and Sahil Bloom.
- Produces: cards `CARD-001` through `CARD-020`, which the topic bank references by exact ID.

- [ ] **Step 1: Research ten Morgan Housel sources**

Select ten public essays or X posts about money psychology, enough, risk, luck, spending, behavior, uncertainty, long-term thinking, freedom, or lifestyle expansion. For each source, save its title, author, publication date, and direct URL. Prefer the author's official site or article archive over reposts.

Reject any source whose central value depends on political commentary, market timing, or a culturally untranslatable anecdote.

- [ ] **Step 2: Research ten Sahil Bloom sources**

Select ten public essays or X posts about time, family, definitions of wealth, career decisions, personal growth, health as an asset, relationships, or life trade-offs. Save the same source metadata and apply the same exclusion rules.

- [ ] **Step 3: Draft cards `CARD-001` through `CARD-020`**

Each card must contain every field from `idea-card.md`. Do not reproduce more than one short source phrase when paraphrasing the idea; prefer no verbatim quotation. Each card must add:

- one Chinese everyday-life scenario;
- one counterexample or boundary;
- at least one fact or claim marked for verification;
- three independently worded Chinese topic directions;
- one of the four category codes.

Mark initial verification status as `partial` unless every consequential factual claim has been opened and checked.

- [ ] **Step 4: Add all 20 cards to `materials.csv`**

Use one row per card. Leave `used_article_id` blank. Set `status` to `unused`. Escape commas and quotation marks using valid CSV quoting.

- [ ] **Step 5: Verify card count, author balance, IDs, and source links**

Run:

```bash
python3 - <<'PY'
import csv
from pathlib import Path
p = Path('outputs/toutiao-content-kit/data/materials.csv')
with p.open(encoding='utf-8', newline='') as f:
    rows = list(csv.DictReader(f))
assert len(rows) == 20, len(rows)
assert sum(r['source_author'] == 'Morgan Housel' for r in rows) == 10
assert sum(r['source_author'] == 'Sahil Bloom' for r in rows) == 10
assert [r['card_id'] for r in rows] == [f'CARD-{i:03d}' for i in range(1, 21)]
assert all(r['source_url'].startswith('https://') for r in rows)
assert all(r['china_context'].strip() for r in rows)
assert all(r['counterexample_boundary'].strip() for r in rows)
print('20 balanced source cards valid')
PY
```

Expected: `20 balanced source cards valid`.

- [ ] **Step 6: Record checkpoint**

Report the ten Morgan Housel source URLs, ten Sahil Bloom source URLs, rejected sources with reasons, and validation output.

---

### Task 5: Build the 30-Day Topic Bank and First-Week Board

**Files:**
- Create: `outputs/toutiao-content-kit/topics/30-day-topic-bank.md`
- Create: `outputs/toutiao-content-kit/topics/week-1-board.md`

**Interfaces:**
- Consumes: cards `CARD-001` through `CARD-020` and the four editorial categories.
- Produces: topic IDs `TOPIC-001` through `TOPIC-036`; the first six become executable assignments for Task 6 and the user's first week.

- [ ] **Step 1: Draft 24 primary topics**

Use these exact category counts:

- `[money_life]`: 10.
- `[family_relationships]`: 6.
- `[human_social]`: 6.
- `[career_wealth]`: 2.

Each topic entry must contain:

- topic ID;
- category tag;
- core conflict in one sentence;
- one or two seed card IDs;
- Chinese lived context;
- evidence target;
- independent thesis;
- five headline angles: story, counterintuitive, question, benefit, restrained;
- risk note explaining what must not be overstated.

- [ ] **Step 2: Draft 12 backup topics**

Backups may use any category distribution but must be easy to verify in under five minutes and cannot duplicate a primary topic's thesis.

- [ ] **Step 3: Select the first six assignments**

Create `week-1-board.md` with two money/everyday-life topics, one family topic, one human/social topic, one career/wealth topic, and one weekend research topic. For each, name the preferred source card, likely Chinese evidence source, planned opening type, and expected release day.

- [ ] **Step 4: Verify counts and references**

Run:

```bash
python3 - <<'PY'
import re
from pathlib import Path
text = Path('outputs/toutiao-content-kit/topics/30-day-topic-bank.md').read_text(encoding='utf-8')
assert len(re.findall(r'^### TOPIC-\d{3}', text, flags=re.M)) == 36
primary = text.split('## 12个备用选题', 1)[0]
expected = {
    'money_life': 10,
    'family_relationships': 6,
    'human_social': 6,
    'career_wealth': 2,
}
for category, count in expected.items():
    actual = len(re.findall(rf'^- 栏目：\[{category}\]$', primary, flags=re.M))
    assert actual == count, (category, actual, count)
refs = set(re.findall(r'CARD-\d{3}', text))
assert refs
assert all(1 <= int(r[-3:]) <= 20 for r in refs)
print('Topic bank counts and card references valid')
PY
```

Expected: `Topic bank counts and card references valid`.

- [ ] **Step 5: Record checkpoint**

Report category counts, the six first-week topic IDs, and validation output.

---

### Task 6: Run One End-to-End Pilot Article

**Files:**
- Create: `outputs/toutiao-content-kit/examples/pilot-source-pack.md`
- Create: `outputs/toutiao-content-kit/examples/pilot-outline.md`
- Create: `outputs/toutiao-content-kit/examples/pilot-article.md`
- Create: `outputs/toutiao-content-kit/examples/pilot-audit.md`
- Modify: `outputs/toutiao-content-kit/data/materials.csv`
- Modify: `outputs/toutiao-content-kit/data/articles.csv`

**Interfaces:**
- Consumes: one green-light topic from `week-1-board.md`, its card, the four prompts, and the daily release gate.
- Produces: pilot article `ARTICLE-001`, an evidence map, a release verdict, and a reusable example of the complete workflow.

- [ ] **Step 1: Select the pilot**

Choose the first-week topic with the clearest Chinese context and the least risky evidence burden. Prefer money/everyday-life over health, investing, or legal implications. Record the selected `TOPIC-` and `CARD-` IDs at the top of every pilot file.

- [ ] **Step 2: Build the source pack**

Use two to four sources. For every factual claim, record:

```markdown
### Claim N
- Claim:
- Source title:
- Publisher:
- Publication date:
- Direct URL:
- Exact support location or short paraphrase:
- Status: verified / excluded
```

Open each URL and confirm that it directly supports the claim. Exclude secondary summaries when an accessible primary source exists.

- [ ] **Step 3: Create the six-part outline**

The outline must name the opening evidence, core conflict, mechanism, boundary condition, Chinese-life application, and restrained final judgment. It must not reproduce the source author's original order.

- [ ] **Step 4: Draft the pilot article**

Write approximately 1,600–2,200 Chinese characters. Keep source markers in the working draft. Provide five headline types below the article. Do not mention either seed author unless the article is explicitly explaining that person's idea.

- [ ] **Step 5: Run the independent audit**

The audit must report:

- unsupported or weakly supported claims;
- possible fabrication or exaggeration;
- source-similarity risk;
- translation-like phrasing and AI clichés;
- weak Chinese relevance;
- weakest paragraph and a concrete revision;
- selected headline and rationale;
- one verdict: `可以发布`, `修改后发布`, or `不建议发布`.

If the verdict is `修改后发布`, revise the article and add a second audit section. If the verdict is `不建议发布`, stop and select another first-week topic rather than forcing publication.

- [ ] **Step 6: Verify character count and source integrity**

Run:

```bash
python3 - <<'PY'
import re
from pathlib import Path
article = Path('outputs/toutiao-content-kit/examples/pilot-article.md').read_text(encoding='utf-8')
body = article.split('## 备选标题', 1)[0]
body = re.sub(r'https?://\S+', '', body)
body = re.sub(r'[#>*_`\-]', '', body)
count = len(re.sub(r'\s+', '', body))
assert 1600 <= count <= 2400, count
pack = Path('outputs/toutiao-content-kit/examples/pilot-source-pack.md').read_text(encoding='utf-8')
urls = re.findall(r'https://\S+', pack)
assert 2 <= len(set(urls)) <= 4, len(set(urls))
audit = Path('outputs/toutiao-content-kit/examples/pilot-audit.md').read_text(encoding='utf-8')
assert any(v in audit for v in ('可以发布', '修改后发布', '不建议发布'))
print(f'Pilot valid: {count} characters, {len(set(urls))} sources')
PY
```

Expected: `Pilot valid: <count> characters, <2-4> sources`.

- [ ] **Step 7: Update trackers**

Set the pilot card to `drafted` or `published` and assign `used_article_id=ARTICLE-001`. Add `ARTICLE-001` to `articles.csv` with blank post-publication metrics until real data exists.

- [ ] **Step 8: Record checkpoint**

Report selected topic/card IDs, sources used, final headline, audit verdict, character count, and tracker changes.

---

### Task 7: Finalize the Operating Kit and Readiness Check

**Files:**
- Modify: `outputs/toutiao-content-kit/README.md`
- Review: every file under `outputs/toutiao-content-kit/`

**Interfaces:**
- Consumes: all Tasks 1–6 outputs.
- Produces: one navigable, internally consistent kit ready for the user's 30-day launch.

- [ ] **Step 1: Add a complete file index to README**

Link every deliverable using relative Markdown links. Add a “第一次使用” section with this sequence:

1. Read `editorial-brief.md`.
2. Open `topics/week-1-board.md`.
3. Copy one topic into the four prompt stages.
4. Record the viewpoint card in `data/materials.csv`.
5. Apply `templates/daily-release-checklist.md`.
6. After publishing, update `data/articles.csv` at 24 and 72 hours.
7. Complete `templates/weekly-review.md` once per week.

- [ ] **Step 2: Run a placeholder and forbidden-pattern scan**

Run:

```bash
rg -n "T[B]D|T[O]DO|待定|以后补充|随便写|虚构一个|我有个朋友|我同事说" outputs/toutiao-content-kit || true
```

Expected: no matches except an explicitly labeled negative example in editorial guidance. Remove or rewrite every unexplained match.

- [ ] **Step 3: Verify all local links**

Run:

```bash
python3 - <<'PY'
import re
from pathlib import Path
root = Path('outputs/toutiao-content-kit')
broken = []
for md in root.rglob('*.md'):
    text = md.read_text(encoding='utf-8')
    for target in re.findall(r'\[[^]]+\]\(([^)]+)\)', text):
        if target.startswith(('http://', 'https://', '#')):
            continue
        resolved = (md.parent / target).resolve()
        if not resolved.exists():
            broken.append((str(md), target))
assert not broken, broken
print('All local links valid')
PY
```

Expected: `All local links valid`.

- [ ] **Step 4: Verify complete spec coverage**

Confirm that the kit contains:

- positioning and four content categories;
- daily 20–30-minute workflow;
- four separate AI prompts;
- idea-card, materials, and article trackers;
- green/yellow/red gate;
- 20 balanced source cards;
- 24 primary and 12 backup topics;
- six first-week assignments;
- one source-backed pilot and audit;
- weekly review and 30-day metric logic.

Record each item as present with its exact file path.

- [ ] **Step 5: Deliver the kit**

Provide one clickable link to `outputs/toutiao-content-kit/README.md`, summarize the pilot verdict, state that factual claims still require human checking before publication, and recommend beginning with the six first-week assignments rather than generating more topics.

---

## Execution Acceptance Criteria

Implementation is complete only when:

1. Every file in the Deliverable Map exists and is linked from README.
2. Both CSV schema checks pass.
3. Exactly 20 idea cards exist, with a 10/10 author split and valid source URLs.
4. Exactly 36 topics exist, with the first 24 matching the 10/6/6/2 category mix.
5. The pilot passes character-count, source-count, and audit-verdict checks.
6. The placeholder scan has no unexplained matches.
7. All local Markdown links resolve.
8. No content claims implementation success without displaying the corresponding verification output.
