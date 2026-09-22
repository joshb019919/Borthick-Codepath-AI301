# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Recent default-branch commits | "last 5 default-branch commits" under Repo facts or the repo's front page: the line above the file list shows the newest commit and its date; click the commit count next to it to see the recent history | last commit within 2 months | required |
| Issue response latency | "maintainer first-response sample" under Repo facts or open a few recently updated issues (Issues tab, sort by recently updated) and see how long the first reply from someone with an Owner, Member, or Collaborator badge took | last response within 3 months | preferred |
| Release recency | "latest release" under Repo facts or the Releases box in the right sidebar of the repo front page: the latest release and its date | last release within 6 months | required |
| Archived flag | "archived:" on the repo line or an archived repo shows a "This repository has been archived" banner across the top and is read-only: hard dead | no | required |
| Adoption scale | stars on the repo line or the star count at the top of the repo page; for libraries, the "Used by" counter in the right sidebar | 3 stars | preferred |
| Assignee | "this issue: assignees:" under Repo facts or the Assignees box in the issue's right sidebar | 0 people | required |
| Linked PRs | "linked PRs:" with state per PR, plus any PRs mentioned in the Comments section or the Development box in the issue's right sidebar lists formally linked PRs: an open one is an active claim | 0 linked, open PRs | required |
| Claim comments | the Comments section or read the thread for "I'll take this", "can I work on this", "working on this"; note the date and whether a maintainer answered | 0 claims within 6 months | required |
| Contribution policy | the "contribution policy" line under Repo facts or `CONTRIBUTING.md` in the repo root or `.github/`, and any contributor docs it links out to | does not say anything related to "no AI allowed" | required |
| Dedicated AI policy files |  files like `AI_POLICY.md` or `AI_USAGE_POLICY.md`; an `AGENTS.md` file is the opposite signal, instructions written for AI coding agents or quoted or summarized on the same line | does not say anything related to "no AI allowed" | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Basically speaking, maintainer must be alive and active, the repo must be active and maintained with a recent release, the issue must not have any PRs already requested or assigned within the last 6 months, and the repo may not require "no AI."  Anything assigned to fellow CodePathers is not counted as "taken."

All "unclear" except this AI use policy is rejected.  An unclear AI use policy could be missing, and can be accepted in this case.  If it is not well worded and AI cannot help me recognize it's use policy from this wording, this issue is rejected.

