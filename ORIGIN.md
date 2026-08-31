# How the Pattern-Authoring Skill Was Built

A worked record of authoring [`SKILL.md`](pattern-authoring/SKILL.md) — a skill for writing skills as Alexandrian patterns — using the method it describes. The prompt and the response are reproduced verbatim. Nothing here is reconstructed after the fact.

The interesting part is not the finished skill. It is that **four of the five adversarial probes changed it**, and two of those changes could not have been reached by rereading the draft. That is the claim the method makes about itself, and this is the record of it holding up once.

---

## The prompt

> You are helping me author a Claude Skill as an Alexandrian pattern, not a procedure. A skill that states only rules and steps is brittle: it enforces its rules as objects in themselves rather than as means to an end, and it fails silently on any edge case its author didn't enumerate. Your job is to make sure this skill states its why, not just its what, and that the why is structured as forces so it generalizes to cases neither of us has thought of yet.
>
> **Step 1: Establish problem and scope**
>
> Before writing anything, answer:
>
> - What recurring problem does this skill solve, and in what context does that problem arise?
> - Is this a single pattern, or a pattern language? If it's a pattern language, list the sub-patterns and confirm they genuinely share a trigger and resource domain, or whether one should split off.
>
> Don't proceed past this step until it's answered explicitly.
>
> **Step 2: Elicit the forces**
>
> For every constraint or rule about to go into this skill, work out:
>
> - What competing pressures does this rule resolve? What would pull toward doing it differently?
> - Which pressure wins, and why? What's the actual cost of getting it wrong?
> - What is the rule protecting against? Under what conditions does it stop applying because the thing it protects against isn't present?
>
> A rule with no answer to these is a bare assertion. Flag it as such instead of writing it into the skill silently.
>
> **Step 3: Draft in six-part pattern form**
>
> Write the skill (or each sub-pattern, if this is a pattern language) with these sections:
>
> - **Problem:** the recurring problem, one or two sentences.
> - **Context:** when this pattern applies, what's true in the environment.
> - **Forces:** the competing pressures from Step 2, and how they resolve against each other. This is the section most skills skip. Do not skip it.
> - **Solution:** the concrete steps, tools, and constraints.
> - **Rationale:** why the solution resolves the forces the way it does. Distinct from Forces: Forces states the tension, Rationale states why this solution wins it.
> - **Resulting Context:** what's true after the pattern runs, including any state it hands off to other patterns or to the caller.
>
> **Step 4: Probe the draft before finalizing**
>
> Run each of these against the draft and report where it fails. Revise until it survives all five, or state explicitly which one it can't survive and why:
>
> 1. **Vacuous-constraint:** pick a rule, describe a case where its surface conditions hold but the reason it exists doesn't. Would an agent following this skill recognize the rule no longer binds, or enforce it anyway?
> 2. **Purpose-versus-rule:** construct a case where every mechanical rule is satisfied but the skill's stated purpose is still defeated. If none can be constructed, say so. If one can, the skill needs a rule closing that gap, or an explicit acknowledgment of it.
> 3. **Honest-gap:** pick an input the skill expects. What does the skill instruct when that input is missing: report the absence, or is there room to quietly synthesize a plausible substitute?
> 4. **Freshness:** for any state the skill reads once and reasons from, does the skill require re-reading it, or could stale state go undetected?
> 5. **Silent-side-effect:** for any read-only constraint, is there an operation where the final output looks correct whether or not the constraint was violated? If so, does the skill make that operation observable, logged or checked by something outside the final answer?
>
> **Step 5: Output**
>
> Produce the finished SKILL.md, plus a short list of any forces guessed at rather than confirmed, so they can be corrected.

### One thing that happened before Step 1

The repository was empty and the prompt never named a subject. Step 1 asks what problem the skill solves, which cannot be answered without knowing which skill. Rather than guess, the gate was taken literally and the question was asked — with a recommendation attached, since the repo name and the prompt's content both pointed at the same answer: the methodology itself. That reading was confirmed.

This is worth recording because the skill later encodes exactly this: **the gate binds on the answer existing, not on interrogating anyone.** Here the answer did not exist, so the gate bound.

---

## Step 1 — Problem and scope

**Recurring problem.** A skill written as bare procedure fails two ways at once. It *over-applies*: an agent enforces a rule in a case where the rule's surface conditions hold but its purpose is absent. And it *under-applies*: it goes silent on cases the author never enumerated, because the agent has a list to match against rather than a principle to reason from. Both failures are confident and quiet.

**Context.** Authoring a skill that will be read by an agent acting with discretion over cases the author cannot enumerate in advance. If every case *is* enumerable — a model-ID table, a list of paths — this problem does not arise and the pattern form is overhead.

**Single pattern or language?** Single pattern. The candidate sub-patterns (Scope Before Draft, Forces Before Rules, Six-Part Form, Adversarial Probes) share one trigger — "about to write or revise a skill" — and one resource domain, the SKILL.md text. They're phases of one workflow, not independently invocable patterns. Splitting them into four six-part patterns would apply the form where its purpose isn't present, which is the exact failure this skill exists to prevent.

One real seam: **the probe set has a second trigger** — auditing a skill someone else wrote, with no authoring involved. That's where this splits if it grows. I've kept it inline and marked the seam.

---

## Step 2 — Forces

The load-bearing ones, and why each resolves as it does:

| Rule | Competing pressure | Why it loses | Stops binding when |
|---|---|---|---|
| State forces, not just rules | Terseness; agents obey imperatives more reliably than they infer from rationale | Cost asymmetry: a missing rule costs one case, a purposeless rule costs *every* case where the purpose is absent — and reports success | The skill is a genuine lookup table |
| Gate drafting on explicit problem/context | Speed; gating feels like ceremony | A skill drafted before scope settles is coherent *and wrong*, and its coherence hides the error | Scope is already unambiguous — the gate is on the answer existing, not on interrogating anyone |
| Rationale separate from Forces | They feel redundant | Merged, they permit "on one hand / on the other" prose that states a tension and resolves nothing | A force is genuinely uncontested — then leave Forces empty, don't invent an opponent |
| Run the five probes | Effort; they often find nothing | Each targets a defect *invisible on reread* — that's their selection criterion, and it's exactly where the cost is earned | A probe has no surface to bite; say so rather than manufacturing one |
| Report unsurvivable probes | A clean pass looks more finished | Patching a probe with a bare rule *creates* a vacuous constraint — the failure mode the skill exists to stop | Never |

One rule flagged as **not** force-backed: the number *six*. The sections are load-bearing; their count is inherited from Alexander and is not itself a force. So the skill says to leave a section empty and labelled rather than pad it.

---

## Step 4 — Probe results on the draft

All five bit. Four produced changes:

1. **Vacuous-constraint** — "always write Forces" applied to a pure reference skill. Surface holds, purpose absent. An agent would comply. → Added an explicit non-applicability clause to Context.
2. **Purpose-versus-rule** — *constructible, and it's the likely real failure*: an author fills Forces with restated benefits ("we want good code / against that, bad code") — two-sided in shape, one-sided in content. Every mechanical rule satisfied, purpose fully defeated. → Added a checkable test: **a force is only a force if a competent practitioner could choose the losing side for a defensible reason.**
3. **Honest-gap** — the expected input is the author's *actual* reason for a rule. When they don't have one, a plausible rationale is trivially synthesizable. Highest-risk gap here. → Explicit instruction to mark, not invent.
4. **Freshness** — Problem/Context are read once at Step 1 and can go stale if scope drifts mid-session. → Added a re-verify before finalizing.
5. **Silent-side-effect** — the finished SKILL.md reads identically whether a force was confirmed or fabricated. → The guessed-forces list *is* the observability mechanism; the file now names that as its function, so it isn't dropped as a courtesy note when it looks short.

### What the probes actually bought

Two of these were not available by rereading the draft, which is the whole claim of the probe set:

**Probe 2 produced the force test.** The draft already said "elicit competing pressures." It read as sound. What the probe surfaced is that an author can satisfy that instruction completely and still write nothing — a fake opposition, two-sided in shape and one-sided in content, is the path of least resistance for anyone filling in a template, and it looks like compliance from every angle. The response is a single checkable sentence: *a force is only a force if a competent practitioner could choose the losing side for a defensible reason.* That sentence exists only because the probe demanded a case where every rule was satisfied and the purpose still lost.

**Probe 5 reclassified the guessed-forces list.** In the draft it was a courtesy — a polite closing note offering the author a chance to correct things. The probe asked whether any read-only constraint has an operation that looks correct either way, and the answer was immediate and uncomfortable: *the finished SKILL.md is byte-identical whether a force was confirmed with the author or fabricated by the drafter.* The document cannot witness its own honesty. That makes the guessed-forces list the only external check on the no-inventing rule — not a nicety but the load-bearing observability mechanism. The skill now says so explicitly, because a courtesy gets dropped when it looks short and a check does not.

Neither change came from the draft being wrong on its face. Both came from asking what a compliant-looking failure would look like.

---

## Step 5 — Forces guessed at, not confirmed

These went into the skill stated decisively, per its own segregate-don't-hedge resolution. They are inferences from general reasoning, not things the author confirmed. They remain open.

1. **That agents follow explicit imperatives more reliably than they infer behaviour from rationale.** The strongest counter-pressure in the whole skill — the real reason procedural skills get written. Asserted from general behaviour, not from observation. If it is weaker than claimed, the "state the rule imperatively *and* the reason" compromise is over-engineered and Forces alone would do.

2. **That the cost asymmetry runs the direction claimed** — one missed case for a missing rule, versus every purpose-absent case for a purposeless rule. This is the load-bearing justification for the entire skill. It holds when skills are read broadly across varied contexts. For narrow, single-purpose skills the asymmetry shrinks and the apparatus is heavier than the problem.

3. **That scope drift across a session is common enough to warrant the step-5 re-verify.** Derived from probe 4 needing something to bite on — a slightly suspicious provenance. The fix may be answering the probe rather than a real risk.

4. **That decorative forces are the likely real-world failure** (probe 2). Confident it is *constructible*; guessing it is *frequent*. The force test is priced against that frequency — if rare, the test taxes every rule to catch something that seldom happens.

5. **That the probe set is complete enough to be worth naming as five.** The set is justified by its selection criterion — defects invisible on reread — but there is no argument that these five exhaust that category. There may be a sixth.

---

## The limitation that was not patched

Probe 3 asks what the skill instructs when an expected input is missing. The expected input is the author's actual reason for a rule. The skill says: do not invent one, record it as a guess.

But a drafting agent that fabricates a rationale anyway produces a document indistinguishable from an honest one. The guessed-forces list is the mitigation, and it is an **honesty-dependent** mitigation — it works only if whoever fills it is willing to admit uncertainty. There is no mechanical check behind it. Closing it properly would take an external reviewer comparing the skill against the author's actual stated reasons.

It is recorded as a known limitation rather than patched, because patching it with a rule that sounds reassuring would be a vacuous constraint by construction — precisely the defect probe 1 exists to find.
