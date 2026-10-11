# Traceability Matrix

**Project:** _[Your project name]_
**Team:** _[Team NN]_
**Version:** 0.1
**Last checked:** _[YYYY-MM-DD, by whom]_

---

_**How to use this template.** Instructions appear in italic square brackets. Fill in underneath them and leave them in place until the document is stable._

_**What this file is.** The map of your project, from the reason something exists to the thing that does it. Every other document owns its own contents; this one owns the **links between them**, so nobody has to restate anything to find out what connects to what._

_**Why it exists before any code does.** The question it answers in week 4 is "did we specify everything we promised, and nothing we did not?" The question it answers in week 12 is "this broke, what was it supposed to do, and who asked for it?" Those are the same question, and the file that answers the second one is the file you started in week 4. Starting it later means reconstructing links from memory, which is the same work done worse._

_**It grows.** Week 4 fills in the first two tables. Week 8 adds the third, which links each use case to its design, code, and tests and carries your release plan._

_**Run the checks by hand this week.** Each table below ends with two checks. They are cheap, and they fail loudly. Hand the whole file to your agent and ask it to run them, then verify what it tells you, because a check reported as passing by the thing that also wrote the table is not evidence._

---

## 1. Feature to use case area

_[Your vision and scope lists product **features** (`FEAT-<slug>`), each a capability a stakeholder can see. Your use case file groups behavior into **use case areas** (`UC-<AREA>-*`). This table connects them, and it is where **business objectives attach**: the objective hangs on the feature, and every use case underneath inherits it. That is why the objective is named here once, rather than repeated on forty use cases._

_Features and areas are deliberately many-to-many. A feature that lands on exactly one area is probably too narrow, and a feature that reads "create, edit, and delete X" is a list of use cases wearing a feature's clothes._

_Worked example, from Project Pulse:]_

| Feature | Business objectives | Use case areas |
|---|---|---|
| `FEAT-performance-tracking` | `BO-PERF-instructor-efficiency`, `BO-PERF-student-participation` | `WAR`, `EVA` |
| `FEAT-administration` | (enabling, serves no objective directly) | `SEC`, `TEA`, `STU`, `INS`, `ACC`, `RUB` |

_[An enabling feature that serves no measurable objective on its own says so, as the second row does. That is different from forgetting to fill the column in.]_

**Checks.**

1. **Every feature has at least one area.** A feature with none means your vision promises something nobody has specified.
2. **Every area is reached by a feature.** An area no feature points at means you have use cases no stakeholder asked for.

---

## 2. Business rule to what enforces it

_[A business rule is a property of your client's business, so it has no implementation of its own. What it has is a set of requirements that enforce it, and this table is how you find them. Rules are **cited, never restated**: the rule's text lives in `business-rules.md` and nowhere else, and this table holds only the identifier and the links._

_The **Source** column is duplicated here from `business-rules.md` on purpose, and it is the one exception in this file. It is the column reviewers and clients actually read, and a rule whose source is one click away is a rule nobody checks._

_Worked example, from Project Pulse:]_

| Business rule | Source | Enforced by |
|---|---|---|
| `BR-evaluation-submission-window` | Not recorded | `UC-EVA-submit-evaluation` step 7 and extension 1b |
| `BR-section-admin-only` | Not recorded | `UC-RUB-assign-rubric`, `UC-SEC-create-section`, `UC-SEC-edit-section`, `UC-SEC-setup-active-weeks` |

**Checks.**

1. **Every rule is enforced by something.** A rule with an empty third column is a policy your software ignores. That may be the right answer, and it is only the right answer if you decided it on purpose. Write the decision in `OPEN-ISSUES.md` rather than leaving the cell blank.
2. **Every requirement that cites a rule cites one that exists.** Search your use cases and specification for every `BR-` identifier and confirm each one is defined in `business-rules.md`. This is the check that catches a draft citing `BR-late-penalty` because a late penalty is the kind of thing a course usually has. A generated document cites plausible identifiers with complete confidence, and nothing else in your process will notice.

---

## 3. Use case to design, code, and test (week 8)

_[In week 8 the spine extends past the use case: **business objective → feature → use case area → use case → design → code → test.** This table has one row per use case, plus one row per non-use-case FR (`FR-<AREA>-<slug>`) that needs building. Add a row the day a use case is written, not the day it is built._

_**Build** and **Verify** are two separate states, so that a use case which is built but untested stays visibly unverified rather than being absorbed into a single "done":_

- _Build: `❌ Not started`, `📐 Designed` (its design pull request merged), `🟡 In progress`, `✅ Built`. It says nothing about tests._
- _Verify: `✅ Verified` (tests cover the main flow and every extension, and pass), `🟡 Partial` (the Tests cell names the gap), `🔎 None`, or left blank while there is nothing built to verify._

_**Release** is your **release plan**: the release the row's code ships in. It tracks the build only; a shipped row with missing tests keeps its Release, and the gap shows in Verify. Use `v0.1.0` (the proving slice, Checkpoint 2), `v0.2.0` (Checkpoint 3), `v1.0.0` (the December MVP), `Spring`, or `Out`. Every row has one by Checkpoint 2; an empty cell is work nobody planned. Place rows by risk first, then by what your client needs first, then by dependency, and change a Release cell only by pull request, saying why. Your client's agreement on scope by feature stays in vision and scope's MVP Scope section; this column carries it down to use cases. How to forecast from it: [Process and Planning](https://washingtonwei.github.io/cosc-40943/modules/process-and-planning/#46-from-estimates-to-a-release-plan)._

_Worked example, from Project Pulse, which numbers its releases from its own tags:]_

| Use case or FR | Build | Verify | Release | Design | Code | Tests |
|---|---|---|---|---|---|---|
| `UC-EVA-submit-evaluation` | ✅ Built | ✅ Verified | `≤ v1.5.0` |  | `EvaluationController.addPeerEvaluation`, `SubmitTeamsEvaluations.vue` | `EvaluationServiceTest`, `EvaluationIntegrationTest` (main flow and extensions) |
| `UC-NOT-remind-non-submitters` | 📐 Designed |  | `v1.6.0` | `design/not.md` |  |  |
| `FR-NOT-weekly-reminder` | 📐 Designed |  | `v1.6.0` | `design/not.md` | `WeeklyReminderScheduler` (predates the amended requirement) | `WeeklyReminderSchedulerTest` (predates it too) |
| `UC-AI-critique` | ❌ Not started |  | `v1.8.0` |  |  |  |

**Checks.**

1. **Every use case and FR has a row, and every row has a Release.** A missing row is a requirement nothing tracks; an empty Release is work nobody planned.
2. **Nothing reads Verified without a test you can name.** Open the test cited in each `✅ Verified` row and confirm it exercises that use case, extensions included.

---

## Working this document with your agent

_[Delegate: running both checks and reporting what fails; finding every `BR-`, `FEAT-`, and `UC-` identifier cited anywhere in `docs/` and listing the ones with no definition; regenerating the second table from the Business Rules fields of your use cases after you have edited them._

_Keep human: whether an area with no feature is a missing feature or a use case that should not exist, and whether an unenforced rule is an oversight or a decision. Both are questions about your client's business, and the answer is not in your repository._

_**The specific failure to watch for:** an agent asked to "fill in the traceability matrix" produces a complete, well-formed table in which every cell is populated and some of the links are invented. A blank cell is information. A confidently wrong link is worse than no link, because it makes the check pass. Verify every row you did not write yourself by opening the document at the other end.]_
