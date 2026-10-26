# Course templates

Blank templates for the documents your team writes this semester, for **COSC 40943, Software Engineering**, and the senior design sequence it starts.

## Get them into your repository

These files belong in your **team repository**, next to your code. That is not a filing preference. Your AI teammate reads your repository and nothing else, so a specification that lives in Google Drive is a specification your agent cannot use.

Clone this repository somewhere outside your project, then copy the folder you need into `docs/`:

```bash
git clone https://github.com/tcu-cosc-40943/course-templates.git
cd your-team-repo
mkdir -p docs
cp -r ../course-templates/requirements docs/
cp ../course-templates/traceability.md docs/
cp -r ../course-templates/design docs/
```

That gives you `docs/requirements/` with all seven files, `docs/traceability.md`, and `docs/design/`. On Windows, copy them in File Explorer if you prefer. Then commit them on a branch and open a pull request, the same way as any other change.

Do not fork this repository. You are copying files into your own project, not tracking this one.

## What is here

### `requirements/`

**Before your first client meeting**, this one:

| File | What it holds |
|---|---|
| `client-interview-guide.md` | Your question script for a client meeting, and the record of what was said in it |

Work it with your agent before you walk in, take it into the meeting on the scribe's laptop, and commit it the same day. Copy it once per meeting as `client-interview-YYYY-MM-DD.md`, so the template stays blank for the next one.

**Week 3**, start these three:

| File | What it holds |
|---|---|
| `vision-and-scope.md` | Why the project exists, what success looks like, who the stakeholders are, and where the line falls between in scope and out |
| `project-glossary.md` | The project's vocabulary, one word per concept |
| `OPEN-ISSUES.md` | Every question you cannot answer yet, and who can answer it |

**Week 4**, these three:

| File | What it holds |
|---|---|
| `use-cases.md` | One goal per use case, written as the dialogue between actor and system, including the paths where it fails |
| `business-rules.md` | The policies, regulations, and formulas your client's business already has |
| `software-requirements-specification.md` | Quality attributes, interfaces, data, constraints, and links to everything above |

Copy all of them now. You will not need the week-4 files yet, and reading their instructions before your client meeting is not wasted time.

### `traceability.md`

**Week 4**, alongside the three above. It holds the links between the documents: feature to use case area, and business rule to what enforces it. It goes in `docs/`, not `docs/requirements/`, because from week 8 it also maps design, code, and tests. If you already copied `requirements/`, copy this one file now.

**Week 8:** section 3 is now drafted: one row per use case and FR, with Build, Verify, and **Release**, your release plan, due at Checkpoint 2. Your copy already holds your first two tables, so paste section 3 into it rather than copying the file again.

### `design/`

**Week 6**, for Checkpoint 1:

| File | What it holds |
|---|---|
| `architectural-design.md` | Your architecture-of-record: every use case area, component, and external system named, the requirements that shape the system, and the decisions that are expensive to change |

Each section says which checkpoint it is due at; leave the later ones as they are. If you cloned this repository earlier in the term, update your clone first, then copy the folder:

```bash
git -C ../course-templates pull
mkdir -p docs/design
cp ../course-templates/design/architectural-design.md docs/design/
```

The filled-in example is [Project Pulse's architecture-of-record](https://github.com/Washingtonwei/project-pulse/blob/main/docs/design/architectural-design.md).

**Week 7**, for your proving slice:

| File | What it holds |
|---|---|
| `design-of-record.md` | How one use case area's use cases will be built: the sequence diagrams, the API contract, the key decisions and what they rejected, and the tests that will prove each flow. One per area, written before the code and approved by pull request |

Copy it once per use case area, named for the lowercase area code, so your proving slice's area gets the first one:

```bash
git -C ../course-templates pull
cp ../course-templates/design/design-of-record.md docs/design/ord.md   # your area code, not ord
```

The template's header gives the order to write it in (sketch it yourselves, then the agent drafts, then compare) and ends with the questions test, which goes in your pull request. The filled-in example is [Project Pulse's `not.md`](https://github.com/Washingtonwei/project-pulse/blob/main/docs/design/not.md).

### `.github/`

**Week 8**, before your first implementation pull request:

| File | What it holds |
|---|---|
| `PULL_REQUEST_TEMPLATE.md` | The description every pull request starts from, whether it changes code, the specification, or a design: why, what changed, how it was verified and what was not, and where your reviewer should focus |

GitHub fills a new pull request's description from this file once it is on your default branch:

```bash
git -C ../course-templates pull
mkdir -p .github
cp ../course-templates/.github/PULL_REQUEST_TEMPLATE.md .github/
```

The comments in the template list what counts as evidence for code, for a specification change, and for a design (where the questions test goes under How it was verified, in a collapsed `<details>` block). They do not appear in the posted description, so the description stays four short sections. Fill in **Not verified** on every pull request: an honest answer tells your reviewer where the risk is, and it is not held against you.

**Keep it to one screen.** If the description will not fit, the pull request does more than one thing; split it. If your agent drafts the description, add this line to your `CLAUDE.md`: "Pull request descriptions follow `.github/PULL_REQUEST_TEMPLATE.md`: at most three lines per section (a design's questions-test list goes in a collapsed `<details>` block, outside the cap), and never restate the diff."

### `.claude/commands/`

**Week 10**, for your proving slice and every use case after it:

| File | What it holds |
|---|---|
| `design.md` | `/design <UC-ID>`: the agent reads the use case, its rules, your architecture-of-record, and the existing code, drafts the area's design-of-record from the template, lists what it had to assume, and stops before any code |
| `implement.md` | `/implement <UC-ID>`: the agent builds a merged design on a branch (any refactor first, then the trunk, then the leaves), writes a test for every row of the design's test list, checks the diff against your crosscutting concepts, and drafts the pull request |

Copy them into your repository's root and merge them by pull request. Claude Code then runs them as slash commands:

```bash
git -C ../course-templates pull
mkdir -p .claude/commands
cp ../course-templates/.claude/commands/design.md ../course-templates/.claude/commands/implement.md .claude/commands/
```

Each stops for a person where judgment goes in: `/design` when you accept the draft's shape, `/implement` before a refactor the design did not name and after the trunk commit. Neither approves its own work; a teammate reviews and merges the pull request. Run each in a fresh session. On Copilot CLI, follow the files' phases by hand, as a checklist.

**Customize them.** Once copied, they are your team's files: change them by pull request to fit your paths, stack, test commands, and the checks your reviews keep catching. Keep the stops for a person. How they work in studio: [week 10](https://washingtonwei.github.io/cosc-40943/studio/#week-10-oct-28-and-30-catch-up-on-your-proving-slice).

More folders arrive as the course reaches them.

## How to work them

Each file opens with instructions in italic square brackets: what the section is for, how to produce it, a worked example, and a checklist. Fill in underneath the instruction and **leave the instructions in place** until the document is finished. They are context for your teammates and for your agent on every later pass, not scaffolding for the first one.

Hand your agent the template, your one-page client brief, and your meeting notes, and give it a role: "You are an experienced business analyst. Using the instructions in this template, draft section X, and list every question you cannot answer from what I gave you." Its list of unanswered questions is the most useful thing it will produce. Those go in `OPEN-ISSUES.md` and become the agenda for your next client meeting.

What the agent cannot do is decide which of its questions are worth your client's limited time, or tell the difference between a client who is enthusiastic and a client who is committed. That is your job, and it is why you are in the room.

## The standard these follow

Structure and identifier conventions come from [Project Pulse's own `docs/requirements/`](https://github.com/Washingtonwei/project-pulse/tree/main/docs/requirements), the running example for this course. When you want to see what a filled-in version looks like, read that folder.

## Corrections

These templates get fixed during the semester. Check back here, or watch the repository, before starting a new section. If an instruction is wrong or unclear, open an issue.

Course site: <https://washingtonwei.github.io/cosc-40943/>
