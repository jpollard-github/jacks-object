# Object

Object is a small experimental AI-assisted judgment skill for challenging a proposed action before meaningful commitment.

Its job is narrow: inspect relevant evidence, preserve uncertainty, and decide whether the action as framed is currently justified.

```text
$object "<proposed action>"
```

Object is advisory. It is not an approval gate, an oracle, a continuous monitor, or authority over the human or any downstream system. It evaluates the proposition against evidence it can reasonably acquire; it does not perform the proposed action.

## Dispositions

Every result begins with exactly one disposition:

- `ACT` — current evidence reasonably justifies the proposed action as framed.
- `OBJECT` — the proposed action is not justified as framed.
- `REQUIRE EVIDENCE` — current evidence cannot responsibly distinguish `ACT` from `OBJECT`.

The disposition is scoped to the proposition and current evidence. `ACT` is not a roadmap, `OBJECT` does not automatically justify an alternative, and `REQUIRE EVIDENCE` does not automatically justify waiting, escalation, or an evidence-acquisition path.

When useful, Object may report:

- `Disposition boundary` — what the current judgment establishes and what remains outside it.
- `Next responsible action` — an earned, actor-controlled continuation.
- `Possible continuation` — a non-authorizing possibility that is not currently established as justified or available.
- `Material discriminator` / `Unresolved condition` — evidence that would matter when no viable acquisition path is established.

Object should not manufacture motion merely because a useful next fact or outcome can be described.

## Current version

```bash
cat .agents/skills/object/VERSION
```

Current version: **0.7.1**.

### 0.7.1

0.7.1 tightens continuation semantics after laboratory and field evidence showed that Object could correctly identify a missing discriminator while overreaching in the action it suggested next.

The change makes next actions actor-relative and evidence-earned, distinguishes useful missing evidence from an available acquisition path, and allows Object to state the semantic boundary of a disposition when downstream readers or systems could overread it.

## Install in another repository

Copy the Object skill directory into the target repository:

```bash
mkdir -p /path/to/repo/.agents/skills
cp -R .agents/skills/object /path/to/repo/.agents/skills/
```

Restart Codex if the copied repository skill is not discovered immediately.

## Repository scope

The authoritative semantics are in:

```text
.agents/skills/object/SKILL.md
```

The authoritative version is in:

```text
.agents/skills/object/VERSION
```

# Provenance

This public repository is a curated snapshot of Jack's Object as of August 2026.

Object was developed iteratively through earlier private experiments, tests, discussions, and revisions. That development history is intentionally not part of the public repository because it contains working material and personal context unrelated to the published artifact.

The repository begins from the current public version rather than reproducing the complete private development history.
