# Agent Product Discovery — Gist

## The idea

A complex engagement — product discovery, a consultancy sprint, a technical assessment, a research programme — produces a flood of raw material: interview notes, documents, transcripts, artefacts, half-remembered claims. The usual pattern is that it scatters across notebooks, chat threads, and slide decks, and by week three nobody can answer "what do we actually know, and how?" with confidence.

This file describes a different approach. Treat the collected knowledge as a wiki that is *compiled*, not *retrieved*. Every new source is digested, integrated, and cross-linked. Pages update as evidence strengthens or challenges them. Contradictions are made explicit. The wiki gets denser and sharper with every ingested source, and by the end of the engagement it is simultaneously a deliverable and a reusable map of the domain.

The design goal is that a colleague joining cold on week six can read the wiki and be caught up on the state of the engagement without asking a single question of the team.

## Two layers in parallel

A wiki run this way carries two complementary layers.

One tracks *the discovery itself*: what problems are we exploring, what we learned in which session, what decisions were taken, what risks remain open, how ready are we to move forward. This layer is temporal and engagement-specific — about the work and the process of doing it.

The other captures *the domain*: the entities, concepts, systems, and relationships that exist in the subject matter regardless of our process. This layer is durable and reusable. Run a second engagement in the same domain later, and the domain layer is where understanding compounds across engagements.

The two layers enrich each other. Sessions surface entities; entities anchor evidence; evidence accrues into concepts; concepts sharpen the questions the next session asks. Both grow in parallel from the same raw material.

## Problems before solutions

The most important commitment is this: units of discovery are *problem spaces*, not solutions. A use case is a problem to understand deeply enough to decide what to build. A core topic is a shared problem space several use cases depend on. Solutions are candidates under investigation, hypotheses to be tested, not starting assumptions dressed up after the fact.

This inverts the common failure mode where a stakeholder proposes a solution in the first session and the team spends the engagement dressing it up as a requirement. Instead, proposed solutions are logged as candidates against the opportunities they claim to address, and they earn promotion by surviving experiments, not by being voiced loudly.

Each problem space carries a measurable outcome (what would change if this were solved), an opportunity-solution tree (the unmet user needs and the candidate bets under them), a set of assumptions, and experiments that test the riskiest of those assumptions. "Riskiest" is not a fixed axis — use whichever framework you trust for classifying product risk, and apply it consistently. A common lens is value, usability, feasibility, or business viability; coverage gaps across those axes are leading indicators of downstream surprise.

## Cite everything, invent nothing

Every claim on a wiki page must be traceable to a source. A claim with no source is one waiting to be contradicted. When a page has to hold an unsupported statement for now — a hypothesis, a stakeholder assumption, an inferred step — mark it as such. The reader should see, at a glance, the status of each line and what it rests on.

When a newer source contradicts an older one, the older claim is not erased. It is marked superseded, with a date and a pointer to what replaced it. Audit trails matter: a year later someone will ask "when did we stop believing that?", and the wiki should answer precisely.

## Promote through tiers

Not every fact deserves the same treatment. Raw capture is immutable. Per-source summaries are permanent once written. Entities and concepts — the semantic layer — evolve as evidence accrues. Patterns and vocabulary spanning the whole engagement promote slowest and carry the highest confidence when they do.

A fact seen once is episodic. One confirmed independently across several sources earns its way into the semantic layer with increasing confidence. A concept recurring across multiple problem spaces earns its way into the programme-level layer. Movement is always upward and outward, and every promotion leaves a trail back to the evidence that supported it.

## Clusters are the unit of ingestion

Raw material is messy and asynchronous. The wiki needs a way to take it in a chunk at a time, on the operator's terms, without drowning in context.

The practical unit is a *cluster*: a bounded set of files that belong together and can be processed in one pass. A cluster could be one interview, one document pack, one data export, or a mixed bag of artefacts from a single contributor. It carries a small manifest describing what is in it, what scope it touches, how large it is, what it depends on.

Operator and agent agree up front on which clusters to process in which order. The agent does not open raw files until a cluster is confirmed. This keeps the working context tractable regardless of how much material is staged. It also creates a natural pause before each integration, during which the operator can re-prioritise or split a cluster that has grown too large.

## Scope expansion is a change-control event

When a new source reveals a problem space not yet in the wiki, the agent does not silently create folders for it. Scope is the operator's call. Instead, the agent surfaces the candidate, with supporting evidence, and waits for a human to confirm whether it is real, whether to split it from an adjacent scope, and what to call it. This holds even when evidence is strong — the cost of an unwanted scope folder exceeds the cost of asking.

The same discipline applies to new entity types, relationship types, and concept categories. The domain vocabulary — the ontology — is the most load-bearing part of the knowledge layer, and it should evolve deliberately rather than drift. When extension is warranted, extend it and record why.

## Confidence, visibility, and the distinct questions they answer

Two fields worth keeping on every consequential page answer two different questions.

Confidence answers *how sure are we?* One source lightly, two sources better, three independent sources strongly, a direct session confirmation strongly. A page that aggregates claims inherits the lowest confidence of any claim on it — a single shaky claim drags the summary down, and that is the correct behaviour because the reader needs to know.

Visibility answers *who can see this?* Working material belongs to the team. Polished outcomes belong to the client. The wiki can carry both side by side, with visibility tags controlling which pages are compiled into a client-facing brief. A single command can produce a shareable deliverable from the wiki at any point, without anyone manually curating what is safe to show and what is not.

## Commands as phases of a rhythm

The operating commands exist to enforce the rhythm of the pattern, not to be memorised individually.

*Bootstrap* scaffolds the wiki once, from minimal context, and writes an engagement-specific operating config that takes over from that moment onward.

*Ingest* is where material becomes knowledge. It selects a cluster, reads it, creates a per-source note, extracts entities and concepts, propagates changes to summaries and checklists, updates personas, and logs what was done. It always writes verbatim evidence first, because every higher-order claim should be able to point back to a real quote.

*Query* is where the wiki becomes useful. A question comes in, the agent reads the relevant pages, produces a cited answer, and files it alongside the question. If the answer surfaces a pattern worth promoting into the domain layer, it is promoted, and the domain layer gets sharper.

*Lint* is the wiki's immune system. It walks the wiki looking for known decay patterns — orphaned entities, unsourced claims, opportunities without experiments, stalled experiments, assumptions without a risk classification, stale summaries, broken cross-links — and fixes or flags each one. The simple discipline of running lint regularly is what keeps a wiki from quietly rotting.

*Status* is a chat-only orientation summary. *Snapshot* captures a point-in-time state for the record. *Brief* compiles everything marked client-ready into a shareable output in whatever format fits the audience.

These are not a zoo of features. They are the beats of a loop: ingest, query, lint, report, ingest again. Everything else follows from the loop running cleanly.

## Images are optional, text is not

Diagrams and generated images are useful when they genuinely aid understanding. A process flow, a system architecture, a persona map, a data model, a timeline, a comparison matrix — these benefit from visuals.

But every page has to stand alone as text. Visuals are always enhancements, never replacements. An image is always accompanied by the text equivalent of what it shows, for accessibility, for grep, for the reader who is scanning on a phone. Image generation is opt-in and on-demand; it is never a silent side effect of ingestion.

## General orientation

A handful of simple habits carry most of the value.

Always read the master navigation page first; it tells you what exists. Cite every claim. Never overwrite a claim that had a source — supersede it with a dated marker. Treat raw captures as immutable, and put all derived work in a separate workspace area. Classify every assumption by the kind of risk it represents. Log every operation briefly, so the history of the engagement is reconstructable from the wiki alone, without needing to ask anyone.

When in doubt about shape — how to model a new concept, where to file a new query, whether a new entity type deserves its own category — pick the option that keeps the wiki readable by someone who is not in this conversation. The wiki is not a personal notebook; it is a compiled document that will be read by strangers, and that constraint should drive every structural decision.

## What this is not

This pattern is not a retrieval index over documents. It does not simply index raw files for later keyword search; it digests them into structured, cited, cross-linked knowledge. If you want search, the wiki supports it, but search is not the product. The product is the wiki itself as a compiled, readable artefact.

It is also not a methodology lock-in. Any sensible product-discovery, UX-research, or consultancy framework can sit on top — the commitments made here are about structure, evidence, and compounding, not about which research school you choose to follow.

## The invitation

This file is a gist, not a specification. A capable agent reading it can derive the specific wiki layout, page templates, and command procedures that follow from these principles, and can tailor them to the engagement at hand. That is the point. A more capable agent, given more freedom, will often produce a better-fitting wiki than a prescriptive template would, because it can respond to the actual shape of the work rather than being forced into a shape decided in advance.

Use this version of the pattern when you trust the agent to make the right concrete choices, and when you want the pattern to mould itself to the domain rather than the other way around. Use the more prescriptive sibling files when you want guaranteed structural consistency across engagements, or when the agent's judgement has not yet earned the wider latitude.

Drop this file into an empty folder, open it in a capable coding agent, and ask the agent to bootstrap a wiki from these principles. Answer the questions it asks about your engagement. Then start feeding it the raw material, a cluster at a time, and let the knowledge compound as sessions and sources accumulate around it.
