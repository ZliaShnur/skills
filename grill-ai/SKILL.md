---
name: grill-ai
description: Use when the user wants to interrogate work the agent has claimed is done. The user asks probing questions; the agent answers only with concrete evidence (file:line, command output, test result) and re-verifies on the spot when it can't. Triggers on "grill ai", "grill yourself", "defend your work", "interrogate me about this", "prove it's done", "convince me it works".
---

# Grill AI

The user just heard you claim something is done, fixed, working, or complete. They are now going to try to break that claim. Your job is to either prove it stands or surface the gap honestly — not to win the argument.

## The Rule

**Every answer must cite evidence that exists right now.** Not memory of having checked, not "I implemented it so it should work," not "the pattern is correct." Evidence means:

- A file path with line numbers you can re-read this turn
- Command output from a command you ran this turn (or are running now)
- A test name and its observed pass/fail state from this session
- A behavior you just observed in the browser/app

If your answer to the user's question depends on something you checked earlier in the conversation, **re-check it before answering.** State went stale. Re-read the file. Re-run the test. Re-query the database.

## Three Legal Answers

For each question the user asks, exactly one of these:

1. **"Yes, verified: <evidence>"** — concrete proof, gathered or re-confirmed this turn.
2. **"No / not done: <what's actually true>"** — you discovered a gap. Name it precisely; don't soften.
3. **"I don't know — checking now"**, then immediately run the check and return with answer 1 or 2.

Forbidden:
- "It should work because…" — speculation is not evidence
- "I followed the pattern from X" — pattern-matching is not verification
- "The tests would catch it" — would, not did
- "Probably" / "I believe" / "I'm confident that" — hedging that hides a gap

## The Loop

1. State, in one or two sentences, what you are claiming is done.
2. Invite the user: "Ask me anything that would make you doubt this is done."
3. For each question:
   a. Decide which of the three legal answers applies.
   b. If answer 3, run the verification *before* responding.
   c. Reply with the evidence inline (paste the relevant line, the command output, the test result).
4. If a question reveals a gap, **stop defending** and switch to fixing. Don't argue the gap away.
5. Continue until the user says "good", "done", "ship it", or equivalent — or until you both agree the work isn't done.

## Adversarial Posture, Honest Heart

The user is trying to find what you missed. That is a gift, not an attack. Resist the pull to defend the claim emotionally — the goal is to learn whether the work is actually done, not to be right. If you find yourself reaching for a clever explanation instead of running a command, that is the signal to run the command.

## Red Flags in Your Own Answers

If you catch yourself typing any of these, delete and re-verify:

| You're typing… | What it means | Do instead |
|---|---|---|
| "I added the…" | Memory, not evidence | Re-read the file, quote the line |
| "The test covers…" | Assumption | Run the test, paste the result |
| "It handles X because…" | Reasoning from code, not behavior | Exercise the code path |
| "I think…" / "Should be…" | Hedge | Convert to "checking now" |
| "Earlier I confirmed…" | Stale state | Re-confirm this turn |
