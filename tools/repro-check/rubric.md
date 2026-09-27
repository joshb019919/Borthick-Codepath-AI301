# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| env record | the claim comment or repro report  | the claim comment names the tool version and the OS | required |
| env match | the claim comment or repro report and repo facts block | the recorded environment (tool version, OS) match the issue or specify mismatch | required |
| steps | the claim comment or repro report | if a stranger could re-run the steps without guessing | required |
| behavior match | the claim comment or repro report and repo issue text | the reproduced issue behavior, if reproduced, matches the issue text | required |
| reproduced | the repro report's record | whether or not the issue was reproduced | required |
| no promises | the claim comment or repro report | no promises of completion date | required |
| no pressure | does not pressure the maintainer(s) into an assignment or acceptance | required |
| ai disclosure | the claim comment or repro report | aligns with ai use requirements in issue text or repo facts (contributing, ai policy, etc.) | required |
| polite | the claim comment or repro report | no cursing or swear words, no fatalistic tone | preferred |
| actual vs expected | the claim comment or repro report and issue text | reproduces the actual versus expected log | preferred |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Pass if all required checks pass.  Preferred checks never fail and are only used to rank results.
An honest reproducibility of "cannot reproduct" is a pass, but a confident wrong-target is a fail.
Anything that looks like it was written by AI will fail.
A conversational tone can still contain technical wording, but not be overly enthusiastic.
Anything that suggests they are moving toward a next action or asks if this is a good first issue passes the "no promises".
"Pressure" shall be considered begging for assignment or trying to rush or otherwise pressure maintainer(s).
If the repo facts, issue text, or contributing, disclosure, or ai use policy are required but the claim mentions nothing about it, it fails.
