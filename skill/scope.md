# Scope: where your issue lives, and its house rules

<!--
This file is the skill's field of view, live mode only: in eval mode
the bundle is the whole world and this file is ignored. The rubric
(rubric.md) decides whether a plan package is READY; the scope decides
which issues a package may belong to at all, and what the house rules
are where that issue lives.

Staff wrote this file. Edit only the `Repo:` line below.
-->

## Where your issue lives

Only issues in the course's Path Review repository are in scope:

- Repo: `<ORG>/<PATH-REVIEW-REPO>` <!-- replace the placeholder with your Path Review repo, shown in step 1 of the Unit 3 Assignment tab -->

If the repo line above still reads as a bracketed placeholder, live
mode stops without grading until the student replaces it with their
Path Review repo. Eval runs never read this file, so they work either
way.

Your plan must belong to the issue you reproduced in unit 2 (or the
house issue a TF gave you). Do not grade plan packages
for issues in any other repository, however tempting; the wider GitHub
comes later in the course.

## Path Review house rules

Everyone posting in your Path Review repo is a classmate, so the house
rules from unit 2 still apply to plans:

- **A classmate's plan comment does not block yours.** Other students
  may post plans on your issue (and several may). Post your own plan
  comment anyway, in your own words, built from your own reproduction;
  this course is the coordination channel that strangers do not have.
- **Never piggyback a plan.** "Same approach as above" is not a plan
  comment. Your plan is your work: your diagnosis from your evidence,
  your scope, your test plan, even on a shared issue.
- **Branch on your own fork, named `<type>/<issue-number>-<slug>`.**
  The type is `fix`, `docs`, `feat`, `test`, `refactor`, `perf`, or
  `chore` (for example, `fix/1234-null-check`). The build happens on
  your fork of the Path Review repo, one branch per issue, so parallel
  fixes never collide. Push the branch to your fork; nobody pushes to
  the shared repo.
- **Credit attaches to the PR you open in unit 4.** Course credit
  rides on your posted plan, your branch, and the pull request that
  follows, not on being first, so a shared issue costs nobody
  anything.
