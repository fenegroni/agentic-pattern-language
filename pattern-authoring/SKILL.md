---
name: pattern-authoring
description: Author or revise a skill as an Alexandrian pattern — stating the forces a rule resolves, not just the rule — so it generalizes to cases the author never enumerated and relaxes correctly where its purpose is absent. Use when writing a new SKILL.md, revising one that fails on edge cases or gets applied where it shouldn't, or auditing an existing skill that reads as a bare list of steps. Not for reference material with no judgment in it.
---

# Pattern Authoring

## Problem

A skill written as bare procedure fails two ways at once. It **over-applies**: an agent enforces a rule in a case where the rule's surface conditions hold but its purpose is absent. It **under-applies**: it goes silent on cases the author never enumerated, because the agent has a list to match against instead of a principle to reason from. Both failures are confident, and both report success.

## Context

You are writing or revising a skill that an agent will read while acting with discretion, over cases you cannot enumerate in advance. The agent will meet inputs you did not foresee and must decide whether your rules still bind.

**This pattern does not apply** when the skill is a genuine lookup table — model IDs, file paths, API parameters, a fixed command sequence with no branch. There is no judgment to generalize and no rule that could be misapplied, so rationale is noise and the six-part form is overhead. Write the table. If you are unsure which you have, ask whether an agent could follow every rule and still defeat the point. If it cannot, you have a table.

## Forces

**Terseness against generality.** Token cost and reader attention pull toward a short rule list, and there is a real effect behind that pull: agents obey explicit imperatives more reliably than they infer behaviour from rationale. A stated rule gets followed; a stated reason gets interpreted. Generality wins anyway, on cost asymmetry. A missing rule costs you one unhandled case. A rule with no stated purpose costs you *every* case where the purpose is absent — it converts the skill from a guide into a source of wrong actions, taken confidently, reported as compliance. State the rule imperatively **and** state what it protects against, so the agent can recognise the case where nothing needs protecting.

**Momentum against scope.** Drafting before problem and context are settled feels faster, and gating feels like ceremony. But a skill drafted on unsettled scope comes out coherent and wrong, and its coherence is what hides the error — it reads well, so nobody rereads it. The gate wins, narrowly: it binds on the *scope question only*, and it is satisfied by the answer existing, not by interrogating anyone. Where the request already makes scope unambiguous, state it in a sentence and move.

**Economy against resolution.** Forces and Rationale look redundant and merging them saves space. Keep them apart. Forces states what pulls each way; Rationale states why this resolution wins. Merged, they license "on the one hand, on the other hand" prose that sounds deliberative and decides nothing, leaving the agent to resolve at runtime the tension you were supposed to resolve at authoring time.

**Shipping against probing.** Probes cost effort and often find nothing. They earn it because each one targets a defect that is *invisible on reread* — that is the selection criterion for the set. A defect you would catch by rereading does not need a probe.

**Completeness against honesty.** A finished document with every section filled and every probe passed looks authoritative, and hedging throughout makes it weak. Resolve this by segregating rather than hedging: keep the body decisive, and put every force you guessed at into one labelled list at the end. An unconfirmed force stated confidently becomes a permanent unexamined premise that later rules build on.

## Solution

**1. Establish problem and scope.** Answer explicitly, before drafting: what recurring problem, in what context. Then decide single pattern or pattern language. Sub-patterns belong in one language only if they share a trigger and a resource domain; if one has a second trigger, it is a separate pattern — say so, and say where the seam is. Do not split a linear workflow into ceremonial sub-patterns.

**2. Elicit forces for every rule.** For each constraint about to go in:

- What competing pressures does it resolve? What would pull toward doing it differently?
- Which pressure wins, and what is the cost of getting it wrong?
- What does it protect against, and under what conditions is that thing absent?

Apply the **force test**: a force is only a force if a competent practitioner could choose the losing side for a defensible reason. If the opposing side is a strawman — "we want it to work / against that, we want it broken" — you have written a benefit, not a force, and the rule behind it is still a bare assertion.

A rule with no answers here is a bare assertion. **Flag it as one. Do not write it into the skill silently, and do not invent a rationale for it** — a plausible-sounding reason is trivially generated and indistinguishable from a real one once written down. If you do not know why a rule exists, that goes in the guessed-forces list.

**3. Draft in six-part form.** Problem, Context, Forces, Solution, Rationale, Resulting Context. Problem precedes Context because scope depends on it. Forces precede Solution because forces elicited afterward are post-hoc justification, not analysis. Resulting Context is last because it is the handoff.

The sections are load-bearing; the number six is not. If a force is genuinely uncontested, leave Forces short and say it is uncontested — do not manufacture an opponent to fill the section.

**4. Probe before finalizing.** Run all five. Report where the draft fails; revise, or state which probe it cannot survive and why.

1. **Vacuous constraint** — pick a rule, construct a case where its surface conditions hold but its reason does not. Would an agent recognise that it no longer binds, or enforce it anyway?
2. **Purpose versus rule** — construct a case where every mechanical rule is satisfied and the stated purpose is still defeated. If none exists, say so. If one does, close it or acknowledge it explicitly.
3. **Honest gap** — pick an expected input. When it is missing, does the skill instruct you to report the absence, or is there room to synthesize a plausible substitute?
4. **Freshness** — for state the skill reads once and reasons from, is re-reading required, or can stale state go undetected?
5. **Silent side-effect** — for each read-only constraint, is there an operation whose output looks correct whether or not the constraint held? If so, is that operation observable outside the final answer?

A probe with no surface to bite on is reported as inapplicable, with the reason. Manufacturing a finding to fill it is itself a probe-1 violation.

**Do not revise until the probes appear to pass.** A rule added to satisfy a check rather than to serve a purpose is a vacuous constraint by construction — you will have created the defect the probe was looking for.

**5. Re-verify, then output.** Before finalizing, re-read the Problem and Context against the *current* request, not the one you started from; scope drifts across a long session and the drift is invisible in a draft that was correct when written. Then output the SKILL.md plus the guessed-forces list.

## Rationale

The six-part form wins because each section absorbs one of the failures above at the point where it happens. Context absorbs over-application by naming where the pattern stops. Forces absorbs under-application by giving the agent the pressures to reason from when it meets an unenumerated case. Rationale forces the resolution to be made at authoring time rather than deferred to runtime. Resulting Context makes the handoff explicit so the next pattern is not guessing at state.

The probe set wins on its selection criterion rather than on thoroughness: five checks, each aimed at a defect that survives rereading. Adding probes that catch what a careful reread already catches would raise the cost without raising the yield.

The guessed-forces list is not a courtesy note. It is the **observability mechanism for probe 5**: a finished SKILL.md reads identically whether a force was confirmed with the author or fabricated by the drafter, so the artifact alone cannot show that the no-inventing constraint held. The list is what makes that checkable from outside the document. Omitting it because it looks short defeats its function.

## Resulting Context

A skill an agent can reason from, not just match against: it knows which rules bind, which have gone inert because what they protect against is absent, and how to act in a case the author never listed.

Handed off to the caller:

- The **SKILL.md** in six-part form, with empty sections labelled empty rather than padded.
- The **guessed-forces list** — every force inferred rather than confirmed, for the author to correct. Each entry stays open until confirmed or removed; a rule resting on a force that the author rejects goes back to step 2.
- Any **probe the skill could not survive**, stated as a known limitation rather than patched.

Skills whose forces are all confirmed and whose probes all pass or are reported inapplicable are finished. The rest are drafts, and the guessed-forces list says which.
