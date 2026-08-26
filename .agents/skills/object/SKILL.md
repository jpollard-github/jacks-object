---
name: object
description: Assess whether a proposed action is justified before meaningful commitment, returning ACT, OBJECT, or REQUIRE EVIDENCE after adaptive inspection. Use when the user invokes $object; asks to challenge a proposed software, writing, or debugging action; asks whether to keep going or whether they are about to build the wrong thing; wants assumptions inspected before implementation; wants to know whether another diagnostic step is justified; or wants to check whether new writing should be added. Do not use as a universal decision arbiter or continuous monitor.
---

# Object

Evaluate a proposed action before performing it. Prevent unnecessary work at the first responsible moment and preserve the underlying goal with the smallest viable alternative when evidence supports one.

Do not perform the proposed action as part of Object.

## Establish the proposition

1. Restate the proposed action without strengthening it.
2. Record the goal only when the user supplies it or inspected evidence strongly supports it. Otherwise, leave the goal unknown.
3. Identify assumptions that must hold for the action to make sense, especially assumptions that make the next commitment expensive, difficult to reverse, or dependent on another boundary.

Treat the proposed action in ordinary language as sufficient input to begin. Do not require the user to conduct the investigation first.

When ordinary-language wording has multiple plausible referents, incorporate contextual clarification into the proposition only when evidence establishes the user's intended referent; a candidate's availability, preference, or stronger support is not evidence of intent. Preserve wording that genuinely proposes multiple options. If intent remains unresolved and the readings could produce different dispositions, return `REQUIRE EVIDENCE` and ask the cheapest discriminating question; do not seek clarification when the distinction cannot materially affect the disposition.

## Acquire context

Acquire relevant context directly when it is reasonably available. Inspect repositories, sibling repositories, local documentation, tests, configuration, Git history, diffs, and other directly accessible material as the proposal requires.

Start locally. Follow consequential accessible boundaries. Do not mistake the starting scope for the evidence boundary. Inspect a relevant sibling repository, service, infrastructure source, corpus, or other context only when the proposal or current evidence points there; do not inspect every neighboring source merely because it exists. Report materially important scope limitations, and return `REQUIRE EVIDENCE` when an unavailable, unknown, or inaccessible source prevents a responsible disposition.

Use a boundary-first, wide-before-deep pass:

1. Locate existing behavior, constraints, ownership, boundaries, duplication, and established patterns.
2. Deepen only where a fact could materially change the disposition.
3. Seek evidence that weakens or disproves an emerging objection.
4. Stop when the evidence is sufficient for the next action-relative decision, even if the larger mystery remains unsolved.

For software work, check immediate differences in runtime, authentication, authorization, networking, data ownership, deployment topology, repository or service ownership, and visible future variation. Determine whether inherited code is a requirement, an example, or historical precedent. Do not turn this pass into an exhaustive architecture review.

For other domains, adapt the inspection to the available corpus and constraints. For example, examine whether proposed writing adds a material contribution rather than merely repeating an existing idea. Do not invent domain adapters or generate the proposed artifact.

Ask the user only when information is both materially necessary to the next responsible decision and not reasonably obtainable from the environment. Ask the cheapest discriminating question, not a broad request for more context.

## Challenge diagnosis-dependent continuations

Do not let a justified disposition imply an established diagnosis. Disproving the user's explanation does not establish a replacement. Treat an alternative as another proposed action: before recommending one that depends on a causal explanation, perform one bounded adversarial pass over the explanation and the assumptions the alternative requires. Check whether the evidence establishes what must be true for the alternative to address the observed problem, whether any material observation remains unreconciled, whether the verification path could share the same representation, abstraction, cache, metadata behavior, interpretation, or blind spot as the system being inspected, and whether non-reproduction under one set of conditions is being used to negate an observation from conditions not established as materially equivalent. This is one internal check, not a recursive Object invocation.

Treat non-reproduction as evidence bounded by the conditions actually tested. Before using it to negate a reported or directly observed failure, establish that the conditions material to the claimed behavior are equivalent. Inspect only differences that could plausibly change the action-relative decision, such as platform or runtime, tool or library version, deployment environment or topology, authentication or identity, network path or policy, configuration or environment variables, data or state, filesystem or metadata semantics, permissions, cache or build mode, external service behavior, or time. If material equivalence or direct falsification cannot be established, preserve the conflict: distinguish what was reported, what was directly observed, what did not reproduce under which conditions, and what remains unknown.

When the original failing artifact, output, log, request, response, trace, or other directly relevant evidence is available, inspect it before relying on a weaker synthetic reproduction to decide whether the original event occurred.

Treat every observation as bounded by the observer's scope: it is evidence about what the observer exposes. When material observations conflict or a diagnosis depends on views from different tools, layers, representations, components, identities, or boundaries, establish whether they concern the same artifact, request, state, event, path, identity, or execution; what each observer actually observed and exposes; and whether each can expose the property being claimed. Account for plausible normalization, hiding, aggregation, caching, translation, or other transformation. Scope negative claims accordingly: an observer's failure to expose a property does not establish that the property does not exist unless the observer can answer that stronger question. Surface unresolved disagreement and seek the smallest observation at the relevant boundary capable of discriminating between the accounts.

Do not use evidence that one local surface appears correct to assign failure to another surface. Before recommending work in another repository, service, layer, or team-owned component, require evidence that crosses the relevant boundary or recommend the smallest boundary observation that could distinguish the competing hypotheses. Otherwise preserve the original failure and leave its domain unknown.

When a materially important claim is directly testable, prefer an observation capable of falsifying it when practical. Deepen verification only when the fact could change the disposition or next action. If the self-challenge fails, label the diagnosis as inference or unknown, withhold or narrow the diagnosis-dependent fix, and identify the smallest discriminating investigation or evidence request.

## Preserve evidence boundaries

Keep these categories distinct:

- **Evidence:** material directly supplied or inspected, such as file paths and relevant lines, tests, configuration, documentation, Git history, diffs, observed command results, or explicit user statements.
- **Inference:** what the evidence appears to imply.
- **Unknown:** what cannot currently be established.
- **Assumption:** an unestablished proposition on which the proposed action depends.

Make claims follow evidence. Label inferred goals and historical intent as inference. Do not use a numeric confidence score.

Treat explicit reports, diagnoses, and proposed solutions as evidence of what a person asserted, not as independently established system state, cause, or fix.

## Choose a disposition

Return exactly one leading disposition:

- **ACT** — Current evidence reasonably justifies the proposed action as framed. This is not a permanent certification; materially new evidence may change the decision.
- **OBJECT** — The action as framed is not justified because evidence contradicts an important constraint or assumption, exposes duplication or disproportionate cost, or supports a smaller path. Preserve the evidenced goal with a viable alternative when possible; do not invent a goal to manufacture one or assume the objection justifies the alternative.
- **REQUIRE EVIDENCE** — Available information cannot responsibly distinguish ACT from OBJECT. Identify the specific missing fact, assumption, or material discriminator that would separate plausible paths. Distinguish a material discriminator from an available acquisition path: missing evidence may be useful without being reasonably obtainable. Use `Discriminating question` only when the available context establishes a relevant actor or system with a reasonably available path to answer it. Otherwise report the discriminator as `Material discriminator` and preserve the unavailable part as an `Unresolved condition`. Do not imply that waiting, escalation, or acquisition is justified merely because the evidence would discriminate.

Apply the disposition only to the proposition evaluated against the current evidence. **ACT is not a roadmap:** it does not justify adjacent enhancements, broader completion criteria, or future work. `OBJECT` does not transfer justification to an alternative, and `REQUIRE EVIDENCE` identifies what prevents a responsible disposition; it does not by itself justify an acquisition path, waiting, escalation, or actions that might follow the missing evidence. Treat recommendations beyond the immediate disposition as non-authorizing possibilities. Materially new evidence or scope requires fresh judgment.

When a downstream reader or system could reasonably overread a disposition, make its semantic scope explicit with `Disposition boundary`. This applies to ACT, OBJECT, or REQUIRE EVIDENCE when the boundary is materially useful. State what the current evidence establishes and what adjacent preference, commitment, authority, later action, or resolution remains outside the judgment. Keep this descriptive rather than granting or withholding external authority: prefer language such as `outside this judgment` or `not established by this disposition` over `not authorized`.

For an `ACT` on a reversible or preparatory step that may expose materially new evidence, state what is justified now and what later commitment remains unevaluated or evidence-dependent. Do not let `ACT` on inspection, preview, patch materialization, or another preparatory step imply that submit, commit, merge, publish, deploy, transact, or another later boundary was also evaluated.

`OBJECT` can coexist with an unresolved causal diagnosis. Use `REQUIRE EVIDENCE` when the evidence cannot distinguish whether the original action is justified; otherwise keep `OBJECT`, surface the unresolved diagnosis, and do not present an unsupported fix as established.

## Report compactly

Put the disposition first. Include only sections that help the human decide what to do next. Useful sections include:

- Proposed action
- Why now
- Evidence
- Inference
- Counterevidence checked
- Unknown
- Assumption
- Alternative
- Material discriminator
- Discriminating question
- Disposition boundary
- Next responsible action
- Possible continuation
- Unresolved condition
- Watch for

Do not force empty boilerplate. Cite inspected evidence precisely enough to verify it. Keep the alternative smaller than or better supported than the objected-to action. A smaller or plausible alternative is not automatically viable.

When a materially plausible competing path, counterargument, or distinction bears on the disposition, surface the decisive comparison compactly enough to explain why the selected disposition survives or why the evidence cannot distinguish the paths. Do not manufacture alternatives merely to demonstrate judgment; when no such comparison materially bears on the disposition, keep the report compact.

If reporting a smallest justified scope, include only capabilities necessary to satisfy the evaluated proposition under current evidence. Cheap, conventional, easy, or likely follow-on work is not thereby justified; mechanically inseparable correctness requirements may remain.

Before labeling anything `Next responsible action`, challenge that continuation as an action in its own right. Establish from the available context that the relevant actor or system can actually perform or control the step, has any authority the step requires, and has a reasonably available and proportionate path to perform it within the relevant decision horizon. If success depends on another actor's response, distinguish the controllable request from the uncontrolled response. Do not convert a desired outcome, another actor's response, unavailable evidence, unowned coordination, or a merely useful future condition into the current actor's earned next action.

A useful discriminator is not automatically a question for the current actor. Use `Discriminating question` only when the context establishes a reasonably available way for a relevant actor or system to answer it. When the fact would discriminate but no viable source or acquisition path is established, use `Material discriminator` and `Unresolved condition` instead of phrasing the missing evidence as homework.

Use `Next responsible action` only for an earned, actor-controlled continuation. If a useful continuation is plausible but not currently justified or available, label it `Possible continuation` and keep it explicitly non-authorizing. `Possible` describes a possibility without implying that it belongs to, is available to, or is justified for the current actor. If the judgment depends on a condition or evidence source for which no viable acquisition path is established, label that fact `Unresolved condition` rather than manufacturing motion. A downstream consumer remains responsible for its own behavior when Object has no earned continuation.

Make any next responsible action singular in spirit. It may contain mechanically inseparable steps, but not a definition of done, test matrix, backlog, or roadmap. Mention useful later concerns under `Watch for` or another compact label only when useful, and mark them as observations rather than commitments.

## Invoke at responsible moments

Use Object before a meaningful commitment deserves challenge. Re-run it only after a material state change, such as:

- a required assumption failing;
- scope expanding materially;
- work crossing a repository, service, data, authentication, network, deployment, ownership, or organizational boundary;
- validation differing across environments;
- an intervention failing to change the observed result;
- new evidence contradicting the reason for continuing; or
- the next action becoming substantially more expensive, irreversible, or dependent on other people.

Do not schedule check-ins, monitor continuously, or interrupt work merely because uncertainty exists.
