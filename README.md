# fable-5-operating-protocol

One `SKILL.md`. It gives any model the Claude Fable 5 operating discipline: how it reframes
before acting, how it discloses reasoning, how it calibrates uncertainty, how it writes code and
comments, how it composes interfaces.

Aligned with **Claude Fable 5.1** (released 2026-09-01).

Not a model. Not a plugin. A single markdown file dropped into a skills directory.

---

## Why

Every session repeats the same failure. The model reads the rules, follows them for two turns,
then quietly forgets. It reasons straight down the literal wording of a request instead of asking
what is actually blocking the user. It performs confidence instead of calibrating. Every interface
it touches comes out identical: card stacked on card, frosted glass, a purple-blue gradient hero,
three equal feature columns.

This file counters with enforced rituals, not polite suggestions.

---

## What it enforces

### Cognitive posture

Effort level is an API parameter and cannot be set from a markdown file. What the protocol
specifies instead is the behavioural signature of maximum-depth reasoning: do not converge on the
first workable answer, hold the problem open, exhaust the boundary scan past the required three,
verify with a fresh context rather than self-critique, surface revisions explicitly, and size work
in hours rather than minutes. Depth is warranted by stakes — routine work steps down, and says so.

### Reasoning

A mandatory five-step reframing protocol. The default path — infer intent from wording and
respond — is disabled. Step 2 forces the angle switch, from "what did they ask for" to "what is
actually blocking them". Steps 1 through 3 are a hard gate: no output before they are complete.

Reasoning must be disclosed in `<reasoning_disclosure>` tags — objective, actual problem, route,
boundaries, verification — before the answer. Silent conclusions are a violation.

### Comments: verbose

Comments are governed by a dedicated section that explicitly overrides the general
anti-decoration policy. This is deliberate: decoration bans target gratuitous ornament, while
explanatory comments are the opposite of gratuitous.

Every function, method, class, and exported component carries a documentation header — TSDoc for
TypeScript, PEP 257 for Python, the idiomatic equivalent elsewhere. Headers carry summary, every
`@param` with its constraints, `@returns` including failure shapes, every `@throws`, and an
`@example` for anything non-obvious to call. Non-obvious logic is annotated section by section.
Magic values are explained at the point of use. Workarounds cite their reason and their expiry.

Still banned even at verbose density: comments restating the signature, change-history comments,
commented-out code, apologetic hedging, and comments that contradict the code they describe.

### Coding standard: self-contained

The standard does not defer to "existing project convention". Where a repository contradicts it,
new and modified code follows the standard and the divergence is noted once — no silently
matching the older pattern, no refactoring surrounding code to conform.

Covers formatting, naming, type discipline, function shape, error handling, file organisation,
security, and version control. TypeScript strict mode with `any` prohibited, discriminated unions
for state, no enums or namespaces, named exports, options objects past three parameters,
validation at system boundaries only, Conventional Commits.

A dedicated `<standalone_html>` section covers self-contained HTML artifacts: one semantic colour
token block with no raw hex outside it, one radius token, and the three themes wired so that
"system" is the *absence* of `data-theme` — setting the attribute to the literal string `"system"`
matches no CSS rule and silently falls back to light. CSS and inline JS are explicitly held to the
same verbose comment standard as TypeScript.

### Design: split by scenario

Rules are selected by surface type, stated before starting.

**Utility** — dashboards, admin, internal tools, settings. Conservative. Density is a feature.
Skeleton before content, spacing from a single 4px scale, regions separated by whitespace and
type hierarchy rather than cards, three themes through semantic tokens, accent reserved for
action points.

**Marketing** — landing pages, showcases, campaigns. Expressive. Large type, deliberate
whitespace, one dominant element per viewport, colour and imagery carrying meaning. Gradients and
oversized type are available here and are not AI tells in this context.

A single product usually contains both: the logged-in console is utility, its pricing page is
marketing.

### Regression countermeasures

Fable 5.1's prompting guide documents sixteen behavioural regressions. All sixteen are countered:
batching tool calls the model now serialises, finishing the task instead of stopping on a
statement of intent, targeted edits over whole-file rewrites, shipping only what was asked,
marking quotation, searching at low effort, append-only history, preserving constraints through
compaction, and the rest.

### Communication

Grounded in the Fable 5.1 system prompt's `tone_and_formatting` and `reply_after_tool_calls`
sections, plus a 125-sample behavioural profile. Warm and never condescending; explains by
illustration; banned outright are filler openings, paper-tone connectives, hedge modifiers,
epistemic hedges used as evasion, and emoji. Calibrated uncertainty — "I don't know" beats
performed confidence. Minimum formatting for clarity, none at all in personal conversation, never
bullets when declining.

### Epistemics and drift

Training data is stale by default; every version, price, and signature carries a source or is
labelled unverified. Five enforced drift rituals: anchor at session start, pass a five-question
gate before every reply, roll back and re-read on drift, pin long tasks to a checklist, archive
lessons to a notes directory.

---

## Load strategy

The file assumes partial loading. `<always_on>` sits at the top and repeats the eight
load-bearing rules, so a truncated read still lands on them. Every section is self-contained:
constraints are restated inside each section rather than cross-referenced, on the assumption that
a model reading one part of a long specification will not have the rest in context. `<file_contract>`
says this explicitly to the model.

---

## Demo

`demo/protocol-comparison.html` — a Compare surface showing `deepseek-v4-flash` with and without
the protocol across two tasks, a per-clause rubric, and a limits section. Open it directly in a
browser; no build step and no remote dependencies.

Three themes (light / dark / system) via the masthead control, persisted in `localStorage`. The
system case removes `data-theme` entirely so the `prefers-color-scheme` media query decides —
setting the attribute to the literal string `"system"` would match no CSS rule and silently fall
back to light.

The page is built to the same standard the skill enforces: semantic colour tokens with no raw hex
outside the token block, a single radius token, comments carrying rationale rather than syntax,
and TSDoc headers on every JS function including documented failure modes.

**The responses shown are derived from the protocol's clauses, not from live inference.** No
DeepSeek or Anthropic API key is configured in this environment, so no model was actually run.
The provenance banner at the top of the page says so, and every claimed difference cites the rule
that produces it. Turning it into measured output requires an API key or a `base_url` pointing at
a gateway.

## Install

Global (all sessions):

```bash
mkdir -p "$HOME/.agents/skills/fable-5-operating-protocol"
cp SKILL/SKILL.md "$HOME/.agents/skills/fable-5-operating-protocol/SKILL.md"
```

Project only:

```text
.opencode/skills/fable-5-operating-protocol/SKILL.md
```

Restart the harness after install. Skills load at startup, not mid-session.

For durable retention, also reference the file path from your global `AGENTS.md` or `instructions`
config. Rituals are the ceiling on fighting decay; wiring it into instructions removes the fight.

## Usage

Say "fable style", or start working in a session where the skill is loaded — the description
carries trigger keywords. To tune behaviour, edit the file. The customization zone at the bottom
overrides any rule above it.

---

## Limits

Stated plainly, because the failure mode of a skill like this is overclaiming:

- **Reasoning ceiling.** This replicates working discipline, not benchmark scores. It will not
  make a weak model smarter. Nothing in a text file can.
- **Effort parameters.** `effort`, token budgets, and thinking time are API-level controls. The
  protocol specifies the behavioural signature of deep reasoning; it cannot set the parameter.
- **Load behaviour.** Whether the file is read whole or in part is decided by the harness. The
  `<always_on>` block and per-section self-containment mitigate partial reads; they do not
  guarantee a full read.
- **Instruction decay.** The five rituals are the ceiling on fighting forgetting in a long
  session, not a solution to it. Wiring the path into instructions is the only real fix.
- **Design judgement.** Rules prevent ugliness; they do not produce good design. Composition,
  taste, and the willingness to cut are not specifiable in a checklist.
- **Checklist conformity.** Obeying any fixed list, this one included, produces a recognisable
  house style. The audit section names this and warns against it, but cannot exempt itself.
