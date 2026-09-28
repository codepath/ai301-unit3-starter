# AI301 Unit 3 starter: plan-check

Materials for Unit 3 of AI301 (Plan and Build): the plan-check skill
and its eval harness. The steps are on the course portal's Unit 3
Assignment tab. This repo is what those steps tell you to install and
run.

## What's here

- `skill/`: the plan-check skill for Claude Code. You write three of
  its files: `rubric.md`, `procedure.md`, and
  `references/evidence-guide.md`. `voice-guide.md` takes your Unit 2
  voice guide, and `scope.md` takes your Path Review repo.
- `eval/`: the eval harness, the gold labels (the staff answer key),
  and 24 practice submissions, which the harness calls packages: 20
  scored, plus the 4 calibration files (`calib-01` to `calib-04`) from
  the class activity. See `eval/README.md` for the full run and output
  guide.

## Install the skill

Clone this repo, then copy `skill/` into Claude Code's skills folder:

    git clone https://github.com/codepath/ai301-unit3-starter.git
    mkdir -p ~/.claude/skills
    cp -R ai301-unit3-starter/skill ~/.claude/skills/plan-check

If `~/.claude/skills/plan-check` already exists, delete it first.
Otherwise `cp` puts the files in `plan-check/skill/` and Claude Code
won't find them.

Then open `~/.claude/skills/plan-check/scope.md` and replace the
placeholder on the `Repo:` line with your Path Review repo (step 1 on
the Assignment tab shows it).

Edit `rubric.md`, `procedure.md`, `references/evidence-guide.md`, and
`voice-guide.md` inside the installed copy. The eval and live runs
below both read from that copy, so they always grade with the same
files.

## Run the skill

The skill runs in two modes. Both need the Claude Code CLI (`claude`)
installed and signed in.

### Eval mode: grade the 20 practice submissions

Run from this repo's `eval/` folder:

    cd ai301-unit3-starter/eval
    python3 run_eval.py \
        --rubric ~/.claude/skills/plan-check/rubric.md \
        --evidence ~/.claude/skills/plan-check/references/evidence-guide.md \
        --save-run eval-run.txt

The harness finds `procedure.md` next to your rubric. A full run costs
about $4 of course credit and writes `eval-run.txt`, the file you
submit. Keep `--save-run` on every full run, so the file always holds
your latest one. Runs with `--limit` or `--only` never write it, so a
quick re-check can't overwrite your full run.

You're aiming for 18 of the 20 agreeing with the gold labels, with at
least one match in every category on the output's `categories:` line.

Add these flags as you need them:

| Flag | What it does | When to use it |
|---|---|---|
| `--limit 3` | Grades only the first 3 | Checking that your setup works |
| `--only pkg-07,pkg-12` | Grades only the ones you name | Re-checking the ones you disagreed on, about $0.20 each instead of about $4 for a full run |
| `--include-calibration` | Also grades the 4 calibration files (never scored) | Checking your rubric on files your class already graded; it works with `--only` |
| `--out results.json` | Saves every check's result as JSON | Digging into why one failed |
| `--workers N` | Grades N at once (default 5) | Rarely needed |

`python3 run_eval.py --help` lists every flag. `eval/README.md`
explains the output table.

### Live mode: check your plan before you post it

Live mode grades your own plan and plan comment for your real issue,
before the comment goes up on GitHub.

Save your drafts as `plan.md` and `comment.md` in the top folder of
your fork's clone. Then, from that folder, run the skill in either of
these ways, with your issue's URL in place of `<URL>`.

**Inside a Claude Code session.** Start `claude` in that folder, then
type the skill's name as a slash command:

    /plan-check grade my plan in plan.md and draft comment in comment.md for issue <URL>

A session is the easier option when you're revising, because you can
ask about a failed check and re-run after each edit.

**As one command from your terminal.** Put the same request in quotes
after `claude`:

    claude "plan-check: grade my plan in plan.md and draft comment in comment.md for issue <URL>"

If your build ends up different from the plan, re-run it after you
update the `## Deviations` section, because the skill grades that
section like the rest of the plan.

**Reading the result.** The last thing the skill prints is a block
like this:

```json
{
  "item": "https://github.com/owner/repo/issues/123",
  "checks": [
    {"name": "diagnosis-follows-repro", "grade": "pass",
     "evidence": "the stated cause matches the failing test output in the repro"},
    {"name": "scope-bounded", "grade": "fail",
     "evidence": "the plan says it will 'clean up the module' and names no files"}
  ],
  "verdict": "reject"
}
```

- `verdict` is the answer. `accept` means the plan is ready to post
  and build from, and `reject` means revise it first.
- `checks` shows why. There's one entry per check in your rubric, so
  the names match whatever you called your checks. The `evidence` line
  is what decided each check, so read the failed ones first.

If it stops with a message about scope, the `Repo:` line in
`scope.md` still has the placeholder. If the output doesn't end with
this block, the skill never ran and Claude answered on its own. Check
that the skill is installed at `~/.claude/skills/plan-check/`, then
try again.
