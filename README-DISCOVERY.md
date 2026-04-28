# Agent Product Discovery

A bootstrap kit for turning any Claude Code session into a **persistent, compounding knowledge base** for product discovery, consultancy engagements, technical assessments, and multi-stakeholder research work.

Three variants — pick one and drop it into an empty project folder to scaffold a structured discovery wiki, then feed it raw material (session notes, transcripts, documents) to compile into accumulating knowledge.

| File | Size | Stance | When to use |
|------|------|--------|-------------|
| [`AGENT-PRODUCT-DISCOVERY.md`](./AGENT-PRODUCT-DISCOVERY.md) | ~63k chars | **Prescriptive** | Full opinionated version: complete templates, inline examples, failure-mode guidance, detailed per-page structure. Use when you want maximum out-of-the-box scaffolding and cross-engagement consistency. |
| [`AGENT-PRODUCT-DISCOVERY-LITE.md`](./AGENT-PRODUCT-DISCOVERY-LITE.md) | <20k chars | **Lean** | Compact starting point. All commands, layout, and core behaviours preserved; engagement-specific detail trimmed. Use when you want a clean base to layer your own bias on top of — domain conventions, persona shape, watch-list themes, risk frameworks. |
| [`AGENT-PRODUCT-DISCOVERY-GIST.md`](./AGENT-PRODUCT-DISCOVERY-GIST.md) | 1,980 words | **Principles-only** | Philosophical version. Explains the *why* and the invariants (compiled artefact, two layers, problem-first, cite everything, clusters, promotion through tiers, scope as change-control) and lets the agent derive the *how*. Use with a capable agent when you want the structure to mould itself to the engagement. |

For a broader view — including how Discovery compares to the Strategy pattern — see the [main README](./README.md).

---

## Why this exists

Most discovery work loses information. Notes sit in scattered docs, insights get re-discovered session after session, decisions drift from the evidence that supported them, and "what do we actually know?" becomes an unanswerable question by week three.

This agent pattern solves that by treating the wiki as a **compiled artifact**, not a retrieval index:

- Evidence is captured verbatim and cited.
- Patterns across evidence are promoted into named insights.
- Named entities, systems, and concepts accumulate into a reusable domain map.
- Contradictions are flagged and superseded rather than overwritten.
- Every claim carries a confidence level and a source.

The result is a wiki that **gets smarter with every session** and can be read by someone joining the engagement cold.

---

## What you get

When you bootstrap a new project, you get a scaffold organised into three complementary layers:

| Layer | Purpose | Lives in |
|-------|---------|----------|
| **Discovery tracking** | What we're finding: use cases, sessions, decisions, risks, readiness checklists | `wiki/01_use-cases/`, `wiki/02_core-topics/`, `wiki/03_shared/` |
| **Domain knowledge** | How the domain works: entities, concepts, typed relationships, ontology | `wiki/06_knowledge/` |
| **Raw capture** | Immutable source material and session notes | `raw/` |

Plus a `workspace/` for generated images, compiled briefs, and snapshots.

---

## Quick start

1. Create an empty folder for your engagement.
2. Copy **one** of the three bootstrap files into it — Full, Lite, or Gist.
3. Open the folder in Claude Code.
4. Run `/bootstrap`.

Claude will ask for:
- Project / engagement name
- Client or org name
- Domain (one sentence)
- Known use cases and core topics
- Known session dates (if any)

Then it will scaffold a wiki structure, seed the knowledge ontology, create templates, and write a project-specific `CLAUDE.md` as the ongoing operating config.

**After bootstrap, the bootstrap file has done its job.** The engagement is now driven by `CLAUDE.md` and the wiki itself. You can delete the bootstrap file, archive it, or leave it as a reference.

### Choosing Full, Lite, or Gist

The three variants are the same pattern at three levels of prescriptiveness. Pick the one that matches how much room you want to give the agent.

- **Full** (`AGENT-PRODUCT-DISCOVERY.md`) — inline page templates (YAML frontmatter + section bodies), worked examples, explicit failure-mode table, long general-rules block. Best when you want the agent to produce richly-shaped pages from day one without extra prompting, and when you care about cross-engagement consistency (same page names, same frontmatter fields, same lint rules every time).
- **Lite** (`AGENT-PRODUCT-DISCOVERY-LITE.md`) — every command, the wiki layout, the problem-space framing, the cluster / ingest / lint / query / brief / snapshot behaviour, plus a compact table-shape summary per page type — but with prose and verbose template bodies trimmed. Best when you want a clean base to extend with your own conventions (domain-specific watch-list themes, a different risk framework, extra deliverable pages, a persona template tuned to your research style). Includes an "Extending this Lite file" section listing the common customisation points.
- **Gist** (`AGENT-PRODUCT-DISCOVERY-GIST.md`) — principles and invariants only, no folder tree, no templates, no command enumeration. Best when you trust the agent to derive a sensible concrete structure from the *why*, and when you want the wiki to mould to the specifics of the engagement rather than the other way around.

### Why Gist exists, and why it might be the better choice

The Full version encodes many small decisions — exact folder numbering (`01_use-cases/`, `03_shared/`), exact filenames (`opportunity-tree.md`, `evidence-log.md`), specific frontmatter fields, a precise lint check list. Those decisions were right for a particular run of engagements, but some of them are arbitrary: an equally good wiki could have a different folder scheme, different file names, or a different lint pass and still satisfy every invariant that actually matters (evidence is cited, claims carry confidence, contradictions are superseded, problems come before solutions, scope expansion is gated by a human).

A prescriptive file asks the agent to *execute* a pre-baked design. A principles-only file asks the agent to *design from the principles*. As agents get more capable, the second mode often produces a better-fitting wiki than the first, because:

- It can shape the structure to the actual engagement (a legal-ops discovery doesn't need the same deliverable pages as a platform-architecture assessment).
- It won't contort itself to fit a template that doesn't match what the source material wants to become.
- It has fewer surface-level rules to carry in context, so it can spend its attention on the real work: extracting, synthesising, challenging claims.
- The pattern is also more likely to improve over time — each run is an opportunity for the agent to re-derive a better shape, rather than reproducing last run's shape by rote.

Prescriptive versions are still the right call when you are coordinating multiple engagements that must look alike, when a less-capable agent needs more guardrails, or when regulatory / audit requirements pin the exact shape of deliverables. Outside those cases, Gist is often enough — and sometimes better.

All three variants share the same DNA and produce compatible output: problem-first framing, cited evidence, consolidation tiers, cluster-based ingestion, a knowledge layer alongside the discovery layer. The difference is how much of the *shape* is decided in advance vs. derived in context.

---

## Core concepts

### Problem-first framing

Use cases and core topics are **problem spaces** — areas where the team is trying to understand a problem deeply enough to choose what to build. Solutions are candidates under investigation, not starting assumptions.

The flow per scope:

```
Problem + Target outcome
  → Opportunities (unmet user needs)
  → Solutions (candidate bets)
  → Experiments (tests of the riskiest assumption)
  → Evidence → Insights → Validated/invalidated assumptions
  → Decisions → Deliverables
```

Every assumption and every experiment is classified by one of four **product-risk types** (Marty Cagan / SVPG):

- **Value** — will users choose this over alternatives?
- **Usability** — can they figure out how to use it?
- **Feasibility** — can we build it with what we have?
- **Viability** — does it work for the business (legal, regulatory, ethical)?

Coverage gaps across the four types are a leading indicator of downstream surprise.

### Clusters and the inbox

Raw material arrives through an **inbox** organised into **clusters** — bounded sets of files that belong together and are processed in one `/ingest` operation.

Cluster types: `session-notes`, `transcript`, `document-pack`, `data-export`, `mixed`, `background`.

Each cluster has a `_manifest.md` that describes its contents, scope, priority, and dependencies. The agent reads manifests to build a menu; it never opens raw files until you've confirmed which cluster to process. This keeps the context manageable no matter how much material is staged.

### Consolidation tiers

Knowledge is promoted through increasingly stable tiers:

| Tier | Location | Lifecycle |
|------|----------|-----------|
| Raw | `raw/` | Immutable, locked after capture |
| Episodic | `04_sources/`, session pages | Permanent reference once written |
| Semantic | `06_knowledge/entities/`, `06_knowledge/concepts/` | Updated as evidence accumulates |
| Procedural | `06_knowledge/ontology.md`, `03_shared/` | Slowest to change, highest confidence |

A fact seen once stays episodic. A fact confirmed across 3+ independent sources gets promoted to a semantic entity or concept page with `confidence: high`.

### Evidence → Insights → Knowledge

- **Evidence** — verbatim quotes and source-cited observations in `findings/evidence-log.md`.
- **Insights** — named patterns synthesised from 2+ evidence rows (`findings/insights.md`).
- **Knowledge** — high-confidence insights that crystallise into reusable domain concepts (`06_knowledge/concepts/`).

Each tier cites the one below it. Nothing is invented; contradictions are made explicit with `[SUPERSEDED YYYY-MM-DD by S-XXX]` markers.

### Visibility and confidence

Every outcome, persona, and shared page carries:

- **Visibility**: `internal` / `team` / `client-ready` — used by `/brief` to compile shareable outputs.
- **Evidence confidence**: `low` / `medium` / `high` — the lowest confidence across claims on the page.

This lets you generate a client-ready deliverable from the wiki at any point without hand-curating what's safe to share.

---

## Command reference

Run these inside Claude Code once the wiki is bootstrapped.

| Command | When to use |
|---------|-------------|
| `/bootstrap` | Once, at the start of a new engagement. Scaffolds the wiki. |
| `/ingest` | Whenever you have new material. Shows available clusters, lets you pick what to process. |
| `/query <question>` | Ask anything about the engagement, domain, or findings. Produces a filed answer page. |
| `/lint` | Health-check: orphan pages, contradictions, stale claims, missing extractions. Scope with `/lint uc-01` or `/lint knowledge`. |
| `/status` | Chat-only orientation: readiness, top blockers, recent activity. |
| `/snapshot` | Capture a point-in-time state record. |
| `/brief` | Compile all `client-ready` pages into a shareable markdown (or `/brief marp` for a slide deck). |
| `/generate-image <ID>` | Render an image opportunity using OpenAI or Gemini APIs. |

---

## A typical workflow

**Day 0 — setup**

```
/bootstrap
```

Answer the prompts. The agent scaffolds everything and reports what was created vs left as placeholders.

**Day 1 — first interview**

Run the session. Capture notes in `raw/sessions/<session-slug>/` using the session-notes template. Fill in `_manifest.md`.

```
/ingest
```

Pick your cluster. The agent reads your notes, creates the source entry, extracts entities and concepts, updates the discovery summary, flips checklist items, promotes recurring evidence into insights, and refreshes the readiness roll-up.

**Day 3 — someone asks a question**

```
/query How does the current approval workflow actually work, and where does it break down?
```

The agent reads the relevant scope pages, cites every claim, writes a filed answer under `wiki/<scope>/queries/`, and asks whether any of it should be promoted into the knowledge layer.

**Day 7 — periodic health check**

```
/lint
```

Auto-fixes what it can (unlinked entities, stale indexes, missing frontmatter). Flags items that need human review.

**Day 14 — mid-engagement checkpoint**

```
/snapshot
/brief
```

Capture the current state for your records. Compile everything marked `client-ready` into a single shareable markdown for the next stakeholder review.

---

## What "good" looks like

A well-run wiki accumulates these properties over the course of an engagement:

- **Every claim is cited.** No free-floating assertions.
- **Assumptions are classified.** No uncategorised `[ASSUMPTION]` rows.
- **Opportunities have solutions. Solutions have experiments.** No dead branches in the opportunity tree.
- **Evidence feeds insights feed concepts.** Nothing orphaned at any tier.
- **Contradictions are flagged and superseded.** Old values preserved for audit.
- **`discovery-readiness.md` matches reality.** Checklist % stays in sync with evidence.

`/lint` checks all of these automatically and reports gaps.

---

> Note: the exact folder/file names below are what Full and Lite scaffold. Gist lets the agent pick — expect the same conceptual layers (raw capture, discovery tracking, domain knowledge, workspace) but possibly different names.

## File layout after bootstrap

```
<engagement-root>/
├── CLAUDE.md                      # ongoing operating config (created by /bootstrap)
├── README.md                      # engagement summary (created by /bootstrap)
├── AGENT-PRODUCT-DISCOVERY*.md    # the bootstrap file you chose (removable post-bootstrap)
│
├── wiki/
│   ├── index.md                   # master navigation — always read first
│   ├── log.md                     # append-only operations log
│   ├── 01_use-cases/              # one folder per use case
│   ├── 02_core-topics/            # cross-cutting topics
│   ├── 03_shared/                 # executive summary, readiness, registers, snapshots
│   ├── 04_sources/                # sequential source log (S-001, S-002, ...)
│   ├── 05_queries/                # global queries
│   ├── 06_knowledge/              # ontology, entities, concepts, relationships
│   └── 07_personas/               # persona clusters
│
├── raw/
│   ├── _inbox-index.md            # auto-maintained cluster index
│   ├── inbox/<cluster>/           # drop zone for document packs, exports, mixed material
│   ├── sessions/<session>/        # live session captures
│   ├── background/<cluster>/      # prior-context materials
│   └── assets/                    # photos, handouts, exports
│
└── workspace/
    ├── image-opportunities.md     # registry of image generation opportunities
    ├── assets/images/             # generated images
    └── brief-YYYY-MM-DD.md        # compiled client-ready briefs
```

---

## Prior art

The structure draws from established product-discovery practice — no single framework is required reading, but contributors familiar with the literature will recognise the shape.

- **Opportunity-solution tree** — Teresa Torres, *Continuous Discovery Habits*
- **Four product-risk types** — Marty Cagan / SVPG, *Inspired*
- **Problem statement + HMW** — Design Thinking (IDEO / Stanford d.school)
- **Jobs-to-be-done** — Christensen / Klement
- **Evidence → Insight synthesis** — classic UX research practice
