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
