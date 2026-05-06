# Decisions Log

Append-only. Most recent at bottom.

## 2026-05-06 — Architecture: static HTML on GitHub Pages
Single static HTML file. Hosted free on GitHub Pages. Add to home
screen on iPhone. Simplest durable option. Caveat: iOS Safari
background audio is quirky; if it becomes a dealbreaker post-Phase-1,
wrap in Capacitor.

## 2026-05-06 — Storage: split repos with fine-grained PAT
App in public repo (this one); data in private workout-data repo.
Fine-grained PAT scoped to workout-data only. localStorage acts as
offline write buffer; GitHub is source of truth. Replaces an earlier
Phase 0 plan to use localStorage + manual iCloud export, which would
have failed under realistic-use conditions (forgetting to export,
Safari clearing localStorage).

## 2026-05-06 — AI as periodic consultant, not daily decision-maker
Plan design and revision happen in Claude chat. Daily execution runs
deterministically from a JSON plan. Same pattern that made the wealth
management app work.

## 2026-05-06 — Audio-first execution
GIFs/follow-along video deferred to Phase 2+. Audio cues + static
exercise visual is sufficient and 10x simpler to build. Validate
with audio first; only build video if it's actually missed.

## 2026-05-06 — PR-based code review
Claude Code commits to feature branches and opens PRs. Reviewer
(Claude in chat) reads the diff via web_fetch on the PR URL — not
a self-summary. This came directly from a wealth-app lesson where
summary-based review let over-engineering slip past unnoticed.

## 2026-05-06 — In-gym flow budget: 30 seconds
Hard ceiling. The wealth app was used quarterly; UX friction was
free. This app is used 4–5x/week mid-workout. Friction is the
single biggest adoption risk and gets a hard budget.

## 2026-05-06 — Research split: three framework chats
Lifelong plan brief originally planned as one document. Split into
CARDIO_FRAMEWORK, STRENGTH_FRAMEWORK, and TRACKING_AND_OKR_FRAMEWORK
to allow deeper per-topic research. Flexibility/mobility and balance
fold into the strength brief (mobility is already shoulder-rehab
adjacent) unless it gets unwieldy.

## 2026-05-06 — Workflow protocol formalized
Locked the working agreement between Claude (chat), product owner,
and Claude Code into WORKFLOW_PROTOCOL.md. Reusable across future
projects. Triggered by friction during Phase 0 setup — Claude
drifted from patterns established on the wealth-management app.
Protocol makes the patterns explicit and self-enforcing via the
kickoff prompt that every new chat must use.

## 2026-05-06 — Backlog and Usage as standing files
docs/BACKLOG.md tracks upcoming branches within the current phase
(volatile, reordered as we learn). docs/USAGE.md is the user-facing
guide, stub now, populated starting Phase 1. Both are in the
kickoff prompt's required-reading list.

## 2026-05-06 — Rule 12 added: one Claude Code prompt at a time
Earlier in Phase 0 setup, Claude issued multiple sequenced prompts
in one turn. Product owner ran them in order, the first prompt's
output should have informed the second's content, and confusion
followed. Rule 12 prevents this: exactly one Claude Code prompt
per Claude turn, response analyzed before the next is issued.

## 2026-05-06 — Chats orient via Desktop Commander, not web_fetch
First attempt to orient a fresh chat via web_fetch on
github.com/.../blob/main/<file> URLs failed: the chat's web_fetch
is gated to URLs that appeared in prior tool results, and a fresh
chat has no priors. The reliable mechanism is the Desktop Commander
MCP tool, which reads from the local clone of the repo. Rule 13
codifies this. Kickoff template now points at local filesystem
paths and requires Desktop Commander; chat must error fast if it
isn't connected. This is reusable across future projects: any
project using this protocol assumes a local clone exists and
Desktop Commander is enabled in chats.
