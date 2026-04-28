# Agent Product Strategy

## What this is

This file turns any Claude Code session into a **persistent, compounding knowledge base for product strategy and product marketing** — the vision, strategy, intelligence, narrative, and go-to-market thinking that guides what a product or portfolio does and why.

It has four complementary purposes that run in parallel:

1. **Strategy** — named strategic theses, bets, capabilities, moats, and non-goals. The structured argument for where we play and how we win.
2. **Intelligence** — market, competitive, and customer-voice evidence. The cited, confidence-tagged world the strategy is reacting to.
3. **Narrative** — core story, positioning, messaging pillars, and thought leadership. How the strategy is told externally.
4. **Domain knowledge** — entities, concepts, ontology, typed relationships. A reusable map that anyone can read to understand the domain independent of the strategy process.

**Thesis-first framing.** Strategies are **structured arguments** — diagnosis → guiding policy → coherent actions (Rumelt), or aspiration → where-to-play → how-to-win → capabilities → management systems (Playing to Win). Every strategy carries cited theses, assumptions classified by strategic risk, bets with pre-committed kill criteria, and research that validates or breaks its load-bearing claims. Convictions (brain dumps, priors) seed theses but cannot alone confirm them.

The wiki is a **compiled artifact**, not a retrieval index. When you add a new source, the agent reads it, integrates it into the existing wiki, updates entity pages, strengthens or challenges existing theses, and promotes knowledge up through consolidation tiers. Knowledge accumulates. Contradictions are flagged. Syntheses persist.

**Research is active.** The agent proposes candidate research as the wiki grows. When you approve it, the agent runs a four-level deep-research loop — always starts at L1 (scoping + public web sweep), gates every escalation with your approval, and writes findings back into the wiki as cited evidence that updates strategies, theses, competitors, and market pages.

**State is in git.** There is no separate snapshot mechanism. Git commits are the snapshots — diffable, point-in-time, reproducible.

**To use:** drop this file into an empty folder, open it in Claude Code, and run `/bootstrap`.

**Lifecycle:** this file is a bootstrap-only tool. Once `/bootstrap` has run, `CLAUDE.md` is the operating config for the engagement. Improvements to the pattern should be made here and then reflected in active `CLAUDE.md` files — not the other way around. `CLAUDE.md` may override or extend any behaviour defined here for engagement-specific needs.

**Section map:** Commands · Common failure modes · Wiki layout · Strategy framing · Inbox and cluster system · Knowledge layer · Research system · Git integration · Labels, status, confidence · `/bootstrap` · `/ingest` · `/research` · `/query` · `/commit` and `/auto-commit` · `/lint` · Reporting commands · Images & diagrams · Page templates · General rules

---

## Commands

| Command | When to use |
|---------|------------|
| `/bootstrap` | Once, at the start. Scaffolds the wiki, initialises git, writes `CLAUDE.md` with config. |
| `/ingest` | Whenever you have new material to process. Shows available clusters and lets you choose what to ingest now vs later. Proposes candidate research and thought-leadership angles. |
| `/research <id>` | Run a deep-research loop on a queued research item. Always L1 first; gated escalation to L2/L3/L4. |
| `/research <id> extend` | Escalate a completed research item to the next level. |
| `/research <id> redo [from-L<n>]` | Fresh run; prior report marked superseded. Default L1. |
| `/research "<free-form question>"` | Shortcut: creates the queue item and kicks off L1 in one shot. |
| `/query <question>` | Ask anything about the strategy, intelligence, or domain. Produces a filed answer page. |
| `/commit ["<message>"]` | Structured git commit of wiki + raw + workspace state. Replaces snapshots. |
| `/auto-commit <mode>` | Configure when the agent commits automatically. Modes: `off`, `after-ingest`, `after-research`, `after-every-command`, `daily`. |
| `/lint` | Periodically, to health-check the wiki. `/lint <scope>` to narrow (e.g. `/lint ai-native`, `/lint knowledge`, `/lint narrative`). |
| `/status` | Quick chat-only orientation: readiness, top blockers, recent commits, uncommitted drift. |
| `/brief [board\|external]` | Compile `visibility` pages into a shareable markdown (default) or Marp deck (`/brief marp`). `board` and `external` are curated presets. |
| `/generate-image <ID>` | Generate the image for an opportunity in `workspace/image-opportunities.md`. Pass no ID to batch-select pending entries. |

---

## Common failure modes

Quick decision reference for ambiguous situations:

| Symptom | Wrong response | Correct response |
|---------|----------------|-----------------|
| Cluster `_manifest.md` missing or malformed | Skip or refuse to ingest | Read what's parseable, flag the gaps, offer to create/fix; ask the user to confirm |
| Query covers the same ground as an existing query | Create a new parallel file | Set `supersedes:` on the new one; mark the old `status: superseded` |
| Brain dump states a strong claim | Treat as evidence | Treat as `[PRIOR]`; inform theses but do not alone confirm a claim |
| Ingested source contradicts a completed research report | Silently update a wiki page | Banner the report with `⚠ contradicted by S-XXX`; append a **suggested redo** to the research queue |
| Load-bearing numeric claim found from a single vendor-marketing source | Accept and move on | Tag source-credibility as `primary-interested`; require ≥2 independent sources before promoting the claim |
| Strategy has bets but no explicit non-goals after 3+ clusters | Leave `anti-strategy.md` empty | Prompt the user: *"Propose non-goals based on what's been consistently excluded?"* |
| Messaging pillar not tied to any strategic pillar | Leave it orphan | Flag in `/lint`; prompt user to ladder it or drop it |
| Research run hits the L3 loop cap without closing contradictions | Pretend it's done | File as **partial** with a "what's still missing" section and suggest a redo |
| Assumption logged without a strategic-risk type | Leave blank | Classify as `market` / `positioning` / `capability` / `execution` / `viability` — unclassified assumptions aren't actionable |
| World-assumption challenged by a new source | Leave the page as-is | Add a contested banner on the assumption page; recommend `/research` if the assumption is load-bearing |

---

## Wiki layout

```
wiki/
  index.md                              — master navigation; always read first
  log.md                                — append-only operations log; never edit, only append

  00_foundation/                        — the why; stable, rarely edited
    vision.md                           — 3–5 year vision of the world we're building toward
    mission.md                          — what we exist to do
    values-and-principles.md            — operating principles the strategy must honour
    world-assumptions.md                — macro priors underpinning everything; cited,
                                           confidence-tagged, banner-flagged when challenged

  01_strategies/                        — the core scopes; one folder per strategic thesis
    <strategy-slug>/
      overview.md                       — aspiration, one-paragraph thesis, scope boundary
      strategy-spine.md                 — the chosen framework's structure (default: Rumelt kernel)
      pillars.md                        — named strategic pillars that organise bets
      anti-strategy.md                  — non-goals, excluded segments, capabilities we won't build
      bets-and-initiatives.md           — bet register; each has hypothesis, owner, horizon, kill criteria
      moats.md                          — defensibility analysis using Helmer's 7 Powers; evidence-based
      findings/
        theses.md                       — named strategic claims, each ≥2 cited sources
        assumptions-and-risks.md        — classified by strategic-risk type
        evidence-log.md                 — verbatim quotes + cited figures from sources
        research/                       — completed research reports scoped to this strategy
        decision-log.md
        deliverables/                   — leadership/board-facing pages
          01-strategy-on-a-page.md
          02-market-position.md
          03-capability-roadmap.md
          04-thought-leadership-angles.md
      research/
        queue.md                        — candidate research items, agent-proposed + user-added
        active.md                       — in-flight research with current level and status
        open-questions.md
        next-steps.md
        checklist.md                    — strategic-readiness tracker (⬜🟡✅⛔🧊)

  02_products/                          — products/services you manage
    <product-slug>/
      overview.md                       — what it is, target segment, current positioning
      product-docs/                     — ingested product documentation summarised
      capabilities.md                   — capability inventory with maturity ratings
      positioning.md                    — our stated positioning vs. market
      market-intelligence.md            — market signals specific to this product
      competition.md                    — competitor comparison scoped to this product
      strategy-alignment.md             — which 01_strategies/ entries this product serves (primary + secondary)
      findings/                         — same shape as strategies
      research/                         — product-specific research queue + active

  03_intelligence/                      — what the world shows us
    market/
      README.md
      segments.md                       — named segments with sizing
      trends.md                         — tracked macro and sector trends
      figures.md                        — TAM/SAM/SOM, growth rates, adoption curves (all cited)
      analyst-views.md                  — Gartner, Forrester, IDC, boutiques
      regulatory.md                     — regulatory and compliance factors
      scenarios.md                      — named futures with leading indicators + strategic response
    competition/
      README.md                         — competitor shortlist + watch-list
      landscape.md                      — market map / positioning grid
      comparison-matrix.md              — capability-by-capability across competitors
      moves-playbook.md                 — pre-thought responses: "if competitor X does Y, we do Z"
      <competitor-slug>/
        profile.md
        strategy-read.md                — our read of their strategy, cited from their materials
        capabilities.md
        moves-log.md                    — date-stamped log of launches, hires, pricing moves
        evidence/
    customer-voice/
      README.md
      verbatim-quotes.md                — cited customer quotes, source-tagged
      case-study-material.md            — raw material for case studies
      review-extracts.md                — G2, Gartner Peer Insights, TrustRadius, etc.
      survey-themes.md                  — patterns from surveys
      win-loss-themes.md                — named patterns across wins and losses (not individual deals)
    audiences/
      README.md
      cluster-NN-<slug>.md              — ICPs, buyer personas, user personas, buying committees

  04_narrative/                         — how we tell the story externally
    core-narrative.md                   — problem → shift → consequence → resolution (Raskin shape)
    positioning.md                      — Dunford template
    messaging-pillars.md                — 3–5 load-bearing messages, each laddered to a strategic pillar
    category-definition.md              — entering / reshaping / designing a category (Play Bigger)
    value-propositions.md               — specific promises per ICP
    thought-leadership/
      pipeline.md                       — suggested → drafting → approved → published
      suggested/                        — agent-proposed drafts awaiting approval
      drafts/                           — user-approved, in development
      published/                        — finalised (links out if externally hosted)

  05_go-to-market/                      — strategic layer only, not tactics
    gtm-motion.md                       — product-led / sales-led / partner-led / community-led
    pricing-and-packaging.md            — strategic frame; tiers and what each signals — not SKUs
    analyst-relations.md                — which firms/analysts matter, target placements, relationship state

  06_knowledge/                         — semantic tier; reusable domain map
    README.md
    ontology.md                         — entity types, relationship types, concept hierarchy
    relationships.md                    — master typed-relationship register
    entities/
      people/                           — named individuals (analysts, execs, experts)
      organisations/                    — customers, partners, regulators, analyst firms
      competitors/                      — companies we compete with (lightweight; depth in 03_/competition)
      markets/                          — named markets and segments
      capabilities/                     — named capabilities (ours, theirs, generic)
      products/                         — products in the world
      publications/                     — named publications (reports, books, white papers)
      analyst-firms/
    concepts/                           — strategy concepts: moat, network effect, JTBD, category, etc.
    queries/README.md

  07_operations/                        — research, sources, queries, shared registers
    research/
      README.md
      queue.md                          — global roll-up of all scope queues
      reports-index.md                  — index across all R-XXX reports
      cross-cutting/                    — reports not owned by a single strategy/product
    sources/
      README.md                         — sequential S-XXX log + source-type taxonomy
    queries/                            — global queries
      README.md
    shared/
      executive-summary.md
      strategic-readiness.md            — roll-up of per-strategy checklist %
      top-strategic-questions.md        — P0/P1/P2 unresolved questions
      master-assumptions-log.md
      master-risks-log.md
      master-decisions-log.md
      cross-strategy-watch-list.md      — themes to listen for across ingests
      stakeholders.md
      project-context.md
      config.md                         — bootstrap config: framework, auto-commit mode, visibility levels

raw/
  _inbox-index.md                       — lightweight index of ALL clusters across all raw/ subfolders
  inbox/<cluster-slug>/                 — generic drop zone; _manifest.md + files
  brain-dumps/<cluster-slug>/           — user's notes, thoughts, memos — treated as priors, not evidence
  strategy-docs/<cluster-slug>/         — internal strategy documents
  product-docs/<cluster-slug>/          — documentation of your products or others'
  market/<cluster-slug>/                — analyst reports, white papers, market figures
  competitive/<cluster-slug>/           — competitor materials, news about them
  news/<cluster-slug>/                  — sector news, signals
  research-outputs/<research-id>/       — source archives from research runs (excerpts + URLs + dates)
  assets/                               — images, handouts, exported data

workspace/
  image-opportunities.md                — registry of image generation opportunities (append-only)
  research-proposals/                   — agent-drafted research proposals awaiting approval
  assets/images/                        — AI-generated images stored here (<ID>.png)
  brief-YYYY-MM-DD.md                   — compiled shareable brief (created by /brief)
```

Not every engagement needs every folder. Optional folders (marked `status: optional` by `/bootstrap`): `moats.md`, `anti-strategy.md`, `04_narrative/thought-leadership/`, `05_go-to-market/analyst-relations.md`. They exist in the scaffold but the agent does not prompt for content until the user opts in or the material naturally arrives.

---

## Strategy framing

### Vocabulary

- **Strategy** — a named, argued thesis about *where to play and how to win*. The scope and unit of work at `01_strategies/<slug>/`. Broader than a single bet.
- **Pillar** — a durable sub-area of a strategy (a "branch" of the tree). Organises bets.
- **Bet** — a concrete investment under a pillar, with a hypothesis, owner, horizon, and **pre-committed kill criteria**. Bets are testable; strategies are arguable.
- **Thesis** — a named strategic claim (e.g. *"Data gravity will dominate vendor choice in EMEA by 2027"*). Theses are cited, confidence-tagged, and feed or challenge strategies.
- **Anti-goal** — something the strategy explicitly will not pursue. Makes trade-offs legible.
- **World-assumption** — a macro prior that must hold for the strategy to make sense. Lives at `00_foundation/world-assumptions.md`. Challenged by incoming evidence.
- **Moat** — a defensibility claim framed via Helmer's 7 Powers; evidence-based, not aspirational.
- **Prior** — a strongly-held belief captured in a brain dump. Informs theses; cannot alone confirm a claim.

### Framework choice

At `/bootstrap`, the user picks the strategy framework used to structure `strategy-spine.md` across the engagement:

- **Rumelt kernel** (default) — diagnosis · guiding policy · coherent actions. Most general; good fit for most engagements.
- **Playing to Win** (Lafley / Martin) — winning aspiration · where to play · how to win · core capabilities · management systems.
- **Wardley mapping** — user need · value chain · evolution axis · climatic patterns · doctrine.

Whichever is chosen, every strategy page in `01_strategies/<slug>/strategy-spine.md` uses the same spine. Changing framework mid-engagement is expensive — flag it explicitly and rewrite spines deliberately.

### The strategy loop

Every strategy is a **structured argument**. The flow:

`Mission + Vision (00_foundation) → Diagnosis of the world (03_intelligence) → Strategy spine (01_strategies/<slug>/strategy-spine.md) → Pillars → Bets (with kill criteria) → Theses → Assumptions classified by strategic risk → Research (validate, extend, or break) → Evidence → Insights → Decisions → Deliverables → Narrative and positioning (04_narrative) → Go-to-market expression (05_go-to-market)`

These artefacts reinforce each other. Evidence in an ingest should always land somewhere; theses should always cite ≥2 sources; bets should always carry kill criteria; messaging pillars should always ladder to a strategic pillar; capabilities should always be traceable to bets that require them.

<details>
<summary>Prior art this structure draws from</summary>

- **Diagnosis / guiding policy / coherent actions** — Richard Rumelt, *Good Strategy / Bad Strategy*
- **Where-to-play / how-to-win** — A.G. Lafley & Roger Martin, *Playing to Win*
- **Wardley mapping** — Simon Wardley, *Wardley Maps*
- **7 Powers** — Hamilton Helmer, *7 Powers: The Foundations of Business Strategy*
- **Category design** — Al Ramadan et al., *Play Bigger*
- **Positioning** — April Dunford, *Obviously Awesome*
- **Strategic narrative** — Andy Raskin, "The greatest sales deck I've ever seen"
- **Jobs-to-be-done** — Christensen / Klement
- **Discovery heritage** — Teresa Torres (*Continuous Discovery Habits*) for the problem-first discipline that sits under strategy work

</details>

---

## Inbox and cluster system

The inbox is the **staging area** for all raw material, organised into **clusters** — bounded sets of files that belong together and can be processed in one operation. A cluster is the unit of ingest: one cluster = one `/ingest` call. Keeping clusters small and scoped prevents context overload and allows phased processing.

**To add material:** create a folder under the correct `raw/` subtree (`inbox`, `brain-dumps`, `strategy-docs`, `product-docs`, `market`, `competitive`, `news`, `research-outputs`), drop your files into it, and fill in the `_manifest.md` (template below). The agent reads manifests to build the cluster menu; it never opens raw files until you confirm a cluster for ingestion.

**Cluster types:** `brain-dump` (user's notes — treated as priors) · `strategy-doc` (internal strategy memo, yours or another org's) · `product-doc` (product documentation, yours or a competitor's) · `analyst-report` (Gartner, Forrester, IDC, boutique analyst) · `white-paper` · `market-figures` (data exports, CSVs, research data) · `news-pack` (articles, press releases, signal clippings) · `competitor-material` (a competitor's own materials) · `research-output` (a completed external research study you commissioned or obtained) · `mixed` (heterogeneous materials from one contributor) · `document-pack` (generic).

**Brain dumps are priors, not evidence.** The agent tags any claim sourced from `raw/brain-dumps/` as `[PRIOR: <slug>]`. Priors seed theses; they do not confirm them. A thesis grounded only in priors is tagged `confidence: low` until ≥2 independent non-prior sources corroborate it.

**Source-credibility tagging.** Every cluster carries a `credibility` field in its `_manifest.md`: `primary-neutral` (filings, primary data, peer-reviewed research) · `primary-interested` (company marketing, vendor-produced material) · `secondary-neutral` (reputable analyst firm, credible journalism) · `secondary-interested` (sponsored content, advocacy). Claims sourced only from `interested` parties never promote above `confidence: medium` without corroboration.

`raw/_inbox-index.md` is a table (columns: #, Cluster, Display name, Scope, Type, Credibility, Size, Priority, Status, Added, Depends on) maintained automatically by the agent after every ingestion. It is the single file read during `/ingest` Phase 1.

---

## Knowledge layer in depth

The `06_knowledge/` section is the **semantic tier** of the wiki. It is organised around the domain, not the strategy — anyone unfamiliar with the strategy process can read these pages to understand how the domain works.

### Consolidation tiers

| Tier | Location | What it contains | Changes how |
|------|----------|-----------------|------------|
| Raw | `raw/` | Immutable source files | Never — locked after capture |
| Episodic | `07_operations/sources/`, research reports | Source summaries, research digests | Permanent reference once written |
| Semantic | `06_knowledge/entities/`, `06_knowledge/concepts/` | Entity profiles, domain concepts, typed relationships | Updated as evidence accumulates; supersession tracked |
| Procedural | `06_knowledge/ontology.md`, `00_foundation/`, `07_operations/shared/` | Cross-cutting patterns, vocabulary, world-level priors | Slowest to change; highest confidence |

A fact seen once stays episodic. A fact confirmed across three independent sources is promoted to a semantic entity or concept page with `confidence: high`.

### Entity types, relationship types, concepts

Defined canonically in `wiki/06_knowledge/ontology.md`. Knowledge extraction and query steps reference the ontology rather than repeating the types here. Seed entity types for a strategy wiki:

- `person`, `organisation`, `analyst-firm`, `publication`
- `competitor`, `product`, `capability`, `market-segment`, `trend`, `scenario`, `regulatory-factor`
- `strategy`, `pillar`, `bet`, `thesis`, `anti-goal`, `moat`, `world-assumption`
- `value-proposition`, `JTBD`, `narrative`, `positioning-statement`, `messaging-pillar`, `category`
- `customer-voice-quote`, `win-loss-theme`
- `concept`

Seed relationship types:

- `owns`, `manages`, `uses`, `depends-on`, `produces`, `consumes`, `related-to`
- `contradicts`, `supersedes`, `caused-by`, `mitigated-by`
- `serves` (strategy → segment), `threatens` (competitor → strategy), `defends` (moat → strategy)
- `enables` (capability → bet), `laddersTo` (messaging-pillar → strategic-pillar)
- `tested-by` (thesis → research-report), `cited-from` (claim → source)
- `aligns-with` (product → strategy; with `primary: true/false`)

### Confidence and supersession

Every entity attribute and concept claim carries a confidence level. Claims contradicted by newer sources are marked `[SUPERSEDED YYYY-MM-DD by S-XXX: <replacement>]` — the old value is preserved for audit.

---

## Research system

Research is the active engine of the strategy wiki. The agent proposes candidate research during `/ingest`; the user approves items onto the queue; `/research <id>` runs a deep, gated research loop that writes cited findings back into the wiki.

### The four levels

Every research run begins at L1. Escalation to each next level is **gated by user approval**. The user can stop, narrow, skip ahead, or approve-as-proposed at every gate. Work compounds across levels — nothing is thrown away.

| Level | Goal | Stop criteria | Rough cost |
|-------|------|---------------|-----------|
| **L1 Orient** *(always runs)* | Read wiki + raw, decompose into sub-questions, run a meaningful public-web sweep (~15–25 searches), produce a **scoping memo** with depth recommendation | Scoping memo written — fixed scope | ~20–40 min |
| **L2 Validate** | Every load-bearing claim from L1 has ≥2 independent sources; easy contradictions resolved; source diversity expanded | Every sub-question has ≥2 independent sources OR is explicitly marked "unresolvable at this depth" | ~45–90 min on top of L1 |
| **L3 Deep** | Primary sources preferred; source-credibility tagged; paywalled PDFs requested from user if needed; adversarial sources read | No new info surfaced in last iteration · all numeric claims have primary-source citations · contradictions closed or flagged as genuinely open | ~2–4 hours on top of L2 |
| **L4 Exhaustive** | Thesis-defining rigour; triangulate three ways; synthesise across disciplines; actively hunt falsification | Agent cannot find a new angle to challenge the finding within the loop cap | Several hours; may span multiple runs; **always requires explicit extra user confirmation** |

L3 has a hard loop cap of 10 iterations. L4 is additionally gated: the agent must name the specific load-bearing thesis that justifies L4, and the user must explicitly confirm before L4 runs. If any cap is hit without stop criteria met, the report is filed as **partial** with a "what's still missing" section — never pretended done.

### Wiki-first at every level

Before any web search in any level, check whether the wiki already holds the answer. Strategy wikis accumulate hard numbers, analyst quotes, and competitor facts — re-searching for what's already in `07_operations/sources/` wastes budget and risks citing a worse version of a claim the wiki has nailed down. Prefer wiki-held facts (with the source page cited) over re-fetched web claims when both exist.

### L1 — Orient (the scoping memo)

L1 always runs and its deliverable is the scoping memo. The memo contains:

- **Question restated** + sub-questions the agent decomposed it into
- **What wiki + raw already hold** (cited page-by-page; often brief, sometimes empty)
- **What the L1 web sweep found** — cited, confidence-tagged, grouped by sub-question
- **Synthesis so far** — the agent's current best answer per sub-question, with confidence
- **Gaps** — sub-questions not answered, claims with only one weak source, contradictions unresolved
- **Recommendation and rationale** — one of:
  - *"L1 is enough. Here's the answer."* (valid outcome for well-covered or low-stakes questions)
  - *"Recommend L2. These specific claims need corroboration: [list]."*
  - *"Recommend L3. This is thesis-defining and current sourcing is weak."*
  - *"Recommend L4. This claim is load-bearing for [specific strategy/bet] and needs board-grade rigour."*

The recommendation is always **evidence-driven**: the agent names specific weak claims or specific gaps, not generic hand-waving.

### Gate behaviour at every transition

At each level boundary the agent:

1. Writes an updated version of the report (appends, does not re-file) with what the completed level produced
2. States what the next level would specifically pursue — named claims, sub-questions, gaps
3. Estimates effort
4. Asks for approval, which can be:
   - **Approve as proposed** → proceed
   - **Narrow** → user restricts scope; agent re-plans and asks again
   - **Skip ahead** → jump past a level
   - **Stop** → finding filed at current level; queue item marked `completed-at-L<n>`
5. **Mid-level escalation**: if during L2 or L3 the agent discovers the question is more load-bearing than earlier levels assessed, it can pause and propose level-up with the same approval gate.

### Paywalled sources and user assistance

During L3/L4, if a load-bearing claim sits behind a paywall the agent can't reach, the agent pauses and asks: *"A Gartner MQ on X would close this gap — do you have access to a PDF I can ingest?"* If yes, the user drops the PDF into `raw/market/<cluster>/` and the agent continues. If no, the agent logs the gap explicitly in the report ("Claim about X could not be independently verified — Gartner MQ would close this") and proceeds.

### Source archiving

Every citation fetched during a research run is archived into `raw/research-outputs/<research-id>/` as:
- a `.url` file (plain text containing the URL)
- an `.excerpt.md` file with the key passages extracted
- the date accessed in the filename

This protects against link rot and makes a finding auditable years later.

### Extensions and redos

**Extend** — `/research <id> extend` — resumes a completed research item and proposes the next level. The report page is updated in place (new level's findings append, supersessions marked where L3 overrides L2 claims). Queue item flips `completed-at-L2` → `in-progress-L3` → `completed-at-L3`. If substantial time has passed since the original run, the agent checks whether underlying sources have changed before extending — if yes, recommends redo instead.

**Redo** — `/research <id> redo [from-L<n>]` — creates a new run with the same question, fresh sources, linked via `supersedes:` field. Default starts at L1. Prior report keeps `status: superseded-by-<new-id>` — nothing deleted. Naming: `R-<NNN>-<slug>-redo-YYYY-MM-DD`.

**Suggested redo — the contradiction trigger.** During `/ingest`, when new raw content contains a claim that contradicts a finding in an existing research report, the agent:

1. Marks the contradiction on both sides — new evidence logs `[CONTRADICTS R-007]`; the research report gets a `⚠ contradicted by S-XXX on YYYY-MM-DD — redo recommended` banner
2. Appends a **suggested redo** to `research/queue.md` with original question unchanged + a new sub-question *"Does the contradiction from S-XXX hold up under fresh research?"* + a rationale (which claim, which new source, how load-bearing) + a priority suggestion (high if cited by a thesis/bet/pillar)
3. **Does not** auto-start the redo — waits for user approval

**Contradiction bar**: a new source contradicts only if it is of equal-or-higher credibility than the original and makes a claim that is either (a) numerically opposite, (b) factually contradictory (does X vs. doesn't), or (c) structurally incompatible. Updates in the same direction (newer figure, incremental change) are **refreshes** and update the wiki claim via supersession without triggering a redo.

**Staleness** — `/lint` flags research reports older than: 6 months for market figures · 12 months for competitor profiles · 24 months for deep theses. Stale reports are logged as **suggested refreshes** with rationale "time-based staleness" rather than contradiction.

### Report outputs

Regardless of level reached, every run produces:

- A **research report page** at `wiki/01_strategies/<slug>/findings/research/R-XXX-<slug>.md` (or `02_products/<slug>/` or `07_operations/research/cross-cutting/`). Updated in place as levels complete.
- Updates to affected **strategy / product / competitor / market / knowledge** pages, including supersessions where a finding overrides a prior claim.
- New `07_operations/sources/` entries — one per citation, with URL, date, source-type, source-credibility, summary, and the excerpt archived into `raw/research-outputs/`.
- The queue item: `status: completed-at-L<n>`, linked to the report.
- `06_knowledge/relationships.md` entries for any new typed relationships surfaced.

### Research proposals

When `/ingest` proposes a candidate research item but the topic is substantial enough to merit explicit scoping, the agent writes a **research proposal** into `workspace/research-proposals/<slug>.md` describing the question, sub-questions, why it matters, estimated levels needed, and dependencies. The user reviews, edits, and approves — then it moves to `research/queue.md`. Smaller candidates skip the proposal and land directly on the queue.

---

## Git integration

State is in git. There is no separate snapshot mechanism.

### What gets committed

- `wiki/` — all wiki content
- `raw/` — immutable source materials (including large PDFs by default; see below)
- `workspace/` — briefs, research proposals, image opportunities, generated images under a size threshold
- `CLAUDE.md`, `README.md`, `.gitignore`

### What does not

- `.env` files, credentials, anything matched by `.gitignore`
- Temporary files (`*.tmp`, `*.log`)

### Default policy

- **Commits are local.** Never pushed automatically, regardless of `auto-commit` mode. Pushing is always a manual user decision.
- **Raw PDFs are committed by default.** This preserves reproducibility; the whole point of the wiki is that findings are auditable against sources. Users on very-large-file engagements can switch to `.gitignore` raw PDFs via a `CLAUDE.md` flag and rely on the source pages in `07_operations/sources/` for audit trail.
- **`workspace/assets/images/` is committed** if images are under 2 MB each; larger images are `.gitignore`'d and regenerated on demand.

### Auto-commit modes

| Mode | Behaviour |
|------|-----------|
| `off` | Never auto-commits. User must run `/commit`. |
| `after-ingest` *(default)* | Commits once at the end of every `/ingest` run, after all clusters processed. |
| `after-research` | Commits at the end of every `/research` run and **once per level reached within a run** — each level transition is its own commit. |
| `after-every-command` | Commits after any command that changes files (`/ingest`, `/research`, `/lint`, `/query`, `/brief`, `/generate-image`). Verbose git log but maximally safe. |
| `daily` | First command of the day triggers a catch-up commit for everything changed since yesterday. |

The current mode lives in `CLAUDE.md` front-matter under `auto-commit:` and in `wiki/07_operations/shared/config.md`. It survives sessions.

### Commit message format

Every commit (auto or manual) uses the same structured format:

```
<type>: <one-line summary>

<grouped change list by wiki section>

Readiness: <per-scope %> | Sources: +<N> | Research: <queue: N / in-flight: N / completed: N>
Generated via /<command>
```

Where `<type>` is one of `bootstrap`, `ingest`, `research`, `lint`, `query`, `brief`, `manual`. Auto-commits never push.

### Brief pinning

When `/brief` compiles a deliverable, it includes the commit SHA it was generated from at the top of the output. A shared brief is always pinned to a reproducible repo state.

---

## Labels, status, and confidence

**Inline labels:**

- `[EVIDENCE]` — claim supported by an ingested non-prior source; always cite
- `[PRIOR: <brain-dump-slug>]` — claim sourced from a brain dump; informs theses but does not alone confirm
- `[ASSUMPTION]` — stated assumption not yet confirmed
- `[THESIS]` — named strategic claim; always cited
- `[OPEN QUESTION]` — unresolved question
- `[RISK]` — identified risk
- `[TO CONFIRM]` — placeholder to be validated
- `[CONTRADICTS R-XXX / S-YYY]` — new claim contradicts a prior research report or source
- `[SUPERSEDED]` — claim overridden by newer evidence; always note what replaced it and when

**Confidence:** `low` (one source, or priors-only, or inferred) · `medium` (2 sources, or 1 non-prior + priors) · `high` (3+ independent sources of equal-or-better credibility, or primary-source corroborated). `primary-interested`-only sourcing caps at `medium`.

**Page status:** `not-started` · `in-progress` · `complete` · `blocked` · `superseded-by-<id>`

**Checklist icons:** ⬜ missing · 🟡 partial · ✅ confirmed · ⛔ blocked · 🧊 deferred

**Visibility field** (required on all strategy, product, deliverable, narrative, and shared pages; used by `/brief`):

- `internal` — working documents: logs, checklists, queue, open questions
- `team` — shared within the product/strategy team, not leadership-facing
- `leadership-ready` — polished deliverables: strategy-on-a-page, moats, readiness, thought-leadership drafts
- `board-ready` — board-grade: signed off, evidence-confidence high, fully cited
- `confidential` — board-only or strictly-need-to-know material; excluded from `/brief external`

**Evidence-confidence field** (on deliverable and summary pages): set to the **lowest** confidence among the claims on the page. Update whenever claim confidence changes.

**Strategic-risk types** (used on every row of `findings/assumptions-and-risks.md`):

- `market` — is the market real, large enough, growing?
- `positioning` — is our read of the landscape and our place in it correct?
- `capability` — can we build/acquire the capabilities needed?
- `execution` — can we run this at the required speed, scale, quality?
- `viability` — economics, regulation, compliance, ethics, brand

Every assumption is classified by exactly one type. Coverage gaps across the five types are a leading indicator of downstream surprise and surface on the strategy's checklist.

**Source-credibility** (per source in `07_operations/sources/`):

- `primary-neutral` · `primary-interested` · `secondary-neutral` · `secondary-interested`

---

## `/bootstrap`

### Step 1 — Capture context

Ask for anything not already provided: organisation name, mission (one sentence), vision (2–3 sentences on the 3–5 year future), known strategies (slugs + 1-line theses), products managed (slugs + 1-line descriptions), primary competitors, target market segments, strategy framework preference (Rumelt / Playing to Win / Wardley — default Rumelt), analyst firms tracked, known ICPs, auto-commit mode preference (default `after-ingest`).

### Step 2 — Initialise git

If the directory is not a git repo, run `git init`. Write `.gitignore` with:

```
.DS_Store
*.log
*.tmp
.env
.env.*
workspace/assets/images/*.png.tmp
```

### Step 3 — Create folder structure

Create every folder and file per the Wiki layout. Mark optional folders (`moats.md`, `anti-strategy.md`, `04_narrative/thought-leadership/`, `05_go-to-market/analyst-relations.md`) with a `status: optional` frontmatter note.

For each **known strategy**, create all standard pages from templates: `overview.md`, `strategy-spine.md` (using the chosen framework), `pillars.md`, `anti-strategy.md`, `bets-and-initiatives.md`, `moats.md`, `findings/` (theses, assumptions-and-risks, evidence-log, decision-log, research/, deliverables/), `research/` (queue, active, open-questions, next-steps, checklist).

For each **known product**, create the standard product folder with `overview.md`, `capabilities.md`, `positioning.md`, `market-intelligence.md`, `competition.md`, `strategy-alignment.md`, `findings/`, `research/`.

For each **known competitor**, create `03_intelligence/competition/<slug>/` with `profile.md`, `strategy-read.md`, `capabilities.md`, `moves-log.md`, `evidence/`.

For each **known ICP**, seed a cluster page in `03_intelligence/audiences/`.

### Step 4 — Initialize the inbox

Create `raw/_inbox-index.md` as an empty index table. Create `raw/inbox/README.md` and a short README inside each of the `raw/` subtrees (`brain-dumps`, `strategy-docs`, `product-docs`, `market`, `competitive`, `news`, `research-outputs`) explaining cluster and manifest conventions.

### Step 5 — Initialize the knowledge layer

Create `wiki/06_knowledge/README.md`, `ontology.md`, and `relationships.md`. Seed the ontology with the strategy entity types and relationship types listed above. Create `README.md` files in all entity subfolders and in `concepts/`.

### Step 6 — Populate foundation

Fill `wiki/00_foundation/vision.md`, `mission.md`, `values-and-principles.md` from bootstrap input. Create `world-assumptions.md` with a short seeded list tailored to the domain (e.g. *"AI will commoditise X by 2027"*, *"EMEA compliance costs will triple"*, *"Category consolidation will accelerate"*). Ask the user to confirm or replace.

### Step 7 — Populate shared pages

Fill `wiki/07_operations/shared/project-context.md` and `stakeholders.md`. Seed `cross-strategy-watch-list.md` with 5–10 themes tailored to the domain (e.g. *"margin compression signals"*, *"platform-vs-product rhetoric"*, *"competitor hiring patterns"*, *"regulatory drift"*). Create `strategic-readiness.md` (row per strategy, counts at 0), `executive-summary.md` (shell), `top-strategic-questions.md` (empty), `master-assumptions-log.md`, `master-risks-log.md`, `master-decisions-log.md`, `config.md` (auto-commit mode, chosen framework, visibility conventions). Create `wiki/log.md` (first entry) and `wiki/index.md` (master navigation).

### Step 8 — Initialize narrative and GTM scaffolds

Create `04_narrative/core-narrative.md`, `positioning.md`, `messaging-pillars.md`, `category-definition.md`, `value-propositions.md` as empty templates. Create `thought-leadership/pipeline.md` with an empty kanban table and `suggested/`, `drafts/`, `published/` folders.

Create `05_go-to-market/gtm-motion.md`, `pricing-and-packaging.md`, `analyst-relations.md` as empty templates.

### Step 9 — Create workspace scaffolds

Create `workspace/image-opportunities.md` with append-only header, `workspace/research-proposals/`, `workspace/assets/images/`.

### Step 10 — Write `CLAUDE.md` at repo root

Create `CLAUDE.md` with frontmatter:

```yaml
---
framework: rumelt | playing-to-win | wardley
auto-commit: after-ingest
commit-footer: true
commit-push: false
visibility-levels: [internal, team, leadership-ready, board-ready, confidential]
raw-pdf-policy: commit | gitignore
---
```

Body: engagement summary, pointer to `wiki/index.md`, the operating rules the agent will follow (distilled from this file).

### Step 11 — Write `README.md` at repo root

Create a `README.md` summarising the engagement and pointing at `wiki/index.md`.

### Step 12 — Initial commit

Run `git add .` (respecting `.gitignore`) and create the initial commit: `bootstrap: initial wiki scaffold`. Append to `wiki/log.md`.

### Step 13 — Confirm

Report to the user: (a) the folder tree created with file counts per top-level section, (b) strategies/products/competitors scaffolded vs. left as placeholders, (c) bootstrap fields missing and needing follow-up, (d) the auto-commit mode set, (e) next recommended command (usually `/ingest`).

---

## `/ingest`

Phased. The agent never reads raw files until the user has confirmed which cluster to process.

### Phase 1 — Scan and present clusters

Read `raw/_inbox-index.md` (only file read in this phase). If missing or empty, scan for `_manifest.md` files across `raw/inbox/`, `raw/brain-dumps/`, `raw/strategy-docs/`, `raw/product-docs/`, `raw/market/`, `raw/competitive/`, `raw/news/`, `raw/research-outputs/`; build the index and write it. Filter to clusters with `status: ready` or `partial` and present a selection table (columns: #, Cluster, Scope, Type, Credibility, Size, Priority, Status, plus `⚠ depends on: <slug>` warnings).

Ask: *"Which clusters would you like to ingest now? Enter numbers, `all`, or `none`."*

### Phase 2 — Confirm and load

For each selected cluster: read its `_manifest.md`, report what will be ingested and which wiki pages will be created or updated. Warn on unmet dependencies. Proceed cluster by cluster, completing each fully before starting the next.

### Phase 3 — Process each cluster

For each cluster, run the steps below. Track which steps ran in the cluster's processing record (frontmatter `steps-completed` on the generated source page) — a missing step is a detectable gap that `/lint` flags.

**Step A — Read raw files.** Read every file listed in `_manifest.md`. Do not read files outside the cluster.

**Step B — Create source page.** Create `wiki/07_operations/sources/S-XXX-<slug>.md` (increment from the sources index). Every claim the agent will cite from this cluster is traced to this source page.

**Step C — Brain-dump handling.** If the cluster type is `brain-dump`, tag extracted claims as `[PRIOR: <cluster-slug>]` in all downstream pages. Priors may seed theses but never alone confirm a claim.

**Step D — Scope-expansion gate.** Scan the content for new strategies, products, competitors, or market segments not yet in the wiki. **Do not silently create new scope folders.** If a new scope is detected:

1. Create `wiki/07_operations/shared/CANDIDATE-<type>-<slug>.md` with the detected evidence, proposed structure, and confirmation questions.
2. Pause and tell the user: *"A potential new <type> '<Name>' was detected. Confirm to scaffold, or dismiss to ignore."*
3. Only scaffold after explicit confirmation. Delete the candidate file and log the scope creation.

**Step E — Knowledge extraction.** Extract entities, concepts, and typed relationships using `06_knowledge/ontology.md`; update `06_knowledge/` pages. Upgrade confidence as evidence accumulates. Add backlinks from each entity/concept page to the source; add forward links from affected strategy/product/competitor pages.

**Step F — Propagate to strategy pages.**

*Strategy root:* `overview.md` (refine thesis if evidence warrants); `strategy-spine.md` (update cited sections); `pillars.md` (update); `bets-and-initiatives.md` (kill criteria triggered? status change?); `moats.md` (new moat evidence?).

*Strategy findings:* `theses.md` (add or sharpen theses, cite new source); `assumptions-and-risks.md` (validated/invalidated; classify new by strategic-risk type); `evidence-log.md` (verbatim quotes as `[EVIDENCE]` — **written first**, anchor everything else); `decision-log.md` (decisions taken); `deliverables/` (update `[TO CONFIRM]` items closed, refresh `evidence-confidence`).

*Strategy research:* `open-questions.md` (close resolved; add new), `next-steps.md`, `checklist.md` (flip rows, recompute counts).

**Step G — Propagate to product pages.** For every product named in the cluster, update `02_products/<slug>/` accordingly — especially `capabilities.md`, `positioning.md`, `competition.md`, `strategy-alignment.md`.

**Step H — Propagate to intelligence pages.**

*Market:* update `segments.md`, `trends.md`, `figures.md`, `analyst-views.md`, `regulatory.md`, `scenarios.md` as the content dictates. Numeric claims must be cited; contradictions with existing figures trigger supersession.

*Competition:* update the relevant `<competitor-slug>/` pages; append to `moves-log.md` with date; refresh `comparison-matrix.md` if a capability changed; check `moves-playbook.md` for pre-thought responses.

*Customer voice:* append verbatim quotes to `verbatim-quotes.md`; update `review-extracts.md`, `survey-themes.md`, `win-loss-themes.md` as applicable.

*Audiences:* update `cluster-NN-<slug>.md` pages for any ICP or persona evidence in the cluster.

**Step I — Propagate to foundation.**

*World-assumptions:* if the cluster challenges a world-assumption, add a contested banner to the assumption page with the source, and (if the assumption is load-bearing) propose a `/research` candidate.

**Step J — Propagate to narrative.**

If the cluster contains customer-voice or competitive-positioning material, check `04_narrative/` for implications: does this validate a messaging pillar? contradict positioning? suggest a thought-leadership angle?

**Step K — Detect contradictions against existing research.** For every finding in the cluster, check against existing research reports (`findings/research/` and `07_operations/research/cross-cutting/`). If a contradiction is detected per the contradiction bar:

1. Add `[CONTRADICTS R-XXX]` to the new evidence
2. Banner the contradicted report with `⚠ contradicted by S-XXX on YYYY-MM-DD — redo recommended`
3. Append a **suggested redo** to the relevant `research/queue.md` with rationale and priority

**Step L — Propose candidate research.** Based on unresolved sub-questions, weakly-sourced claims, or contradictions surfaced during the cluster, append 1–N candidate research items to the relevant `research/queue.md` with a short rationale each. Items that merit explicit scoping go to `workspace/research-proposals/`.

**Step M — Propose thought-leadership angles.** If the cluster's syntheses crystallise into a narrative-worthy angle (grounded in at least one thesis + one customer-voice piece + one market/competitive piece), draft a short proposal in `04_narrative/thought-leadership/suggested/` — title, angle, target audience, supporting evidence. Wait for user approval before promoting to drafts.

**Step N — Evaluate image opportunities.** For every wiki page created or substantially updated, evaluate whether a generated image would meaningfully improve understanding (see Images & diagrams). Append strong opportunities to `workspace/image-opportunities.md`.

**Step O — Update shared registers.** Propagate cross-cutting decisions, risks, assumptions to `07_operations/shared/` master registers; update `cross-strategy-watch-list.md` with new patterns; refresh `strategic-readiness.md`; update `top-strategic-questions.md` if blockers changed.

**Step P — Anti-strategy prompt.** After the cluster is processed, for each strategy that has received ≥3 clusters and has an empty `anti-strategy.md`, prompt the user: *"This strategy has no explicit non-goals yet. Propose candidates based on what's been consistently excluded in the evidence?"*

**Step Q — Update indexes.** Add a row to `wiki/index.md`; mark the cluster `status: ingested` in its `_manifest.md`; update `raw/_inbox-index.md`. Update `07_operations/research/queue.md` (global roll-up) and `reports-index.md` if contradictions changed any report.

**Step R — Update steps-completed.** Record which letters ran in the source page frontmatter.

**Step S — Log.** Append to `wiki/log.md`: cluster name, files read, pages created/updated, entity/concept count, research candidates added, thought-leadership angles proposed, contradictions detected, anti-strategy prompts issued.

### Phase 4 — Summary and commit

After all selected clusters are processed, report: clusters ingested, new wiki pages, existing pages updated, new entities/concepts, research candidates added, thought-leadership angles proposed, contradictions detected, remaining clusters with priorities.

If `auto-commit: after-ingest` (default) or `after-every-command`, run the `/commit` flow with type `ingest` and a summary of what changed. Otherwise remind the user of uncommitted drift.

---

## `/research`

### Entry points

- `/research <id>` — run the queued research item with id `R-<NNN>`. Always starts at L1.
- `/research <id> extend` — escalate a completed research item to the next level.
- `/research <id> redo [from-L<n>]` — fresh run; prior report superseded. Default from L1.
- `/research "<free-form question>"` — create queue item and kick off L1 in one shot.

### L1 flow (always runs)

**Step 1 — Wiki-first.** Decompose the question into sub-questions. Read wiki and raw materials relevant to each sub-question. Record what is already held, page-by-page, with citations.

**Step 2 — Public-web sweep.** Run ~15–25 targeted searches across web, news, analyst summaries, primary-company materials, regulatory feeds, and definitional sources. For each result used, plan a `07_operations/sources/` entry.

**Step 3 — Triangulate.** For each sub-question, record what wiki says, what web says, where they agree, where they conflict. Tag each finding with a confidence and a source-credibility.

**Step 4 — Write the scoping memo.** File at `wiki/<scope>/findings/research/R-XXX-<slug>.md` (or `07_operations/research/cross-cutting/`). Sections:

- Question restated + sub-questions
- What wiki + raw already hold (cited page-by-page)
- What the L1 web sweep found (cited per sub-question)
- Synthesis so far (per sub-question)
- Gaps (unanswered sub-questions, weak claims, unresolved contradictions)
- Recommendation + rationale (one of: *L1 is enough* / *L2 recommended* / *L3 recommended* / *L4 recommended*)

**Step 5 — Archive sources.** Write every cited source to `07_operations/sources/S-XXX-<slug>.md` and archive excerpts to `raw/research-outputs/R-XXX/`.

**Step 6 — Ask for approval.** Present the memo, ask: *"Stop at L1 / proceed to L2 as proposed / narrow scope / skip ahead?"*

**Step 7 — Commit (if auto-commit applies).** Commit with type `research` and summary "L1 scoping memo for R-XXX".

### L2 / L3 / L4 flow

Proceed only after user approval. Each level continues from where the previous left off — work is additive.

**L2:** For every load-bearing claim from L1 that is single-sourced or contradicted, find independent corroboration (or mark "unresolvable at this depth"). Expand source diversity. Tag source-credibility on every new source. Append findings to the report; mark supersessions where L2 contradicts L1 findings. At end, ask to proceed to L3.

**L3:** Seek primary sources; read adversarial sources for competitive claims; weight synthesis by source-credibility; request paywalled PDFs from user where needed. Iterate until stop criteria met or loop cap (10 iterations) hit. If cap hit, file as partial with explicit gap list. Ask to proceed to L4.

**L4:** Requires **explicit extra confirmation** — agent names the specific load-bearing thesis that justifies L4 and the user confirms. Triangulate three ways; synthesise across disciplines (economic, technological, regulatory, sociological); actively hunt falsification. Terminates when agent cannot find a new angle to challenge the finding.

### Report updates at every level

Update in place:

- Append new findings under a `## L<n> additions` heading
- Mark supersessions where newer level contradicts earlier
- Update the **recommendation** block at the top to reflect current state
- Update `evidence-confidence:` and `status:` fields in frontmatter
- Update all affected strategy / product / intelligence / knowledge pages with new findings (with citations) and supersessions
- Update `research/queue.md` status (`in-progress-L<n>` → `completed-at-L<n>`)
- Update `07_operations/research/reports-index.md`

### Mid-run escalation and user pausing

If during L2 or L3 the agent discovers the question is more load-bearing than earlier levels assessed, it pauses and proposes level-up with the same approval gate: *"During L2, it became clear this claim underpins the AI-native strategy's core bet. Recommend escalating to L3."*

If the agent needs user-held material mid-run (paywalled PDF, internal document), it pauses and asks; if the user doesn't have it, the agent logs the gap and continues.

### Extend and redo flows

**Extend** (`/research <id> extend`): read the existing report. Check whether underlying sources have changed substantially since last run — if yes, recommend redo instead and stop. Otherwise propose the next level's plan, get approval, run that level, append to report in place.

**Redo** (`/research <id> redo [from-L<n>]`): create a new report at `R-<NNN>-<slug>-redo-YYYY-MM-DD.md` with `supersedes: R-<NNN>-<slug>`. Mark the old report `status: superseded-by-<new-id>`. Default start L1; override via `from-L<n>`. Proceeds through gated flow.

**Suggested redo** (agent-initiated during `/ingest`): appended to `research/queue.md` with rationale; waits for user approval like any other queue item.

---

## `/query`

If no question is provided, ask for one.

**Step 1 — Scope.** Route to the right queries folder: `01_strategies/<slug>/queries/`, `02_products/<slug>/queries/`, `03_intelligence/queries/`, `04_narrative/queries/`, `05_go-to-market/queries/`, `06_knowledge/queries/`, or `07_operations/queries/` (global). When in doubt, default to global. If the question genuinely touches 3+ scopes, prefer global.

**Step 2 — Check for overlap.** Scan the target queries folder for an existing query covering the same ground. If one exists and this refines it, set `supersedes:` in the new query's frontmatter. If essentially identical, update the existing query instead. Queries that are `status: superseded` or `promoted: true` stay indexed with a strikethrough.

**Step 3 — Research.** Read `wiki/index.md` first. Then read all plausibly relevant pages: for scoped areas, at minimum `overview.md`, `strategy-spine.md`, `pillars.md`, `findings/theses.md`, `findings/evidence-log.md`; relevant entity/concept pages from `06_knowledge/`; and `07_operations/sources/README.md`. For global queries also read `00_foundation/` and `07_operations/shared/executive-summary.md`. Cite every claim: `[Source: page-name.md]` or `[Source: S-XXX]`.

**Step 4 — Choose format.** Markdown page · comparison table · Mermaid diagram · Marp deck · matplotlib chart · PIL infographic · multi-part markdown.

**Step 5 — Write and file.** Frontmatter: `title`, `query`, `scope`, `scope-ref`, `format`, `date`, `status: draft`, `supersedes: ""`, `promoted: false`, `visibility: internal`. Body: Answer (with citations), Sources consulted, Limitations and caveats, Follow-on questions. File as `YYYY-MM-DD-<slug>.md`. Add to `wiki/index.md`. Append to `wiki/log.md`.

**Step 6 — Evaluate image opportunities.** Apply image-opportunity evaluation to the query page.

**Step 7 — Crystallize.** Ask: does this answer contain facts, relationships, or concepts worth promoting into `06_knowledge/`? If so, update relevant entity or concept pages, add the query as a source reference, and add entries to `relationships.md` for any new typed relationships. Also ask: does this query surface a worthwhile research candidate? If yes, append to the relevant `research/queue.md`.

---

## `/commit` and `/auto-commit`

### `/commit`

**Step 1 — Check repo state.** If not a git repo, tell user and stop.

**Step 2 — Summarise changes.** Read `git status` and `git diff --stat`. Group changed files by wiki section.

**Step 3 — Compose message.** Structured format:

```
<type>: <one-line summary>

<grouped change list by wiki section>

Readiness: <per-scope %> | Sources: +<N> | Research: queue: N / in-flight: N / completed: N
Generated via /commit
```

`<type>` inferred from the last command that changed files (`ingest` / `research` / `lint` / `query` / `brief` / `manual`). If the user passed `/commit "<message>"`, use their message as the one-line summary; the footer is still auto-appended.

**Step 4 — Stage and commit.** Stage only files under `wiki/`, `raw/`, `workspace/`, and root-level `CLAUDE.md`, `README.md`, `.gitignore`. Run `git commit`. Never push.

**Step 5 — Log.** Append to `wiki/log.md`: commit SHA (short), type, summary, files-changed count.

### `/auto-commit <mode>`

**No argument:** reports current mode read from `CLAUDE.md` frontmatter.

**With argument (`off` | `after-ingest` | `after-research` | `after-every-command` | `daily`):** updates `CLAUDE.md` frontmatter `auto-commit:` field and `wiki/07_operations/shared/config.md`. Confirms the new mode to the user. Appends to `wiki/log.md`.

Auto-commits follow the same structured message format as `/commit`. For `after-research`, each level transition within a run produces its own commit (so an L1→L2→L3 run is three commits). Auto-commits never push.

---

## `/lint`

Optional scoping: `/lint` (full), `/lint <strategy-slug>`, `/lint <product-slug>`, `/lint knowledge`, `/lint intelligence`, `/lint narrative`, `/lint gtm`, `/lint research`, `/lint git`.

### Checks

**Knowledge layer:**

- Entity page with no inbound links → `[ORPHAN]`; add backlinks
- Concept mentioned inline but no concept page → create it
- Relationship in `relationships.md` without source → `[UNSOURCED]`
- `confidence: low` attributes upgradable from wiki content → upgrade
- Chained `[SUPERSEDED]` with still-stale replacement → update chain
- Contradicting entity attributes with no supersession → flag
- Source notes with no entity/concept extractions → run extraction
- Duplicate concept pages → merge; redirect weaker
- Entity or relationship type used but not in `ontology.md` → add to ontology

**Strategy layer:**

- `overview.md` missing thesis, or `strategy-spine.md` missing a required section for the chosen framework → flag
- `pillars.md` has pillars with no bets → flag
- `bets-and-initiatives.md` has a bet without hypothesis or kill criteria → flag
- `theses.md` has a thesis with only 1 source (or priors-only) → flag; cannot promote above `confidence: medium`
- `assumptions-and-risks.md` row missing `risk-type` → flag; prompt to classify
- Strategic-risk coverage gap (e.g. no viability assumptions tracked) → flag on checklist
- `anti-strategy.md` empty after 3+ clusters → prompt
- `moats.md` with claims unmapped to 7 Powers → flag
- `high`-severity risk without mitigation → flag in master-risks-log
- Checklist % out of sync with evidence → recalculate

**Product layer:**

- Product without `strategy-alignment.md` entries → flag
- Product serving zero strategies → flag
- `capabilities.md` with capabilities not cited to evidence → flag

**Intelligence layer:**

- Competitor `moves-log.md` not updated in >90 days → flag stale
- `figures.md` numeric claim without source → flag
- `scenarios.md` scenario without leading indicators or strategic response → flag
- `customer-voice` evidence not tagged to an audience cluster → flag
- Audience cluster without JTBD → flag

**Narrative layer:**

- `messaging-pillars.md` pillar not laddered to a strategic pillar → flag
- `positioning.md` not updated after 3+ strategy-changing ingests → flag
- Thought-leadership suggestion in `suggested/` >30 days → prompt to drop or promote
- Thought-leadership draft with no cited thesis / customer-voice / market evidence → flag

**GTM layer:**

- `gtm-motion.md` without segment rationale → flag
- `pricing-and-packaging.md` tiers not linked to value propositions → flag
- `analyst-relations.md` without state-of-relationship updates in >90 days → flag

**Research layer:**

- Research report >6 months (market figures), >12 months (competitor profiles), or >24 months (deep theses) → **suggested refresh** with rationale
- Report hit loop cap but not marked partial → flag
- Contradicted report without a suggested redo on the queue → add it
- Queue item sitting >30 days without action → prompt to progress or drop
- Research run's `steps-completed` missing required steps → flag

**Git layer:**

- `.gitignore` missing or stripped → restore
- Uncommitted drift: >20 files changed since last commit AND last command >2 ago → suggest `/commit`
- `auto-commit: off` with no commits in >7 days despite activity → flag
- `raw-pdf-policy: gitignore` but PDFs are tracked in git (or vice versa) → flag

**Foundation layer:**

- World-assumption challenged by ≥2 sources with no research proposed → prompt
- World-assumption with confidence: high but no citation → flag

### Report and fix behaviour

Report per-section counts. List items requiring human review with file paths. Apply automatic fixes immediately; flag ambiguous items. Append to `wiki/log.md`. If `auto-commit: after-every-command`, commit with type `lint`.

---

## Reporting commands

### `/status`

Chat-only orientation (no files written). Reads `wiki/index.md`, `07_operations/shared/strategic-readiness.md`, `top-strategic-questions.md` (P0 rows), `wiki/log.md` (last 5 entries), `git log --oneline -10`, `git status --porcelain`. Responds with:

- Strategies: count, per-strategy readiness %
- Products: count
- Intelligence freshness: days since last competitor update, days since last market figure refresh
- Research: queue size, in-flight count, completed count, pending redos, stale reports
- Top P0 strategic questions
- Recent activity: last 10 commits
- Uncommitted drift: N files since last commit
- Pending workspace items: image opportunities, research proposals, candidate scopes

### `/brief [board|external]`

Compile `visibility` pages into a single shareable output. Default format markdown; pass `/brief marp` for slide deck.

**Default** — includes all `visibility: leadership-ready` pages + `visibility: board-ready` pages. Output: `workspace/brief-YYYY-MM-DD.md`.

**`/brief board`** — curated preset: strategy-on-a-page per strategy, moats, strategic-readiness, top-3 risks, bets-with-kill-criteria, key world-assumptions, latest intelligence summaries. Includes `board-ready` and `leadership-ready`; excludes `confidential` unless the operator explicitly confirms.

**`/brief external`** — shareable outside the org: narrative + positioning + thought-leadership published content + public-facing strategy-on-a-page with internals redacted. Excludes anything `confidential`, `internal`, or `team`. Requires explicit user confirmation before writing.

Every brief pins to git: the compiled output includes the commit SHA it was generated from at the top. If uncommitted changes exist, warn: *"4 uncommitted files — brief may not match committable state. Run /commit first?"*

Sections (default): cover + engagement summary, foundation (vision + mission + world-assumptions), strategy summaries, product summaries, intelligence highlights, narrative and positioning, GTM expression, research in-flight, readiness snapshot, risks and open questions, recommended next steps.

Marp rules: fenced slide separators, ≤3 bullets per slide, `<!-- fit -->` for large headings.

Append to `wiki/log.md`. If auto-commit applies, commit with type `brief`.

### `/generate-image <ID>`

Same pattern as discovery. Load entry from `workspace/image-opportunities.md`. Check API keys in order: `OPENAI_API_KEY` → `GEMINI_API_KEY`. Call the API with the entry's Prompt. Size: 1792×1024 for flowcharts/architectures; 1024×1024 for persona maps and matrices. Save to `workspace/assets/images/<ID>.png`. Embed with alt text after the named section heading in the target page. Update entry `Status: embedded`. Log.

---

## Images & diagrams

Generate a visual when it genuinely aids understanding more than text alone. Every image has alt-text and a text equivalent — a page must stand alone as text.

**Mermaid** — embed directly in wiki pages as fenced code blocks. Use `flowchart TD` for strategy spines, `graph LR` for entity relationship maps, `classDiagram` for ontology, `timeline` for roadmap horizons, `quadrantChart` for positioning grids and competitor landscapes.

**Matplotlib** — for charts driven by wiki data (readiness heatmaps, capability coverage, market-share breakdowns). Runnable Python in `tools/`; output to `workspace/assets/`.

**PIL/Pillow** — for layout-heavy composites (persona cards, strategy-on-a-page layouts, moat summaries).

**External image API** (`/generate-image`) — on-demand only, never auto during `/ingest` or `/research`.

### Image opportunity evaluation

After creating or substantially updating any wiki page, evaluate whether a generated image would meaningfully improve understanding. Flag when the page contains: strategy spine diagram · competitor positioning grid · capability map · scenario tree · narrative arc · pricing-tier comparison · GTM motion flow · persona card. Do **not** flag log/register tables, simple Q&A lists, or pages that already contain a Mermaid diagram covering the same content. Only append if it provides **strong** additional clarity — not decoration.

Append to `workspace/image-opportunities.md` as a `## IMG-NNN` block with fields: **ID**, **Status** (pending | generated | embedded), **Wiki page**, **Page section**, **Image type**, **Rationale**, **Prompt** (complete self-contained image-generation prompt including style, colour palette, labelling, domain specifics).

---

## Page templates

### `overview.md` (strategy)

```markdown
---
title: "<Strategy Name> — Overview"
scope: "strategy"
slug: "<strategy-slug>"
framework: rumelt | playing-to-win | wardley
status: not-started
confidence: low
visibility: internal
last-updated: YYYY-MM-DD
---

# <Strategy Name>

## Aspiration
<One paragraph: what winning looks like for this strategy. Tied to vision.>

## One-paragraph thesis
<The strategic claim in compressed form. Cited.>

## Scope boundary
<What is and is not in this strategy's remit. See also: anti-strategy.md>

## Primary products served
<Links to 02_products/<slug>/ pages. Mark primary vs secondary alignment.>

## Target segments
<Links to 03_intelligence/audiences/ cluster pages.>

## Horizon
<Now / Next / Later — when does this strategy need to deliver?>

## Key world-assumptions this relies on
<Links to 00_foundation/world-assumptions.md entries.>

## Claims to validate
- [TO CONFIRM] <claim>

---

## Navigation

**Structure:** [Strategy Spine](./strategy-spine.md) · [Pillars](./pillars.md) · [Anti-strategy](./anti-strategy.md) · [Bets](./bets-and-initiatives.md) · [Moats](./moats.md)

**Findings:** [Theses](./findings/theses.md) · [Assumptions & Risks](./findings/assumptions-and-risks.md) · [Evidence](./findings/evidence-log.md) · [Decisions](./findings/decision-log.md) · [Research](./findings/research/) · [Deliverables](./findings/deliverables/)

**Research:** [Queue](./research/queue.md) · [Active](./research/active.md) · [Open Questions](./research/open-questions.md) · [Checklist](./research/checklist.md)
```

### `strategy-spine.md` (Rumelt default)

```markdown
---
title: "<Strategy Name> — Strategy Spine (Rumelt)"
scope-ref: "<strategy-slug>"
framework: rumelt
status: in-progress
visibility: internal
evidence-confidence: low
last-updated: YYYY-MM-DD
---

# <Strategy Name> — Strategy Spine

## Diagnosis
<What is the actual challenge? What is going on in the environment? What makes winning hard? Cited.>

## Guiding policy
<The overall approach to addressing the diagnosis. Not specific actions — the approach. Cited to theses.>

## Coherent actions
<Mutually-reinforcing moves. Each links to a pillar and a bet. No contradictions. Sequenced.>

## What this rests on
<The theses and world-assumptions that must hold. Each cited.>

## What would break this
<The contradictions or facts that would invalidate this strategy. Explicit, not hidden.>
```

Playing-to-Win and Wardley variants swap the section headings to that framework's canonical shape; `strategy-spine.md` is rewritten deliberately if the framework changes at engagement level.

### `bets-and-initiatives.md`

```markdown
---
title: "<Strategy Name> — Bets and Initiatives"
scope-ref: "<strategy-slug>"
status: in-progress
visibility: internal
last-updated: YYYY-MM-DD
---

# <Strategy Name> — Bets and Initiatives

> Each bet has: hypothesis, owner, horizon, pre-committed kill criteria. Bets without kill criteria are flagged by /lint.

| ID | Under pillar | Bet | Hypothesis | Owner | Horizon | Risk type | Status | Kill criteria |
|----|-------------|-----|-----------|-------|--------|-----------|--------|---------------|
| BET-001 | P-01 | <"Invest in X capability"> | We believe doing Y will produce outcome Z for segment S | <name> | now / next / later | capability | active | We abandon if <specific evidence> by <date> |
```

### `moats.md` (optional)

```markdown
---
title: "<Strategy Name> — Moats"
scope-ref: "<strategy-slug>"
status: optional
visibility: leadership-ready
evidence-confidence: low
last-updated: YYYY-MM-DD
---

# <Strategy Name> — Moats

> Defensibility via Helmer's 7 Powers. Evidence-based, not aspirational. Each claim cited.

| Power | Present? | Evidence | Confidence | Notes |
|-------|---------|---------|-----------|-------|
| Scale economies | — | — | — | — |
| Network economies | — | — | — | — |
| Counter-positioning | — | — | — | — |
| Switching costs | — | — | — | — |
| Branding | — | — | — | — |
| Cornered resource | — | — | — | — |
| Process power | — | — | — | — |
```

### `anti-strategy.md` (optional, prompted after 3+ clusters)

```markdown
---
title: "<Strategy Name> — Anti-strategy"
scope-ref: "<strategy-slug>"
status: optional
visibility: team
last-updated: YYYY-MM-DD
---

# <Strategy Name> — What this strategy will NOT do

> Named non-goals, excluded segments, capabilities we won't build. Each with rationale.

## Segments we will not serve
| Segment | Why not | Decided |
|--------|---------|---------|

## Capabilities we will not build
| Capability | Why not | Decided |
|-----------|---------|---------|

## Competitive games we will not play
| Game | Why not | Decided |
|------|---------|---------|

## Channels we will not pursue
| Channel | Why not | Decided |
|---------|---------|---------|
```

### `theses.md`

```markdown
---
title: "<Strategy Name> — Theses"
scope-ref: "<strategy-slug>"
status: in-progress
visibility: internal
last-updated: YYYY-MM-DD
---

# <Strategy Name> — Theses

> Named strategic claims. Each ≥2 cited sources before promoting above `confidence: medium`.
> Brain-dump-only theses stay `confidence: low` until corroborated.

| ID | Thesis | Confidence | Sources | Risk type | Tested-by | Status |
|----|--------|-----------|---------|-----------|-----------|--------|
| T-001 | <"Data gravity dominates EMEA vendor selection by 2027"> | medium | S-007, S-012 | market | R-003 | active |
```

### Research report template

```markdown
---
title: "R-XXX — <Question>"
research-id: R-XXX
scope: "<strategy-slug | product-slug | cross-cutting>"
question: "<one-line>"
status: in-progress | completed-at-L1 | completed-at-L2 | completed-at-L3 | completed-at-L4 | partial | superseded-by-<id>
supersedes: ""
level-reached: L1
evidence-confidence: low
visibility: internal
last-updated: YYYY-MM-DD
steps-completed: []
---

# R-XXX — <Question>

> **Contradicted?** — if banner: `⚠ contradicted by S-XXX on YYYY-MM-DD — redo recommended`

## Question and sub-questions
- Main: <...>
- Sub 1: <...>
- Sub 2: <...>

## Recommendation (updated at every level)
<Current recommendation: stop / proceed to L<n+1> / partial.>

---

## L1 findings — Scoping memo

### What wiki + raw already hold
<Page-by-page, cited.>

### What the L1 web sweep found
<Per sub-question, cited, confidence-tagged.>

### Synthesis so far
<Per sub-question.>

### Gaps
<Unanswered, weak, contradicted.>

### Depth recommendation and rationale
<L1 enough / L2 / L3 / L4 — with specific named claims.>

---

## L2 additions
<Appears after L2 runs. Supersessions noted.>

## L3 additions
<Appears after L3 runs.>

## L4 additions
<Appears after L4 runs.>

---

## Sources
<Full list of S-XXX entries cited in this report.>

## Limitations and caveats

## Follow-on questions
```

### Research queue row

```markdown
---
queue-id: RQ-XXX
proposed-by: agent | user
proposed-on: YYYY-MM-DD
proposed-from: "<ingest cluster slug or free-form>"
status: proposed | approved | in-progress-L<n> | completed-at-L<n> | dropped | suggested-redo
priority: p0 | p1 | p2
scope: "<strategy-slug | product-slug | cross-cutting>"
linked-report: ""
---

Question: <one line>
Sub-questions (agent draft): <list>
Rationale: <why this is worth researching — load-bearing for what?>
Redo-trigger (if suggested-redo): <contradicting source S-XXX; which claim>
```

### `positioning.md`

```markdown
---
title: "Positioning Statement"
status: in-progress
visibility: leadership-ready
last-updated: YYYY-MM-DD
---

# Positioning Statement

> Dunford template: for [segment] who [context], our product is a [category] that [key benefit] unlike [alternative] which [weakness].

## Current positioning
**For** <segment>  
**who** <context/situation>,  
**<Product>** is a **<category>**  
**that** <key benefit>,  
**unlike** <alternative>  
**which** <weakness>.

## Evidence base
| Element | Cited from |
|---------|-----------|
| Segment | <source / audience cluster> |
| Context | <...> |
| Category | <category-definition.md> |
| Benefit | <customer-voice / thesis> |
| Alternative | <competitor profile> |
| Weakness | <competitor comparison> |

## Alternatives considered and rejected
| Alt positioning | Why rejected |
|----------------|--------------|
```

### `messaging-pillars.md`

```markdown
---
title: "Messaging Pillars"
status: in-progress
visibility: leadership-ready
last-updated: YYYY-MM-DD
---

# Messaging Pillars

> Each pillar ladders to exactly one strategic pillar. /lint flags orphans.

| ID | Pillar (message) | LaddersTo (strategic pillar) | Proof points | Target audience | Where it appears |
|----|-----------------|------------------------------|-------------|----------------|------------------|
| MP-001 | <"X is the new Y"> | [P-02](../01_strategies/.../pillars.md#p-02) | [thesis T-003](...), [voc V-011](...), [market figure](...) | Economic buyer | Website hero, sales deck |
```

### `world-assumptions.md`

```markdown
---
title: "World Assumptions"
status: in-progress
visibility: internal
last-updated: YYYY-MM-DD
---

# World Assumptions

> Macro priors underpinning the strategy. Each cited, confidence-tagged, challenged when evidence arrives.

| ID | Assumption | Confidence | Sources | Contested? | Last-reviewed |
|----|-----------|-----------|---------|-----------|--------------|
| WA-001 | <"AI will commoditise X by 2027"> | medium | S-005, S-018 | — | YYYY-MM-DD |
| WA-002 | <"EMEA compliance costs will triple by 2028"> | low | priors-only | — | YYYY-MM-DD |

## Contested log

| ID | Contested-on | By source | Nature of challenge | Action |
|----|-------------|----------|--------------------|-------|
```

### Competitor profile (`<competitor-slug>/profile.md`)

```markdown
---
title: "<Competitor Name>"
competitor-slug: <slug>
confidence: low
last-updated: YYYY-MM-DD
last-moves-review: YYYY-MM-DD
---

# <Competitor Name>

## Snapshot
- Founded: <year>
- HQ: <place>
- Funding / ownership: <...>
- Employees: <range>
- Primary segment: <...>
- Primary category: <...>

## What they do
<One paragraph, cited.>

## Our read of their strategy
<Link to strategy-read.md>

## Capabilities we track them on
<Link to capabilities.md>

## Moves log
<Link to moves-log.md — last date>

## Evidence
<Folder — quotes, cited figures>

## Threat level to our strategies
| Strategy | Threat | Rationale |
|---------|-------|-----------|
```

### Audience cluster (`03_intelligence/audiences/cluster-NN-<slug>.md`)

```markdown
---
title: "Cluster N — <Label>: <Full Name>"
audience-cluster: "<slug>"
type: icp | buyer-persona | user-persona | buying-committee
confidence: low
serves-strategies: []
last-updated: YYYY-MM-DD
visibility: internal
---

# Cluster N — "<Label>": <Full Name>

## Jobs-to-be-done
- **Primary job:** When <situation>, I want to <motivation>, so I can <expected outcome>.

## Who they are
<Paragraph.>

## Firmographics / demographics
| Dimension | Profile |
|-----------|---------|

## Buying behaviour
- Triggers: <what starts a purchase consideration>
- Evaluation criteria: <what they judge on>
- Typical buying committee: <who else is involved>
- Objections: <common pushback>

## Pains and frustrations
- <what goes wrong today>

## What they need from solutions
- <concrete promises>

## Where this cluster appears
| Page | Role / context |
|------|---------------|

## Evidence trail
| Evidence | Source |
|----------|--------|
```

### Cluster manifest (`_manifest.md`)

```markdown
---
cluster: "<cluster-slug>"
display-name: "<human-readable name>"
scope: "<strategy-slug | product-slug | cross-cutting | unknown>"
type: brain-dump | strategy-doc | product-doc | analyst-report | white-paper | market-figures | news-pack | competitor-material | research-output | mixed | document-pack
credibility: primary-neutral | primary-interested | secondary-neutral | secondary-interested
size: small | medium | large
priority: p0 | p1 | p2 | p3
status: ready | partial | pending-files | ingested
added: YYYY-MM-DD
ingested: ""
depends-on: []
---

# Cluster: <display-name>

## Files
| File | Description | Format | Size estimate |
|------|-------------|--------|--------------|

## Expected wiki impact
- Creates: <new pages>
- Updates: <existing pages>
- Knowledge extraction: <rough entity/concept count>
- Research candidates likely: <rough number>

## Notes
<Optional context for the operator.>
```

### Source page (`07_operations/sources/S-XXX-<slug>.md`)

```markdown
---
source-id: S-XXX
title: "<source title>"
type: brain-dump | strategy-doc | product-doc | analyst-report | white-paper | market-figures | news | competitor-material | research-citation
credibility: primary-neutral | primary-interested | secondary-neutral | secondary-interested
url: ""
accessed: YYYY-MM-DD
publication-date: ""
cluster: <cluster-slug>
status: complete
visibility: internal
steps-completed: []
---

# S-XXX — <title>

## Summary
<One paragraph.>

## Key claims extracted
- <claim> [confidence: <level>]

## Key figures
| Figure | Value | Context |
|--------|-------|---------|

## Key quotes
- "<verbatim>" — p. <N>

## Pages updated from this source
| Wiki page | Nature of update |
|-----------|-----------------|

## Archive
<Link to raw/ folder holding the original.>
```

### Thought-leadership suggestion template

```markdown
---
title: "<Proposed TL title>"
status: suggested
proposed-on: YYYY-MM-DD
proposed-from: "<ingest cluster or synthesis context>"
target-audience: <ICP / buyer persona>
laddersTo-strategy: <strategy-slug>
supporting-evidence:
  thesis: <T-XXX>
  customer-voice: <V-XXX>
  market-or-competitive: <S-XXX or entity-ref>
visibility: internal
---

# <Proposed TL title>

## Angle
<The core claim, 2–3 sentences.>

## Why now
<Timing rationale — why is this the moment for this piece?>

## Supporting evidence
- Thesis: <...>
- Customer voice: <...>
- Market / competitive: <...>

## Call to action
<What the reader should do / think / share.>

## Suggested distribution
<LinkedIn / blog / conference / analyst briefing / internal>

## Pre-commit check (for /lint)
- [ ] Grounded in at least one thesis
- [ ] Grounded in at least one customer-voice piece
- [ ] Grounded in at least one market or competitive piece
- [ ] Laddered to a strategic pillar
```

---

## General rules

1. **Cite everything.** Every claim in a query answer, strategy page, thesis, or entity page references its source.
2. **Never invent facts.** Unsupported claims carry `[ASSUMPTION]`, `[TO CONFIRM]`, or `[PRIOR]`.
3. **Brain dumps are priors, not evidence.** Priors can seed theses; they cannot alone confirm claims. A thesis grounded only in priors stays `confidence: low`.
4. **Supersede, don't overwrite.** Preserve old values with `[SUPERSEDED YYYY-MM-DD by S-XXX: <replacement>]` for audit.
5. **`raw/` is immutable.** Files under `raw/` are written once and never modified. Derived content goes in `wiki/` or `workspace/`.
6. **A page must stand alone as text.** Visualisations enhance; they never replace.
7. **Always read `wiki/index.md` first** before any operation.
8. **`/ingest` never reads raw files until the user has confirmed the cluster.** The selection step reads manifests only.
9. **Scope expansion always pauses for user confirmation.** Never silently scaffold new strategy, product, or competitor folders — always use the CANDIDATE-file pattern.
10. **Every assumption carries a strategic-risk type.** `market` · `positioning` · `capability` · `execution` · `viability`. Unclassified assumptions are not actionable.
11. **Every bet carries kill criteria.** Bets without pre-committed kill criteria are flagged by `/lint` and blocked from `visibility: leadership-ready`.
12. **Every messaging pillar ladders to a strategic pillar.** Orphan messaging is flagged.
13. **Every thought-leadership article is grounded.** Must cite ≥1 thesis + ≥1 customer-voice + ≥1 market/competitive source before promoting from `suggested/` to `drafts/`.
14. **Research is gated.** L1 always runs. L2/L3/L4 require explicit user approval at each transition. L4 requires additional confirmation.
15. **Wiki-first at every research level.** Always check wiki + raw before fetching from the web.
16. **Source-credibility is tagged, always.** Claims sourced only from `interested` parties cap at `confidence: medium` without independent corroboration.
17. **Auto-commits never push.** Pushing is a manual user decision; `/commit` is local-only by default.
18. **Contradictions trigger suggested redos, not auto-redos.** Agent banners the contradicted report and appends to the queue; user decides.
19. **World-assumptions are watched.** When an ingest challenges one, flag on the assumption page; if load-bearing, recommend research.
20. **Anti-strategy gets prompted.** After 3+ clusters on a strategy with no non-goals, the agent prompts the user rather than leaving trade-offs hidden.
21. **Framework is chosen once.** Changing strategy framework mid-engagement is expensive — do it deliberately and rewrite all `strategy-spine.md` pages.
