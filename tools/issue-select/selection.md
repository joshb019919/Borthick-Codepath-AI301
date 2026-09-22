# FIRST RUN

python eval/run_eval.py --rubric skill/rubric.md --gold eval/gold-labels.json 
grading 20 bundle(s) with rubric.md, model sonnet, 5 worker(s)...
  issue-02: reject
  issue-04: reject
  issue-01: reject
  issue-05: reject
  issue-03: reject
  issue-07: reject
  issue-08: reject
  issue-06: reject
  issue-09: reject
  issue-10: reject
  issue-11: reject
  issue-13: reject
  issue-14: accept
  issue-16: reject
  issue-12: reject
  issue-15: reject
  issue-17: reject
  issue-19: reject
  issue-18: reject
  issue-20: reject

item      gold    verdict  agree  note
issue-01  accept  reject   NO     failed: Issue response latency (preferred), Model is decided upon
issue-02  reject  reject   yes    
issue-03  reject  reject   yes    
issue-04  accept  reject   NO     failed: Issue response latency (preferred), Model is decided upon, Contribution policy, Dedicated AI policy files
issue-05  reject  reject   yes    
issue-06  accept  reject   NO     failed: Recent default-branch commits, Issue response latency (preferred), Release recency
issue-07  reject  reject   yes    
issue-08  reject  reject   yes    
issue-09  accept  reject   NO     failed: Issue response latency (preferred), Claim comments, Dedicated AI policy files
issue-10  reject  reject   yes    
issue-11  accept  reject   NO     failed: Issue response latency (preferred), Model is decided upon
issue-12  reject  reject   yes    
issue-13  reject  reject   yes    
issue-14  accept  accept   yes    
issue-15  reject  reject   yes    
issue-16  accept  reject   NO     failed: Issue response latency (preferred), Model is decided upon, Dedicated AI policy files
issue-17  reject  reject   yes    
issue-18  reject  reject   yes    
issue-19  accept  reject   NO     failed: Issue response latency (preferred), Model is decided upon
issue-20  reject  reject   yes    

# SECOND RUN

python eval/run_eval.py --rubric skill/rubric.md --gold eval/gold-labels.json --save-run eval-run-9-22-7:52AM.txt
grading 20 bundle(s) with rubric.md, model sonnet, 5 worker(s)...
  issue-01: accept
  issue-02: reject
  issue-03: reject
  issue-04: accept
  issue-07: reject
  issue-06: reject
  issue-05: reject
  issue-09: accept
  issue-08: reject
  issue-11: accept
  issue-12: reject
  issue-13: reject
  issue-10: reject
  issue-14: accept
  issue-17: reject
  issue-16: accept
  issue-18: reject
  issue-19: accept
  issue-20: accept
  issue-15: reject

item      gold    verdict  agree  note
issue-01  accept  accept   yes    
issue-02  reject  reject   yes    
issue-03  reject  reject   yes    
issue-04  accept  accept   yes    
issue-05  reject  reject   yes    
issue-06  accept  reject   NO     failed: Issue response latency (preferred), Release recency, Dedicated AI policy files
issue-07  reject  reject   yes    
issue-08  reject  reject   yes    
issue-09  accept  accept   yes    
issue-10  reject  reject   yes    
issue-11  accept  accept   yes    
issue-12  reject  reject   yes    
issue-13  reject  reject   yes    
issue-14  accept  accept   yes    
issue-15  reject  reject   yes    
issue-16  accept  accept   yes    
issue-17  reject  reject   yes    
issue-18  reject  reject   yes    
issue-19  accept  accept   yes    
issue-20  reject  accept   NO     graded accept

# CHANGES

Removed:

| model is decided upon | issue text or acceptance criteria | one suggested or required fix, not a list of possible fixes; tool model already decided upon, acceptance criteria being full denotes the author knows this | required |

Made the following 3 months instead of 3 weeks:

| Issue response latency | "maintainer first-response sample" under Repo facts or open a few recently updated issues (Issues tab, sort by recently updated) and see how long the first reply from someone with an Owner, Member, or Collaborator badge took | last response within 3 weeks | preferred |

Added "within 6 months" to the following:

| Claim comments | the Comments section or read the thread for "I'll take this", "can I work on this", "working on this"; note the date and whether a maintainer answered | 0 claims within 6 months | required |

Changed the following from 'allows "AI assisted" for this course' to 'does not say anything related to "no AI allowed"':

| Contribution policy | the "contribution policy" line under Repo facts or `CONTRIBUTING.md` in the repo root or `.github/`, and any contributor docs it links out to | does not say anything related to "no AI allowed" | required |
| Dedicated AI policy files |  files like `AI_POLICY.md` or `AI_USAGE_POLICY.md`; an `AGENTS.md` file is the opposite signal, instructions written for AI coding agents or quoted or summarized on the same line | does not say anything related to "no AI allowed" | required |

Updated the verdict rule to match these changed requirements and added the following:

Anything marked "required" is necessary to adhere to the check to pass, or it fails.
