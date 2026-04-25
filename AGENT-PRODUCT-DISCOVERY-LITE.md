# Agent Product Discovery — Lite

## What this is

Compact bootstrap that turns a Claude Code session into a **persistent, compounding knowledge base** for multi-stakeholder engagements — discovery, consultancy, assessments, research.

Two purposes: (1) **Discovery tracking** — use cases, sessions, decisions, risks, readiness. (2) **Domain knowledge** — entities, concepts, relationships.

**Problem-first.** Use cases and core topics are **problem spaces**, not pre-decided solutions. Each carries a measurable target outcome, an opportunity-solution tree, assumptions classified by product risk (value/usability/feasibility/viability), and experiments testing the riskiest.

The wiki is a **compiled artifact**, not a retrieval index. New sources integrate: entities update, claims strengthen or get challenged, knowledge promotes through tiers. Contradictions flagged; syntheses persist.

**Use:** drop into an empty folder, open in Claude Code, `/bootstrap`. After bootstrap, `CLAUDE.md` takes over.

**Lite vs full.** Generic starting point; all commands, layout, core behaviours preserved. Add your own bias. Full opinionated version: `AGENT-PRODUCT-DISCOVERY.md`.

---

## Commands

- `/bootstrap` — once at start; scaffolds the wiki.
- `/ingest` — new material; shows clusters, you pick.
- `/query <question>` — ask anything; produces a filed, cited answer.
- `/lint` (or `/lint <slug>`, `/lint knowledge`, `/lint discovery`) — health-check.
- `/status` — chat-only: readiness, blockers, recent log.
- `/snapshot` — point-in-time state record.
- `/brief` (or `/brief marp`) — compile `visibility: client-ready` pages.
- `/generate-image <ID>` — render a pending image opportunity.

---

## Wiki layout

```
wiki/
  index.md · log.md
  01_use-cases/<uc-slug>/       (scope root; same shape for 02_core-topics/<slug>/)
    overview.md · discovery-summary.md · opportunity-tree.md
    findings/   insights · assumptions-and-risks · experiments
                dependencies · decision-log · evidence-log
                deliverables/ (client-facing; adapt)
    discovery/  prep · checklist · open-questions
                next-steps · sessions/README.md
    queries/README.md
  03_shared/   executive-summary · discovery-readiness · top-open-questions
               project-context · participants-and-stakeholders
               cross-session-watch-list · workshop-insights
               master-{decision,risks,assumptions}-log
               open-questions-register · snapshots/
  04_sources/README.md · 05_queries/README.md
  06_knowledge/   README · ontology · relationships
                  entities/{people,systems,processes,organisations,document-types}/
                  concepts/ · queries/README.md
  07_personas/            clusters; README + page per cluster
raw/
  _inbox-index.md         cluster index
  inbox/<cluster>/        drop zone; _manifest + files
  sessions/<session>/     live capture (optional)
  background/<cluster>/   prior-context (optional)
  assets/
workspace/  image-opportunities.md · assets/images/ · brief-YYYY-MM-DD.md
```

No live sessions → `raw/sessions/` empty. Adapt session/workshop/onsite vocabulary.

---

## Core concepts

**Vocabulary.** *Use case* = a problem space (broader than a single user scenario). *Core topic* = a shared problem space several use cases depend on. *Opportunity* = unmet user need, pain, or desire (Torres) — not a feature, not a market opportunity.

**Discovery loop.** `Problem + Target outcome → Opportunities → Solutions → Experiments → Evidence → Insights → Validated/invalidated assumptions → Decisions → Deliverables`. Evidence lands somewhere; insights link to opportunities; opportunities drive experiments; experiments sharpen assumptions.

**Inbox and clusters.** Raw material arrives in **clusters** — bounded file sets processed in one `/ingest`. Each has `_manifest.md`. The agent reads manifests to build a menu; never opens raw files until you confirm. Types: `session-notes` · `transcript` · `document-pack` · `data-export` · `mixed` · `background`. `raw/_inbox-index.md` is auto-maintained (#, Cluster, Display name, Scope, Type, Size, Priority, Status, Added, Depends on).

**Consolidation tiers.** Raw (immutable) → Episodic (`04_sources/`, session pages) → Semantic (`06_knowledge/entities/`, `concepts/`) → Procedural (`ontology.md`, `03_shared/`). Seen once = episodic; 3+ independent sources → semantic, `confidence: high`.

**Ontology** (`06_knowledge/ontology.md`). Defaults:
- Entities: `person`, `system`, `process`, `organisation`, `document-type`, `concept`.
- Relationships: `owns`, `manages`, `uses`, `depends-on`, `produces`, `consumes`, `contradicts`, `supersedes`, `caused-by`, `mitigated-by`, `related-to`.

Add domain-specific types deliberately; update the ontology when you do.

---

## Labels, status, confidence

- **Inline:** `[EVIDENCE]` · `[ASSUMPTION]` · `[OPEN QUESTION]` · `[RISK]` · `[TO CONFIRM]` · `[SUPERSEDED YYYY-MM-DD by S-XXX: <replacement>]`.
- **Confidence:** `low` (1 source/inferred) · `medium` (2 sources or 1 session) · `high` (3+ independent or session-confirmed).
- **Page status:** `not-started` · `in-progress` · `complete` · `blocked`. **Checklist:** ⬜ missing · 🟡 partial · ✅ confirmed · ⛔ blocked · 🧊 deferred.
- **Visibility** (outcome/persona/shared; drives `/brief`): `internal` · `team` · `client-ready`. **Evidence-confidence** (deliverables, summaries): **lowest** confidence of any claim on the page.
- **Product-risk types** (every assumption and experiment): `value` · `usability` · `feasibility` · `viability` (legal/regulatory/economic/ethical/brand). Coverage gaps predict downstream surprise; surface on `discovery-summary.md`.

---

## Common failure modes

- Manifest missing/malformed → read what's parseable, flag gaps, confirm.
- Query duplicates existing → `supersedes:`; mark old `superseded`.
- Stakeholder proposes solution before the problem is understood → log as candidate under an opportunity; don't promote until validated.
- Many verbatim quotes on a theme → promote 2+ to a named insight.
- Assumption without risk type → classify value/usability/feasibility/viability.

---

## `/bootstrap`

1. **Capture context** — project, client, domain (one sentence), known use cases/core topics, session dates.
2. **Folder structure** — every folder in the layout. Each scope → root pages + `findings/`, `discovery/`, `queries/`. Each known session → `raw/sessions/<slug>/` with blank manifest + notes template.
3. **Inbox** — `raw/_inbox-index.md` empty; `raw/inbox/README.md` drop-zone.
4. **Knowledge layer** — `06_knowledge/README.md`, `ontology.md` (defaults + domain-specific), `relationships.md`, READMEs in entity subfolders and `concepts/`.
5. **Shared pages** — `project-context.md`; `cross-session-watch-list.md` seeded with 5–10 domain-tailored themes (e.g. "manual workaround as system-of-record", "SPOF expert"); `discovery-readiness.md` (row per scope); `executive-summary.md` shell; `top-open-questions.md` empty register; `wiki/log.md` first entry; `wiki/index.md` master nav.
6. **Session templates** — `_TEMPLATE-session-notes.md` + `_TEMPLATE-daily-sync.md` (consecutive-day).
7. **Persona + workspace** — `07_personas/README.md`, `workspace/image-opportunities.md`, `workspace/assets/images/`, `03_shared/snapshots/`.
8. **Root `README.md`** + **`CLAUDE.md`** (operating config, engagement-specific overrides, pointer to this file).
9. **Confirm** — tree (file counts), scopes scaffolded vs placeholder, missing fields, next command. Don't skip.

---

## `/ingest`

Phased. Agent never reads raw files until a cluster is confirmed.

**Phase 1 — Scan.** Read `_inbox-index.md` only. If missing/empty, scan manifests and write it. Filter `ready`/`partial`. Present selection table; flag unmet deps. Ask: *"Which clusters now? Numbers, `all`, or `none`."*

**Phase 2 — Confirm.** Per selected cluster: read manifest, report what will be ingested and which pages change. Warn on unmet deps. Cluster-by-cluster.

**Phase 3 — Process.** Run in order; track in session page's `steps-completed` (missing steps are `/lint` gaps).

- **A** — Read raw files in manifest. Nothing outside.
- **B** — Source note `04_sources/YYYY-MM-DD-<slug>.md` (S-XXX). Session clusters also write `wiki/<scope>/discovery/sessions/YYYY-MM-DD-session-notes.md`.
- **C — Scope-expansion gate.** Scan for new scopes. **Never silently scaffold.** If detected: `03_shared/CANDIDATE-<slug>.md` with evidence + proposed structure; pause and ask. One candidate per scope.
- **D — Knowledge extraction.** Entities, concepts, typed relationships per ontology. Update `06_knowledge/`; upgrade confidence; mark superseded; add back/forward links between `overview.md`, `evidence-log.md`, and entity/concept pages. Unclear type → closest + note; don't invent without ontology update.
- **E — Propagate.** Verbatim quotes → `evidence-log.md` **first** (anchors everything). Then: rewrite `discovery-summary.md`; update `opportunity-tree.md`; promote 2+-source patterns to `insights.md`; update `assumptions-and-risks.md` + `experiments.md`; close `[TO CONFIRM]` and refresh `evidence-confidence` in `deliverables/`; log decisions. Discovery: `open-questions.md`, `next-steps.md`, `discovery-checklist.md` (flip + recompute). Shared: master registers, `workshop-insights.md`, `top-open-questions.md`, `discovery-readiness.md`.
- **F — Personas.** Update matching `07_personas/` cluster or create one (medium+). Cross-link via `persona-cluster`.
- **G — Image opportunities** (see Images).
- **H — Indexes.** Row in `wiki/index.md`; session README row; cluster `status: ingested` + `ingested:` date; update `_inbox-index.md`.
- **I — `steps-completed`** in session FM.
- **J — Log** (cluster, files, pages, entity/concept count, personas, steps).

**Phase 4 — Summary.** Clusters ingested, new/updated pages, new entities/concepts, remaining clusters + priorities.

---

## `/query`

If no question, ask.

1. **Scope.** Route to relevant `queries/` folder: scope-specific, `06_knowledge/`, or `05_queries/` (global). Default global when unsure; 3+ scopes → global.
2. **Overlap.** Scan for existing query on same ground. Refinement → `supersedes:`; mark old `superseded`. Identical → update in place. Superseded/`promoted: true` stay indexed with strikethrough.
3. **Research.** `wiki/index.md` first. Then scope min: `overview.md`, `discovery-summary.md`, `opportunity-tree.md`, `insights.md`, `open-questions.md`, `evidence-log.md`, entity/concept pages, `04_sources/README.md`. Global also reads `03_shared/executive-summary.md`. Cite: `[Source: page.md]` / `[Source: S-XXX]`.
4. **Format.** Markdown · table · Mermaid · Marp · matplotlib · PIL · multi-part.
5. **Write and file.** FM: `title`, `query`, `scope`, `scope-ref`, `format`, `date`, `status: draft`, `supersedes: ""`, `promoted: false`. Body: Answer (cited), Sources consulted, Limitations, Follow-ons. File `YYYY-MM-DD-<slug>.md`. Index + log.
6. **Image opportunities** on the query page.
7. **Crystallize.** Ask: *promote facts/concepts to `06_knowledge/`?* If yes: update entity/concept pages, add query as source, add `relationships.md` entries for new typed relationships.

---

## `/lint`

Scopes: `/lint` · `/lint <slug>` · `/lint knowledge` · `/lint discovery`.

**Knowledge:** orphan entities · concept mentioned but no page → create · unsourced relationship · upgradable `low` confidence → upgrade · stale supersession chains · contradictions without supersession · source notes without extractions · duplicate concepts → merge · type missing from ontology → add.

**Discovery:** `overview.md` missing problem/target outcome/HMW · opportunities without solutions after 2+ sessions · solutions without experiments · assumption missing risk-type · product-risk coverage gap · 3+ same-theme evidence without insight · experiment running >2 weeks without result · persona without JTBD · `[TO CONFIRM]` answered in session · OQ resolved elsewhere · decision without owner/date · high-severity risk without mitigation · checklist/readiness out of sync · index rows missing/stale · summary `last-updated` older than latest session · session page missing/empty `steps-completed` (or missing step G) · deliverable/summary without `visibility`/`evidence-confidence` · persona ↔ entity link broken.

**Report and fix.** Per-section counts. Auto-fix immediately; list ambiguous items with file paths for review. Log.

---

## Reporting

- **`/status`** — chat-only. Reads index header, `discovery-readiness.md`, P0 rows of `top-open-questions.md`, last 5 log entries. Responds: ingested count, phases done, per-scope readiness, P0 blockers, recent log, pending workspace items.
- **`/snapshot`** — `03_shared/snapshots/YYYY-MM-DD-snapshot.md`: readiness, OQ/risk/decision counts, new sources, 2–4 sentence narrative, cross-scope blockers. Row in `wiki/index.md`. Log.
- **`/brief`** — compile `visibility: client-ready` pages → `workspace/brief-YYYY-MM-DD.md` (or `-slides.md` for Marp). Cover · readiness · per-scope outcomes · personas · cross-cutting findings · next steps. Marp: fenced separators, ≤3 bullets/slide, `<!-- fit -->` large headings. Log.

---

## Images & diagrams

Generate a visual only when it meaningfully aids understanding. Every image has alt-text + text equivalent — pages stand alone as text.

- **Mermaid** — fenced blocks. `flowchart TD`, `graph LR`, `sequenceDiagram`, `classDiagram`.
- **Matplotlib / PIL** — scripts in `tools/`, output `workspace/assets/`.
- **External image API** (`/generate-image`) — architectural diagrams, swimlanes, art-directed visuals. On-demand.

**Opportunity evaluation.** After creating/substantially updating a page, flag if it contains a multi-step workflow, named-component architecture, role/persona map, data model, timeline, or 2+-option comparison. **Don't** flag log/register tables, simple Q&A, or pages already with covering Mermaid. Strong additions only — no decoration.

Append to `workspace/image-opportunities.md` as `## IMG-NNN`: ID, Status (pending/generated/embedded), Wiki page, Page section, Image type (flowchart/swimlane/architecture/persona-map/er-diagram/timeline/comparison-matrix), Rationale, Prompt.

**`/generate-image <ID>`.** Locate; if not pending, confirm. No ID → list pending, ask. Provider: `OPENAI_API_KEY` (`gpt-image-1`) → `GEMINI_API_KEY` (Imagen). Size 1792×1024 flowcharts/architectures; 1024×1024 persona-maps/matrices. Save `workspace/assets/images/<ID>.png`. Embed under the named section. Set `Status: embedded`. Log.

---

## Page templates (compact)

All FM is YAML. Every page: `title`, `last-updated`, `status`. Dates `YYYY-MM-DD`. Adapt as needed.

- **`overview.md`** (+ `scope`, `slug`, `confidence`) — Problem statement · Target outcome (table: dimension/current/target/measurement) · HMW · Trigger · Current workflow (numbered; unconfirmed `[ASSUMPTION]`) · Inputs · Outputs · Key personas · Key entities · Related concepts · Related scopes · `[TO CONFIRM]` · Navigation.
- **`discovery-summary.md`** (+ `evidence-confidence`, `visibility`, `last-session`) — Current state (paragraph) · What changed · Readiness snapshot · Top blockers · Product-risk coverage · Known well · Still assumed · Next action · Related pages.
- **`opportunity-tree.md`** — Opportunities (OPP-NNN, user-framed, Evidence, Reach, Value, Confidence, Status) · Candidate solutions (SOL-NNN, Addresses, Solution, Hypothesis "We believe … will … by …", Complexity S/M/L/XL, Status) · Experiments in flight (pointer; canonical in `experiments.md`) · Parked/rejected.
- **`findings/` tables.** `insights.md` → I-NNN, Insight, Evidence (≥2), Confidence, So what? · `experiments.md` → EXP-NNN, Tests, Risk type, Hypothesis, Method, Success criteria, Status, Result, Implication · `assumptions-and-risks.md` → ID, Claim, Type, Risk-type, Severity, Status, Source, Mitigation · `evidence-log.md` → E-NNN, Date, Source, Quote, Scope-ref, Notes · `decision-log.md`/`dependencies.md` → ID, item, Owner, Date, Rationale, Related.
- **`discovery/discovery-checklist.md`** — Readiness overview (%s, blocked, deferred, overall) · Top-5 blockers · P0/P1/P2 tables (#, Item, Type, Status, Who to ask, Evidence, Refs). `open-questions.md`/`next-steps.md` → ID, item, owner, due, status, links.
- **Entity** (FM `entity-type`, `confidence`, `sources`, `last-confirmed`) — Description · Attributes (superseded preserved) · Relationships · Appearances · Open questions · Change log. **Concept** (+ `domain-area`) — Definition · Why it matters · Related concepts · Entities involved · Appearances · Evidence · Open questions.
- **Ontology** — Entity types · Relationship types · Concept hierarchy · Domain-specific additions. **Relationships register** — #, Source, Relationship, Target, Confidence, Source, Notes.
- **Persona cluster** (FM `persona-cluster`, `confidence`, `use-cases`, `visibility`) — JTBD (When…, I want to…, so I can…) + functional/emotional/social · Who · Named individuals · Day in life · Goals · Frustrations · Needs · Design principle · Profile dimensions · Appearances · Open questions · Evidence trail.
- **Cluster manifest** (FM `cluster`, `display-name`, `scope`, `type`, `size`, `priority` p0–p3, `status` ready/partial/pending-files/ingested, `added`, `ingested`, `depends-on`) — Files · Expected impact · Notes.
- **Session notes** (FM `session`, `date`, `sources`, `visibility`, `steps-completed`) — Attendance · Key findings · Decisions · Validated/invalidated · New OQs · New risks · Watch-list signals · Entities/concepts · Artefacts · Post-session actions.
- **Raw session capture** — Attendance · Block-by-block notes (timestamped) · Decisions taken/deferred · Risks · Entities/concepts · Watch-list · Verbatim quotes · OQs. Inline tags: `[EVIDENCE]` `[DECISION]` `[RISK]` `[VALIDATED]` `[INVALIDATED]` `[NEW-OQ]` `[ENTITY]` `[CONCEPT]`. Immutable.
- **Inter-session sync** (optional, ~20 min) — Watch-list roll-call · Contradictions · Adjustments · Clusters to add.

---

## General rules

1. **Cite everything.**
2. **Never invent facts.** Unsupported → `[ASSUMPTION]` / `[TO CONFIRM]`.
3. **Supersede, don't overwrite.** `[SUPERSEDED YYYY-MM-DD by S-XXX: <replacement>]`.
4. **`raw/` is immutable.** Derived work goes in `workspace/`.
5. **A page stands alone as text.** Visuals enhance, never replace.
6. **Always read `wiki/index.md` first.**
7. **`/ingest` never reads raw files until a cluster is confirmed.**
8. **Scope expansion always pauses for user confirmation.** Use `CANDIDATE-<slug>.md` even at high confidence.
9. **`steps-completed` required on every session page.**
10. **Problem before solution.** Stakeholder solutions are candidates under an opportunity, not requirements, until validated.
11. **Every assumption carries a product-risk type.** Unclassified = not actionable.

---

## Extending this Lite file

Tune by adding:
- **Watch-list themes** (seed in `/bootstrap` Step 5).
- **Entity / relationship types** beyond defaults — declare in `ontology.md` with rationale.
- **Deliverable pages** under `findings/deliverables/` — replace defaults with what your client expects.
- **Persona dimensions** — adapt to your research framework (not every engagement is UX).
- **Risk framework** — replace SVPG's four types if they don't fit; keep consistent across assumptions, experiments, summary coverage.
- **Visibility tiers** — replace `internal`/`team`/`client-ready` if needed; update `/brief`.
- **Prior art** — bolt on references (Torres, Cagan, JTBD, Design Thinking).

Keep edits terse, load-bearing, cite-everything. Promote reusable patterns to your base file.
