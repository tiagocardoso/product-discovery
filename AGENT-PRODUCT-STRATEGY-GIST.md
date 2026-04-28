# Agent Product Strategy — Gist

## The idea

A product strategy and product-marketing practice — a vision to argue, a handful of strategies to defend, products to position, competitors to watch, markets to read, narrative to tell — produces a flood of raw material: brain dumps, memos, analyst reports, white papers, news, competitor materials, market figures, and research outputs. The usual pattern is that it scatters across documents, chat threads, and slide decks, and by month three nobody can answer "what is our strategy, and what is it built on?" with a cited sentence.

This file describes a different approach. Treat the collected strategic thinking as a wiki that is *compiled*, not *retrieved*. Every new source is digested, integrated, and cross-linked. Pages update as evidence strengthens or challenges them. Contradictions are made explicit. The wiki gets denser and sharper with every ingested source, and by the end it is simultaneously a leadership-ready argument and a reusable map of the domain, the market, and the narrative.

The design goal is that a colleague joining cold on month six can read the wiki and understand the strategy, the evidence it rests on, and the open questions that threaten it, without asking a single question of anyone.

## Four layers in parallel

A strategy wiki run this way carries four complementary layers.

The first is *strategy*: the argued theses about where to play and how to win, the pillars that organise them, the bets beneath those pillars, the moats that protect them, and the non-goals that sharpen them. This layer is the argument the organisation is making about its future.

The second is *intelligence*: the market, the competitors, the customers, and the regulatory and technological weather the strategy is reacting to. This is where the outside world enters the wiki and gets interpreted.

The third is *narrative*: the story the strategy tells externally — the core narrative, positioning, messaging pillars, category definition, value propositions, and the thought-leadership articles that express the thesis to the world. Narrative without strategy is marketing theatre; strategy without narrative is a private memo. Keeping both in the same wiki forces them to speak to each other.

The fourth is *domain knowledge*: the entities, concepts, and typed relationships that exist in the subject matter regardless of the current strategy. This layer is the most durable. Strategies change; a competitor profile or a capability definition survives across multiple strategic cycles.

The four layers enrich each other. Intelligence feeds strategy; strategy shapes narrative; narrative tests strategy against the world; domain knowledge is the shared vocabulary that lets the other three be consistent. All four grow from the same raw material.

## Strategy as a structured argument

The most important commitment is this: a strategy is an *argument*, not a wish. It has a diagnosis of the situation, a guiding policy for responding to it, and a set of coherent actions that put the policy into practice. You can call those three parts by other names — Rumelt's kernel, Lafley and Martin's cascade of choices, Wardley's mapping — and the choice of framework matters less than using one consistently so that every strategy in the wiki is argued in the same shape.

Whatever frame is chosen, every load-bearing claim in the strategy earns its place by citing evidence. A thesis with one source is weaker than a thesis with three independent sources. A bet without a pre-committed kill criterion is a vibe. A pillar without bets beneath it is aspiration. A strategy without explicit non-goals has not made trade-offs yet — it has only made promises. The wiki makes each of these failures visible by refusing to let pages look finished when they are not.

## Priors and evidence are not the same

A strategy practice accumulates two kinds of material that look alike and are fundamentally different: *priors* and *evidence*.

Priors are the user's own convictions — brain dumps, memos, working hypotheses, strong opinions held with varying degrees of weight. They are precious: they seed theses, shape questions, and point at where to look. But they cannot confirm anything. A claim grounded only in a brain dump is a hypothesis in formal dress, and it should carry its own tag and its own confidence ceiling until corroborated.

Evidence is everything else — cited analyst views, figures drawn from market research, quotes from customers, statements from a competitor's own materials, findings from a commissioned study. Evidence is what promotes a thesis from *what we believe* to *what we can defend*.

Keeping the distinction legible in the wiki is what prevents a strategy from being quietly overfitted to the founder's worldview. A thesis that only your priors support is a thesis that the world has not yet voted on.

## Credibility is part of the claim

Not all evidence is equal. A figure from a regulatory filing and the same figure from a competitor's marketing site are not the same fact; they are a strong claim and a weak one sharing a sentence. The wiki should carry a credibility signal on every source: whether the source is primary or secondary, and whether the source is neutral or has an interest in the claim being true.

A claim corroborated only by interested parties is weaker than one corroborated by neutral ones, and the wiki should refuse to promote it to high confidence no matter how many interested voices repeat it. This one discipline, applied consistently, catches the most common failure mode in strategy work: believing the category's collective marketing.

## Cite everything, invent nothing

Every claim on a wiki page must be traceable to a source. A claim with no source is one waiting to be contradicted. When a page has to hold an unsupported statement for now — a prior, a stated assumption, an inferred link — mark it as such. The reader should see, at a glance, the status of each line and what it rests on.

When a newer source contradicts an older one, the older claim is not erased. It is marked superseded, with a date and a pointer to what replaced it. Audit trails matter: a year later someone will ask "when did we stop believing that?", and the wiki should answer precisely.

## Promote through tiers

Not every fact deserves the same treatment. Raw capture is immutable. Per-source summaries are permanent once written. Entities, concepts, and typed relationships — the semantic layer — evolve as evidence accrues. The vocabulary of the domain, the world-assumptions the whole strategy rests on, and the cross-strategy patterns move slowest and carry the highest confidence when they do.

A fact seen once is episodic. One confirmed independently across several sources earns its way into the semantic layer with increasing confidence. A pattern recurring across multiple strategies or multiple products earns its way into the programme-level layer. Movement is always upward and outward, and every promotion leaves a trail back to the evidence that supported it.

## Clusters are the unit of ingestion

Raw material is messy and heterogeneous. The wiki needs a way to take it in a chunk at a time, on the operator's terms, without drowning in context.

The practical unit is a *cluster*: a bounded set of files that belong together and can be processed in one pass. A cluster could be an analyst report, a competitor's materials, a pack of market figures, a brain-dump folder, or a mixed bag from a single source. It carries a small manifest describing what is in it, what scope it touches, how large it is, what it depends on, and — critically — the credibility of the material inside.

Operator and agent agree up front on which clusters to process in which order. The agent does not open raw files until a cluster is confirmed. This keeps the working context tractable regardless of how much material is staged. It also creates a natural pause before each integration, during which the operator can re-prioritise or split a cluster that has grown too large.

## Scope expansion is a change-control event

When a new source reveals a strategy, a product, a competitor, or a market segment not yet in the wiki, the agent does not silently create folders for it. Scope is the operator's call. Instead, the agent surfaces the candidate, with supporting evidence, and waits for a human to confirm whether it is real, whether to split it from an adjacent scope, and what to call it. This holds even when evidence is strong — the cost of an unwanted scope folder exceeds the cost of asking.

The same discipline applies to new entity types, relationship types, and concept categories. The ontology is the most load-bearing part of the knowledge layer, and it should evolve deliberately rather than drift. When extension is warranted, extend it and record why.

## Research is active, gated, and compounding

The behaviour that distinguishes a strategy wiki from a discovery wiki is that the agent does not wait passively for evidence to arrive. It proposes research continuously. When an ingested source raises a question, leaves a sub-question unanswered, or makes a claim that contradicts something the wiki holds, the agent queues a candidate research item, explains why it matters, and waits for the operator to approve it.

An approved research item is then pursued in escalating depths, gated by the operator at every step. The first level always runs: it grounds the question in what the wiki already holds, decomposes it into sub-questions, runs a meaningful public-web sweep, and produces a scoping memo with a recommendation — stop here, go deeper, or go much deeper, with specific named claims justifying the depth. Higher levels add validation, primary-source preference, adversarial reading, and at the top end a board-grade triangulation that actively hunts for what would falsify the finding.

At every transition the agent reports what the next level would specifically pursue and the operator decides. The operator can approve, narrow, skip, or stop. Work compounds across levels; nothing is thrown away. The loop has stop conditions and hard caps, and when a cap is hit without closure the finding is filed as partial with an explicit list of what is still missing, rather than pretended complete.

This discipline lets the agent do multi-hour deep-research runs when they are warranted without committing the budget before the operator has seen the shape of the question. Cheap questions stay cheap. Thesis-defining questions earn their weight.

## Wiki-first at every level

Before any search against the public web, at every level of a research run, the agent first checks what the wiki and the raw materials already hold. A strategy wiki accumulates hard numbers, analyst quotes, and competitor facts over time, and re-fetching a claim from the web when the wiki has already captured and cited it is worse than wasteful — it risks citing a weaker version of a fact the wiki has already nailed down. Wiki-held knowledge takes precedence; the web is where gaps are filled.

## Findings are living, not frozen

A research report is not a frozen artifact. It can be *extended* — resumed at the next level when an operator decides the question deserves more depth than was originally approved. It can be *redone* — rerun from scratch when time has passed or the world has shifted, with the old report preserved as superseded rather than deleted. And it can be *challenged by ingestion* — when a new source arriving through `/ingest` contradicts a claim the report made, the wiki flags both sides and queues a suggested redo for operator approval.

Contradiction is the engine. The wiki earns its keep by noticing when the outside world has voted differently than the report said it would, and by making that disagreement impossible to miss.

Staleness is the quieter engine. Strategy material decays even without contradiction; a two-year-old market figure is suspect regardless. The wiki's immune system should flag time-stale reports as suggested refreshes on its own rhythm — more often for fast-moving figures, less often for deep theses.

## Non-goals, moats, and world-assumptions

Three small disciplines carry disproportionate weight in making a strategy honest.

*Non-goals* — explicit statements of what a strategy will not pursue — are the clearest sign that trade-offs have been made. A strategy with only goals has chosen nothing; a strategy with named non-goals has decided what it is willing to be wrong about. The wiki should prompt for non-goals once enough evidence has accumulated that the exclusions could be named.

*Moats* — the defensibility the strategy relies on — must be evidence-based, not aspirational. Helmer's seven powers is one workable lens. A strategy that claims a moat without a cited basis is making a wish; the wiki should flag it.

*World-assumptions* — the macro priors underneath every strategy — are the most load-bearing and the most often implicit. If the world behaves as assumed, the strategy makes sense; if it doesn't, the strategy breaks. Naming them explicitly, citing them, and flagging them when an ingested source challenges them is what lets the strategy stay honest as reality arrives.

## Narrative must ladder to strategy

Product marketing and strategy are often separated in organisations, and separated in messy ways: marketing writes messaging that doesn't match the strategy; strategy ignores how the market reads the product. Keeping them in the same wiki forces a simple structural rule — every messaging pillar ladders to a strategic pillar; every piece of thought leadership cites a thesis, a customer-voice element, and a market or competitive fact.

This rule sounds bureaucratic and is genuinely not. It catches the common failure where a compelling phrase makes it into the deck but connects to nothing the company is actually betting on, or where a strategic pillar is articulated without any testable implication for how the market will hear it. Orphan messages and ungrounded thought leadership are the visible surface of a deeper disconnect; the wiki flags them early.

## Confidence, visibility, and the questions they answer

Two fields worth keeping on every consequential page answer two different questions.

Confidence answers *how sure are we?* One source lightly, two sources better, three independent sources strongly. A claim sourced only from interested parties caps at medium no matter how many interested voices repeat it. A page that aggregates claims inherits the lowest confidence of any claim on it — a single shaky claim drags the summary down, and that is the correct behaviour because the reader needs to know.

Visibility answers *who can see this?* Working material belongs to the team. Polished artefacts belong to leadership. Strategy work additionally produces material that is board-only or strictly need-to-know, and some — the published narrative, the positioning — is intended to leave the organisation entirely. The wiki can carry all of these side by side, with visibility tags controlling which pages are compiled into which shareable output. A single command can produce a board-grade brief, a leadership review, or an externally shareable narrative from the wiki at any point, without anyone manually curating what is safe to show and what is not.

## State is in git

There is no separate snapshot mechanism. Git commits are the snapshots: diffable, point-in-time, reproducible, and free. Every meaningful operation that changes files is followed by a commit — automatically after ingests by default, configurable to other rhythms depending on how granular a history the operator wants. Commits are local; pushing is always an explicit human decision, because strategy material is more sensitive than the average repo.

A compiled brief is pinned to the commit SHA it was generated from, so a shared artefact is always reproducible against the repo state that produced it. This is the one structural dependency the wiki has on the outside world, and it is worth it.

## Commands as phases of a rhythm

The operating commands exist to enforce the rhythm of the pattern, not to be memorised individually.

*Bootstrap* scaffolds the wiki once, from minimal context, initialises git, and writes an engagement-specific operating config that takes over from that moment onward.

*Ingest* is where material becomes knowledge. It selects a cluster, reads it, creates a per-source note with credibility tagged, extracts entities and concepts, propagates changes across the strategy, intelligence, narrative, and knowledge layers, checks for contradictions against existing research, proposes candidate research items and candidate thought-leadership angles, and logs what was done. It always writes verbatim evidence first, because every higher-order claim should be able to point back to a real quote or figure.

*Research* is where the wiki reaches beyond itself. It runs the gated four-level loop against an approved question, with the operator approving each escalation. It writes findings back into the wiki as updates to the affected pages, with citations, and archives source excerpts against the inevitable link rot.

*Query* is where the wiki becomes useful. A question comes in, the agent reads the relevant pages, produces a cited answer, files it alongside the question, and — if the answer surfaces a pattern worth promoting into the domain layer or a question worth queuing as research — it promotes or queues.

*Commit* is the heartbeat of git integration: a structured commit of the wiki state, with a message that summarises what changed and a footer that snapshots readiness, sources, and research counts. *Auto-commit* configures when the agent commits on its own.

*Lint* is the wiki's immune system. It walks the wiki looking for known decay patterns — orphaned entities, uncited claims, bets without kill criteria, theses with only one source, moats without mappings, messaging without laddering, stale competitor profiles, research reports past their staleness thresholds, world-assumptions challenged but not researched, uncommitted drift — and fixes or flags each one. The simple discipline of running lint regularly is what keeps a wiki from quietly rotting.

*Status* is a chat-only orientation summary, including recent git activity. *Brief* compiles pages by visibility into a shareable output, pinned to a commit SHA.

These are not a zoo of features. They are the beats of a loop: ingest, propose research, run research, query, lint, report, commit, ingest again. Everything else follows from the loop running cleanly.

## Images are optional, text is not

Diagrams and generated images are useful when they genuinely aid understanding. A strategy spine, a competitor positioning grid, a capability map, a scenario tree, a narrative arc, a pricing-tier comparison, a persona card — these benefit from visuals.

But every page has to stand alone as text. Visuals are always enhancements, never replacements. An image is always accompanied by the text equivalent of what it shows, for accessibility, for grep, for the reader who is scanning on a phone. Image generation is opt-in and on-demand; it is never a silent side effect of ingestion or research.

## General orientation

A handful of simple habits carry most of the value.

Always read the master navigation page first; it tells you what exists. Cite every claim. Never overwrite a claim that had a source — supersede it with a dated marker. Treat raw captures as immutable, and put all derived work in a separate workspace area. Tag the credibility of every source. Classify every assumption by the kind of strategic risk it represents. Attach kill criteria to every bet. Ladder every messaging pillar to a strategic pillar. Let research go deeper only when the operator says so. Commit often, push never, unless you mean to.

When in doubt about shape — how to model a new concept, where to file a new research report, whether a new entity type deserves its own category — pick the option that keeps the wiki readable by someone who is not in this conversation. The wiki is not a personal notebook; it is a compiled document that will be read by strangers, and that constraint should drive every structural decision.

## What this is not

This pattern is not a retrieval index over strategy documents. It does not simply index raw files for later keyword search; it digests them into structured, cited, cross-linked knowledge. If you want search, the wiki supports it, but search is not the product. The product is the wiki itself as a compiled, readable, defensible argument about the future.

It is also not a methodology lock-in. Rumelt, Lafley and Martin, Wardley, Helmer, Dunford, Raskin, Play Bigger, Christensen — any sensible strategy or product-marketing frame can sit on top. The commitments made here are about structure, evidence, credibility, and compounding, not about which strategic school you choose to follow.

And it is not a substitute for judgement. The wiki makes the argument legible, the evidence traceable, and the gaps visible. It does not decide the strategy — that is the operator's job, and the wiki's value is that it makes that job honestly harder and more rewarding.

## The invitation

This file is a gist, not a specification. A capable agent reading it can derive the specific wiki layout, page templates, research procedures, and command behaviours that follow from these principles, and can tailor them to the engagement at hand. That is the point. A more capable agent, given more freedom, will often produce a better-fitting wiki than a prescriptive template would, because it can respond to the actual shape of the strategy work — the specific category, the particular competitors, the live regulatory weather — rather than being forced into a shape decided in advance.

Use this version of the pattern when you trust the agent to make the right concrete choices, and when you want the pattern to mould itself to the strategy rather than the other way around. Use the more prescriptive sibling files when you want guaranteed structural consistency across engagements, or when the agent's judgement has not yet earned the wider latitude.

Drop this file into an empty folder, open it in a capable coding agent, and ask the agent to bootstrap a strategy wiki from these principles. Answer the questions it asks about your mission, your strategies, the products you manage, the competitors you watch, the analysts you track, and the framework you want your strategies argued in. Then start feeding it the raw material — brain dumps, strategy memos, product docs, analyst reports, market figures, competitor materials, news — a cluster at a time, and let the strategy compound as sources and research accumulate around it.
