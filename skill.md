---
name: novel-forge
description: >-
  Collaborative novel and fiction creation system. Activate when user wants to write,
  plan, design, revise, review, or iterate on any long-form fiction — novels, web novels,
  serialized fiction, 网文, light novels, short story collections. Covers world-building,
  character design, plot architecture, outline planning, chapter writing, pacing, prose
  polish, consistency checking, foreshadowing management, state tracking, anti-AI prose
  defense, and editorial review. Triggers on: "write a novel", "start a new story",
  "design a character", "build a world", "plan a plot", "write chapter N", "continue
  my novel", "fix pacing", "revise this chapter", "write the next chapter", "review
  chapters", "check consistency", "通读审查", "人物设计", "世界观", "大纲", "章节",
  "写小说", "创意写作", "续写", "写一章", "网文写作", "修这章", "检查一致性",
  "爽点设计", "伏笔", "状态提取", "角色卡". Also activates when working in a
  directory containing novel-state.md or chapters/ with chapter-*.md files. ALWAYS
  activate when the user asks to write, revise, or review any fiction content. Not for
  non-fiction, articles, poetry, or technical writing.
origin: community
allowed-tools: Read Write Glob Grep Bash
---

# Novel Forge

Collaborative novel creation system. The human directs; the AI co-creates. Propose options, respect choices, make the story live.

## When to Activate

- Starting a new novel or fiction project from scratch
- Continuing work on an existing novel project (has project directory with state files)
- Writing individual chapters or scenes within an established project
- Redesigning world, characters, or plot for an existing project
- Fixing pacing, tone, or prose quality issues in drafted chapters
- User says anything about writing fiction, novels, web fiction, 网文, 小说

### Avoid When

- Non-fiction writing (use `article-writing` instead)
- Short-form content under 2000 words (use standard writing)
- Academic or technical writing
- Poetry (different craft, different workflow)
- User just wants a quick story draft without structure (overkill)

## Trigger Routing

| User says / Situation | Mode | Entry Point |
|---|---|---|
| "I want to write a novel" / "帮我写小说" / no project dir found | **New Project** | Phase 1: Project Setup |
| "Continue my novel" / existing project dir with state files | **Resume** | Read `novel-state.md`, resume at current phase |
| "Fix the pacing in chapter 5" / "revise the outline" | **Targeted Fix** | Jump to relevant phase, fix, update state |
| "Write chapter 8" / "写第八章" | **Chapter Write** | Phase 7: Chapter Writing (load prior state) |
| "Redesign this character" / "change the magic system" | **Phase Revision** | Go back to specific phase, rework, propagate changes |
| User provides partial work (existing outline, world notes) | **Bootstrap** | Phase 1 with import, skip to appropriate phase — see [references/advanced-workflows.md](references/advanced-workflows.md) Section 六 |
| "Teach me while writing" / "当我的写作教练" / "标注技法" / "给我两个版本" | **Writing Coach** | Phase 7 with coach mode — see [references/advanced-workflows.md](references/advanced-workflows.md) Section 一 |

---

## Core Principles

### 1. Director-Co-Creator Dynamic

The human is the DIRECTOR. The AI is the CO-CREATOR.
- Propose **2-3 options** for every meaningful decision, never just one
- Explain tradeoffs between options in plain language
- Human picks, mixes, or rejects. Human always has final say
- Express creative opinions but never override the director

### 2. Dialogue-First, Templates-Second

Conversation drives creation. Templates capture decisions.
- Start every phase with a dialogue about vision and constraints
- Fill templates AFTER discussion, not before
- If the user has strong opinions, skip proposal and capture directly
- If the user is uncertain, offer more options with reasoning

### 3. File-as-Memory

All project state lives in human-readable markdown files in the project directory.
- Read files to restore context between sessions
- Output updated files after every phase — the human can read and edit directly
- No hidden state. No databases. Just markdown.
- Detect and respect manual edits to any file

### 4. Nonlinear Phase Access

Phases are listed in order but are not a rigid pipeline.
- Jump back to any phase at any time to revise
- Changes propagate forward (e.g., new character affects outline)
- The state file tracks which phases are complete and which need rework
- No phase is ever "locked" -- the story evolves

### 5. Anti-AI as Narrative Technique

Fight AI-sounding prose at the craft level, not the word level.
- Address sentence structure, rhythm, and narrative approach — not just word choice
- Use word replacement lists as a last resort, not the primary defense
- Target prose that could not have been written by filling in a template
- See [references/anti-ai-system.md](references/anti-ai-system.md) for the full technique library

### 6. Relentless Validation (HARD RULE — MANDATORY IN ALL COLLABORATIVE PHASES)

After every creative decision in Phases 1–6, apply five mandatory questioning rules: post-selection probing ("why this one?"), contradiction detection (flag conflicts with prior choices immediately), readiness confirmation (one final question before advancing), one-question-at-a-time (never stack), and always recommend (suggest a preferred resolution). The AI must initiate questioning — never wait for the user to prompt it.
See **[references/proposal-system.md](references/proposal-system.md)** for the complete protocol with examples.

---

## Iron Rules (MANDATORY — EVERY WRITING SESSION)

These rules are NON-NEGOTIABLE. They apply to every chapter draft, every revision, every edit. Violating the letter of these rules IS violating the spirit. No excuse — not "the user didn't ask", not "it's just a small edit", not "I'll catch it next time" — justifies skipping them.

### IR-1: POV Lock + Uncertain Assessment

Once a chapter's POV character is set:
- ONLY describe what the POV character can perceive (see, hear, smell, feel, think)
- NEVER reveal other characters' thoughts/feelings unless the POV character infers them from observable behavior
- When the POV character judges based on LIMITED info (distant sounds, brief glimpses), use hedging language ("不像" "大约" "应该是") — NOT absolute ("不是" "肯定是"). This prevents contradictions when the character later sees close-up.

### IR-2: Vocabulary Register Audit (NON-MODERN SETTINGS)

AI doesn't distinguish register — it only checks "correctness." These modern analytical/technical terms are FORBIDDEN in non-modern settings. Search EVERY draft. Replace on sight.

| 禁用 | 替换（按语境选） |
|------|-----------------|
| 数据 | 观察、线索、情报、记忆、见闻 |
| 参数 | 条件、变化、因素 |
| 变量 | 变化、未知、变数 |
| 指标 | 标记、征兆、迹象 |
| 系统 | 体系、规矩、一套 |
| 配置 | 布置、安排、部署 |
| 模型 | 模样、形态、样子 |
| 效率 | 效力、速度、快慢 |
| 输入 | 传入、灌入、供给 |
| 输出 | 产出、释放、外泄 |
| 反馈 | 回应、反应、回馈 |
| 优化 | 改善、调整、打磨 |
| 模块 | 部分、部件、一截 |
| 架构 | 构造、骨架、格局 |
| 协议 | 约定、规矩、契约 |
| 接口 | 交汇处、接触面、衔接 |

### IR-3: Context Loading Protocol (Phase 7 Hard Limits) — AUTHORITATIVE DEFINITION

> **权威声明**: 本节是上下文加载协议的唯一定义源。其他文件涉及加载优先级时，以本节为准。

When writing a chapter, load context in this order — NEVER exceed the cap:
1. **P0 (MUST load first):** 本章大纲（from outline.md）+ 前章状态快照（`state/chNNN.md`，NNN 为零填充章节号）+ 前章最后500字 + 术语一致性表 + 关键数字表（≈3000字）
2. **P1 (Next):** 出场角色档案 + 活跃伏笔列表 + 相关里程碑 + 前两章状态 Delta Summary（≈4000字）
3. **P2 (As needed):** 本章涉及的世界观细节 + 非活跃伏笔 + 关系网络（≈8000字）
4. **HARD CAP: 15,000 characters total context loaded.** Exceeding this = chapter loses coherence.
5. **Overflow protocol:** 优先保留 P0 → 压缩 P1（角色只取关键属性）→ 跳过 P2
6. **NEVER load a prior chapter's full text.** Use state snapshots instead.

### IR-4: State Extraction = Chapter Complete

A chapter is NOT "done" until ALL of the following are done:
1. `state/chNNN.md` written (immutable snapshot, NNN = zero-padded)
2. `timeline.md` updated with scene-level entries
3. `novel-state.md` updated (chapter summary + foreshadowing + character states)
4. Consistency check passed (state matches chapter text + world rules)

No exceptions. No "I'll do it in the next turn." The chapter draft is not presented as complete until the state is extracted.

### IR-5: Anti-AI 6-Point Self-Check (Before Delivery)

Before presenting any chapter draft, run these 6 checks. If any fail, DELETE AND REWRITE the offending passage. Do not patch — rewrite.

1. **Show Don't Tell:** Every directly named emotion replaced with action/sensory detail?
2. **Sentence Rhythm:** No 3+ consecutive sentences of similar length?
3. **Dialogue Subtext:** Characters say 70% — the important content is in what they DON'T say?
4. **Vocabulary Register:** All IR-2 words are clean? (Skip for modern/sci-fi settings where these words are register-appropriate.)
5. **Structural Asymmetry:** No AI-typical parallel structures (排比, 对称收束)?
6. **Punctuation Audit:** Grep all dialogue lines ending in "。" — is every one actually a statement, not a question? Any sentence containing 什么/怎么/呢/哪/谁/吗/为什么/多久/etc. MUST end with "？". This is the most common AI punctuation error. CHECK EXPLICITLY. Do not trust your writing-time judgment — verify after drafting.

Do NOT present a draft that has known issues. If you catch yourself thinking any of these, STOP and fix:

| Excuse | Why it's wrong |
|--------|---------------|
| "It's just one word" | One register mismatch breaks immersion for attentive readers |
| "The user can fix it" | Your job is to deliver clean prose, not rough drafts |
| "The setting is ambiguous" | When in doubt, use the safer register |
| "This word is common enough" | Common ≠ register-appropriate |
| "I'll catch it in revision" | Catch it NOW. Revision is for craft, not basic compliance |

### IR-6: Prose Iron Laws (7 Rules — DELETE AND REWRITE on violation)

1. **Narrator never concludes for the reader.** Delete any sentence that spells out what the reader should infer. ("他这么做是为了让小王信任他" → DELETE. Show the behavior, let readers infer.)
2. **No analytical language in prose.** "核心动机""利益最大化""信息边界""权衡利弊" — DELETE on sight in narrative prose. These are writing tools, not story words. (Exception: acceptable in dialogue when a character's profession or personality would naturally use such language.) Replace with behavior: "他把两份合同并排放在桌上，盯着看了十分钟，签了左边那份。"
3. **Surprise markers rate-limited.** "仿佛/忽然/竟/竟然/猛地/猛然/不禁/宛如/骤然/陡然" combined max 1 per 3000 chars. Exceed this → DELETE excess markers, rewrite with action/scenes instead.
4. **Same sensation max 2 rounds.** 3rd repetition of any sensation → DELETE and switch to new info/action. "心跳加速→心脏狂跳→心脏跳出来" = 3rd round fails.
5. **Planning terms never in chapter text.** "处境""动机""信息边界" stay in notes. Found in chapter text → DELETE, translate to scenes and actions.
6. **Hard bans — zero tolerance.** "不是...而是..." construction: DELETE entire sentence, rewrite. "——" em-dash: max one per sentence. Both are AI markers visible at a glance.
7. **Questions must use "？" — zero tolerance.** Any dialogue or interior monologue that is grammatically a question (contains 什么/怎么/呢/哪/谁/吗/为什么/怎么办/多久/什么时候/在哪 etc.) MUST end with "？", never "。". Flat/cold tone is achieved through word choice and sentence structure, NEVER by replacing "？" with "。". AI over-applies this pattern to all characters indiscriminately. Found → replace with "?" immediately.

### IR-7: Cool Point Engineering (Web Novel Satisfaction)

**Formula:** 满足感 = 压抑深度 × 兑现力度 × 意外程度

**6 Core Modes:**

| Mode | Beat Structure | Payoff Signature |
|------|---------------|-----------------|
| 装逼打脸 | 被轻视→底线触发→一击碾压 | 全场震惊 (needs 3 factions: mockers/shocked/smug) |
| 扮猪吃虎 | 隐藏目的→危机→身份暴露 | 关系重组 (must have logical reason for hiding) |
| 越级反杀 | 差距悬殊→伏笔激活→以巧胜拙 | 有代价的胜利 (zero-cost = hollow) |
| 打脸权威 | 权威压制→坚持→权威动摇 | 被承认 (authority need not be evil) |
| 反派翻车 | 反派布局→意外→连锁崩盘 | 自食其果 (信息差 drives tension) |
| 甜蜜超预期 | 情感压抑→一方主动→超预期甜蜜 | 关系升级 (方式/时机/深度, one exceeds expectation) |

**Density Rules:** Every 2-3 chapters ≥ 1 micro payoff. Every 5 chapters ≥ 1 combo climax. Every 10-15 chapters ≥ 1 milestone climax. Below minimum = readers drift. **Rotation rule:** consecutive payoffs must use different modes.

**Structure:** 30/40/30 for single-chapter payoff (铺垫/爆发/余波). 60/20/20 for cross-chapter arc.

**Extended modes:** 迪化误解 + 身份掉马 — see [references/excitement-engineering.md](references/excitement-engineering.md) Section 1.3.

### IR-8: Psychology 3-Layer + Emotion 4-Level

**3 Psychology Layers** — use all three, not just the surface:
- **Conscious** (意识): character actively thinks. "他明白现在不能冲动。" Use for decisions and rational judgment.
- **Subconscious** (潜意识): behavior contradicts words. Checks door lock three times, says "just being careful." Use for depth and hidden motivation.
- **Unconscious** (无意识): body betrays truth. Says "I'm fine", hand grips table edge white. Use for dramatic tension — reader sees what character doesn't.

**4 Emotion Intensity Levels** — match scale to importance, never mismatch. 详细技巧见 [emotion-psychology.md](references/emotion-psychology.md)：
- **Level 1** (日常, ~10 chars): "他皱了下眉。" One beat.
- **Level 2** (明显, ~30 chars): 1 action + 1 reaction. "她的手顿了一下，指尖发凉。"
- **Level 3** (强烈, ~50 chars): External + internal. "他猛地站起来，椅子撞上墙。胸口像被攥住——不能在这里崩掉。"
- **Level 4** (爆发, 100-200 chars): Multi-layer: behavior + sensation + decision. Reserve for climactic moments.

---

## Phase Overview

Eight phases of novel creation. Phases produce files. Files are memory. Memory persists across sessions.

```
Phase 1: Project Setup          --> novel-state.md, project-config.md
Phase 2: Core Concept + Title   --> title-synopsis.md (logline + working title)
Phase 3: World-Building         --> world.md
Phase 4: Character Design       --> characters/main/<name>.md + characters/supporting/<name>.md + knowledge-state.md
Phase 5: Plot Architecture      --> plot.md
Phase 6: Outline + Pacing       --> outline.md (volumes + milestones) + timeline.md + foreshadowing-ledger.md
Phase 7: Chapter Writing        --> chapters/chapter-NNN.md (via direction proposals)
Phase 8: State Extraction       --> state/chNNN.md + updates novel-state.md + timeline.md + world.md (if new lore) + foreshadowing-ledger.md + knowledge-state.md
```

### Dependency Map

```
Phase 1 ──> Phase 2 ──> Phase 3 ──> Phase 4 ──> Phase 5 ──> Phase 6 ──> Phase 7
            (concept)   (world)     (chars)     (plot)      (outline)  (writing)
                 +─── any phase can loop back ────+
                                          Phase 8 (runs after every chapter)
```

---

## Workflow Steps

> **⚠️ PHASE LOADING RULE:** Before entering ANY phase below, you MUST Read the reference files listed in that phase's PRE-LOAD line. Skipping the Read = skipping the rules = producing inferior work. No exceptions.

### Phase 1: Project Setup

Establish the project container and initial vision.

**⚠️ PRE-LOAD:** `references/proposal-system.md`

1. **Create project directory** at user-specified location (default: `~/novels/<title-slug>/`)
2. **Dialogue**: Ask about genre, tone, target length, audience, and initial spark
3. **Create `novel-state.md`** with phase tracker and project metadata
4. **Create `project-config.md`** with agreed parameters

Output files: `novel-state.md`, `project-config.md`
Templates: [templates/novel-state.md](templates/novel-state.md), [templates/project-config.md](templates/project-config.md)
Quality gate: directory exists, both files written, user confirmed vision
⚠️ VALIDATION REQUIRED: Before advancing to Phase 2, confirm readiness — ask the user one question that tests whether the project vision is truly settled.

### Phase 2: Core Concept + Title

Distill the story's soul before building anything. A strong concept guides every later decision.

**⚠️ PRE-LOAD:** `references/proposal-system.md`

1. **Dialogue**: Ask what excites the user most about this story. What's the emotional core? What's the "what if?"
2. **Propose 2-3 logline options** — each in one sentence, each capturing a different angle of the core conflict
3. **Propose 2-3 title options** with reasoning (genre-appropriate, memorable, not generic)
4. **Capture core concept**: logline, central conflict, thematic question, emotional promise to reader
5. **Create `title-synopsis.md`** with working title, logline, and concept notes (full synopsis refined after Phase 5)

Output file: `title-synopsis.md` (initial version — logline + working title + concept)
Template: [templates/title-synopsis.md](templates/title-synopsis.md)
Quality gate: logline is one clear sentence with conflict + stakes, title resonates with genre and tone
⚠️ VALIDATION REQUIRED: After user picks logline and title, ask "why this one?" — surface the real reason. Before advancing to Phase 3, check for contradictions between the core concept and the genre/tone choice.

### Phase 3: World-Building

Build the story world through dialogue, not questionnaire.

**⚠️ PRE-LOAD:** `references/world-building-guide.md`

1. **Dialogue**: Ask what makes this world different from ours. Start with the one thing the user is most excited about.
2. **Propose 2-3 world-building approaches** (hard magic system vs. soft; near-future vs. far; geopolitical focus vs. cultural)
3. **Build iteratively**: flesh out the areas that matter to the story first
4. **Create `world.md`** organized by what the reader needs to know, not encyclopedia order

Output file: `world.md`
Template: [templates/world.md](templates/world.md)
Detailed guide: [references/world-building-guide.md](references/world-building-guide.md)
Quality gate: rules are internally consistent, key conflicts emerge from world design, no unexplained contradictions
⚠️ VALIDATION REQUIRED: After each world-building choice, check for contradictions with the core concept (Phase 2). Before advancing to Phase 4, ask one question that tests whether the world truly serves the story's emotional promise.

### Phase 4: Character Design

Create characters who drive plot through desire and flaw.

**⚠️ PRE-LOAD:** `references/character-design-guide.md`（知识状态追踪已整合入 `references/consistency-system.md` Section 1.4，按需查阅）

1. **Start with the protagonist**: what do they want, what stops them, what will they sacrifice
2. **Propose 2-3 character archetypes** as starting points, let user pick or blend
3. **Build supporting cast** based on story needs (antagonist, mirror, foil, catalyst)
4. **Create character files**: main characters get detailed profiles in `characters/main/<name>.md`; supporting characters get brief profiles in `characters/supporting/<name>.md`
5. **Create `knowledge-state.md`** for cumulative knowledge tracking across chapters (updated after each chapter in Phase 8)

Output: `characters/main/<name>.md` (per main character) + `characters/supporting/<name>.md` (per supporting character) + `knowledge-state.md`
Detailed guide: [references/character-design-guide.md](references/character-design-guide.md)
Template: [templates/character-card.md](templates/character-card.md), [templates/knowledge-state.md](templates/knowledge-state.md)
Quality gate: each character has distinct voice, conflicting desires exist between characters, no character is purely good or evil without reason
⚠️ VALIDATION REQUIRED: After each character is defined, check for contradictions with the world rules (Phase 3) and core concept (Phase 2). Ask "does this character's desire create genuine conflict with other characters?" Before advancing, confirm the cast is complete enough to drive the plot.

### Phase 5: Plot Architecture

Design the structural backbone before filling in details.

**⚠️ PRE-LOAD:** `references/plot-architecture.md`

1. **Propose 2-3 structural frameworks** (three-act, seven-point, hero's journey, web-novel arc structure, etc.) with tradeoffs
2. **Define the central question** the story answers
3. **Map major turning points** and their emotional targets
4. **Create `plot.md`** with structure, central conflict, key turning points, and thematic throughlines

Output file: `plot.md`
Template: [templates/plot.md](templates/plot.md)
Detailed guide: [references/plot-architecture.md](references/plot-architecture.md)
Quality gate: central conflict is clear, stakes escalate, resolution follows from established rules
⚠️ VALIDATION REQUIRED: After the plot structure is chosen, check for contradictions with character desires (Phase 4) and world constraints (Phase 3). Ask "does every turning point require a character to make a painful choice?" Before advancing, confirm the plot structure serves the core concept's emotional promise.

### Phase 6: Outline + Pacing

Plan the story's milestone architecture. NOT a per-chapter script — a roadmap with key events and open space for discovery.

**⚠️ PRE-LOAD:** `references/outline-template-guide.md`, `references/pacing-curve-reference.md`

1. **Propose 2-3 volume structures** (how many volumes, how many chapters per volume)
2. **Define 3-5 milestones per volume**: the MUST-HAPPEN events that drive the story forward
3. **Set volume-level tone and tension direction** (rising / peaking / recovering), NOT per-chapter tension numbers
4. **Leave the space between milestones OPEN** — these will be filled during Phase 7 through discussion
5. **Create `outline.md`** with volume overview + milestones + tension direction
6. **Create `timeline.md`** for scene-level time tracking (updated after each chapter)
7. **Create `foreshadowing-ledger.md`** for foreshadowing tracking (initially empty, populated from Phase 8)

Output: `outline.md` (volumes + milestones), `timeline.md` (empty initially), `foreshadowing-ledger.md` (initially empty)
Detailed guide: [references/outline-template-guide.md](references/outline-template-guide.md)
Template: [templates/outline-master.md](templates/outline-master.md), [templates/timeline.md](templates/timeline.md), [templates/foreshadowing-ledger.md](templates/foreshadowing-ledger.md)
Quality gate: every milestone has clear narrative purpose, milestones escalate across volumes, breathing room exists between peaks
⚠️ VALIDATION REQUIRED: After the outline is complete, check for contradictions with the plot turning points (Phase 5). Ask "does every milestone earn its place?" Before advancing to writing, do a final readiness check — confirm the user is satisfied with the story shape, not just "good enough to start."

### Phase 7: Chapter Writing

Write chapters through collaborative discussion. One chapter at a time. Each chapter starts with a direction proposal — the AI never writes without the user choosing where to go.

**⚠️ PRE-LOAD (TIERED LOADING — load in order):**

| Tier | When to Load | File | Content |
|------|-------------|------|---------|
| 1 (PRE-LOAD) | Before direction proposal | `references/chapter-writing-guide.md` + `references/pre-writing-brief.md` | Operational guide (direction proposals, scene structure, quality guardrails) + Pre-writing briefing format (7-segment memo, 5-segment task sheet) |
| 2 (PRE-DRAFT) | After user selects direction, before drafting | `references/anti-ai-system.md` Part 1 | Writing-time defense: 7 structural layers, 8 rewrite algorithms, hard bans |
| 3 (SELF-CHECK) | After drafting, before delivery | `references/anti-ai-system.md` Appendix + `references/advanced-detection.md` | Post-writing detection: pattern system, clustering, signal stacking, word bank |
| 4 (ON-DEMAND) | Only for deep prose diagnosis | `references/prose-quality-framework.md` | Four reward channels, psychic distance, free indirect discourse — NOT loaded by default |

**Never load all tiers simultaneously.** Tier 1 is always loaded. Tiers 2-3 are loaded when needed. Tier 4 is reference only.

**⚠️ PREFLIGHT (MANDATORY — two phases):**

**Phase A — BEFORE direction proposal (load context):**
```
NOVEL_FORGE_PREFLIGHT_A: preload=pass|fail ir3_context=pass|fail
```
Load references per PRE-LOAD, load project state per IR-3, then propose 2-3 direction options.

**Phase B — BEFORE drafting (after user selects direction):**
```
NOVEL_FORGE_PREFLIGHT_B: direction_proposed=pass|fail user_selected=pass|fail ir1_pov=pass|fail ir2_register=pass|fail|n/a ir6_prose=pass|fail ir5_check=pass|fail
```
`direction_proposed=pass` requires 2-3 options actually shown to user. `user_selected=pass` requires explicit user pick/blending. BOTH must be pass before drafting.

1. **Propose 2-3 direction options** for this chapter based on: current volume milestones, prior chapter state snapshot, and where the story wants to go next
2. **User selects** a direction (or proposes their own, or blends options) — DO NOT draft until user has explicitly chosen
   - *Optional: if user requests writing guidance, activate coach mode — offer 2-3 opening versions, annotate techniques, provide alternate key-scene versions, and post-writing self-assessment. See [references/advanced-workflows.md](references/advanced-workflows.md) Section 一.*
3. **Load context per IR-3** (P0→P1→P2, 15K char cap, never load full prior chapter)
4. **State PREFLIGHT_B** — declare all gates pass before drafting
5. **Draft the chapter** following Iron Rules IR-1 (POV lock), IR-2 (register audit), IR-5 (anti-AI check), IR-6 (prose iron laws), IR-7 (cool point), IR-8 (psychology layers)
6. **Self-review**: IR-5 5-point check + IR-6 iron laws + quality score >= 12/20（评分标准见 [pre-writing-brief.md](references/pre-writing-brief.md) Section 3.1 十大标准20分制）
7. **Write chapter file** to `chapters/chapter-NNN.md`
8. **IMMEDIATELY execute Phase 8** — per IR-4, the chapter is not done until state is extracted (Phase 8 handles timeline update)

Output: `chapters/chapter-NNN.md`（Phase 8 随后自动执行，产出 state 快照 + 更新 timeline）
Quality gate: PREFLIGHT declared + IR-5 checks pass + quality >= 12/20（评分标准见 pre-writing-brief.md Section 3.1）+ **state snapshot per IR-4**

### Phase 8: State Extraction (MANDATORY — runs after EVERY chapter)

After each chapter, create an immutable state snapshot file AND update supporting files. This prevents "amnesia" across chapters — every chapter's aftermath is preserved exactly, not overwritten.

**⚠️ PRE-LOAD (CRITICAL):** `references/consistency-system.md`, `references/state-extraction-guide.md`

1. **Create `state/chNNN.md`** using the state snapshot template (one file per chapter, never overwrite, NNN = zero-padded chapter number). Populate Snapshot Identity: chapter number, title, POV character, story timestamp, real date
2. **Record chapter summary** (≤200 chars): what happened, what changed
3. **Record character state changes**: for each character who appeared, capture physical, emotional, location, status, items/skills gained/lost, key changes. Include 伤势追踪表 for any injury. Record knowledge state changes (Knows/Believes/Doesn't Know per character)
4. **Record relationship changes**: any relationship temperature shifts with cause and direction
5. **Record foreshadowing updates**: new plants, advances, resolutions, deferrals — with chapter IDs. Update foreshadowing-ledger.md accordingly
6. **Record timeline**: story-internal time position, gap since previous chapter
7. **Record new elements**: new proper nouns, new locations, new props introduced
8. **Record open questions**: questions raised, still open, or answered this chapter
9. **Verify new lore elements** against world.md and characters/ — add consistent new elements to canon files
10. **Update `timeline.md`** with scene-level entries for this chapter
11. **Update `novel-state.md`**: add chapter summary to 章节摘要 table, update 活跃伏笔摘要（类型/紧迫度从 foreshadowing-ledger.md 同步）, update 角色状态摘要, update 术语一致性表 and 关键数字表, update current_chapter counter
12. **Update `knowledge-state.md`**: merge snapshot knowledge changes into cumulative file
13. **Write Delta Summary**: 3-5 bullet points of the most important changes for quick reference by next chapter
14. **Run consistency check**: verify state snapshot against chapter text and world rules, flag contradictions

Output: `state/chNNN.md` (immutable snapshot) + updated `novel-state.md` + updated `timeline.md` + updated `foreshadowing-ledger.md` + updated `knowledge-state.md` + updated `world.md` (if new lore)
Template: [templates/state-snapshot.md](templates/state-snapshot.md)
Detailed guide: [references/state-extraction-guide.md](references/state-extraction-guide.md)
Consistency system: [references/consistency-system.md](references/consistency-system.md)
Quality gate: state snapshot written, novel-state.md updated, timeline updated, no contradictions with prior state

---

## File Structure Reference

```
<project-dir>/
  novel-state.md          # Phase tracker, chapter summaries, foreshadowing, 术语表, 数字表
  project-config.md       # Genre, tone, length, audience
  world.md                # World rules — minimum viable, grows with content
  characters/main/        # Main character profiles (detailed)
  characters/supporting/  # Supporting characters (brief, created as they appear)
  knowledge-state.md      # Cumulative knowledge tracking per character (Phase 4+)
  relationship-map.md     # Relationship network (created as needed in Phase 4+)
  plot.md                 # Structure, central conflict, turning points
  outline.md              # Volumes + milestones (NOT per-chapter scripts)
  foreshadowing-ledger.md # Foreshadowing tracking (Phase 6+, updated in Phase 8)
  timeline.md             # Scene-level time tracking (updated after each chapter)
  title-synopsis.md       # Title, synopsis, metadata
  chapters/               # chapter-001.md, chapter-002.md, ...
  state/                  # ch001.md, ch002.md, ... (immutable snapshots per IR-4, zero-padded)
  import/                 # (Bootstrap only) Original imported material
```

---

## Error Handling

Flag problems to the user with specific details and proposed resolutions — never silently patch or ignore. See **[references/error-handling.md](references/error-handling.md)** for the full protocol.

---

## Examples

- **New:** User says "I want to write a xianxia novel" → Phase 1, create project, begin dialogue
- **Resume:** User says "继续写我的小说" → Read novel-state.md, identify current phase, resume
- **Targeted:** User says "chapters 15-25 drag" → Jump to Phase 6, re-examine outline, propose fixes

---

## References

Loaded on demand — each phase's PRE-LOAD directive specifies which are mandatory.

> **Authority declarations:** 上下文加载协议 → SKILL.md IR-3 · Anti-AI 防御与检测 → anti-ai-system.md · 一致性追踪（含知识状态、伏笔账本）→ consistency-system.md · 节奏张力 → pacing-curve-reference.md

### Phase-Specific References (loaded per PRE-LOAD directive)

**Core Craft:** [anti-ai-system.md](references/anti-ai-system.md) (写作防御 Part 1 + 写后检测 Part 2) · [advanced-detection.md](references/advanced-detection.md) (写后审计，Tier 3 加载) · [chapter-writing-guide.md](references/chapter-writing-guide.md) · [prose-quality-framework.md](references/prose-quality-framework.md) (Tier 4, on-demand only) · [writing-styles.md](references/writing-styles.md) · [emotion-psychology.md](references/emotion-psychology.md) · [combat-scenes.md](references/combat-scenes.md)

**Story Architecture:** [excitement-engineering.md](references/excitement-engineering.md) · [plot-architecture.md](references/plot-architecture.md) · [outline-template-guide.md](references/outline-template-guide.md) · [pacing-curve-reference.md](references/pacing-curve-reference.md) · [narrative-craft.md](references/narrative-craft.md) · [subplot-management.md](references/subplot-management.md) · [genre-configs.md](references/genre-configs.md) · [craft-specialization.md](references/craft-specialization.md)

**World & Characters:** [world-building-guide.md](references/world-building-guide.md) · [character-design-guide.md](references/character-design-guide.md)

**Consistency & State:** [consistency-system.md](references/consistency-system.md) (含知识状态追踪 + 伏笔账本系统) · [state-extraction-guide.md](references/state-extraction-guide.md) · [pre-writing-brief.md](references/pre-writing-brief.md) · [editorial-roles.md](references/editorial-roles.md)

**Process & Advanced:** [proposal-system.md](references/proposal-system.md) · [memory-management.md](references/memory-management.md) · [error-handling.md](references/error-handling.md) · [advanced-workflows.md](references/advanced-workflows.md) · [revision-workflow.md](references/revision-workflow.md)

**Templates:** [project-config.md](templates/project-config.md) · [novel-state.md](templates/novel-state.md) · [title-synopsis.md](templates/title-synopsis.md) · [world.md](templates/world.md) · [character-card.md](templates/character-card.md) · [plot.md](templates/plot.md) · [outline-master.md](templates/outline-master.md) · [timeline.md](templates/timeline.md) · [chapter-plan.md](templates/chapter-plan.md) · [chapter-draft.md](templates/chapter-draft.md) · [state-snapshot.md](templates/state-snapshot.md) · [foreshadowing-ledger.md](templates/foreshadowing-ledger.md) · [knowledge-state.md](templates/knowledge-state.md) · [relationship-map.md](templates/relationship-map.md) · [editorial-report.md](templates/editorial-report.md)
