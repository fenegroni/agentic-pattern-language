# agentic-pattern-language

A workbench for developing **`pattern-authoring`** — a Claude Skill for writing other skills as Alexandrian patterns rather than procedures.

A skill written as a bare list of steps fails two ways at once. It *over-applies*, enforcing a rule in cases where the rule's surface conditions hold but its purpose is absent. And it *under-applies*, going silent on cases the author never enumerated, because the agent has a list to match against instead of a principle to reason from. Both failures are confident, and both report success.

`pattern-authoring` addresses this by requiring a skill to state the **forces** each rule resolves — the competing pressures, which one wins, and the conditions under which the rule stops binding — in six-part form: Problem, Context, Forces, Solution, Rationale, Resulting Context. It then runs five adversarial probes aimed specifically at defects that survive rereading.

See [ORIGIN.md](ORIGIN.md) for the verbatim record of how the skill was built, including the probe pass that changed four of its rules.

## Installation

The skill is a single folder: [`pattern-authoring/`](pattern-authoring/). Copy it into a repo's skills directory.

**Per-project** — available only in that repo. Run from the target repo's root:

```bash
mkdir -p .claude/skills && cp -r /path/to/agentic-pattern-language/pattern-authoring .claude/skills/
```

**User-level** — available in every project:

```bash
mkdir -p ~/.claude/skills && cp -r /path/to/agentic-pattern-language/pattern-authoring ~/.claude/skills/
```

Restart Claude Code, or start a new session, for the skill to be picked up.

### Keep the folder name

Claude Code derives the skill's identity from its directory name, and `SKILL.md` declares `name: pattern-authoring` in its frontmatter. Rename the folder and the two disagree. Copy the folder, don't copy `SKILL.md` into a folder called something else.

### Which scope

Per-project is the safer default. A skill installed user-level is loaded in *every* session, including ones editing skills where you'd rather it not participate — and its `description` is written to fire on "writing or revising a SKILL.md," which is a real trigger you may hit while not wanting it.

## Why this repo doesn't install the skill

There is deliberately no `.claude/skills/` here. This repo is where the skill is *developed*, not used — and a skill under `.claude/skills/` loads into every session in its repo. Installed here, it would be steering the reasoning meant to be revising it critically.

So `pattern-authoring/SKILL.md` is a source artifact in this repo: inert text to edit and attack. It becomes a skill only at its destination.

## Status

The skill carries five **guessed forces** — inferences stated decisively in the text but never confirmed against practice. They are listed at the end of [ORIGIN.md](ORIGIN.md) and remain open. Two of them, the cost asymmetry that justifies the whole approach and the claimed frequency of decorative forces, are load-bearing: if either is wrong, the method is heavier than the problem it solves.

It also carries one **unpatched limitation**. The skill instructs an author not to invent a rationale for a rule they don't understand, and to record it as a guess instead. But a document that fabricates one is indistinguishable from an honest one. The guessed-forces list is the only check, and it is honesty-dependent with no mechanism behind it. This is recorded rather than patched, because a rule added to sound reassuring would be exactly the defect the first probe exists to catch.
