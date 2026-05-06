# Workout App — Project Context

**Status:** Phase 0 in progress. Research briefs underway.

**Workflow:** see WORKFLOW_PROTOCOL.md. Read it first.

**Local repo path:** /Users/ashish/Claude/personal/workout-app
(also at /Users/ashish/Claude/personal/workout-data for the data
repo).

**Purpose:** Personal workout app for daily execution, tracking, and
OKR review. Cardio (stationary bike) + strength training. Replaces
IntervalTimer + Gym Day + a Google Sheets coach.

**User:** One person. 55M, 5'6", 130 lbs. Recovering shoulder
(anterior overload + long-head biceps tendinopathy). Equipment:
DBs to 52.5 lb, adjustable bench, pull-up bar, bands. Currently
doing 2x/week strength + 2x/week HIIT spin + mobility/yoga.

**Goal frame:** healthspan, not competitive performance. Lifelong
habit formation. Injury-free, full mobility into later decades.
Not feeling guilty if a session is missed.

**Architecture:**
- Single static HTML file
- App repo (this one): public, GitHub Pages hosted
- Data repo: workout-data, private, JSON via fine-grained PAT
- localStorage as offline write buffer, GitHub as source of truth
- AI as periodic consultant; deterministic engine for daily execution
- Audio-first execution; adaptive video deferred to Phase 2+

**Out of scope:** nutrition tracking, AI-on-the-fly workouts, social,
gamification, camera form analysis, workout design happening inside
the app.

**Design principle:** any in-gym flow that takes > 30 seconds is a
Phase 1 failure regardless of code quality.

**Phase 0 deliverables (in progress):**
- [x] WORKFLOW_PROTOCOL.md
- [ ] docs/CURRENT_STATE.md (user-authored, via interview)
- [ ] docs/CARDIO_FRAMEWORK.md
- [ ] docs/STRENGTH_FRAMEWORK.md
- [ ] docs/TRACKING_AND_OKR_FRAMEWORK.md
- [ ] docs/DECISIONS.md (accreting throughout)
