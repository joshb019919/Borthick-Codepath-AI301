# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

The exact environment with all named components and version values to ensure the claim matches the issue.

- Where it lives:
| Signal | On github.com | In the eval bundle |
| --- | --- | --- |
| operating system | the student's draft repro report | the repro report's environment section |
| kernel | the student's draft repro report | the repro report's environment section |
| tool | the student's draft repro report | the repro report's environment section |
| browser | the student's draft repro report | the repro report's environment section |

- What good looks like:
| Signal | Match Example | Passing Mismatch Example | Failing Mismatch Example |
| --- | --- | --- | --- |
| operating system | Ubuntu 22.04+ | The issue says this bug occurs on Windows 10+, but the tool is for Windows, Mac, and Linux.  I've found that it occurs on Ubuntu 22.04+, as well, which is part of my environment. | Linux Mint (no version number, issue specifies Mac OS X) |
| kernel | Linux 5.0+ | The issue says this bug occurs on Windows 10+, but the tool is for Windows, Mac, and Linux.  I've found that it occurs on Linux 5.0+, as well, which is part of my environment. | 11 (no OS name) |
| tool | 1.4.44 | 1.4.43+ (change logs specify this version is when the feature was introduced, so all versions after this one will have this bug) | 1.4.46 (issue specifies 1.4.44 LTS) |
| browser | Firefox 145 | Firefox 135+ | Chrome 101 (issue specifies Firefox 151) |

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

The steps a stranger could reproduce the bug or test the feature without having to guess,
which match the steps listed in the issue, if listed.

Where it lives:
| Signal | On github.com | In the eval bundle |
| --- | --- | --- |
| reproduction steps | the student's draft repro report | the repro report's environment section |
| issue steps | the Github repo's issue text | the issue context block |

What good looks like (relative to a new search feature):
| Step Number | Step Example |
| --- | --- |
| 1 | Launch the website in Firefox browser. |
| 2 | Click into the search text box (top left). |
| 3 | Type a search query. |
| 4 | Press enter or click the green arrow. |
| 5 | Review the returned results and their order, including the relevance to the query. |
| 6 | Click the first three results to ensure they do link to a real web page. |

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

Where it lives:
| Signal | On github.com | In the eval bundle |
| --- | --- | --- |
| output | the student's draft repro report | the repro report |
| logs | the student's draft repro report | the repro report |
| screenshots | the student's draft repro report | the repro report |

What good looks like:
| Matching Behavior | Mismatching Behavior |
| --- | --- |
| the new search system displays most of the same results in the same order as the old search system | a new LLM question and answer bot |
| reading file contents no longer triggers the null pointer exception | changed the file content colors to a different contrast pallette |
| bug: the dependency is not found because it is not properly configured in Gradle | bug: the dependency management system is not using the most up-to-date version of Gradle |
| the user's email is now saved in the session object for cross-page persistence | the user's email is already being committed to the database |
| the user's email is not persistent across page changes (when they click a link on the same domain) | I don't understand, the user's email is showing already being saved to the database |

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

Where it lives:
| Signal | On github.com | In the eval bundle |
| --- | --- | --- |
| reproducibility | the student's draft repro report | the repro report |
| logs | the student's draft repro report | the repro report |
| skill level claims | the student's draft repro report | the repro report |

What good looks like:
| Signal | Example | Lie |
| --- | --- | --- |
| reproducibility | I've copied environment but can't reproduce the issue | I've reproduced the error (but really only looked at the code) |
| logs | These are the full, raw logs with nothing left out | Here are the logs I came across as I fixed it (reformatted, intermediate sections removed) |
| skill level claims | I notice that the new feature expects a RAG to feed ranked documents into an LLM.  I have learned to build a RAG but need help making sure the ranking system does enough | This is totally done now and works as expected (the ranking system is misranking comapred to the non-LLM approach) |

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

Where it lives:
| Signal | On github.com | In the eval bundle |
| --- | --- | --- |
| claim comment against the issue | the student's draft claim comment vs repo issue | the claim comment vs repo facts issue |
| comments against repo's stated templates and contribution policy | the student's draft claim comment vs repo issue | the claim comment vs repo facts issue |
| AI-use disclosure | the student's draft claim comment vs issue text or disclosure or use policy | the claim comment vs repo facts or issue |
 
What good looks like:
| Issue Requirement | Claim Comment |
| --- | --- |
| AI is allowed to help with code but comments must be hand-written | I used Claude Code to help teach me what I needed and in debugging but I wrote the code and these comments, myself |
| We need new min and max functions that take more than two arguments | I have developed new functions to find the min or max of an arbitrary number of arguments |
| We'd like a new search system that implements RAG with an LLM instead of classic information retrieval in our website | Here are my suggestions for the system (which ranking, which LLM base, fine-tuned or not, etc.) |
| Strict AI policy: contributors must understand their submissions | AI built this code, here you go (demonstrates no understanding of AI-generated code) |
| No AI Allowed | AI built this code or helped me debug |
| No AI Allowed | (code and/or comments are such that the are obviously AI-generated, even if comments say otherwise) |
