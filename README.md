# Vibe — Agent Bootstrap Kits

Bootstrap kits for turning any Claude Code session into a **persistent, compounding knowledge base**. Two patterns, sharing the same DNA, tuned to different kinds of work.

| Pattern | For | Bootstrap files | Deep-dive README |
|---------|-----|-----------------|------------------|
| **Product Discovery** | Consultancy sprints, discovery workshops, technical assessments, multi-stakeholder research. Problem-space exploration driven by primary research (sessions, interviews, workshops). | `AGENT-PRODUCT-DISCOVERY.md` · `AGENT-PRODUCT-DISCOVERY-LITE.md` · `AGENT-PRODUCT-DISCOVERY-GIST.md` | [README-DISCOVERY.md](./README-DISCOVERY.md) |
| **Product Strategy** | Vision, strategy, and product marketing. Thesis-driven argument built from secondary research (analyst reports, market data, competitor materials) plus the user's own convictions, with an active agent-driven research loop. | `AGENT-PRODUCT-STRATEGY.md` · `AGENT-PRODUCT-STRATEGY-LITE.md` · `AGENT-PRODUCT-STRATEGY-GIST.md` | [README-STRATEGY.md](./README-STRATEGY.md) |

---

## Shared DNA

Both patterns treat the wiki as a **compiled artifact**, not a retrieval index. Every new source is digested, integrated, and cross-linked. Pages update as evidence strengthens or challenges them. Contradictions are made explicit. The wiki gets denser and sharper with every ingested source.

The commitments both patterns share:

- **Evidence is cited.** Every claim traces to a source. No free-floating assertions.
- **Clusters are the unit of ingestion.** Raw material arrives in bounded sets with a manifest; the agent never opens raw files until the operator confirms a cluster.
- **Knowledge promotes through tiers.** Raw → Episodic → Semantic → Procedural. A fact seen once is episodic; confirmed across independent sources, it earns a place in the semantic layer with rising confidence.
- **Contradictions are flagged and superseded.** Old claims are never overwritten — they're marked superseded with a date and a pointer to the replacement.
- **Scope expansion is a change-control event.** New use cases, strategies, products, or competitors never get scaffolded silently — the agent surfaces candidates and waits for human confirmation.
- **Confidence and visibility are explicit on every consequential page.** Both answer different questions: *how sure are we?* and *who can see this?*
- **A page must stand alone as text.** Images enhance; they never replace.
- **`/lint` is the immune system.** Regular linting catches orphans, unsourced claims, stale pages, and decay before they compound.

---

## What's different

| Axis | Discovery | Strategy |
|------|-----------|----------|
| **Unit of work** | Use case = *problem space* to explore | Strategy = *argued thesis* about where to play and how to win |
| **Primary evidence** | Verbatim session quotes, workshop artefacts, interview notes | Cited analyst figures, market data, competitor materials, customer voice |
| **Central spine per scope** | Opportunity-solution tree (Torres) | Strategy spine — Rumelt's kernel (default), Playing to Win, or Wardley |
| **Risk framework** | Cagan's four (value · usability · feasibility · viability) | Strategic (market · positioning · capability · execution · viability) |
| **Research model** | Passive — evidence captured as it arrives | **Active** — agent proposes research; user approves; four-level gated deep-research loop (L1 always, L2/L3/L4 on approval) |
| **User's own priors** | Not a distinct concept | Brain dumps are first-class input *as priors*, not evidence — they seed theses but cannot alone confirm |
| **Product marketing / narrative** | Not covered | First-class: core narrative, positioning, messaging pillars, category, value propositions, thought leadership |
| **State mechanism** | `/snapshot` — point-in-time markdown files in the wiki | **Git** — `/commit` and `/auto-commit` replace snapshots; briefs are SHA-pinned |
| **Scope types** | Use cases + core topics | Strategies + products + competitors + market + foundation + narrative + GTM |
| **Visibility tiers** | `internal` · `team` · `client-ready` | `internal` · `team` · `leadership-ready` · `board-ready` · `confidential` |

Both patterns also ship with `/bootstrap`, `/ingest`, `/query`, `/lint`, `/status`, `/brief`, and `/generate-image`. Strategy adds `/research` (plus `extend` / `redo` / free-form), `/commit`, and `/auto-commit`.

---

## Three variants per pattern

Each pattern ships in three levels of prescriptiveness. Pick the one that matches how much room you want to give the agent.

| Variant | Stance | When to use |
|---------|--------|-------------|
| **Full** (~60–90k chars) | **Prescriptive** — complete templates, inline examples, failure-mode tables, explicit per-page structure, detailed command steps, full general-rules block | Maximum out-of-the-box scaffolding, cross-engagement consistency, or when coordinating multiple engagements that must look alike |
| **Lite** (~1,980 words — same target both patterns) | **Lean** — every command, layout, core behaviour preserved; verbose templates trimmed; compact table-shape summary per page type | Clean base to layer your own bias on top — domain conventions, custom deliverables, adapted frameworks, engagement-specific extensions |
| **Gist** (~1,980 words discovery / ~3,700 words strategy, prose-only) | **Principles-only** — explains the *why* and the invariants; lets the agent derive the *how*. No folder tree, no templates, no command enumeration | When you trust the agent to make concrete choices and want the wiki to mould to the engagement rather than the other way around |

### Why Gist often wins

Prescriptive files encode many small decisions — folder numbering, exact filenames, specific frontmatter fields, a precise lint list. Some of those decisions are arbitrary: an equally good wiki could have a different folder scheme or different file names and still satisfy every invariant that matters. As agents get more capable, principles-only files often produce a better-fitting wiki than prescriptive ones, because the agent can shape the structure to the actual work rather than contort itself to fit a template.

Prescriptive versions are still the right call for regulated/audit-pinned deliverables, for less-capable agents needing more guardrails, or when multiple engagements must look identical. Outside those cases, Gist is often enough — and sometimes better.

---

## Quick start

1. Create an empty folder for your engagement.
2. Pick a pattern (**Discovery** or **Strategy**) and a variant (**Full**, **Lite**, or **Gist**).
3. Copy that one bootstrap file into your folder.
4. Open the folder in Claude Code.
5. Run `/bootstrap`.

The agent asks a handful of context questions, scaffolds the wiki, writes a `CLAUDE.md` that takes over as ongoing operating config, and reports what it created.

After bootstrap, the bootstrap file has done its job. You can delete it, archive it, or leave it as reference.

See [README-DISCOVERY.md](./README-DISCOVERY.md) or [README-STRATEGY.md](./README-STRATEGY.md) for pattern-specific setup and typical workflows.

---

## Lifecycle and evolution

- Bootstrap files are **bootstrap-only** tools. Once `/bootstrap` has run, the active `CLAUDE.md` inside the engagement is the operating config.
- Improvements to the pattern should be made **here first**, in the relevant bootstrap file, and then reflected in future engagements. Don't edit the pattern file from inside a running engagement.
- Individual engagements can override or extend any behaviour in their own `CLAUDE.md` without touching the bootstrap.
- Prescriptive learnings (new fields, new lint checks, new cluster types) belong in Full and Lite. Conceptual learnings (a new invariant, a better way to frame a layer) belong in Gist — and often propagate down into Full and Lite afterwards.
- Keep changes in the spirit of each file: terse and load-bearing in all three, prescriptive in Full, compact in Lite, principles-only in Gist.

---

## Contributing improvements back

If you run an engagement and discover:

- A failure mode the agent should handle better
- A template field that was consistently empty or consistently missing
- A command phase that needed a manual workaround
- A new cluster type, entity type, or visibility level worth promoting

…update the appropriate variant in this repo so the next engagement benefits.

---

## License and usage

These are prompt/pattern files, not software. Drop them into your own engagements, adapt them, fork them. The only hard requirement is that they're used with a capable coding agent — Claude Code is the reference target.
