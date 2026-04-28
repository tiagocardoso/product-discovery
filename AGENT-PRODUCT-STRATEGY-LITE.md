# Agent Product Strategy — Lite

## What this is

Compact bootstrap turning a Claude Code session into a **persistent, compounding knowledge base** for product strategy and product marketing — vision, strategy, intelligence, narrative, go-to-market.

Four purposes: **Strategy** (theses, bets, moats, non-goals) · **Intelligence** (market, competitive, customer-voice) · **Narrative** (story, positioning, messaging, TL) · **Domain knowledge** (entities, concepts, relationships).

**Thesis-first.** Strategies are structured arguments (Rumelt default; P2W, Wardley alternatives). Cited theses, assumptions by strategic risk, bets with kill criteria. Brain dumps are **priors**, not evidence.

Wiki is a **compiled artifact**. **Research is active** — agent proposes, user approves; `/research` runs a four-level gated loop, wiki-first. **State is git** — commits replace snapshots.

**Use:** drop into empty folder, `/bootstrap`. Full: `AGENT-PRODUCT-STRATEGY.md`.

---

## Commands

- `/bootstrap` · `/ingest` · `/query <q>` · `/lint` (scoped) · `/status` · `/brief [board|external|marp]` · `/generate-image <ID>`.
- `/research <id>` — L1 always; gated L2/L3/L4. Variants: `extend`, `redo [from-L<n>]`, `"<free-form>"`.
- `/commit ["<msg>"]` · `/auto-commit <mode>`.

---

## Wiki layout

```
wiki/
  index.md · log.md
  00_foundation/      vision · mission · values · world-assumptions
  01_strategies/<slug>/
    overview · strategy-spine · pillars · anti-strategy · bets · moats
    findings/ theses · assumptions-and-risks · evidence-log · decision-log
              research/ · deliverables/
    research/ queue · active · open-questions · next-steps · checklist
  02_products/<slug>/ overview · product-docs/ · capabilities · positioning
                      market-intelligence · competition · strategy-alignment
                      findings/ · research/
  03_intelligence/
    market/         segments · trends · figures · analyst-views · regulatory · scenarios
    competition/    landscape · comparison-matrix · moves-playbook · <competitor>/
    customer-voice/ verbatim · case-study · reviews · survey · win-loss
    audiences/      cluster-NN-<slug>
  04_narrative/     core-narrative · positioning · messaging-pillars
                    category · value-propositions · thought-leadership/
  05_go-to-market/  gtm-motion · pricing-and-packaging · analyst-relations
  06_knowledge/     ontology · relationships · entities/ · concepts/ · queries/
  07_operations/    research/ · sources/ · queries/ · shared/
raw/ _inbox-index.md · inbox/ · brain-dumps/ · strategy-docs/ · product-docs/
     market/ · competitive/ · news/ · research-outputs/ · assets/
workspace/ image-opportunities · research-proposals/ · assets/images/ · brief-*
```

Optional (`moats`, `anti-strategy`, `thought-leadership`, `analyst-relations`) flagged `status: optional`.

---

## Core concepts

**Vocabulary.** *Strategy* = argued thesis on where-to-play/how-to-win. *Pillar* organises bets. *Bet* has hypothesis/owner/horizon/**kill criteria**. *Thesis* = cited claim. *Anti-goal* = non-pursuit. *World-assumption* = macro prior. *Moat* = Helmer 7-Powers. *Prior* = brain-dump belief; seeds but can't confirm.

**Framework** (chosen once): Rumelt (diagnosis · guiding policy · coherent actions) · P2W · Wardley.

**Inbox/clusters.** Raw in bounded clusters, each `_manifest.md`. Agent reads manifests until confirmed. Types: `brain-dump` · `strategy-doc` · `product-doc` · `analyst-report` · `white-paper` · `market-figures` · `news-pack` · `competitor-material` · `research-output` · `mixed` · `document-pack`. Brain-dumps → `[PRIOR: <slug>]`.

**Credibility:** `primary-neutral` · `primary-interested` · `secondary-neutral` · `secondary-interested`. `interested`-only caps at `medium`.

**Tiers:** Raw → Episodic (sources, reports) → Semantic (knowledge) → Procedural (ontology, foundation, shared). 3+ independent → `high`.

**Ontology seed.** Entities: people/orgs/analyst-firms/publications · competitor/product/capability/market-segment/trend/scenario/regulatory · strategy/pillar/bet/thesis/anti-goal/moat/world-assumption · value-prop/JTBD · narrative/positioning/messaging/category · customer-voice/win-loss · concept. Relationships: `owns`, `uses`, `depends-on`, `produces`, `consumes`, `contradicts`, `supersedes`, `serves`, `threatens`, `defends`, `enables`, `laddersTo`, `tested-by`, `cited-from`, `aligns-with`, `related-to`.

---

## Labels, status, confidence

- **Inline:** `[EVIDENCE]` · `[PRIOR]` · `[ASSUMPTION]` · `[THESIS]` · `[OPEN QUESTION]` · `[RISK]` · `[TO CONFIRM]` · `[CONTRADICTS R-XXX/S-YYY]` · `[SUPERSEDED YYYY-MM-DD by S-XXX]`.
- **Confidence:** `low` (1 source / priors-only) · `medium` (2 sources) · `high` (3+ independent). `primary-interested`-only caps at `medium`.
- **Status:** `not-started` · `in-progress` · `complete` · `blocked` · `superseded-by-<id>`. **Checklist:** ⬜🟡✅⛔🧊.
- **Visibility:** `internal` · `team` · `leadership-ready` · `board-ready` · `confidential`.
- **Strategic-risk:** `market` · `positioning` · `capability` · `execution` · `viability`.

---

## Common failure modes

Malformed manifest → flag · Duplicate query → `supersedes:` · Brain-dump claim → `[PRIOR]` · Ingest contradicts report → banner + suggested redo · Vendor-only number → `medium` cap · No non-goals ≥3 clusters → prompt · Unladdered messaging → flag · Loop-cap → partial · Assumption without risk-type → classify · World-assumption challenged → banner; if load-bearing, research.

---

## Research system

Four gated levels. L1 always. Work compounds.

| Level | Goal | Stop | Cost |
|-------|------|------|------|
| **L1 Orient** *(always)* | Wiki + raw, sub-qs, web sweep ~15–25, **scoping memo** | Memo written | 20–40 min |
| **L2 Validate** | Load-bearing ≥2 independent | Sub-qs ≥2 or unresolvable | +45–90 min |
| **L3 Deep** | Primary; credibility-weighted; paywalled PDFs; adversarial; cap 10 | Numerics primary; contradictions closed | +2–4 h |
| **L4 Exhaustive** | Thesis-grade; triangulate 3 ways; **extra confirmation** | No new challenge | Hours |

**Wiki-first every level.** Prefer wiki-held over refetched.

**Scoping memo:** question + sub-qs · holdings (cited) · L1 findings (cited) · synthesis · gaps · recommendation with named weak claims.

**Gates:** next-level plan + effort; user *approves/narrows/skips/stops*. Mid-level escalation allowed.

**Paywalled:** L3/L4 may pause for user PDF; else log gap.

**Archive:** citations → `raw/research-outputs/R-XXX/`.

**Reports** at `wiki/<scope>/findings/research/R-XXX-<slug>.md`. In place; levels appended; supersessions marked.

**Extend** → next level. **Redo** → `-redo-YYYY-MM-DD`; old superseded. Default L1.
**Suggested redo (auto):** in `/ingest`, contradiction at ≥ equal credibility (numeric/factual/structural) → queue. Same-direction = refresh.
**Staleness:** >6 mo figures · >12 mo competitor profiles · >24 mo deep theses → refresh.

---

## Git integration

State is git. No snapshots. Commits local, never auto-pushed.

`/commit ["<msg>"]` stages `wiki/`, `raw/`, `workspace/`, root configs. Message:

```
<type>: <summary>
<grouped changes>
Readiness: <%> | Sources: +N | Research: queue/in-flight/completed
```

`<type>` ∈ `bootstrap`·`ingest`·`research`·`lint`·`query`·`brief`·`manual`.

**`/auto-commit <mode>`:** `off` · `after-ingest` *(default)* · `after-research` · `after-every-command` · `daily`.

Briefs SHA-pinned; warn on drift.

---

## `/bootstrap`

1. **Capture** — org, mission, vision, strategies, products, competitors, segments, framework (default Rumelt), analysts, ICPs, auto-commit mode.
2. **Git init** + `.gitignore`.
3. **Folders** — full tree; optional folders flagged.
4. **Scope scaffolds** per known strategy/product/competitor/ICP.
5. **Inbox** empty `_inbox-index.md`; READMEs.
6. **Knowledge** — `ontology.md`, `relationships.md`, READMEs.
7. **Foundation** — vision, mission, values, `world-assumptions` (5–10 priors).
8. **Shared** — watch-list (5–10 themes), readiness, exec summary, top-questions, master logs, config, log, index.
9. **Narrative, GTM, workspace** empty templates.
10. **`CLAUDE.md`** (FM: `framework`, `auto-commit`, `commit-push: false`, `visibility-levels`, `raw-pdf-policy`) + **`README.md`**.
11. **Initial commit**.
12. **Confirm** — counts, placeholders, missing, next command.

---

## `/ingest`

Phased. Never reads raw until cluster confirmed.

**Phase 1** scan `_inbox-index.md`; filter ready/partial; ask.
**Phase 2** confirm per cluster: manifest, impact, deps.
**Phase 3** steps (tracked in source `steps-completed`):

- **A** Read files · **B** Source `S-XXX` · **C** `[PRIOR]` on brain-dumps · **D** Scope-expansion → `CANDIDATE-<type>-<slug>.md`, pause · **E** Knowledge extraction.
- **F Strategy.** Thesis · spine · pillars · bets · moats · theses · assumptions · evidence-log **first** · decisions · deliverables · OQs.
- **G Product.** Capabilities · positioning · competition · strategy-alignment.
- **H Intelligence.** Market · competition (moves) · customer-voice · audiences.
- **I Foundation.** Challenged world-assumption → banner; load-bearing → research.
- **J Narrative.** Messaging/positioning/TL angles.
- **K Contradictions** vs reports → banner + `[CONTRADICTS]` + suggested redo.
- **L** Propose research · **M** Propose TL · **N** Images · **O** Shared registers · **P** Anti-strategy prompt if ≥3 clusters empty · **Q** Indexes · **R** steps-completed · **S** Log.

**Phase 4** summary + commit if `after-ingest`.

---

## `/research`

**L1** always: decompose → wiki-first → web sweep → triangulate → scoping memo → archive → gate → commit.

**L2/L3/L4** on approval. Additive. L4 extra-confirmed. Caps → partial. Reports in place; supersessions marked; wiki updated.

`extend` · `redo [from-L<n>]` · auto-suggested-redo.

---

## `/query`

1. **Scope** — scope-specific, knowledge, or global. 3+ scopes → global.
2. **Overlap** — `supersedes:` or update in place.
3. **Research** — `wiki/index.md` first; scope min: overview, spine, pillars, theses, evidence-log, entities/concepts, sources. Global adds foundation + exec summary.
4. **Format** — markdown · table · Mermaid · Marp · matplotlib · PIL.
5. **Write/file** FM: `title`, `query`, `scope`, `format`, `date`, `status: draft`, `supersedes`, `visibility`. Body: Answer (cited) · Sources · Limitations · Follow-ons.
6. **Image opportunities** · **7. Crystallize** — promote to knowledge? Seed research?

---

## `/lint`

Scopes: full · `<slug>` · knowledge · intelligence · narrative · gtm · research · git.

**Knowledge:** orphans · unsourced relationships · upgradable confidence · duplicates.
**Strategy:** thesis <2 sources · bet without kill criteria · assumption missing risk-type · empty anti-strategy ≥3 clusters · moats unmapped · high-risk unmitigated.
**Product:** missing strategy-alignment · uncited capabilities.
**Intelligence:** moves-log >90d · uncited figures · scenario without indicators.
**Narrative:** unladdered messaging · stale positioning · TL suggested >30d · ungrounded TL.
**GTM:** motion without rationale · pricing unlinked · analyst-relations >90d.
**Research:** past-staleness · loop-cap without partial · contradicted without queued redo · queue idle >30d.
**Git:** `.gitignore` missing · drift nudge · auto-commit-off >7d.

Auto-fix safe; list ambiguous; log.

---

## Reporting

- **`/status`** — strategies/readiness · products · intelligence freshness · research counts · P0 questions · `git log -10` · drift · workspace.
- **`/brief`** — default = `leadership-ready` + `board-ready`. **`board`**: strategy-on-a-page, moats, readiness, top-3 risks, bets+kill. **`external`**: narrative, positioning, published TL. `marp` for slides. SHA-pinned.

---

## Images & diagrams

Generate only when it aids understanding. Alt-text + text equivalent always.

Mermaid (`flowchart`, `quadrantChart`, `timeline`, `classDiagram`) · matplotlib/PIL in `tools/` · `/generate-image` on-demand. Flag: spine · positioning grid · capability map · scenario tree · narrative arc · pricing · GTM motion · persona. Don't flag tables or already-diagrammed.

Append `## IMG-NNN` (ID, Status, Page, Section, Type, Rationale, Prompt). Provider: `OPENAI_API_KEY` → `GEMINI_API_KEY`. 1792×1024 or 1024×1024.

---

## Page templates (compact)

All FM YAML; every page has `title`, `last-updated`, `status`.

- **`overview.md`** — aspiration · thesis · scope · products · segments · horizon · world-assumptions.
- **`strategy-spine.md`** (Rumelt) — Diagnosis · Guiding policy · Coherent actions · What rests on · What would break it.
- **`pillars.md`** — Pillar · Rationale · Linked bets · Evidence.
- **`anti-strategy.md`** — Segments/capabilities/games/channels we won't pursue.
- **`bets-and-initiatives.md`** — BET · Pillar · Hypothesis · Owner · Horizon · Risk-type · Status · **Kill criteria**.
- **`moats.md`** — 7 Powers · Present · Evidence · Confidence.
- **`theses.md`** — Thesis · Confidence · Sources (≥2) · Risk-type · Tested-by · Status.
- **`assumptions-and-risks.md`** — Claim · Risk-type · Severity · Status · Source · Mitigation.
- **`evidence-log.md`** — Date · Source · Quote · Scope-ref.
- **Research report** (FM `research-id`, `status`, `supersedes`, `level-reached`, `steps-completed`) — Question + sub-qs · Recommendation · L1 memo · L2/L3/L4 appended.
- **Queue item** (FM `queue-id`, `status`, `priority`, `scope`) — Question · Rationale · Redo-trigger.
- **`positioning.md`** — Dunford template · Evidence · Rejected alternatives.
- **`messaging-pillars.md`** — Pillar · **LaddersTo** · Proof · Audience.
- **`world-assumptions.md`** — Assumption · Confidence · Sources · Contested.
- **Competitor profile** — Snapshot · Strategy read · Capabilities · Moves · Threat.
- **Audience cluster** (FM `type`, `serves-strategies`) — JTBD · Firmographics · Buying · Pains · Needs.
- **Cluster manifest** (FM `cluster`, `scope`, `type`, `credibility`, `priority`, `status`) — Files · Impact.
- **Source** (FM `source-id`, `type`, `credibility`, `url`, `accessed`) — Summary · Claims · Figures · Quotes.
- **TL suggestion** (FM `laddersTo-strategy`, `supporting-evidence`) — Angle · Why now · Evidence · CTA.

---

## General rules

1. **Cite everything.** 2. **Never invent.** 3. **Brain dumps are priors.** 4. **Supersede, don't overwrite.** 5. **`raw/` immutable.** 6. **Page stands alone as text.** 7. **Read `wiki/index.md` first.** 8. **`/ingest` never reads raw until confirmed.** 9. **Scope expansion pauses** via `CANDIDATE-<slug>.md`. 10. **Every assumption gets risk-type.** 11. **Every bet gets kill criteria.** 12. **Every messaging pillar ladders.** 13. **TL grounded** (thesis + VoC + market). 14. **Research gated.** L1 always; L4 extra-confirmed. 15. **Wiki-first every research level.** 16. **Credibility tagged.** 17. **Auto-commits never push.** 18. **Contradictions → suggested redos.** 19. **World-assumptions watched.** 20. **Anti-strategy prompted** after 3+ clusters. 21. **Framework chosen once.**

---

## Extending this Lite file

- **Watch-list** · **ontology** — declare with rationale.
- **Framework** — swap Rumelt for P2W/Wardley.
- **Deliverables** — replace defaults.
- **Audience dimensions** · **Risk types** — adapt.
- **Visibility tiers** — drop `confidential` if overkill.
- **Research levels** — tighten caps, staleness.
- **Auto-commit** — `off` for exploratory phases.

Keep edits terse, load-bearing, and cite-everything.
