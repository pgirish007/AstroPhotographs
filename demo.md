# Operational Cross-Skilling & Production Readiness Playbook
*A Structured Framework for Flipped Code Walkthroughs ("Code Archaeology") and Silo Elimination*

---

## 1. Executive Summary & Objective

In complex technical platforms (such as infrastructure automation web applications), engineering teams often suffer from severe operational silos—where a small subset of engineers shoulder production support while the rest remain isolated in specific module domains.

The primary barriers preventing broad participation in on-call rotations are:
1. **Psychological Fear:** Fear of being blamed for breaking production systems in unfamiliar domains.
2. **Passive Training Ineffectiveness:** Video walkthroughs and static documents fail to create hands-on troubleshooting capability.
3. **Phantom Deprioritization:** Knowledge transfer tasks getting perpetually displaced by ad-hoc managerial requests and urgent sprint work.
4. **SME Condescension / Gatekeeping:** Experts inadvertently using dismissive tones (*"I could do this faster/better"*), crushing learner confidence.

This document establishes a structured **Flipped Code Walkthrough ("Code Archaeology")** framework tailored for **1-week (5-day) sprint cadences**, utilizing the existing **Friday 1-Hour Daily Tech Call (split into two 30-minute presentations)** to accelerate cross-training across the 18 engineers.

---

## 2. Weekly Sprint Execution Framework (Monday–Friday)

By pairing two presenters per sprint and using the Friday Tech Call, the team trains **2 engineers per week**, cycling through the entire 18-person engineering group in roughly 9 weeks.

| Sprint Day | Phase & Action | Learner (Presenter A & B) Actions | Domain SME (Co-Pilot) Actions | Expected Outcome & Deliverable | Time Commitment |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Mon (Day 1)** | **Phase 1: Bounded Assignment** | • Presenters A & B each accept an official Jira story ticket (1–2 pts).<br>• Receive separate, tightly bounded scopes (e.g., A: `/provision/node`, B: `/cluster/health-check`). | • Provides entry-point files for both topics.<br>• Links relevant monitoring/logging dashboards.<br>• Defines 1 primary failure scenario per topic. | Eliminates analysis paralysis; sets concrete starting boundaries for both engineers. | 15 mins *(during Sprint Planning)* |
| **Tue–Wed (Days 2–3)** | **Phase 2: Independent Archaeology** | • Independently traces execution paths and maps data contracts.<br>• Notes confusing variables, dead ends, missing docs, and unhandled edge cases. | • Remains strictly asynchronous.<br>• Available only if either learner hits a hard blocker. | Forces active mental model creation; simulates realistic off-hours triage. | 1.5–2 hrs *(spread over 2 days)* |
| **Thu (Day 4)** | **Phase 3: Pre-Flight Private Syncs** | • Shares draft findings and flow diagram with SME in two separate 15-min syncs.<br>• Clarifies ambiguous business logic. | • Validates assumptions in private.<br>• Explains historical context (*"why it was designed this way"*).<br>• Bolsters presenters' confidence. | Removes stage fright; ensures neither engineer is caught off-guard in public. | 15 mins per presenter *(locked calendar blocks)* |
| **Fri (Day 5)** | **Phase 4: Dual Walkthrough (Friday Tech Call)** | • **Slot 1 (00–30 min):** Presenter A walks through Domain X.<br>• **Slot 2 (30–60 min):** Presenter B walks through Domain Y. | • Serves as supportive co-pilot for both slots.<br>• Helps field obscure edge-case questions from the audience without taking over. | Maximizes recurring meeting time; doubles team cross-training velocity without adding new meetings. | 60 mins *(2 x [20 min talk + 10 min Q&A])* |
| **Fri PM / Mon AM** | **Phase 5: Value Realization PR** | • Submits targeted micro-PRs adding docstrings, Ops Cheat Sheet mitigations, or health-check assertions. | • Reviews and approves PRs promptly.<br>• Acknowledges contributions in team channels. | **Tangible achievement:** Both learners leave a permanent improvement on the codebase. | 30–45 mins |

---

## 3. Friday 1-Hour Tech Call Agenda Structure

To keep both 30-minute blocks disciplined and prevent overruns:

```
┌─────────────────────────────────────────────────────────────┐
│ 00:00 – 00:20 | Presenter A: Flow, Observability & Friction │
│ 00:20 – 00:30 | Presenter A: Team Q&A + SME Context Notes   │
├─────────────────────────────────────────────────────────────┤
│ 00:30 – 00:50 | Presenter B: Flow, Observability & Friction │
│ 00:50 – 01:00 | Presenter B: Team Q&A + SME Context Notes   │
└─────────────────────────────────────────────────────────────┘
```

---

## 4. SME Facilitation Protocol & Coaching Norms (Zero Gatekeeping)

The goal of the Domain SME during these sessions is **coaching and enablement, not showcasing personal mastery**. SMEs must actively avoid condescending attitudes or "I can do this better" dynamics.

### Coaching Communication Guidelines

| Forbidden Anti-Pattern (What NOT to Say/Do) | Recommended Coaching Alternative | Why This Matters |
| :--- | :--- | :--- |
| *"That's obvious / simple, you should know this line."* | *"That part is notoriously tricky—here is why it behaves that way."* | Validates that confusion is caused by architectural nuance, not learner capability. |
| Taking over screen-share or interrupting to present the module themselves. | Letting the presenter finish their flow; answering questions only when directly prompted or invited. | Keeps ownership firmly in the presenter's hands; prevents public disempowerment. |
| *"Why didn't you just look at class Y instead?"* | *"Class Y handles that under the hood—great catch identifying that friction point."* | Frames omissions as missing breadcrumbs in documentation rather than personal oversights. |
| Dismissing friction points (*"It’s fine the way it is, I understand it"*). | *"If it wasn't clear to you, it won't be clear to on-call engineers. Let's update the Ops Cheat Sheet."* | Reinforces that the code and docs must serve the entire 18-person team, not just the original author. |

---

## 5. Standard 4-Part Walkthrough Presentation Format

Presenters use a standardized, lightweight structure (15–20 minutes presentation + 10 minutes discussion):

```
┌─────────────────────────────────────────────────────────────┐
│ 1. Entry Point & Execution Flow                             │
│    • What triggers this subsystem (API, queue, scheduler)?  │
│    • Step-by-step trace through primary classes/functions.  │
├─────────────────────────────────────────────────────────────┤
│ 2. External Dependencies & Boundaries                       │
│    • What databases, external microservices, or tools       │
│      are invoked? What are the timeout/retry policies?      │
├─────────────────────────────────────────────────────────────┤
│ 3. Observability & Triage Map                               │
│    • Which dashboard or log stream reflects this operation? │
│    • What specific error signature indicates failure?       │
├─────────────────────────────────────────────────────────────┤
│ 4. Friction Points & Documentation Gaps                     │
│    • What was missing, misleading, or hard to follow?       │
│    • Proposed Ops Cheat Sheet or code comment updates.      │
└─────────────────────────────────────────────────────────────┘
```

---

## 6. Tackling "Phantom Deprioritization" & Avoidance Loops

When knowledge transfer is treated as informal or optional, engineers inevitably defer commitments with excuses like:
> *"Sorry, I got pulled into another task by my manager; can someone else take my slot this week and I'll do it next?"*

To prevent avoidance and ensure sustained participation in a fast weekly cycle, enforce the following operational guardrails:

```
                  ┌──────────────────────────────────────────────┐
                  │       WEEKLY SPRINT PLANNING INGESTION       │
                  │ 2 Official Story Tickets (1–2 Pts Each)      │
                  └──────────────────────┬───────────────────────┘
                                         │
                                         ▼
                  ┌──────────────────────────────────────────────┐
                  │          CAPACITY PROTECTION POLICY          │
                  │ Feature capacity reduced for Presenters A/B. │
                  │ PO & Scrum Master protect sprint scope.      │
                  └──────────────────────┬───────────────────────┘
                                         │
                                         ▼
                  ┌──────────────────────────────────────────────┐
                  │          LOCKED CALENDAR DISCIPLINE          │
                  │ Uses existing Friday Tech Call (No new mtgs) │
                  │ Mandatory 15-min syncs on Thursday.          │
                  └──────────────────────┬───────────────────────┘
                                         │
                                         ▼
┌────────────────────────────────────────────────────────────────────────────────┐
│                           EXCLUSION & ESCALATION RULES                         │
│                                                                                │
│  [X] NO "PASS & SWAP"       If postponed, the slot remains locked to that      │
│                             engineer. No passing to ad-hoc volunteers.         │
│                                                                                │
│  [X] MANAGERIAL OVERRIDE    Only genuine Sev-1 production incidents can        │
│                             preempt the ticket (requires explicit PO trade-off)│
│                                                                                │
│  [X] LIVE WORKING FALLBACK  If unprepared, the 30-min slot shifts to an open   │
│                             live code-reading workshop with the SME.           │
└────────────────────────────────────────────────────────────────────────────────┘
```

### Operational Guardrails Matrix

| Barrier / Excuse Pattern | Root Cause | Structural Mitigation | Governance Owner |
| :--- | :--- | :--- | :--- |
| **"I didn't have time / was pulled into a feature."** | Untracked effort; knowledge transfer viewed as personal side project. | **Sprint Story Pointing:** Create 1–2 point backlog tickets (`[Archaeology] Component X`). Deduct equivalent points from the engineer's sprint feature allocation. | Scrum Master / Product Owner |
| **"Can someone else take my turn this week?"** | Frictionless postponement enabling indefinite avoidance. | **The "No-Swap" Rule:** The assignment cannot be transferred to a volunteer. If a genuine blocker occurs, their slot is locked as the mandatory first agenda item in the following sprint. | Tech Lead |
| **"Manager assigned an ad-hoc request mid-sprint."** | Scope creep and lack of leadership alignment on bus-factor risk. | **Sprint Scope Boundary Defense:** The Scrum Master requires the manager to officially descope a sprint item or log an off-sprint impediment before overriding the training ticket. | Scrum Master / Engineering Manager |
| **"I didn't know where to start / felt stuck."** | Intimidation by massive legacy or unfamiliar codebase. | **Paired Pre-Flight Safeguard:** Thursday includes a mandatory 15-minute calendar block with the SME. The SME acts as an unblocker, not an evaluator. | Domain SME |
| **Fear of public embarrassment or being judged.** | Imposter syndrome and fear of getting system logic wrong in public. | **The "Code Is On Trial" Policy:** The team charter explicitly states that confusion highlights code/doc debt, not presenter inadequacy. Tech Lead leads the first session to model vulnerability. | Tech Lead / Engineering Manager |

---

## 7. Transition to Full-Team On-Call Rotation

Once engineers complete their code archaeology walkthroughs, production support is rolled out via a 3-tier safety net rotation:

```
[ Tier 1: Primary On-Call (Frontline) ]
  • Rotates weekly across ALL 18 engineers (including Tech Lead).
  • Follows standard Ops Cheat Sheets for mitigation (restarts, rollbacks, traffic draining).
  • Zero expectation of deep code refactoring under live incident conditions.
                            │
                            ▼ (Escalation / Safety Net)
[ Tier 2: Secondary On-Call (Experienced Wingman) ]
  • Staffed from the seasoned core support group (original 5–6 engineers).
  • Shadows and provides live backup during complex alerts.
                            │
                            ▼ (Breach SLA: > 30 Mins Unresolved)
[ Tier 3: Domain SME (Subject Matter Expert) ]
  • On-call during standard working hours for complex subsystem failures.
```

---

## 8. Engineering Team Working Agreement (Charter)

1. **Mitigate First, Investigate Later:** On-call shifts focus on fast service restoration (toggles, rollbacks, pod scaling). Root-cause fixes are logged as standard sprint backlog items.
2. **Ops Cheat Sheet Completeness:** Every production alert must link to an actionable Ops Cheat Sheet. If an alert lacks an Ops Cheat Sheet, the shift output is creating one.
3. **Blameless Operations:** If an engineer follows an approved Ops Cheat Sheet and an unintended failure occurs, it is categorized as an automation/documentation defect, never an individual fault.
4. **Shared Bus Factor:** No component is considered production-ready unless at least two non-author engineers have successfully completed a code archaeology walkthrough of its core flows.
5. **Constructive Enablement:** SMEs are evaluated on how well they empower others to support their code. Any gatekeeping, condescending remarks, or disempowering behavior violates team engineering values.
