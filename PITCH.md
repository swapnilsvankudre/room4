# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A disruption-care chat agent on the Claude Messages API — a tool loop over Larkspur's own booking, OpsFeed, policy and inventory data, with nine given tools plus one we specified ourselves, next_available_day, which we then moved out of the agent and behind an MCP server so it is versioned and owned separately.
Does: For a stranded customer it reads the booking, checks the flight's real status, resolves what Larkspur owes from the policy table with the row id attached, then either offers a seat it can hold or hands the conversation to a human — and it answers "when is the first day I can actually fly?" from live inventory instead of guessing.
Number: 62,818 input tokens per pass over the five ticket types before Build 2, 77,974 after — +24.1% for identical work (19 turns, 14 tool calls, 5/5 answered both times), because two registered tools that fired zero times still cost 792 input tokens on every turn.
Safety check: It cannot take an irreversible action on its own — confirm_rebooking needs a confirmation_token that only the customer's own click produces, so "the customer said yes" in chat does not reissue a ticket. Proved on the wire, not in the source: on the twelve-passenger group ticket the agent called escalate_to_human instead of acting, 1 of the 14 tool calls in the measured run, and gates 1.2, 1.3, 1.4, 2.1 and 2.2 all read the wire.
Next: Turn the token count into money — a bench that gives cost per resolved contact against the $6.90 a human contact costs — and eval cases that grade whether the answers are actually right, which nothing does today.
Still broken: Nothing watches tone. The abusive-message ticket gets a calm, helpful, entirely correct answer and no gate fires, so the first time a customer is abusive in production we find out from the customer. Two smaller ones we would rather say than have found: next_available_day answers for a party of one, so it cannot tell a family of three they will fit; and no answer this agent gives has ever been graded for correctness — every number above is about cost and completion, not about being right.
Lever: <cost | speed | intelligence>

## Priya asked

Costs:
Wrong:
Runs it:
Left out:
