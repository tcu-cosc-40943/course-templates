---
description: Design one use case, non-use-case FR, or subsystem into its area's design-of-record, drafted from the template. Stops before any code.
argument-hint: <UC-ID, FR-ID, or subsystem>  (for example /design UC-EVA-submit-evaluation or /design FR-NOT-weekly-reminder)
---

# /design: turn a use case, a non-use-case FR, or a subsystem into a design-of-record

Take the use case named in `$ARGUMENTS` (for example `UC-EVA-submit-evaluation`), or the non-use-case FR or subsystem named there (see the next section), and produce its **design-of-record**: the document for its area at `docs/design/<area>.md`, written from the team's template. This is the first of two build stages. **It stops before any code.** `/implement` with the same handle is the second stage, and it builds only from a design this command leaves behind after a teammate has merged it.

The use case is the contract, its business rules and cited `FR-*` are the acceptance criteria, and the glossary fixes the vocabulary. The design says only *how* the code will realize them. It **cites** `UC-*`, `FR-*`, and `BR-*` by identifier and never restates them.

**The specification is authoritative, not infallible. Challenge it.** You will meet steps that are ambiguous, rules that contradict each other, assumptions the existing code does not support, and constraints that are out of date or simply not good practice. When that happens, **ask the developer or push back. Do not silently comply, do not invent the missing detail, and do not inherit a constraint just because it is written down.** Name the gap, say what you would do and why, and propose the edit to the specification. A step no requirement backs, or a cited identifier that does not exist, is a question to raise, not something to paper over.

## Designing a non-use-case FR or a subsystem

The target in `$ARGUMENTS` can also be machinery no single use case owns, named by one handle: a **non-use-case FR** by its identifier (`/design FR-NOT-weekly-reminder`) or a **subsystem** by name (`/design AI proxy`). The developer names the thing; gathering its requirements is your job, as it is for a use case. The phases below apply, with these substitutions:

- **Resolve the handle.** A subsystem name must match a cross-cutting row in section 5.2 of the architecture-of-record. If the words fit more than one row, ask which. A name that matches no row is a component the architecture does not have yet: say so, and treat it as a change to the architecture-of-record rather than inventing its scope.
- **Gather the contract.** In place of the use case's steps and extensions, Phase 1 collects the requirement set: the named FR, or the FRs the subsystem serves, and every `SI-*`, `CO-*`, `DI-*`, quality attribute, and `BR-*` that cites one of them or that they cite. Also list the callers, the use cases that will use the machinery, since a design no caller needs is speculative. **Show the gathered set at the top of the Phase 2 draft**, each item with one line on why it is in, so the developer checks a list instead of writing one.
- **The home.** The design goes in `docs/design/<area>.md` for the FR's area code (`FR-NOT-*` in `not.md`), under a sequence heading named after the FR or subsystem. A subsystem whose FRs share one area goes in that area's document (the AI proxy serves `FR-AI-*`, so `ai.md`); one that serves FRs from several areas gets a document of its own, named after its section 5.2 row. An `SI-*`, `CO-*`, `DI-*`, or quality attribute has no area; it is designed in the document of the FR or subsystem it serves.
- **Sequence labels.** Each interaction is labeled with the "shall" clause or stated condition it realizes, in place of a use case step, and the scope check in Phase 2 applies to those labels: an interaction no clause names is a missing requirement or scope creep.
- **The tests.** One row per "shall" clause and per stated condition across the set, in place of the main success scenario and every extension. For `FR-NOT-weekly-reminder`: a student who owes an item due that day gets exactly one email, and a student who has submitted, or owes nothing due that day, gets none.
- **Missing requirements.** If the machinery must do something no gathered requirement states (a retry, a rate limit, what data may leave the system), that is a specification gap: raise it in Phase 2 as a proposed requirement. Do not design a behavior no requirement asks for.
- **The record.** Phase 4 updates the row of each FR the design realizes in `docs/traceability.md`. An FR whose row is already past `📐 Designed` keeps its Build and Verify; only its Design cell gets the link. An `SI-*` has no row of its own; name it in the design's *Realizes* line with the FRs, which is also how `/implement` finds the design.

If no target is given, ask what to design, or list the rows in `docs/traceability.md` (use cases and non-use-case FRs) whose **Build** is `❌ Not started`, earliest **Release** first.

Work in phases. **Draft the design yourself; do not ask the developer to sketch or draft anything first.** Phase 2 stops for approval before the document is written.

## Phase 1: understand the specification (read only)

Read widely but skeptically. Note anything that looks wrong and raise it in Phase 2, or sooner if it blocks you.

1. **The use case** in `docs/requirements/use-cases.md`. Find it by its identifier rather than reading the whole file. Capture the actors, trigger, preconditions, postconditions, main success scenario, every extension, the Business Rules field, and Associated Information.
2. **Its business rules** in `docs/requirements/business-rules.md`, each `BR-*` the use case cites, and any `FR-*` or quality attribute in `docs/requirements/software-requirements-specification.md` it depends on. Confirm every cited identifier exists.
3. **The vocabulary** in `docs/requirements/project-glossary.md`. Use its terms in the design; introduce no synonyms.
4. **Open questions** in `docs/requirements/OPEN-ISSUES.md` that touch this use case.
5. **The architecture-of-record**, `docs/design/architectural-design.md`: the use case area's component, the containers, the ranked architecturally significant requirements, and **section 8 (Crosscutting Concepts) in full**. Section 8.2's rules (error handling, time, and the rest) are binding on this design; cite them, do not restate them.
6. **What already exists**: the row in `docs/traceability.md`, and `docs/design/<area>.md` if the area already has a design. One document per area: if it exists, you are revising it in place for this use case.
7. **The template**, `docs/design/design-of-record.md` if the team keeps it there, or the course copy at https://github.com/tcu-cosc-40943/course-templates/blob/main/design/design-of-record.md. Its italic instructions are part of the brief. Read them, except its first step ("Sketch it yourselves first"): you draft directly.
8. **The existing code** the area touches, if any. The design extends what exists. Record the commit of `main` you read for the template's *Designed against* line.
9. **The team's charter** (`CLAUDE.md` or `AGENTS.md`) for project-wide constraints and the things the agent must not do.

## Phase 2: draft the design and wait

Draft every section of the template **in the proposal itself**, so the shape is reviewed now while it is cheap to change:

- **Realizes / Depends on**: the `UC-*` and `FR-*` identifiers, and the `BR-*` and constraints it builds on.
- **Sequence diagram** of the main success scenario in mermaid, with each interaction labeled by the use case step it implements. Add a class diagram for new structure, an ER diagram for the data change, and a state diagram for any lifecycle.
- **Components and classes**, each marked reused or new, as a pointer to the file where one exists.
- **API contract**, one row per endpoint or scheduled job: caller and who may call it, request fields, success response, and the error each extension returns, in the error shape section 8.2 fixes. **Never drop this section.**
- **Key decisions**, only the ones a reader could not recover from the code, each naming the alternative it rejected and why. If you cannot name a rival, it probably is not a decision.
- **Data model**: the change only, or "No change" with its reason.
- **Tests**: one row per flow, the main success scenario and **every** extension, with the level and what the test asserts. No code. `/implement` writes exactly these.
- **Changes to the architecture-of-record**, or "None".
- **Open questions and risks.**

**Then list what you had to assume:** every point the specification, the architecture, and the code did not settle. That list is context the specification is missing; propose where each item belongs (the specification, the charter, or this design), and ask the developer about each one.

**Watch your own scope.** Every interaction in the sequence diagram must name a use case step. An interaction with no step is a missing requirement, which goes to the specification and the client, or scope creep, which comes out. Do not add an admin override, a retry queue, a status field, or a notification the use case does not ask for.

**Present the draft and the list of assumptions in plan mode, and wait for the developer to accept the shape.** Accepting the shape lets you write the document. It is not the approval: that is a teammate's review of the pull request in Phase 4. **Edit nothing in Phase 2.**

## Phase 3: write the design-of-record (after the shape is accepted)

Work on a branch, never on `main`. Write or revise `docs/design/<area>.md` from the template, named for the lowercase area code (`eva.md` for `UC-EVA-*`):

- **One document per area.** If the file exists, append this use case's identifiers to *Realizes*, append its sequence diagram, API contract rows, and test rows, and revise the overview, class diagram, and data model in place. Never add a `## UC-…` section that repeats the skeleton.
- **Cite, do not restate.** Link the use case, the rules, and the architecture-of-record.
- **Pin down what a wrong guess would break**, and leave the rest (names, field types, exact JSON) to the build.
- **A change to the architecture-of-record** that the developer accepted in Phase 2 goes into `docs/design/architectural-design.md` in the same branch, listed under "Changes to the architecture-of-record". Never make one the developer has not seen.
- **A specification defect** the developer agreed to fix is edited in `docs/requirements/` on the same branch, and a question only the client can answer goes into `OPEN-ISSUES.md`.

## Phase 4: record the design and open the gate

1. In `docs/traceability.md`, on the branch, set the use case's **Build** (or each realized FR's) to `📐 Designed` and **Design** to `design/<area>.md`, and leave Code, Tests, and Verify empty for `/implement` to fill. The row becomes true when the pull request merges, which is what `📐 Designed` means.
2. **Run the questions test** in a fresh session: tell the developer to open a new agent session in plan mode and give it only the use case, its business rules, section 8 of the architecture-of-record, and the design, with the prompt in the template's last section. For each guess on the list, fix the design or keep it with a one-line reason a wrong guess breaks no requirement.
3. **Commit** the design, the traceability row, and any specification fix, and draft the pull request description from `.github/PULL_REQUEST_TEMPLATE.md`: the use case under Traces to; the assumptions and what the challenge found, and the specification edits they caused, under What changed; the questions test in a collapsed `<details><summary>Questions test</summary> … </details>` block under How it was verified; and under Reviewer focus, the decisions most likely to be wrong and any change to the architecture-of-record.
4. **Hand off.** Tell the developer the design is on a branch with a pull request ready. **It is approved when a teammate who did not write it reviews and merges it.** After it merges, run `/clear` and then `/implement` with the same handle (the UC-ID, FR-ID, or subsystem name) in a fresh session, which reads the merged design rather than this conversation.

The method behind these steps is Phase C of the course's [method](https://washingtonwei.github.io/cosc-40943/method/), and the worked example is Project Pulse's [`not.md`](https://github.com/Washingtonwei/project-pulse/blob/main/docs/design/not.md).
