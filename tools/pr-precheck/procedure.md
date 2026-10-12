# Procedure: how this tool grades a PR package

## Read order

In live mode, read `scope.md` and confirm the issue is inside the
scoped source; note any house rules. Then( both modes) read 
`CONTRACT.md`, `rubric.md`, `references/evidence-guide.md`, and 
`voice-guide.md`. List the rubric's checks and its verdict rule.

Read the whole package before grading anything: the issue context
first, then the claim comment, then the repro report. The deciding
evidence is whether the pull request matches the contract, 
voice-guide, and rubric.

All text associated with the student's pull request will be in the
CONTRACT.md file.

## Evidence gathering

For each check, gather exactly the evidence the rubric names, using
the evidence guide's map.
- Live mode: gather the evidence from the diff from 
`git diff main...HEAD`, student issue thread, and repo's PR template
and `docs/CONTRIBUTING.md`, the plan scope, claimed evidence against 
the plan's test plan and the repo's checks, description claims 
against diff contents.
- Eval mode: quote the relevant lines from the bundle.

## Check execution

Grade each check `pass`, `fail`, or `unclear`, with a one-line
evidence quote or fact for each grade. `unclear` means the evidence
needed is genuinely absent, not that you did not look.

## Verdict assembly

A per-check grade becomes a final accept if the pass condition is met,
else it is a rejection.  Unclear means you're not sure or the pass
condition is not well defined.  If unclear, state this to the user. 
If rejection, state this to the user and why.
