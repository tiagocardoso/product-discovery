# Agent Product Discovery

## What this is

This file turns any Claude Code session into a **persistent, compounding knowledge base** for complex, multi-stakeholder engagements — consultancy sprints, product discovery workshops, technical assessments, or any initiative requiring structured knowledge capture across multiple sessions, topics, and participants.

It has two complementary purposes that run in parallel:

1. **Discovery tracking** — use cases, sessions, decisions, risks, readiness checklists. The structured record of what you are finding and what you still need to confirm.
2. **Domain knowledge** — entities, concepts, ontology, typed relationships. A reusable map of how the domain works that anyone can read to understand the subject matter, independent of the discovery process.

**Problem-first framing.** Use cases and core topics are **problem spaces** the team is exploring — not pre-decided solutions. Each scope's job is to understand a problem deeply enough to choose what to build. Every scope carries a measurable target outcome, an opportunity-solution tree, assumptions classified by product risk (value, usability, feasibility, viability), and experiments that test the riskiest assumptions. Solutions only emerge once the problem space is understood.

The wiki is a **compiled artifact**, not a retrieval index. When you add a new source, the agent reads it, integrates it into the existing wiki, updates entity pages, strengthens or challenges existing claims, and promotes knowledge up through consolidation tiers. Knowledge accumulates. Contradictions are flagged. Syntheses persist.

**To use:** drop this file into an empty folder, open it in Claude Code, and run `/bootstrap`.

**Lifecycle:** this file is a bootstrap-only tool. Once `/bootstrap` has run, `CLAUDE.md` is the operating config for the engagement. Improvements to the pattern should be made here and then reflected in active `CLAUDE.md` files — not the other way around. `CLAUDE.md` may override or extend any behaviour defined here for engagement-specific needs.

**Section map:** Commands · Common failure modes · Wiki layout · Problem-space framing · Inbox and cluster system · Knowledge layer · Labels, status, confidence · `/bootstrap` · `/ingest` · `/query` · `/lint` · Reporting commands · Images & diagrams · Page templates · General rules

---

## Commands

| Command | When to use |
|---------|------------|
| `/bootstrap` | Once, at the start of a new engagement. Scaffolds the entire wiki. |
| `/ingest` | Whenever you have new material to process. Shows available clusters and lets you choose what to ingest now vs later. |
| `/query <question>` | Ask anything about the engagement, domain, or findings. Produces a filed answer page. |
| `/lint` | Periodically, to health-check the wiki — find orphans, contradictions, stale claims, missing extractions. `/lint <scope>` to narrow (e.g. `/lint uc-01`, `/lint knowledge`). |
| `/status` | Quick chat-only orientation: readiness numbers, top blockers, last 5 log entries. |
| `/snapshot` | Capture a point-in-time state record in `wiki/03_shared/snapshots/`. |
| `/brief` | Compile all `visibility: client-ready` pages into a shareable markdown (default) or Marp deck (`/brief marp`). |
| `/generate-image <ID>` | Generate the image for an opportunity in `workspace/image-opportunities.md` and embed it in the target wiki page. Pass no ID to batch-select from pending entries. |

---

## Common failure modes

Quick decision reference for ambiguous situations that come up mid-operation:

| Symptom | Wrong response | Correct response |
|---------|----------------|-----------------|
| Cluster `_manifest.md` missing or malformed | Skip or refuse to ingest | Read what's parseable, flag the gaps, offer to create/fix; ask the user to confirm |
| Query covers the same ground as an existing query | Create a new parallel file | Set `supersedes:` on the new one; mark the old `status: superseded` |
| Stakeholder proposes a solution before the problem is understood | Add it as a requirement | Log it as a candidate in `opportunity-tree.md` under the relevant opportunity; do not promote to requirement until an experiment validates it |
| Session yields many verbatim quotes | Stop at evidence-log | After logging, check for 2+ quotes on the same theme and promote to a named insight in `findings/insights.md` |
| Assumption logged without a risk type | Leave blank | Classify as `value` / `usability` / `feasibility` / `viability` — unclassified assumptions aren't actionable |

Other ambiguous situations (new scope mid-ingest, superseded claims, unclear entity type, missing `steps-completed`) are covered directly by the General rules and the relevant command steps.

---

## Wiki layout

```
wiki/
  index.md                        — master navigation; always read first
  log.md                          — append-only operations log; never edit, only append
  01_use-cases/
    <uc-slug>/                    — one folder per use case (problem space)
      overview.md                 — scope entry point; problem statement, target outcome, HMW
      discovery-summary.md        — rolling current-state brief; updated after every session ingest
      opportunity-tree.md         — target outcome → opportunities → solutions → experiments
      findings/                   — what we know: deliverable content and accumulated evidence
        insights.md               — named insights synthesised from evidence; the "so what" layer
        assumptions-and-risks.md  — classified by product risk (value/usability/feasibility/viability)
        experiments.md            — hypothesis → experiment → result register
        dependencies.md
        decision-log.md
        evidence-log.md           — verbatim quotes and source-cited claims
        deliverables/             — client-facing deliverable pages; defaults below, adapt to engagement
          01-e2e-workflow.md
          02-scope-and-dependencies.md
          03-personas-and-operating-model.md
          04-requirements.md
      discovery/                  — how we are getting there: process, prep, tracking
        discovery-prep.md
        discovery-checklist.md    — live readiness tracker (⬜🟡✅⛔🧊)
        open-questions.md
        next-steps.md
        sessions/README.md
      queries/README.md
  02_core-topics/                 — cross-cutting topics (platforms, shared capabilities)
    <topic-slug>/                 — same structure as 01_use-cases/
  03_shared/                      — cross-cutting registers and snapshots
    executive-summary.md
    discovery-readiness.md        — roll-up of all scope checklist percentages
    top-open-questions.md         — curated P0/P1/P2 shortlist of blockers
    snapshots/                    — point-in-time state captures (one per day or on /snapshot)
    project-context.md · participants-and-stakeholders.md · cross-session-watch-list.md · workshop-insights.md
    master-{decision,risks,assumptions}-log.md · open-questions-register.md
  04_sources/README.md            — sequential source log (S-001, S-002 …)
  05_queries/README.md
  06_knowledge/                   — domain knowledge layer; independent of discovery tracking
    README.md
    ontology.md                   — entity types, relationship types, concept hierarchy (canonical)
    relationships.md              — master typed-relationship register
    entities/{people,systems,processes,organisations,document-types}/
    concepts/
    queries/README.md
  07_personas/                    — persona clusters; one page per cluster + README index
raw/
  _inbox-index.md                 — lightweight index of ALL clusters across all raw/ subfolders
  inbox/<cluster-slug>/           — drop zone; one folder per ingest cluster; _manifest.md + files
  sessions/                       — live capture during interviews, workshops, or onsite events
    _TEMPLATE-session-notes.md
    _TEMPLATE-daily-sync.md       — optional; for consecutive-day engagements
    <session-slug>/               — _manifest.md + notes and artefacts
  background/<cluster-slug>/      — immutable prior-context materials added before engagement starts
  assets/                         — photos, handouts, exported data
workspace/
  image-opportunities.md          — registry of image generation opportunities (append-only)
  assets/images/                  — AI-generated images stored here (<ID>.png)
  brief-YYYY-MM-DD.md             — compiled client-ready brief (created by /brief)
```

Not every engagement has live sessions. If the engagement is fully remote, document-driven, or asynchronous, `raw/sessions/` stays unused and all material arrives via `raw/inbox/`. The terms "session", "workshop", and "onsite" are used interchangeably — adapt to your engagement's vocabulary.

---

## Problem-space framing

### Vocabulary

Three terms are worth pinning down — they have overloaded meanings in product literature and this file uses specific ones:

- **Use case** — a **problem space** that is the unit of discovery. Broader than the software-engineering sense (a single user scenario); a use case here may encompass many user scenarios, journeys, and personas.
- **Core topic** — a shared problem space that several use cases depend on (e.g. an identity platform, a shared data layer, a cross-cutting capability). Same structure as a use case; exists separately so cross-cutting work has an obvious home.
- **Opportunity** — an **unmet user need, pain, or desire** (Torres sense). *Not* a feature request, *not* a market opportunity. Opportunities are problems to explore; solutions sit under them.

### The discovery loop

Every use case and core topic is a **problem space** — a named area where the team is trying to understand a problem deeply enough to choose what to build. Solutions are candidates under investigation, not starting assumptions. The flow:

`Problem + Target outcome (overview.md) → Opportunities → Solutions → Experiments (opportunity-tree.md + findings/experiments.md) → Evidence (findings/evidence-log.md) → Insights (findings/insights.md) → Validated/invalidated assumptions (findings/assumptions-and-risks.md) → Decisions (findings/decision-log.md) → Deliverables (findings/deliverables/)`

These artefacts reinforce each other. Evidence in a session should always land somewhere; insights should always connect to an opportunity; opportunities should always drive experiments; experiments should always sharpen assumptions.

<details>
<summary>Prior art this structure draws from</summary>

The artefacts are composed from established product-discovery practice — no single framework is required reading to use the wiki, but contributors familiar with the literature will recognise the shape.

- `opportunity-tree.md` follows the **Teresa Torres** opportunity-solution tree (*Continuous Discovery Habits*)
- Four product-risk types on experiments and assumptions follow **Marty Cagan / SVPG** (*Inspired*)
- `overview.md` problem statement + HMW follows the Define phase of **Design Thinking** (IDEO / Stanford d.school)
- `findings/insights.md` is the classic synthesis tier between raw evidence and decisions
- Persona JTBD statements follow **Christensen / Klement** "jobs to be done"

</details>

---

## Inbox and cluster system

The inbox is the **staging area** for all raw material, organised into **clusters** — bounded sets of files that belong together and can be processed in one operation. A cluster is the unit of ingest: one cluster = one `/ingest` call. Keeping clusters small and scoped prevents context overload and allows phased processing.

**To add material:** create a folder under `raw/inbox/<cluster-slug>/` (or `raw/sessions/<session-slug>/` for live session capture), drop your files into it, and fill in the `_manifest.md` (template below). The agent reads manifests to build the cluster menu; it never opens raw files until you confirm a cluster for ingestion.

**Cluster types:** `session-notes` (facilitator notes from a live session) · `transcript` (audio/video transcript — `.vtt`, `.srt`, `.txt`) · `document-pack` (related docs: specs, reports, standards) · `data-export` (structured data: CSV, XLSX, JSON) · `mixed` (heterogeneous materials from one contributor) · `background` (prior-context materials added before the engagement).

`raw/_inbox-index.md` is a table (columns: #, Cluster, Display name, Scope, Type, Size, Priority, Status, Added, Depends on) maintained automatically by the agent after every ingestion. It is the single file read during `/ingest` Phase 1.

---

## Knowledge layer in depth

The `06_knowledge/` section is the **semantic tier** of the wiki. It is organised around the domain, not the engagement — anyone unfamiliar with the discovery process can read these pages to understand how the domain works.

### Consolidation tiers

| Tier | Location | What it contains | Changes how |
|------|----------|-----------------|------------|
| Raw | `raw/` | Immutable source files and session notes | Never — locked after capture |
| Episodic | `04_sources/`, session pages | Source summaries, session digests | Permanent reference once written |
| Semantic | `06_knowledge/entities/`, `06_knowledge/concepts/` | Entity profiles, domain concepts, typed relationships | Updated as evidence accumulates; supersession tracked |
| Procedural | `06_knowledge/ontology.md`, `03_shared/` | Cross-cutting patterns, vocabulary, programme-level insights | Slowest to change; highest confidence |

A fact seen once stays episodic. A fact confirmed across three independent sources is promoted to a semantic entity or concept page with `confidence: high`.

### Entity types, relationship types, concepts

Entity types, relationship types, and the concept hierarchy are defined canonically in `wiki/06_knowledge/ontology.md`. Knowledge extraction and query steps reference the ontology rather than repeating the types here. See the ontology page template below.

**Concepts** are domain ideas — not named instances, but the categories, rules, and patterns that govern the domain. A concept page defines the idea, explains why it matters, and links to every entity and use case where it appears.

### Confidence and supersession

Every entity attribute and concept claim carries a confidence level. Claims contradicted by newer sources are marked `[SUPERSEDED YYYY-MM-DD by S-XXX: <replacement>]` — the old value is preserved for audit. Example:

| Attribute | Value | Confidence | Source | Status |
|-----------|-------|-----------|--------|--------|
| Repo deploy frequency | 2×/week | low | S-003 | [SUPERSEDED 2025-09-14 by S-011: corrected to 5×/week after CI pipeline rebuild] |
| Repo deploy frequency | 5×/week | high | S-011, engineering interview | Active |

---

## Labels, status, and confidence

**Inline labels:**

- `[EVIDENCE]` — claim supported by an ingested source; always cite the source
- `[ASSUMPTION]` — stated assumption not yet confirmed
- `[OPEN QUESTION]` — unresolved question requiring an answer
- `[RISK]` — identified risk
- `[TO CONFIRM]` — placeholder to be validated
- `[SUPERSEDED]` — claim overridden by newer evidence; always note what replaced it and when

**Confidence:** `low` (one source, inferred) · `medium` (2 sources or 1 session) · `high` (3+ independent sources, or explicitly confirmed in session). These levels apply to entity attributes, concept claims, and the `evidence-confidence` field on outcome/summary pages.

**Page status:** `not-started` · `in-progress` · `complete` · `blocked`

**Checklist icons:** ⬜ missing · 🟡 partial · ✅ confirmed · ⛔ blocked · 🧊 deferred

**Visibility field** (required on all outcome, persona, and shared pages; used by `/brief`):
- `internal` — working documents: logs, checklists, session notes, open questions
- `team` — shared within the delivery team but not client-facing
- `client-ready` — polished deliverables: exec summary, outcome pages, personas, readiness roll-up

**Evidence-confidence field** (on deliverable and summary pages): set to the **lowest** confidence among the claims on the page. Update whenever claim confidence changes.

**Product-risk types** (used on every row of `findings/assumptions-and-risks.md` and `findings/experiments.md`):
- `value` — will users / customers choose this over alternatives? Will they use it?
- `usability` — can they figure out how to use it?
- `feasibility` — can we build it with what we have (tech, data, skills, time)?
- `viability` — does it work for the business (legal, regulatory, economic, ethical, brand)?

Every assumption and every experiment is classified by exactly one type. Coverage gaps across the four types are a leading indicator of downstream surprise and surface on `discovery-summary.md`.

---

## `/bootstrap`

### Step 1 — Capture context

Ask for anything not already provided: project / engagement name, client or org name, domain (one sentence describing the field), known use cases, known core topics, session dates if any.

### Step 2 — Create folder structure

Create every folder and file in the Wiki layout. Each use case and core topic is treated as a **problem space** — not a pre-decided solution. For each **known use case or core topic**, create all standard pages from the templates, organised into:
- Root: `overview.md` (problem statement + target outcome + HMW), `discovery-summary.md`, `opportunity-tree.md`, `queries/README.md`
- `findings/`: `insights.md`, `assumptions-and-risks.md` (risk-type classified), `experiments.md`, `dependencies.md`, `decision-log.md`, `evidence-log.md`, `deliverables/` (four default client-facing pages — adapt to the engagement)
- `discovery/`: `discovery-prep.md`, `discovery-checklist.md`, `open-questions.md`, `next-steps.md`, `sessions/README.md`

For each **known session or workshop day**, create the session folder under `raw/sessions/<session-slug>/` with a blank `_manifest.md` and the session-notes template.

### Step 3 — Initialize the inbox

Create `raw/_inbox-index.md` as an empty index table. Create `raw/inbox/README.md` with drop-zone instructions explaining the cluster and manifest conventions.

### Step 4 — Initialize the knowledge layer

Create `wiki/06_knowledge/README.md`, `wiki/06_knowledge/ontology.md`, and `wiki/06_knowledge/relationships.md`. Seed the ontology with the standard entity types (`person`, `system`, `process`, `organisation`, `document-type`, `concept`) and standard relationship types (`owns`, `manages`, `uses`, `depends-on`, `produces`, `consumes`, `contradicts`, `supersedes`, `caused-by`, `mitigated-by`, `related-to`). Add domain-specific types if the bootstrap context implies them. Create `README.md` files in all entity subfolders and in `concepts/`.

### Step 5 — Populate shared pages

Fill `wiki/03_shared/project-context.md` from bootstrap context. Seed `cross-session-watch-list.md` with a short list of recurring-pattern themes **tailored to the domain the user described** — pick 5–10 themes that represent the failure modes or hidden dependencies the agent should listen for across sessions (e.g. for a technical-assessment engagement: "undocumented coupling", "on-call toil", "silent failure modes"; for an operations-discovery engagement: "manual workaround as system-of-record", "single-point-of-failure expert", "audit-trail gaps"). Create `discovery-readiness.md` (row per scope, counts at 0), `executive-summary.md` (shell), `top-open-questions.md` (empty prioritized register — columns: ID, Question, Why it blocks delivery, Who to ask, Status), `wiki/log.md` (first entry), and `wiki/index.md` (master navigation table).

### Step 6 — Create session templates

Create `raw/sessions/_TEMPLATE-session-notes.md` and, for consecutive-day engagements, `raw/sessions/_TEMPLATE-daily-sync.md`.

### Step 7 — Create persona and workspace scaffolds

Create `wiki/07_personas/README.md` (header, empty cluster table, "Key design implications" and "How this section is maintained" sections). Do not create individual cluster pages yet — they appear when personas are first identified during `/ingest`.

Create `workspace/image-opportunities.md` with an append-only header, the directory `workspace/assets/images/`, and `wiki/03_shared/snapshots/`.

### Step 8 — Write README.md at repo root

Create a `README.md` summarising the engagement and pointing at `wiki/index.md`.

### Step 9 — Confirm

Report to the user: (a) the folder tree created with a count of files per top-level section, (b) which use cases and core topics were scaffolded vs. left as placeholders, (c) any bootstrap-context fields that were missing and need follow-up, (d) the next recommended command (usually `/ingest` once manifests are ready). This is a forcing function for completeness — do not skip.

---

## `/ingest`

This command is phased. The agent never reads raw files until the user has confirmed which cluster to process, keeping context manageable regardless of how much material is staged.

### Phase 1 — Scan and present clusters

Read `raw/_inbox-index.md` (the only file read in this phase). If it does not exist or is empty, scan for `_manifest.md` files across `raw/inbox/`, `raw/sessions/`, and `raw/background/`; build the index and write it. Filter to clusters with `status: ready` or `partial` and present a selection table (columns: #, Cluster, Scope, Type, Size, Priority, Status, plus a `⚠ depends on: <slug>` warning on any row whose dependency is unmet).

Ask: *"Which clusters would you like to ingest now? Enter numbers, `all`, or `none`."*

If a cluster's `_manifest.md` is malformed or partially filled, read what's parseable, flag the gaps to the user, and ask whether to proceed.

### Phase 2 — Confirm and load

For each selected cluster: read its `_manifest.md`, report what will be ingested and which wiki pages will be created or updated. If the selection includes a cluster with an unmet dependency, warn explicitly and ask whether to proceed. Proceed cluster by cluster, completing each fully before starting the next.

### Phase 3 — Process each cluster

For each cluster, run the steps below in order. Track which steps ran in the session page's `steps-completed` frontmatter field — a missing step is a detectable gap that `/lint` flags.

**Step A — Read raw files.** Read every file listed in the cluster's `_manifest.md`. Do not read files outside the cluster.

**Step B — Create source note.** Create `wiki/04_sources/YYYY-MM-DD-<slug>.md` (increment S-XXX from `04_sources/README.md`). For `session-notes` clusters, also create the session page at `wiki/<scope>/discovery/sessions/YYYY-MM-DD-session-notes.md`.

**Step C — Scope-expansion gate.** Scan the content for new use cases or core topics not yet in the wiki. **Do not silently create new scope folders.** If a new scope is detected:
1. Create `wiki/03_shared/CANDIDATE-<slug>.md` with the detected evidence, proposed structure, and confirmation questions.
2. Pause and tell the user: *"A potential new scope '<Name>' was detected. Confirm to scaffold, or dismiss to ignore."*
3. Only scaffold after explicit confirmation. Delete the candidate file and log the scope creation.

This applies regardless of confidence. Scope expansion is a change-control event. If the source ambiguously references multiple potential new scopes, create one `CANDIDATE-<slug>.md` per scope rather than combining them.

**Step D — Knowledge extraction.** Extract entities, concepts, and typed relationships using the types defined in `06_knowledge/ontology.md`; update `06_knowledge/` pages (create where absent, update attributes, mark superseded claims). Upgrade confidence (`low` → `medium` → `high`) as evidence accumulates. Add backlinks from each entity/concept page to the source or session that introduced it, and forward links from `overview.md` and `findings/evidence-log.md` to the relevant entity/concept pages. If an entity's type is unclear, use the most specific existing type and add a note — do not invent a new entity type without updating the ontology deliberately.

**Step E — Propagate to wiki pages.**

*Root:* `discovery-summary.md` (rewrite "Current state" and "What changed"; update confidence, readiness %, and top blockers); `opportunity-tree.md` (add newly-surfaced opportunities under the target outcome; add candidate solutions; mark any tested opportunities/solutions).

*Findings:* `findings/evidence-log.md` (verbatim quotes as `[EVIDENCE]` — **write these first**, they anchor everything else); `findings/insights.md` (promote recurring evidence into named insights — each insight references 2+ evidence rows); `findings/assumptions-and-risks.md` (validated/invalidated; add new risks; classify each by product-risk type: value/usability/feasibility/viability); `findings/experiments.md` (log experiment results; update hypothesis status; add new planned experiments); `findings/deliverables/` pages (fill `[TO CONFIRM]` items closed; update `evidence-confidence`); `findings/decision-log.md` (decisions taken).

*Discovery:* `discovery/open-questions.md` (close resolved; add new), `discovery/next-steps.md` (post-session actions), `discovery/discovery-checklist.md` (flip rows, add ✅ links, recompute counts and top-5 blockers).

*Shared:* propagate cross-cutting decisions, risks, and open questions to master registers; update `workshop-insights.md` with new patterns or contradictions; update `top-open-questions.md` if blockers change; refresh `discovery-readiness.md`.

**Step F — Update persona pages.** For every named individual or group confirmed in the cluster, check whether they belong to an existing cluster in `wiki/07_personas/`. If yes, update the cluster page (named individuals, day-in-their-life, frustrations, what-they-need, evidence trail, open questions). If a new cluster is warranted (confidence medium or higher), create it from the persona template and add it to the README. Cross-link to each named individual's entity page in `06_knowledge/entities/people/` via a `persona-cluster` field.

**Step G — Evaluate image opportunities.** For every wiki page created or substantially updated, evaluate whether a generated image would meaningfully improve understanding (see Images & diagrams). Append strong opportunities to `workspace/image-opportunities.md`.

**Step H — Update indexes.** Add a row to `wiki/index.md`; add a row to `wiki/<scope>/discovery/sessions/README.md` (for session clusters); mark the cluster `status: ingested` and set `ingested: YYYY-MM-DD` in its `_manifest.md`; update `raw/_inbox-index.md`.

**Step I — Update steps-completed.** Record which letters ran in the session page frontmatter (e.g. `steps-completed: [A, B, C, D, E, F, G, H, I]`).

**Step J — Log.** Append to `wiki/log.md`: cluster name, files read, pages created/updated, entity/concept count, persona pages updated, steps-completed list.

### Phase 4 — Summary

After all selected clusters are processed, report: clusters ingested, new wiki pages, existing pages updated, new entities/concepts, remaining clusters with priorities.

---

## `/query`

If no question is provided, ask for one.

**Step 1 — Scope.** Route to `wiki/01_use-cases/<slug>/queries/`, `wiki/02_core-topics/<slug>/queries/`, `wiki/06_knowledge/queries/`, or `wiki/05_queries/` (global). When in doubt, default to global. If the question genuinely touches 3+ scopes, prefer global over artificially narrowing to one.

**Step 2 — Check for overlap.** Scan the target queries folder for an existing query covering the same ground. If one exists and this refines it, set `supersedes: <filename>` in the new query's frontmatter and mark the old as `status: superseded`. If essentially identical, update the existing query instead. Queries that are `status: superseded` or `promoted: true` stay in the index with a strikethrough; they are not deleted.

**Step 3 — Research.** Read `wiki/index.md` first. Then read all plausibly relevant pages: for scoped areas, at minimum `overview.md`, `discovery-summary.md`, `opportunity-tree.md`, `findings/insights.md`, `discovery/open-questions.md`, `findings/evidence-log.md`; relevant entity/concept pages from `06_knowledge/`; and `04_sources/README.md`. For global queries also read `03_shared/executive-summary.md`. Cite every claim: `[Source: page-name.md]` or `[Source: S-XXX]`.

**Step 4 — Choose format.** Markdown page · comparison table · Mermaid diagram · Marp deck · matplotlib chart · PIL infographic · multi-part markdown. Pick the format that best fits the question.

**Step 5 — Write and file.** Frontmatter: `title`, `query`, `scope`, `scope-ref`, `format`, `date`, `status: draft`, `supersedes: ""`, `promoted: false`. Body: Answer (with citations), Sources consulted, Limitations and caveats, Follow-on questions. File as `YYYY-MM-DD-<slug>.md` in the correct scope folder. Add to `wiki/index.md`. Append to `wiki/log.md`.

**Step 6 — Evaluate image opportunities.** Apply the image opportunity evaluation to the query page.

**Step 7 — Crystallize.** Ask: *does this answer contain facts, relationships, or concepts worth promoting into `06_knowledge/`?* A good query often synthesises across sources in a way that reveals new entity relationships or sharpens a concept definition. If so, update the relevant entity or concept pages, add the query as a source reference, and add entries to `relationships.md` for any new typed relationships.

---

## `/lint`

Optional scoping: `/lint` (full), `/lint <scope>` (single use case or topic), `/lint knowledge` (knowledge layer only), `/lint discovery` (discovery layer only).

### Checks

**Knowledge layer:**
- Entity page with no inbound links → flag `[ORPHAN]`; add backlinks
- Concept mentioned inline but no concept page → create it
- Relationship in `relationships.md` without source → flag `[UNSOURCED]`
- `confidence: low` attributes upgradable from wiki content → upgrade
- Chained `[SUPERSEDED]` with still-stale replacement → update the chain
- Contradicting entity attributes with no supersession → flag; supersede older
- Source notes with no entity/concept extractions → run extraction
- Duplicate concept pages → merge; redirect weaker
- Entity or relationship type used but not in `ontology.md` → add to ontology

**Discovery layer:**
- `overview.md` missing problem statement, target outcome, or HMW → flag
- `opportunity-tree.md` opportunities without solutions after 2+ sessions → flag
- `opportunity-tree.md` solutions without experiments → flag
- Assumption missing `risk-type` → flag; prompt to classify
- Product-risk coverage gap (e.g. no viability tests) → flag on `discovery-summary.md`
- 3+ same-theme evidence rows without named insight → flag; synthesise
- Experiment `status: running` >2 weeks without result → flag stalled
- Persona without JTBD statement → flag
- `[TO CONFIRM]` in `findings/deliverables/` answered in sessions → fill
- Open question resolved elsewhere → close with link
- Decision without owner or date → flag
- `high`-severity risk without mitigation → flag in `master-risks-log.md`
- Checklist % out of sync with evidence-log → recalculate
- `discovery-readiness.md` out of sync with per-scope checklists → recalculate
- `wiki/index.md` rows missing or stale vs. disk → add/remove
- `discovery-summary.md` `last-updated` older than most recent session → flag stale
- Session page missing or empty `steps-completed` → flag
- Session page `steps-completed` missing step G → evaluate image opportunities
- Deliverable or summary page without `visibility:` or `evidence-confidence:` → add defaults
- Persona cluster without `visibility:` → set `internal`
- Persona ↔ entity cross-link broken → create or link

### Report and fix behaviour

Report per-section counts (knowledge: orphans, unsourced, confidence upgrades, supersessions, new/merged concepts; discovery: `[TO CONFIRM]` resolved, open questions closed, checklist rows updated, index rows added/removed). List items requiring human review with file paths. Apply all automatic fixes immediately; flag ambiguous items. Append to `wiki/log.md`.

---

## Reporting commands

### `/status`

Chat-only orientation brief (no files written). Read `wiki/index.md` (header), `wiki/03_shared/discovery-readiness.md` (readiness + blockers), `wiki/03_shared/top-open-questions.md` (P0 rows only), `wiki/log.md` (last 5 entries). Respond with: ingested count, days or phases complete, per-scope readiness table, top P0 blockers, last 5 log entries, pending workspace items (image opportunities, candidate scopes, snapshots).

### `/snapshot`

Create `wiki/03_shared/snapshots/YYYY-MM-DD-snapshot.md` capturing: readiness table (from `discovery-readiness.md`), open question counts, risk counts, decision counts, sources ingested since last snapshot, 2–4 sentence state-of-play narrative, current cross-scope blockers. Add a row to `wiki/index.md` under Snapshots. Append to `wiki/log.md`.

### `/brief`

Compile all pages with `visibility: client-ready` into a single shareable output. Default format is markdown; pass `/brief marp` for a slide deck. Create in `workspace/brief-YYYY-MM-DD.md` (or `-slides.md` for Marp). Sections: cover + engagement summary, readiness snapshot, per-scope outcome summaries, persona clusters overview, cross-cutting findings, recommended next steps. Marp rules: fenced slide separators, ≤3 bullets per slide, `<!-- fit -->` for large headings. Append to `wiki/log.md`.

---

## Images & diagrams

Generate a visual when it would genuinely aid understanding more than text alone. Every image has alt-text and a text equivalent — a page must stand alone as text.

**Mermaid** — embed directly in wiki pages as fenced code blocks. Use `flowchart TD` for process flows and architecture, `graph LR` for entity relationship maps, `sequenceDiagram` for actor interactions, `classDiagram` for ontology structure.

**Matplotlib** — for charts driven by wiki data (readiness heatmaps, coverage bars). Write a runnable Python script in `tools/`; run it with `! python tools/<script>.py`; output to `workspace/assets/`.

**PIL/Pillow** — for layout-heavy composites that don't fit a chart (persona cards, cluster overviews). Also a runnable script in `tools/`; output to `workspace/assets/`.

**External image API** (`/generate-image`) — for rich architectural diagrams, swimlanes, and visuals that need natural-language art direction. On-demand only, never called automatically during `/ingest` or `/query`.

### Image opportunity evaluation

After creating or substantially updating any wiki page, evaluate whether a generated image would meaningfully improve the reader's understanding. Flag when the page contains a multi-step end-to-end workflow, system architecture with named components, role/persona map, data model or schema, timeline or phased plan, or comparison of two or more options. Do **not** flag pages that are primarily log/register tables, simple Q&A lists, or pages that already contain a Mermaid diagram covering the same content. Only append an opportunity if it would provide **strong** additional clarity — not decoration.

Append to `workspace/image-opportunities.md` as a `## IMG-NNN` block with fields: **ID** (increment from last; start at IMG-001), **Status** (pending | generated | embedded), **Wiki page** (relative path), **Page section** (heading where the image should be inserted), **Image type** (flowchart | swimlane | architecture | persona-map | er-diagram | timeline | comparison-matrix), **Rationale** (one sentence), **Prompt** (complete self-contained image-generation prompt including style, colour palette, labelling, and all domain-specific details drawn from the page content).

### `/generate-image <ID>`

**Step 1 — Load.** Locate the entry in `workspace/image-opportunities.md`. If not found, tell the user and stop. If `Status` is already `generated` or `embedded`, confirm with the user before regenerating. With no ID passed, list all `pending` entries and ask which to generate.

**Step 2 — Provider.** Check API keys in order: `OPENAI_API_KEY` (OpenAI `gpt-image-1`, POST to `https://api.openai.com/v1/images/generations`) → `GEMINI_API_KEY` (Gemini Imagen, POST to `https://generativelanguage.googleapis.com/v1beta/models/imagen-3.0-generate-001:predict`). If neither is set, tell the user to export one and stop.

**Step 3 — Generate.** Call the API with the **Prompt** from the entry. Size: 1792×1024 for flowcharts/architectures; 1024×1024 for persona maps and comparison matrices. Save to `workspace/assets/images/<ID>.png`.

**Step 4 — Embed.** Insert the image reference immediately after the named section heading in the target page: `![<alt>](../../../../workspace/assets/images/<ID>.png)` (adjust depth).

**Step 5 — Update status.** Set `Status: embedded` on the entry.

**Step 6 — Log.** `[YYYY-MM-DD] /generate-image <ID> — embedded in <path> section "<section>"`.

---

## Page templates

### `overview.md` (use case or core topic)

```markdown
---
title: "<Name> — Overview"
scope: "use-case | core-topic"
slug: "<uc-XX-name | topic-name>"
status: not-started
confidence: low
last-updated: YYYY-MM-DD
auto-detected-from: ""
---

# <Name>

## Problem statement
<One paragraph: what problem are we exploring? Whose problem is it? Why does it matter now? Frame as a problem to understand, not a solution to build. Avoid naming a specific technology or feature.>

## Target outcome
<The measurable business or customer outcome that solving this problem would produce. Must be measurable.>

| Dimension | Current state | Target state | Measurement |
|-----------|---------------|-------------|-------------|
| <metric name> | <value today> | <value we want> | <how we'll measure> |

## How might we (HMW) reframes
Alternative framings of the problem that open up solution space. Each HMW should be broad enough to admit multiple solutions, narrow enough to focus exploration.

- How might we <...>?
- How might we <...>?

## Trigger
<What event or condition starts work in the current-state workflow?>

## Current workflow (as-is)
<Numbered steps. Mark unconfirmed steps [ASSUMPTION]. This is the problem landscape, not a proposed design.>

## Inputs
| Input | Source system | Format | Owner |
|-------|--------------|--------|-------|

## Outputs
| Output | Destination | Format | Consumer |
|--------|-------------|--------|---------|

## Key personas
Links to persona cluster pages in `wiki/07_personas/`. Each cluster carries a JTBD statement.

| Persona cluster | Primary relationship to this problem |
|-----------------|-------------------------------------|

## Key entities
<Links to pages in wiki/06_knowledge/entities/>

## Related concepts
<Links to pages in wiki/06_knowledge/concepts/>

## Related use cases / topics
<Links>

## Claims to validate
- [TO CONFIRM] <claim>

---

## Navigation

**Current state:** [Discovery Summary](./discovery-summary.md) · [Opportunity Tree](./opportunity-tree.md)

**Findings** (what we know): [Insights](./findings/insights.md) · [Deliverables](./findings/deliverables/) · [Assumptions & Risks](./findings/assumptions-and-risks.md) · [Experiments](./findings/experiments.md) · [Dependencies](./findings/dependencies.md) · [Decisions](./findings/decision-log.md) · [Evidence](./findings/evidence-log.md)

**Discovery** (how we get there): [Prep](./discovery/discovery-prep.md) · [Checklist](./discovery/discovery-checklist.md) · [Open Questions](./discovery/open-questions.md) · [Next Steps](./discovery/next-steps.md) · [Sessions](./discovery/sessions/README.md)
```

---

### `discovery-summary.md` (scope root)

The single page a reader should check first to understand where a scope stands right now. Updated after every session ingest. Does not duplicate content from other pages — references them.

```markdown
---
title: "<Name> — Discovery Summary"
scope: "use-case | core-topic"
slug: "<slug>"
status: not-started
evidence-confidence: low
visibility: internal
last-updated: YYYY-MM-DD
last-session: YYYY-MM-DD
---

# <Name> — Discovery Summary

> **Last updated:** YYYY-MM-DD · **Last session:** YYYY-MM-DD · **Readiness:** ~N%

## Current state in one paragraph
<Two to four sentences: what is understood, what is still open, and the single most important thing to resolve next. Written for someone joining cold.>

## What changed this session
<Bullet list of the most significant things learned or decided in the most recent session.>

## Readiness snapshot
| Measure | Value |
|---------|-------|
| Checklist items confirmed ✅ | N / N total |
| Open questions | N open · N closed |
| Key decisions landed | N |
| Blocking risks | N high-severity |
| Evidence confidence | <level> |

## Top blockers right now
1. <blocker — link to open question or risk>

## Product-risk coverage
Which of the four product risks are we actively testing? Gaps here are a leading indicator of downstream surprise.

| Risk type | Coverage | Notes |
|-----------|----------|-------|
| Value (will they use it?) | not-started / partial / covered | — |
| Usability (can they use it?) | — | — |
| Feasibility (can we build it?) | — | — |
| Viability (should we build it — business/compliance/ethics?) | — | — |

## What we know well
<High-confidence insights — link to `findings/insights.md` entries.>

## What is still assumed or uncertain
<Open assumptions — link to `findings/assumptions-and-risks.md`.>

## Next most important action
<Single most impactful thing to do before the next session or deliverable. Owner and deadline if known.>

## Related pages
- [Overview](./overview.md)
- [Opportunity tree](./opportunity-tree.md)
- [Insights](./findings/insights.md)
- [Discovery checklist](./discovery/discovery-checklist.md)
- [Open questions](./discovery/open-questions.md)
- [Sessions](./discovery/sessions/README.md)
```

---

### `opportunity-tree.md` (scope root)

The organising spine of discovery for this scope, in the Teresa Torres / Continuous Discovery sense. Flows: Target Outcome → Opportunities (unmet needs, pain points, desires grounded in evidence) → Solutions (candidate bets) → Experiments (tests of the riskiest assumption behind each solution). Every element carries an ID so evidence, insights, and experiments can reference it.

```markdown
---
title: "<Name> — Opportunity Tree"
scope: "use-case | core-topic"
slug: "<slug>"
status: in-progress
visibility: internal
last-updated: YYYY-MM-DD
---

# <Name> — Opportunity Tree

> **In this file, an opportunity is an unmet user need, pain, or desire — not a feature, not a market opportunity.** Opportunities are problems to explore, not solutions. Solutions sit under opportunities and are tested by experiments.
>
> **Target outcome:** see `overview.md` → Target outcome. This tree's job is to organise how we move that outcome — not to restate it.

## Opportunities

Unmet needs, pain points, and desires grounded in evidence. Framed as problems, not solutions. Each opportunity is evidenced (link to `findings/evidence-log.md` rows or `findings/insights.md` entries) and sized (reach × value × confidence).

| ID | Opportunity (user-framed need) | Evidence | Reach | Value | Confidence | Status |
|----|-------------------------------|----------|-------|-------|-----------|--------|
| OPP-001 | <"Users can't tell when a change is safe to ship"> | [E-007](./findings/evidence-log.md#e-007), [I-003](./findings/insights.md#i-003) | high | high | medium | exploring |
| OPP-002 | — | — | — | — | — | — |

## Candidate solutions

Solutions map 1-to-many under opportunities. Each solution has a hypothesis about how it moves the target outcome, a rough complexity signal from engineering, and a status (proposed / testing / validated / invalidated / parked). Complexity is a t-shirt size (S / M / L / XL) contributed by engineering — it is not a commitment to build, it is signal for prioritisation.

| ID | Addresses | Solution (candidate bet) | Hypothesis | Complexity | Status |
|----|-----------|--------------------------|-----------|-----------|--------|
| SOL-001 | OPP-001 | <"Pre-deploy safety check dashboard"> | We believe showing <signal> to <user> will reduce <metric> by <amount> | M | testing |
| SOL-002 | — | — | — | — | — |

## Experiments in flight

**Pointer only — the canonical register is `findings/experiments.md`.** One row per experiment currently testing an opportunity or solution, so the tree can be read end-to-end without leaving the page.

| Experiment | Tests | Status | Link |
|-----------|-------|--------|------|
| EXP-001 | SOL-001 | running | [EXP-001](./findings/experiments.md#exp-001) |

## Parked / rejected branches

Record anything considered and set aside with ID, reason, and date — one row per parked item. Protects against re-litigation and preserves rationale.
```

---

### `findings/insights.md`

The synthesis layer between raw evidence and decisions. An insight is a **named, source-cited pattern** that consolidates 2+ pieces of evidence into something actionable. Insights answer "so what?" — they turn a pile of quotes into a claim about the problem space.

```markdown
---
title: "<Name> — Insights"
scope-ref: "<slug>"
status: in-progress
visibility: internal
last-updated: YYYY-MM-DD
---

# <Name> — Insights

> Named patterns synthesised from evidence. Each insight references ≥2 evidence rows and has a clear "so what" implication. Insights feed opportunities and challenge assumptions.

| ID | Insight (named pattern) | Evidence | Confidence | So what? (implication) |
|----|-------------------------|---------|-----------|------------------------|
| I-001 | <"Users work around the official workflow when X happens"> | [E-004](./evidence-log.md#e-004), [E-011](./evidence-log.md#e-011), [E-019](./evidence-log.md#e-019) | high | Workarounds are invisible to dashboards — metrics likely underestimate incident rate |
| I-002 | — | — | — | — |

## How insights flow

- Evidence rows (verbatim quotes, observations) accumulate in `evidence-log.md`
- When a pattern is seen across 2+ independent sources, it is named and promoted to an insight here
- Insights feed `opportunity-tree.md` (new opportunities) and challenge `assumptions-and-risks.md` (validate/invalidate)
- High-confidence insights promote to `06_knowledge/concepts/` via the crystallize step of `/query`
```

---

### `findings/experiments.md`

The hypothesis register: each experiment tests the riskiest assumption behind a solution or opportunity. Follows the Lean/SVPG pattern: hypothesis → method → success criteria → result → implication.

```markdown
---
title: "<Name> — Experiments"
scope-ref: "<slug>"
status: in-progress
visibility: internal
last-updated: YYYY-MM-DD
---

# <Name> — Experiments

> Every riskiest-assumption test, planned or run. Each experiment is linked to a solution or opportunity in `opportunity-tree.md` and classified by product-risk type.

| ID | Tests | Risk type | Hypothesis | Method | Success criteria | Status | Result | Implication |
|----|-------|-----------|-----------|--------|------------------|--------|--------|-------------|
| EXP-001 | SOL-001 | usability | We believe target users will notice the new signal in their existing flow | 5 moderated usability sessions with think-aloud | ≥4/5 users surface the signal without prompting | running | — | — |
| EXP-002 | OPP-002 | value | We believe users will pay for this outcome | Smoke test: landing page + CTA over 2 weeks | ≥8% click-through | planned | — | — |

## Product-risk reminder

Every hypothesis tests exactly one of:
- **Value** — will users / customers choose this over alternatives?
- **Usability** — can they figure out how to use it?
- **Feasibility** — can we build it with what we have?
- **Viability** — does it work for our business (legal, regulatory, economic, ethical)?

A discovery with coverage on only one or two risk types has a blind spot. See `discovery-summary.md` → Product-risk coverage.

## Parked experiments

Record parked experiments with ID, reason parked, and date.
```

---

### `discovery-checklist.md`

```markdown
---
title: "<Name> — Discovery Readiness Checklist"
scope-ref: "<slug>"
status: not-started
last-updated: YYYY-MM-DD
---

# <Name> — Discovery Readiness Checklist

## Readiness overview
| Measure | Value |
|---|---|
| Total items | **0** |
| Confirmed ✅ | 0 (0%) |
| Partial 🟡 | 0 (0%) |
| Missing ⬜ | 0 (0%) |
| Blocked ⛔ | 0 |
| Deferred 🧊 | 0 |
| **Overall readiness** | **0%** |

### Top 5 blockers
1. ⬜ TBD

---

## Legend
⬜ missing · 🟡 partial · ✅ confirmed · ⛔ blocked · 🧊 deferred

## P0 — critical
| # | Item | Type | Status | Who to ask | Evidence so far | Wiki refs |
|---|------|------|:---:|---|---|---|
| 1 | Process owner identified | stakeholder | ✅ | — | Confirmed by session 2025-03-14 | [session notes](../discovery/sessions/2025-03-14-session-notes.md) |
| 2 | End-to-end workflow documented | process | 🟡 | Process owner | Steps 1–4 confirmed; steps 5–7 inferred | [deliverable 01](../findings/deliverables/01-e2e-workflow.md) |
| 3 | Upstream data contract | data | ⬜ | Data team lead | — | [overview.md](../overview.md) |

## P1 — important
| # | Item | Type | Status | Who to ask | Evidence so far | Wiki refs |
|---|------|------|:---:|---|---|---|

## P2 — useful
| # | Item | Type | Status | Who to ask | Evidence so far | Wiki refs |
|---|------|------|:---:|---|---|---|

## How this page updates
Every `/ingest` run that touches this scope must update this page: flip rows, add evidence links, recompute counts.
```

---

### Entity page (`06_knowledge/entities/<type>/<slug>.md`)

```markdown
---
title: "<Entity Name>"
entity-type: <type-from-ontology>
confidence: low
sources: []
last-confirmed: YYYY-MM-DD
last-updated: YYYY-MM-DD
---

# <Entity Name>

> **Type:** <entity-type> · **Confidence:** <level> · **First seen:** [S-XXX](../../04_sources/slug.md)

## Description
<One paragraph: what this entity is and why it matters.>

## Attributes
| Attribute | Value | Confidence | Source | Notes |
|-----------|-------|-----------|--------|-------|
| Team size | 8 engineers | medium | S-004 | 6 confirmed by name; 2 inferred |

## Relationships
| Relationship | Target | Confidence | Source |
|-------------|--------|-----------|--------|
| `owns` | [Deployment Pipeline](../systems/deployment-pipeline.md) | high | S-007 |

## Appearances in wiki
| Page | Context |
|------|---------|
| [UC-XX overview](../../01_use-cases/uc-xx/overview.md) | Named as workflow owner |

## Open questions
- [OPEN QUESTION] <what is still unknown>

## Change log
| Date | Change | Source |
|------|--------|--------|
| YYYY-MM-DD | Created | S-XXX |
```

---

### Concept page (`06_knowledge/concepts/<slug>.md`)

```markdown
---
title: "<Concept Name>"
entity-type: concept
confidence: low
sources: []
domain-area: "<broad area>"
last-updated: YYYY-MM-DD
---

# <Concept Name>

> **Confidence:** <level> · **Domain area:** <area>

## Definition
<What does this concept mean? Explain it to someone unfamiliar with the domain.>

## Why it matters
<Why does this show up in discovery? What decisions or risks does it drive?>

## Related concepts
| Concept | Relationship |
|---------|-------------|
| [Feature flagging](./feature-flagging.md) | A mechanism that enables this concept |

## Entities involved
| Entity | Role |
|--------|------|
| [Deployment Pipeline](../entities/systems/deployment-pipeline.md) | Primary enforcement point |
| [Engineering Manager](../entities/people/eng-manager.md) | Accountable for compliance |

## Appearances
| Page | Context |
|------|---------|
| [UC-XX](../../01_use-cases/uc-xx/overview.md) | Drives the scope boundary |

## Evidence
- [EVIDENCE] "<verbatim quote>" [Source: S-XXX]

## Open questions
- [OPEN QUESTION] <unresolved aspect>
```

---

### Ontology (`06_knowledge/ontology.md`)

This is the canonical definition of entity types, relationship types, and the concept hierarchy. All other pages reference it.

```markdown
---
title: "Domain Ontology"
status: in-progress
last-updated: YYYY-MM-DD
---

# Domain Ontology

> Vocabulary of this wiki. Updated whenever new entity types, relationship types, or major concepts are introduced.

## Entity types
| Type | Description | Folder |
|------|-------------|--------|
| `person` | Named individuals: role, org, responsibilities | `entities/people/` |
| `system` | Software, tools, platforms | `entities/systems/` |
| `process` | Named workflows or business procedures | `entities/processes/` |
| `organisation` | Teams, departments, committees, external orgs | `entities/organisations/` |
| `document-type` | Categories of document — domain-specific (e.g. spec, report, form, contract) | `entities/document-types/` |
| `concept` | Domain ideas, rules, and patterns | `concepts/` |

## Relationship types
| Type | Direction | Meaning |
|------|-----------|---------|
| `owns` | A → B | A is accountable for B |
| `manages` | A → B | A supervises or coordinates B |
| `uses` | A → B | A depends on system B in their workflow |
| `depends-on` | A → B | Process A cannot run without B |
| `produces` | A → B | Process A outputs B |
| `consumes` | A → B | Process A requires B as input |
| `contradicts` | A ↔ B | Claim A and claim B cannot both be true |
| `supersedes` | A → B | Decision/claim A replaces older B |
| `caused-by` | A ← B | Risk/problem A is caused by condition B |
| `mitigated-by` | A → B | Risk A is reduced by control B |
| `related-to` | A ↔ B | Connected; relationship not yet typed |

## Concept hierarchy
| Domain area | Concepts |
|-------------|---------|
| — | — |

## Domain-specific additions
<Any entity or relationship types added beyond the standard set, with rationale.>
```

---

### Relationships register (`06_knowledge/relationships.md`)

```markdown
---
title: "Typed Relationship Register"
status: in-progress
last-updated: YYYY-MM-DD
---

# Typed Relationship Register

> Every typed relationship between entities. Updated on every /ingest and /lint.

| # | Source entity | Relationship | Target entity | Confidence | Source | Notes |
|---|--------------|-------------|---------------|-----------|--------|-------|
```

---

### Persona cluster page (`07_personas/cluster-NN-<slug>.md`)

The sections below are the default UX-research shape. Drop or adapt sections that don't fit a given engagement.

```markdown
---
title: "Cluster N — <Label>: <Full Name>"
persona-cluster: "<slug>"
confidence: low
use-cases: []
last-updated: YYYY-MM-DD
status: not-started
visibility: internal
---

# Cluster N — "<Label>": <Full Name>

> **Confidence:** <level> · **Primary use cases:** <list>

## Jobs-to-be-done

Canonical JTBD format: When [situation], I want to [motivation], so I can [expected outcome]. One primary job; optional secondary jobs.

- **Primary job:** When <situation>, I want to <motivation>, so I can <expected outcome>.
- **Secondary jobs:** <optional>

Functional / emotional / social dimensions:

| Dimension | What the job looks like on this axis |
|-----------|-------------------------------------|
| Functional | <what they are trying to get done> |
| Emotional | <how they want to feel, or avoid feeling> |
| Social | <how they want to be perceived> |

## Who they are
<One paragraph.>

### Named individuals confirmed across sessions and sources
| Name / Group | UC / Domain | Role / What they do |
|-------------|-------------|---------------------|

## A day in their life
<Narrative: typical day, concrete volumes, tool names, pain points.>

## Goals and motivations
- <what they are trying to achieve>

## Frustrations and pain points
- <what goes wrong today>

## What they need from solutions
- <concrete capabilities>

> **Design principle:** <one-sentence rule that should never be violated for this cluster>

## Profile dimensions
| Dimension | Profile |
|-----------|---------|
| <dimension — adapt to engagement> | <value> |

## Where this cluster appears
| Page | Role / context |
|------|---------------|

## Open questions
- `[OPEN QUESTION]` <unresolved>

## Evidence trail
| Evidence | Source |
|----------|--------|
```

---

### Cluster manifest (`_manifest.md`)

```markdown
---
cluster: "<cluster-slug>"
display-name: "<human-readable name>"
scope: "<uc-slug | topic-slug | multi | unknown>"
type: session-notes | transcript | document-pack | data-export | mixed | background
size: small | medium | large        # small <5pp, medium 5-50pp, large 50+pp
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

## Notes
<Optional context for the operator.>
```

---

### Session notes page (created by `/ingest` for session-type clusters)

This page is *derived* from the raw session capture template below and mirrors its structure.

```markdown
---
title: "<Session Name> — Session Notes, <YYYY-MM-DD>"
session: "<session-slug>"
date: YYYY-MM-DD
sources:
  - raw/sessions/<session-slug>/<file>
status: complete
visibility: internal
steps-completed: []
---

# <Session Name> — Session Notes

> **YYYY-MM-DD · <duration>** — synthesised from cluster `<cluster-slug>`.

## Attendance
<who was present; missing must-have attendees and impact>

## Key findings
<bullet list; cite as [EVIDENCE] where backed by session quotes>

## Decisions taken
| Decision | Owner | Notes |
|----------|-------|-------|

## Validated / invalidated assumptions
| Assumption | Outcome | Evidence |
|------------|---------|---------|

## New open questions
| # | Question | Who to ask | Priority |
|---|---------|-----------|---------|

## New risks
| Risk | Severity | Owner |
|------|---------|-------|

## Watch-list signals
Use the watch-list themes defined in `wiki/03_shared/cross-session-watch-list.md`. One row per theme: seen Y/N + signal description.

## Entities and concepts confirmed or introduced
| Entity / Concept | Type | New or updated | Notes |
|-----------------|------|---------------|-------|

## Artefacts and evidence
<links to photos, verbatim quotes, documents>

## Post-session actions
<outstanding actions>
```

---

### Raw session capture template (`_TEMPLATE-session-notes.md`)

```markdown
---
session: "<scope-slug>"
date: <YYYY-MM-DD>
start-time: <HH:MM>
end-time: <HH:MM>
location: <where — room, venue, video link>
facilitators:
  - <name (role)>
note-taker: <name>
---

# Session notes — <session>

> **Raw capture. Immutable after session closes.**
> Tag inline: `[EVIDENCE]` `[DECISION]` `[RISK]` `[VALIDATED]` `[INVALIDATED]` `[NEW-OQ]` `[ENTITY]` `[CONCEPT]`

## Attendance
- [ ] All must-have attendees present
- [ ] Missing: <names + impact>

## Block-by-block notes

### Block 1 — <topic> (<start>–<end>)
- <HH:MM> <quote or bullet>

## Decisions taken
| Decision | Owner | Notes |
|----------|-------|-------|

## Decisions deferred
| Decision | Reason | Owner | By when |
|----------|--------|-------|---------|

## New risks / assumptions
| Item | Type | Summary |
|------|------|---------|

## Entities / concepts to extract
| Entity / Concept | Type | Key facts |
|-----------------|------|-----------|

## Watch-list signals
Use the watch-list themes defined in `wiki/03_shared/cross-session-watch-list.md`.

| # | Theme | Seen? | Note |
|---|-------|-------|------|

## Verbatim quotes
- "…"

## Open questions to escalate
| # | Question | Who to ask | By when |
|---|---------|-----------|---------|
```

---

### Inter-session sync template (`_TEMPLATE-daily-sync.md`)

Optional — for engagements with consecutive sessions that benefit from a short between-sessions recalibration (e.g. multi-day workshops).

```markdown
---
date: <YYYY-MM-DD>
session-ref: <e.g. "Day 1" or "Sprint 2 interviews">
facilitators:
  - <name>
---

# Inter-session sync — <session-ref>

> ~20 minutes. Do not solve — surface.

## 1. Watch-list roll-call
| Session | Theme | Signal | New? |
|---------|-------|--------|------|

## 2. Contradictions
Log confirmed contradictions to `wiki/03_shared/workshop-insights.md` and flag on affected entity pages.

| Session A | Session B | Contradiction | Entity/concept affected |
|-----------|-----------|--------------|------------------------|

## 3. Next-session adjustments
| Change | Reason |
|--------|--------|

## 4. Clusters to add to inbox for next session
| Cluster | Scope | Files to collect | Who will drop them |
|---------|-------|-----------------|-------------------|
```

---

## General rules

1. **Cite everything.** Every claim in a query answer, outcome page, or entity page references its source.
2. **Never invent facts.** Unsupported claims carry `[ASSUMPTION]` or `[TO CONFIRM]`.
3. **Supersede, don't overwrite.** Preserve old values with `[SUPERSEDED YYYY-MM-DD by S-XXX: <replacement>]` for audit.
4. **`raw/` is immutable.** Files under `raw/` are written once and never modified. All working and derived files go in `workspace/`.
5. **A page must stand alone as text.** Visualisations enhance; they never replace.
6. **Always read `wiki/index.md` first** before any operation. It is the canonical navigation page.
7. **`/ingest` never reads raw files until the user has confirmed the cluster.** The selection step reads manifests only, regardless of how much material is staged.
8. **Scope expansion always pauses for user confirmation.** Never silently scaffold new scope folders — always use the CANDIDATE-file pattern, even at high confidence.
9. **`steps-completed` is required on every session page.** A missing step is a detectable gap, not a silent omission. `/lint` flags incomplete step lists.
10. **Problem before solution.** Use cases and core topics are problem spaces. When a stakeholder proposes a solution, log it as a candidate in `opportunity-tree.md` under the relevant opportunity — do not promote it to a requirement until an experiment validates it.
11. **Every assumption carries a product-risk type.** `value` · `usability` · `feasibility` · `viability`. Unclassified assumptions are not actionable.
