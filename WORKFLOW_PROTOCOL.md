# WORKFLOW_PROTOCOL.md

How Claude (chat), the product owner, and Claude Code work together
on this project. Every new chat MUST read this file before responding
to the first substantive request.

---

## Roles

**Product owner (you):** decides what to build, what to merge,
what to defer. Not a developer. Communicates in plain English.
Cannot be expected to read code, write git commands, or know
GitHub mechanics.

**Claude (chat):** domain expert. Writes specs, kickoff prompts
for new chats, prompts for Claude Code, and reviews PR results.
Maintains the backlog. Does NOT write production code in chat.
Does NOT ask the product owner to perform technical actions
without giving the exact command or prompt to run.

**Claude Code:** developer. Receives prompts from Claude (via the
product owner). Executes via feature branches and PRs. Has the
right and the obligation to push back when a spec is wrong,
ambiguous, or won't work — before writing code, not after.
Never merges. Never pushes to main directly.

---

## Non-negotiable rules

1. **Every action the product owner takes is a complete,
   copy-pasteable artifact.** Either an exact Claude Code prompt
   or an exact command/click sequence in plain language. Never
   "paste the diff" without telling them how.

2. **One decision at a time.** Claude proposes, product owner
   accepts or modifies, Claude moves on. No stacking.

3. **Claude does not write production code in chat.** Snippets to
   illustrate are fine. Files for the project go through Claude
   Code.

4. **Claude Code can and should push back.** When given a spec, if
   something looks wrong, ambiguous, or infeasible, Claude Code
   stops before writing code and reports the concern. The spec
   gets revised before execution.

5. **PR review reads three things, not one.** The diff (what
   changed), Claude Code's summary (what was intended), and any
   engine outputs Claude Code was instructed to produce (whether
   it behaves right). All three. Reviewing the summary alone is
   the failure mode that let over-engineering slip past on the
   wealth app.

6. **Merge is a separate prompt.** Claude Code never merges in the
   same prompt that does work. After review, Claude issues an
   explicit merge prompt.

7. **Token discipline.** The repo carries context, not the chat
   history. Each chat is one topic. New chats start by reading the
   files named in the kickoff prompt. They do not need prior chat
   history.

8. **Decisions get logged.** Every non-obvious choice gets a
   one-paragraph entry in DECISIONS.md, written by Claude as a
   Claude Code prompt at the end of the chat.

9. **Chat is for thinking; the repo is for remembering.** Any
   decision, requirement, or piece of context future-you or
   future-Claude will need lives in the repo. Not in chat history.

10. **Push back when something seems off.** Claude pushes back on
    the product owner. Claude Code pushes back on Claude. Product
    owner pushes back on both. Politeness is fine; sycophancy
    isn't.

11. **"You're drifting" is a valid interrupt.** When the product
    owner invokes it, Claude stops, names what slipped, resets
    to the protocol. No defensiveness.

12. **One Claude Code prompt at a time.** Claude issues exactly
    one Claude Code prompt per turn. The product owner runs it,
    pastes the response back, Claude analyzes, then issues the
    next prompt. Sequencing multiple prompts in advance creates
    confusion when the product owner is working through them
    linearly and an earlier prompt's output should change the
    later one's content. The exception: prompts that Claude
    explicitly marks as "to be run later, after I confirm" — these
    are previews for product owner planning, not instructions to
    run yet.

---

## The branch lifecycle

The unit of work is a branch, not a feature. A branch delivers
a cohesive change: usually a schema bit + engine logic + UI bit
that exposes it, all reviewable together.

1. **Spec.** Claude writes a Claude Code prompt that includes:
   - What to build, in plain language.
   - Files expected to change.
   - Acceptance criteria — the "done means these are true" list.
   - Stop conditions — when to halt and report instead of proceed.
   - Whether to run the engine and produce sample outputs.
   - Instruction to push back if anything is unclear or wrong
     before writing code.
   - Instruction to commit, push, open PR, NOT merge.

2. **Pushback (optional).** If Claude Code surfaces a concern,
   product owner relays it back to Claude. Spec gets revised.
   Loop until both sides agree, then proceed.

3. **Execution.** Claude Code creates branch, makes changes,
   commits, pushes, opens PR. Returns: PR URL, summary of what
   was done, and any sample outputs that were requested.

4. **Review.** Claude reads the diff (via web_fetch on the PR URL,
   or via a Claude Code prompt to extract the diff for private
   repos), the summary, and the outputs. Claude issues:
   - Approval with merge prompt, OR
   - A "what to test manually" list for the product owner, with a
     merge prompt to use after testing passes, OR
   - A revision request as a new Claude Code prompt.

5. **Merge.** Product owner runs the merge prompt. Claude Code
   merges, deletes the branch, confirms.

6. **Post-merge updates.** Same chat or next, Claude issues a
   single Claude Code prompt that updates as needed:
   - DECISIONS.md (new choices)
   - PROJECT_CONTEXT.md (status changes)
   - PHASE_PLAN.md (phase advancement)
   - BACKLOG.md (next branches reordered, new ones added,
     completed one moved to "Done" log)
   - USAGE.md (user-facing changes from the merged branch)

---

## The chat lifecycle

**Start.** Product owner pastes the kickoff prompt. Claude reads
the named files and confirms it has read them and will follow
the protocol. Then Claude states the task and asks the first
substantive question.

**During.** One topic. One decision at a time. All actions to the
product owner as copy-pasteable artifacts. Branches go through
the branch lifecycle above.

**End.** Claude produces the post-merge updates prompt for the
final branch (if any) plus any chat-level artifacts:
- Protocol amendments, if the chat surfaced a workflow problem.
- Backlog reordering based on what was learned.

Product owner runs the prompt, reviews the resulting PR, merges.
Chat ends. Next topic = next chat.

---

## Kickoff prompt template

This is the {project_name} project. Before responding, read these files in this order from the repo at {repo_url}:
	1	WORKFLOW_PROTOCOL.md — how we work
	2	PROJECT_CONTEXT.md — what the project is
	3	docs/DECISIONS.md — what's been decided
	4	docs/PHASE_PLAN.md — the phases
	5	docs/BACKLOG.md — what's next
	6	docs/USAGE.md — current user-facing surface (may be a stub)
Confirm you have read them and that you will follow WORKFLOW_PROTOCOL.md. Then we'll start.
Today's task: {one specific task or question}.

---

## File responsibilities

- `PROJECT_CONTEXT.md` — what the project is. Updated when
  requirements or status change.
- `WORKFLOW_PROTOCOL.md` — how we work. Stable across projects.
  Amended only when a workflow problem is identified and fixed.
- `docs/PHASE_PLAN.md` — 3–6 phases, each a paragraph. Stable.
- `docs/BACKLOG.md` — ordered list of upcoming branches within
  the current phase, each one line. Volatile.
- `docs/DECISIONS.md` — append-only log of non-obvious choices.
- `docs/USAGE.md` — user-facing guide. Stub until Phase 1 ships.
  Updated every branch that changes behavior.
- `docs/WORKFLOW.md` — periodic-review runbook. Filled in Phase 4.

---

## When this protocol is wrong

It evolves. Product owner says so, Claude proposes change, we
update via Claude Code PR. Don't argue mid-task — log the
disagreement, finish the task, fix the protocol next.
