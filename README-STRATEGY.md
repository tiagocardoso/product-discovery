# Agent Product Strategy

A bootstrap kit for turning any Claude Code session into a **persistent, compounding knowledge base** for product strategy and product marketing — vision, strategies, products, intelligence, narrative, and go-to-market thinking.

Three variants — pick one and drop it into an empty project folder to scaffold a structured strategy wiki, then feed it raw material (brain dumps, strategy memos, analyst reports, competitor materials, market figures, news) and let the agent compile it into a cited, defensible argument.

| File | Size | Stance | When to use |
|------|------|--------|-------------|
| [`AGENT-PRODUCT-STRATEGY.md`](./AGENT-PRODUCT-STRATEGY.md) | ~86k chars | **Prescriptive** | Full opinionated version: complete templates for every layer, detailed command steps, page templates with frontmatter, explicit failure-mode table, 21 general rules. Use when you want maximum out-of-the-box scaffolding across strategy, intelligence, narrative, and GTM. |
| [`AGENT-PRODUCT-STRATEGY-LITE.md`](./AGENT-PRODUCT-STRATEGY-LITE.md) | 1,980 words | **Lean** | Compact starting point. All commands, layout, framings, research system, git integration, page templates preserved; verbose bodies trimmed. Use when you want a clean base to layer your own bias on top of — alternate strategic framework, engagement-specific deliverables, custom risk taxonomy. |
| [`AGENT-PRODUCT-STRATEGY-GIST.md`](./AGENT-PRODUCT-STRATEGY-GIST.md) | ~3,700 words | **Principles-only** | Philosophical version. Explains the *why* and the invariants (four layers, priors vs evidence, source credibility, gated research, scope as change-control, narrative-laddering, git-as-state) and lets the agent derive the *how*. Use with a capable agent when you want the structure to mould itself to your strategy. |

For a broader view — including how Strategy compares to the Discovery pattern — see the [main README](./README.md).

---

## Why this exists

Strategy work loses information in a particular way. Brain dumps sit in notebooks, memos drift away from the analyst reports that inspired them, a thesis lands in a deck and is never cited again, a competitor's move goes unnoticed until someone asks at a board meeting, and "what is our strategy, and what is it built on?" becomes an unanswerable question by month three.

This agent pattern solves that by treating the wiki as a **compiled argument**, not a retrieval index:

- Theses are cited, with ≥2 sources required before promoting above `confidence: medium`.
- Priors (brain dumps) and evidence are kept distinct — priors seed theses but cannot alone confirm them.
- Source credibility is tagged on every citation, and interested-party-only claims cap at medium confidence.
- The agent actively proposes research when gaps or contradictions appear, and runs a gated four-level deep-research loop when the user approves.
- Competitors are watched, market figures are refreshed, and staleness is lint-flagged on a time-based rhythm.
- Narrative (positioning, messaging, thought leadership) is kept in the same wiki and structurally laddered to strategy.

The result is a strategy wiki that **gets sharper with every source** and can be read by someone joining the organisation cold.

---

## What you get

When you bootstrap a new project, you get a scaffold organised into four complementary layers plus operations and raw capture:

| Layer | Purpose | Lives in |
|-------|---------|----------|
| **Foundation** | Vision, mission, values, world-assumptions | `wiki/00_foundation/` |
| **Strategies** | Argued theses: strategy spine, pillars, bets (with kill criteria), moats, anti-strategy | `wiki/01_strategies/<slug>/` |
| **Products** | Products you manage: capabilities, positioning, product-specific intelligence, strategy alignment | `wiki/02_products/<slug>/` |
| **Intelligence** | Market, competition, customer voice, audiences (ICPs, buyer/user personas) | `wiki/03_intelligence/` |
| **Narrative** | Core narrative, positioning, messaging pillars, category, value props, thought leadership | `wiki/04_narrative/` |
| **Go-to-market** | GTM motion, pricing & packaging, analyst relations (strategic layer only) | `wiki/05_go-to-market/` |
| **Domain knowledge** | Ontology, typed relationships, entities, concepts | `wiki/06_knowledge/` |
| **Operations** | Research queue + reports, sources, queries, shared registers | `wiki/07_operations/` |

Plus `raw/` for immutable source materials (split by type: brain-dumps, strategy-docs, product-docs, market, competitive, news, research-outputs) and `workspace/` for briefs, image opportunities, and research proposals.

---

## Quick start

1. Create an empty folder for your strategy practice.
2. Copy **one** of the three bootstrap files into it — Full, Lite, or Gist.
3. Open the folder in Claude Code.
4. Run `/bootstrap`.

Claude will ask for:
- Organisation and mission
- Vision (2–3 sentences on the 3–5 year future)
- Known strategies, products, primary competitors, target segments
- Strategy framework preference (Rumelt / Playing to Win / Wardley — default Rumelt)
- Analyst firms tracked, known ICPs
- Auto-commit mode (default `after-ingest`)

Then it scaffolds the wiki, initialises git, writes a `.gitignore`, seeds the ontology with strategy-specific entity and relationship types, creates templates, makes the initial commit, and writes a project-specific `CLAUDE.md`.

**After bootstrap, the bootstrap file has done its job.** The engagement is now driven by `CLAUDE.md` and the wiki itself.

### Choosing Full, Lite, or Gist

- **Full** (`AGENT-PRODUCT-STRATEGY.md`) — inline templates for every page type (strategy overview, Rumelt spine, bets with kill criteria, moats via 7 Powers, theses, research reports, positioning, messaging, world-assumptions, competitor profiles, audience clusters, thought-leadership suggestions), a 13-step `/bootstrap`, a 19-step `/ingest`, a fully specified `/research` gated loop, explicit failure-mode table, 21 general rules. Best when you want the agent to produce richly-shaped pages from day one and care about cross-engagement consistency.
- **Lite** (`AGENT-PRODUCT-STRATEGY-LITE.md`) — every command, the wiki layout, thesis-first framing, the four-level research system, git integration, plus a compact table-shape summary per page type. Best when you want a clean base to extend with your own conventions (alternate strategic framework, different strategic-risk taxonomy, extra deliverable pages, a narrative template tuned to your org).
- **Gist** (`AGENT-PRODUCT-STRATEGY-GIST.md`) — principles and invariants only, no folder tree, no templates, no command enumeration. Best when you trust the agent to derive a sensible concrete structure from the *why*, and when you want the wiki to mould to the specifics of your strategy and category.

All three variants share the same DNA and produce compatible output: thesis-first framing, cited evidence, priors kept distinct, source credibility tagged, gated research, git-as-state, narrative laddered to strategy.

---

## Core concepts

### Thesis-first framing

A strategy is a **structured argument**, not a wish. Each strategy carries:

- A **strategy spine** — diagnosis · guiding policy · coherent actions (Rumelt default), or winning aspiration · where-to-play · how-to-win · capabilities · management systems (Playing to Win), or Wardley mapping. Whichever is chosen at bootstrap is used consistently across all strategies.
- **Pillars** organising bets
- **Bets** with hypothesis, owner, horizon, and **pre-committed kill criteria**
- **Theses** — named cited claims; ≥2 sources required above medium confidence
- **Moats** — evidence-based defensibility via Helmer's 7 Powers, not aspirational
- **Anti-strategy** — explicit non-goals, excluded segments, capabilities we won't build

Every assumption is classified by one of five **strategic-risk types**:

- **Market** — is the market real, large enough, growing?
- **Positioning** — is our read of the landscape correct?
- **Capability** — can we build/acquire what we need?
- **Execution** — can we run this at the required speed, scale, quality?
- **Viability** — economics, regulation, compliance, ethics, brand

Coverage gaps across the five types are a leading indicator of downstream surprise.

### Priors vs evidence

The pattern distinguishes two kinds of material that look alike and are fundamentally different:

- **Priors** — the user's own convictions, captured via brain dumps. Precious: they seed theses and shape questions. But they cannot alone confirm anything. Claims grounded only in priors carry `[PRIOR: <slug>]` tags and cap at `confidence: low` until corroborated.
- **Evidence** — cited analyst views, market figures, customer quotes, competitor-material statements, research outputs. Evidence is what promotes a thesis from *what we believe* to *what we can defend*.

This distinction is what prevents a strategy from being quietly overfitted to the founder's worldview.

### Source credibility

Not all evidence is equal. Every source carries a credibility tag:

- `primary-neutral` — filings, primary data, peer-reviewed research
- `primary-interested` — vendor/company marketing
- `secondary-neutral` — reputable analyst firm, credible journalism
- `secondary-interested` — sponsored content, advocacy

Claims sourced only from `interested` parties cap at `confidence: medium` no matter how many interested voices repeat them. This catches the most common failure mode: believing the category's collective marketing.

### The gated research loop

The behaviour that most distinguishes the Strategy pattern from Discovery is that the agent actively proposes research, and runs deep research loops when the user approves. Four levels, gated at every transition:

| Level | Goal | Runs when |
|-------|------|-----------|
| **L1 Orient** | Wiki-first check, ~15–25 web searches, scoping memo with depth recommendation | Always |
| **L2 Validate** | Load-bearing claims get ≥2 independent sources | User approves |
| **L3 Deep** | Primary sources, credibility-weighted, paywalled PDFs requested, adversarial reads | User approves |
| **L4 Exhaustive** | Thesis-grade, triangulated three ways, hunt falsification | User gives **extra** confirmation |

At every transition the agent reports what the next level would pursue and the user can **approve / narrow / skip / stop**. Work compounds across levels; nothing is thrown away. Caps enforce termination, and when a cap is hit without closure the report is filed as **partial** with an explicit gap list.

Findings are **living artifacts**: reports can be *extended* to the next level, *redone* from scratch when the world has shifted (old one preserved as superseded), or *challenged by ingestion* — when a new source contradicts a report at ≥ equal credibility, the agent banners both sides and queues a **suggested redo** for user approval. Staleness lint flags time-old reports as suggested refreshes on their own rhythm.

### Narrative laddered to strategy

Product marketing and strategy often drift apart in practice. The pattern prevents this structurally: every messaging pillar references exactly one strategic pillar; every thought-leadership article cites at least one thesis, one customer-voice element, and one market or competitive fact. Orphan messaging and ungrounded thought leadership are flagged by `/lint`.

### Clusters and the inbox

Raw material arrives through an **inbox** organised into **clusters** — bounded sets of files that belong together and are processed in one `/ingest` operation.

Cluster types: `brain-dump` · `strategy-doc` · `product-doc` · `analyst-report` · `white-paper` · `market-figures` · `news-pack` · `competitor-material` · `research-output` · `mixed` · `document-pack`.

Each cluster has a `_manifest.md` describing its contents, scope, priority, dependencies, and **credibility**. The agent reads manifests only until you've confirmed a cluster for ingestion.

### Consolidation tiers

| Tier | Location | Lifecycle |
|------|----------|-----------|
| Raw | `raw/` | Immutable, locked after capture |
| Episodic | `07_operations/sources/`, research reports | Permanent reference once written |
| Semantic | `06_knowledge/entities/`, `06_knowledge/concepts/` | Updated as evidence accumulates |
| Procedural | `06_knowledge/ontology.md`, `00_foundation/`, `07_operations/shared/` | Slowest to change, highest confidence |

### Git is the state mechanism

There is no separate snapshot mechanism — **git commits are the snapshots**: diffable, point-in-time, reproducible. Every meaningful operation that changes files can be followed by a commit, automatically after `/ingest` by default. Commits are always local; pushing is a manual user decision. Briefs are pinned to the commit SHA they were generated from, so shared artefacts are always reproducible against the repo state that produced them.

### Visibility tiers

- `internal` — working documents
- `team` — shared within the delivery team
- `leadership-ready` — polished deliverables for leadership review
- `board-ready` — board-grade: fully cited, evidence-confidence high
- `confidential` — board-only or strictly need-to-know

`/brief` supports `default`, `board`, and `external` presets, with the `external` preset excluding `internal`, `team`, and `confidential`.

---

## Command reference

Run these inside Claude Code once the wiki is bootstrapped.

| Command | When to use |
|---------|-------------|
| `/bootstrap` | Once, at the start. Scaffolds the wiki, inits git, writes `CLAUDE.md`. |
| `/ingest` | Whenever you have new material. Processes clusters; proposes research and thought-leadership angles; detects contradictions. |
| `/research <id>` | Run a gated deep-research loop. Variants: `extend`, `redo [from-L<n>]`, or `/research "<free-form question>"` as a shortcut. |
| `/query <question>` | Ask anything. Produces a cited answer filed to the right scope. |
| `/commit ["<msg>"]` | Structured git commit of wiki + raw + workspace state. |
| `/auto-commit <mode>` | Configure when the agent commits automatically. Modes: `off`, `after-ingest` *(default)*, `after-research`, `after-every-command`, `daily`. |
| `/lint` | Health-check with auto-fix. Scope with `/lint <slug>`, `/lint knowledge`, `/lint research`, `/lint git`, etc. |
| `/status` | Chat-only orientation: readiness, blockers, recent commits, uncommitted drift. |
| `/brief [board\|external]` | Compile visibility-filtered pages into a shareable markdown (or `/brief marp` for slides). SHA-pinned. |
| `/generate-image <ID>` | Render an image opportunity using OpenAI or Gemini APIs. |

---

## A typical workflow

**Day 0 — setup**

```
/bootstrap
```

Answer the prompts. The agent scaffolds everything, inits git, and makes the initial commit.

**Day 1 — first material**

Drop brain dumps in `raw/brain-dumps/<cluster>/`, an analyst PDF in `raw/market/<cluster>/`, and competitor materials in `raw/competitive/<cluster>/`. Fill in each `_manifest.md`.

```
/ingest
```

Pick your clusters. The agent reads, creates source pages, extracts entities and concepts, refines your strategy theses, updates competitor profiles and market intelligence, proposes candidate research, and — if `auto-commit: after-ingest` — commits the whole set.

**Day 3 — approve and run research**

Review the research queue. Approve an item. Kick off:

```
/research R-007
```

L1 runs: wiki-first grounding + web sweep + scoping memo with a depth recommendation. The agent asks whether to proceed to L2. You approve. L2 runs: every load-bearing claim gets ≥2 independent sources. The agent asks about L3. You approve (or stop). L3 runs, possibly asking you for a paywalled PDF mid-loop. Findings are written back into strategy, intelligence, and knowledge pages with citations.

**Day 5 — query**

```
/query What's our best-defensible thesis for EMEA expansion, and where is the evidence weakest?
```

The agent reads the relevant strategy, intelligence, and research pages, cites every claim, files the answer, and asks whether it should promote anything into the knowledge layer or queue new research.

**Day 10 — ingest new material, contradiction surfaces**

A new analyst report contradicts a figure a completed research report relied on. During `/ingest`, the agent banners the report, adds `[CONTRADICTS R-007]` to the new evidence, and queues a **suggested redo** with rationale and priority.

**Day 14 — periodic health check**

```
/lint
```

Auto-fixes what it can. Flags: one bet without kill criteria, a messaging pillar unladdered to a strategic pillar, a competitor whose `moves-log.md` hasn't been updated in >90 days, a research report >6 months old flagged for refresh, uncommitted drift from the last few commands.

**Day 30 — board review**

```
/commit "pre-board checkpoint"
/brief board
```

Compile a board-grade brief: strategy-on-a-page per strategy, moats, readiness, top-3 risks, bets with kill criteria, key world-assumptions, intelligence highlights. Pinned to a reproducible commit SHA.

---

## What "good" looks like

A well-run strategy wiki accumulates these properties:

- **Every claim is cited.** No free-floating assertions.
- **Priors and evidence are distinct.** Brain-dump-only theses stay `confidence: low`.
- **Source credibility is tagged.** Interested-only claims never reach `high`.
- **Theses have ≥2 sources.** No single-sourced theses at medium+ confidence.
- **Bets carry kill criteria.** No bet lives at `leadership-ready` without one.
- **Messaging pillars ladder to strategic pillars.** No orphan marketing.
- **Thought leadership is grounded.** Every article cites ≥1 thesis + ≥1 customer voice + ≥1 market/competitive piece.
- **Competitor moves are fresh.** No `moves-log.md` stale >90 days.
- **Research reports are gated and audited.** Every run's findings trace back to archived source excerpts.
- **Contradictions trigger suggested redos.** Stale material gets refresh suggestions.
- **Anti-strategy is explicit.** Strategies with ≥3 clusters of material name their non-goals.
- **World-assumptions are watched.** Challenges banner the foundation; load-bearing challenges become research.
- **Commits tell the story.** Every meaningful operation has a structured commit.

`/lint` checks all of these automatically and reports gaps.

---

> Note: the exact folder/file names below are what Full and Lite scaffold. Gist lets the agent pick — expect the same conceptual layers but possibly different names.

## File layout after bootstrap

```
<engagement-root>/
├── CLAUDE.md                      # operating config with auto-commit, framework, visibility levels
├── README.md                      # engagement summary
├── .gitignore                     # repo hygiene
├── AGENT-PRODUCT-STRATEGY*.md     # the bootstrap file you chose (removable post-bootstrap)
│
├── wiki/
│   ├── index.md                   # master navigation — always read first
│   ├── log.md                     # append-only operations log
│   ├── 00_foundation/             # vision, mission, values, world-assumptions
│   ├── 01_strategies/<slug>/      # one folder per strategic thesis
│   ├── 02_products/<slug>/        # products you manage
│   ├── 03_intelligence/
│   │   ├── market/                # segments, trends, figures, analyst-views, regulatory, scenarios
│   │   ├── competition/           # landscape, comparison-matrix, moves-playbook, per-competitor pages
│   │   ├── customer-voice/        # verbatim quotes, case-study material, review extracts, win-loss themes
│   │   └── audiences/             # ICPs, buyer personas, user personas, buying committees
│   ├── 04_narrative/              # core narrative, positioning, messaging pillars, thought leadership
│   ├── 05_go-to-market/           # GTM motion, pricing & packaging, analyst relations (strategic layer)
│   ├── 06_knowledge/              # ontology, typed relationships, entities, concepts
│   └── 07_operations/             # research queue + reports, sources, queries, shared registers
│
├── raw/
│   ├── _inbox-index.md
│   ├── inbox/<cluster>/           # generic drop zone
│   ├── brain-dumps/<cluster>/     # priors (not evidence)
│   ├── strategy-docs/<cluster>/   # internal strategy memos
│   ├── product-docs/<cluster>/    # product documentation (yours or competitors')
│   ├── market/<cluster>/          # analyst reports, white papers, market figures
│   ├── competitive/<cluster>/     # competitor materials
│   ├── news/<cluster>/            # sector news, signals
│   ├── research-outputs/<R-XXX>/  # archived research citations (excerpts + URLs + dates)
│   └── assets/
│
└── workspace/
    ├── image-opportunities.md     # registry of image generation opportunities
    ├── research-proposals/        # agent-drafted proposals awaiting approval
    ├── assets/images/             # generated images
    └── brief-YYYY-MM-DD.md        # compiled briefs (SHA-pinned)
```

---

## Prior art

The structure draws from established strategy and product-marketing practice — no single framework is required reading.

- **Strategy as structured argument** — Richard Rumelt, *Good Strategy / Bad Strategy*
- **Where-to-play / how-to-win cascade** — A.G. Lafley & Roger Martin, *Playing to Win*
- **Wardley mapping** — Simon Wardley, *Wardley Maps*
- **Seven Powers** (moats) — Hamilton Helmer, *7 Powers: The Foundations of Business Strategy*
- **Positioning** — April Dunford, *Obviously Awesome*
- **Strategic narrative** — Andy Raskin, "The greatest sales deck I've ever seen"
- **Category design** — Al Ramadan et al., *Play Bigger*
- **Jobs-to-be-done** — Christensen / Klement
- **Discovery heritage** — Teresa Torres (*Continuous Discovery Habits*) for the problem-first discipline underneath strategy work
