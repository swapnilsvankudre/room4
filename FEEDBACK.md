# Overnight review: Larkspur disruption-care agent

**To:** swapnilsvankudre_room4  
**From:** Larkspur client review agent, on behalf of Priya Raghavan  
**Re:** the disruption-care agent you walked us through in our last session  
**Generated:** 2026-09-22 17:24

## Priya's note

> Our vendor says we should just be using your best model.
>
> Why aren't we?
>
> Priya Raghavan, Larkspur Airlines

She sent that before this session opened. She means it. A vendor told her to buy
the biggest model, and she has a number to defend upstairs. Her four questions from
day one are still open. Naming a model answers none of them.

## Still open from day one

| Her question | What she means by it |
| --- | --- |
| **What it costs** | Per resolved contact, against the $6.90 a human contact costs us. |
| **When it is wrong** | The first untrue thing it says, and what happens after that. |
| **Who runs it** | In June, after you have left. |
| **What you left out** | The scope you cut, and why. |

## What the review agent found

Overnight, Larkspur pointed a review agent at your repository. It read the
code. It did not run your agent, and the only file it changed is this one. Each
item below names the file and the line it is about.

**1. PITCH.md reports a 24.1% token increase after moving next_available_day to the MCP server, with no bench file to check it.**

PITCH.md states 62,818 input tokens per pass before Build 2 and 77,974 after, attributing the rise to two registered tools that fired zero times costing 792 input tokens per turn. The diff confirms tool_list() now returns build_tools() plus mcp_client.tools(), which the comment says also carries fare_rules alongside next_available_day. No bench-after.json or bench-before.json exists in the file list to back the two totals or the 792 figure.

Run python3 bench.py --compare before after and paste the token totals it prints.

**2. search_alternatives description grew from 6 characters to 462, but readout-trace.json never shows it called.**

The diff replaces the placeholder description "search" with 462 characters specifying option_id, departure time, and a warning to never invent a flight. The last committed wire run only calls lookup_booking and next_available_day, tool calls: 2, so nothing in the run evidence exercises the new description against a live model turn.

Run python3 run.py K7PQ2M --trace on a case that triggers search_alternatives and paste the tool call sequence.

**3. TONE_ADDENDUM is 0 characters while PITCH.md names tone as the open gap.**

The static scan confirms TONE_ADDENDUM: still empty (0) characters. PITCH.md's Still broken line states "the abusive-message ticket gets a calm, helpful, entirely correct answer and no gate fires" and that nothing watches tone. This is a policy gap in SYSTEM_PROMPT composition, not a model capability question: a bigger model reading the same empty TONE_ADDENDUM has nothing to enforce a tone check with either.

Run python3 verify.py 4.1 to see whether a tone gate exists and paste its output.

**4. Gates 1.2, 1.3, 1.4, 2.1, 2.2 are banked in readout.html; no eval case file exists to say what they graded against.**

The evidence block lists gates banked: 1.2, 1.3, 1.4, 2.1, 2.2, banked by Ali Chadli on 2026-09-22T14:39:35. There is no evals/cases.json in this repository, so the banked gates rest on the single wire run in readout-trace.json (3 API turns, 2 tool calls, 11559 in / 342 out tokens) rather than on a labeled suite.

Run python3 eval_harness.py and paste the pass count against the banked gate list.

**5. PITCH.md's Next line admits no answer from this agent has been graded for correctness, only for cost and completion.**

The line reads "eval cases that grade whether the answers are actually right, which nothing does today," and Still broken repeats "no answer this agent gives has ever been graded for correctness." The 5/5 answered figure quoted in Number refers to whether a response was produced, not whether it was correct, per PITCH.md's own distinction. This gap sits above the model layer entirely: swapping MODEL changes nothing about whether an unwritten eval suite catches a wrong policy_row_id or a bad voucher amount.

Paste evals/cases.json once written, or run python3 eval_harness.py and show a correctness metric distinct from completion.

## Your four answers

The four lines under `## Priya asked` in your PITCH.md are still empty. They
are one line each and they are not a coding job: cost, what happens when it is
wrong, who runs it in June, and what you left out. Whoever on your side is not
editing agent.py is the right person to write them, and they are the four
things I will ask about first.

## Before our next meeting

> Before our next meeting, tell me: which model should we be on, and how will you prove it is the right call?
>
> Priya Raghavan, Larkspur Airlines

Bring two things. A recommendation, and the measurement behind it. If the model is
not the problem, say so, and bring the number that shows it.

## What this review read

- `agent.py (253 lines)`
- `PITCH.md`
- `TEAM.md (unchanged template)`
- `readout-trace.json`
- `readout.html (evidence block)`

Reviewer: `claude-sonnet-5`. Static read only: nothing in this repository was executed, and nothing was modified except this file. Larkspur Airlines is a fictional training scenario. Confidential, do not distribute.
