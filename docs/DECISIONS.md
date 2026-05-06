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
