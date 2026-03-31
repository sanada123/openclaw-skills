---
name: team-lead
description: >
  Engineering management for first-time and experienced tech leads. Covers: 1:1 meetings,
  hiring engineers, interview frameworks, giving feedback (radical candor), sprint planning,
  retrospectives, standups, managing underperformers, delegation, first 90 days as manager,
  remote team management, performance reviews, team culture, technical decision-making,
  and growing engineers. Not HR theory — practical playbooks from real engineering orgs.
  Use when discussing team management, hiring, 1:1s, feedback, sprints, retros, performance,
  delegation, or engineering leadership. Triggers on: "team lead", "engineering manager",
  "1:1", "hire", "interview", "feedback", "sprint", "retro", "performance review",
  "underperformer", "delegation", "remote team", ניהול, צוות, גיוס, ראיון, פידבק.
license: MIT
metadata:
  author: ASD-AI
  version: "1.0.0"
  category: management
  tags: [engineering-management, team-lead, hiring, 1on1, feedback, sprint, agile, performance, delegation, remote-team, cto, tech-lead]
  platforms: [openclaw, claude-code, gemini-cli, codex-cli, cursor]
  homepage: https://github.com/sanada123/openclaw-skills
---

# Team Lead

**The engineering management playbook for people who'd rather write code.**

You got promoted (or promoted yourself) because you're a great engineer. Nobody taught you how
to manage humans. This skill fills that gap — practical frameworks that work in real engineering
teams, from 2-person startups to 50-person departments.

## Core Philosophy

```
PEOPLE > PROCESS.     A great team with bad process will fix the process. Bad team with great process will fail.
CLARITY > CONSENSUS.  Decide, communicate, move. Don't committee-ize everything.
FEEDBACK > SILENCE.   Uncomfortable truth now beats explosive problem later.
TRUST > CONTROL.      Hire well, set expectations, then get out of the way.
GROW > RETAIN.        People leave managers, not companies. Grow them or lose them.
```

---

## When to Activate

- Running or joining a team as lead/manager
- Preparing for 1:1 meetings
- Hiring: writing job descriptions, interviewing, evaluating
- Giving difficult feedback
- Sprint planning, retros, standups
- Dealing with underperformers
- Remote team management
- First-time manager seeking guidance
- Performance review season

---

## 1. The 1:1 — Your Most Important Meeting

### Structure (30 min, weekly, never cancel)

```
First 10 min: THEIR agenda
  "What's on your mind?"
  "What do you need from me?"
  "Anything blocking you?"

Middle 10 min: YOUR agenda
  Progress on goals
  Feedback (both ways)
  Career development check-in

Last 10 min: ACTION ITEMS
  What will they do before next 1:1?
  What will YOU do before next 1:1?
  Write it down. Both of you.
```

### Questions That Actually Work

| Purpose | Question |
|---------|---------|
| **Open up** | "What's the thing you're spending the most energy on right now?" |
| **Unblock** | "If you could change one thing about how we work, what would it be?" |
| **Career** | "What skill do you want to be known for in 2 years?" |
| **Feedback** | "What's one thing I could do differently to help you more?" |
| **Satisfaction** | "On a scale of 1-10, how happy are you at work? Why not higher?" |
| **Trust** | "Is there anything you're hesitant to tell me?" |

### 1:1 Anti-Patterns

| ❌ Don't | ✅ Do |
|----------|------|
| Status update meeting | Coaching + unblocking session |
| You talking 80% of the time | They talk 70%+ |
| Cancel when busy | Reschedule, never cancel |
| Same questions every week | Rotate, go deeper |
| Skip when "everything is fine" | "Fine" often means "I'm not telling you" |

---

## 2. Hiring Engineers

### Job Description Formula

```
[Company — 1 line what you do]

We're looking for [role] to [impact in 1 sentence].

## What you'll do
- [3-5 concrete responsibilities, not vague buzzwords]

## What you bring
- [2-3 must-haves (be honest — only REAL requirements)]
- [2-3 nice-to-haves (explicitly labeled)]

## What we offer
- [Salary range (post it — saves everyone time)]
- [2-3 actual perks, not "fast-paced environment"]

## How to apply
[Clear instructions. 1 step, not 5.]
```

### Interview Framework (4 stages)

| Stage | Duration | What to Assess | Who |
|-------|----------|---------------|-----|
| 1. **Screen** | 30 min | Communication, motivation, basic fit | Recruiter or you |
| 2. **Technical** | 60-90 min | Coding ability, problem-solving, technical depth | Senior engineer |
| 3. **System Design** | 45-60 min | Architecture thinking, trade-offs, real-world experience | You or CTO |
| 4. **Culture/Values** | 30-45 min | Collaboration, ownership, growth mindset, team fit | Team member |

### Interview Scorecard

Rate each 1-5:

```
TECHNICAL
  [ ] Problem-solving approach (not just answer)
  [ ] Code quality and readability
  [ ] System design and trade-offs
  [ ] Depth in their claimed expertise

COLLABORATION
  [ ] Communication clarity
  [ ] How they handle disagreement
  [ ] Do they ask good questions?
  [ ] Would the team enjoy working with them?

GROWTH
  [ ] Self-awareness of weaknesses
  [ ] Learning from past mistakes
  [ ] Curiosity / asks questions back
  [ ] Takes ownership vs blames others

DECISION: Strong Hire / Hire / No Hire / Strong No Hire
```

### Hiring Red Flags

| Red Flag | What It Signals |
|----------|----------------|
| Can't explain a past project simply | Low communication skills |
| "That was someone else's fault" consistently | No ownership |
| No questions about the team or product | Not genuinely interested |
| Perfect answers, no depth when probed | Rehearsed, not experienced |
| Talks badly about previous employers | Will talk badly about you |
| Salary is the ONLY consideration | Mercenary — will leave for $5K more |

---

## 3. Giving Feedback (Radical Candor)

### The Framework

```
                    CARE PERSONALLY
                         |
         Ruinous     |   Radical
         Empathy     |   Candor ←── THE GOAL
                     |
    ─────────────────┼───────────── CHALLENGE DIRECTLY
                     |
         Manipulative|   Obnoxious
         Insincerity |   Aggression
                     |
```

**Radical Candor = Care Personally + Challenge Directly.** Both. Always.

### Feedback Formula: SBI (Situation, Behavior, Impact)

```
"In [SITUATION], when you [BEHAVIOR], the impact was [IMPACT]."

Example (corrective):
"In yesterday's code review [situation], when you dismissed Sarah's 
suggestion without explaining why [behavior], she felt her input 
wasn't valued and stopped contributing [impact]."

Example (positive):
"In the client demo this morning [situation], when you handled 
that unexpected question with a clear, honest answer [behavior], 
the client's confidence in our team visibly increased [impact]."
```

### Feedback Timing

| When | How |
|------|-----|
| **Positive feedback** | Public (in Slack, standup) or private. Both work. |
| **Corrective feedback** | ALWAYS private. Never in front of others. |
| **Timing** | Within 48 hours. Stale feedback loses power. |
| **Frequency** | Weekly minimum. Don't save it all for reviews. |

### Having Difficult Conversations

```
1. STATE the issue clearly (SBI format)
2. PAUSE — let them respond
3. LISTEN — really listen, don't plan your rebuttal
4. AGREE on the problem (or understand their perspective)
5. CO-CREATE a plan to fix it
6. SET a follow-up date
7. DOCUMENT what was agreed
```

---

## 4. Sprint Planning & Agile (Practical)

### Standup That Doesn't Suck (10 min max)

Each person, 2 minutes:
```
1. What did I ship yesterday? (not "worked on" — "shipped")
2. What will I ship today?
3. Am I blocked? (if yes, who can unblock me?)
```

**Rules:**
- Stand up (it really helps keep it short)
- No problem-solving during standup — "let's take that offline"
- Start on time even if people are missing
- If remote: cameras on, async updates OK for simple days

### Sprint Planning (2 hours max for 2-week sprint)

```
1. Review: what shipped last sprint? What didn't? (15 min)
2. Priorities: what MUST ship this sprint? (from PM/product) (15 min)
3. Breakdown: split each priority into tasks ≤ 1 day (45 min)
4. Estimate: rough T-shirt sizes — S (half day), M (1 day), L (2-3 days) (15 min)
5. Commit: team agrees on sprint scope (15 min)
6. Buffer: leave 20% capacity empty for bugs/emergencies (always)
```

### Retrospective Template (45 min, end of sprint)

```
1. WHAT WENT WELL? (10 min)
   Each person: 1-2 things that worked
   
2. WHAT DIDN'T GO WELL? (10 min)
   Each person: 1-2 pain points (no blame)
   
3. ROOT CAUSE for top 2 issues (10 min)
   "Why did this happen?" (ask 5 times — 5 Whys technique)
   
4. ACTION ITEMS (10 min)
   For each issue: WHO will do WHAT by WHEN
   Max 3 action items per retro (more = none get done)
   
5. CHECK last retro's action items (5 min)
   Did we actually follow through?
```

---

## 5. Managing Underperformers

### The 3-Strike Framework

**Strike 1: Feedback conversation**
- Clear SBI feedback
- Ask: "What's going on?" (sometimes there's a personal issue)
- Co-create improvement plan with specific, measurable goals
- Timeline: 2-4 weeks
- Document the conversation

**Strike 2: Formal warning**
- Progress check: did they improve?
- If not: escalate to formal PIP (Performance Improvement Plan)
- Specific goals, weekly check-ins, 30-day timeline
- Document everything in writing
- Involve HR if you have one

**Strike 3: Exit**
- If no improvement after PIP → it's time to part ways
- Do it respectfully: "This isn't working for either of us"
- Provide notice, help with transition
- Don't drag it out — it hurts everyone, including them

### Common Causes (and actual fixes)

| Symptom | Possible Cause | Fix |
|---------|---------------|-----|
| Missing deadlines | Unclear expectations | Be more specific about what "done" means |
| Low quality code | No code review culture | Implement PR reviews, pair programming |
| Not participating | Feeling unheard | Ask them directly in 1:1. Make space. |
| Constant conflicts | Cultural mismatch | Mediate once. If pattern continues → exit. |
| Good work, bad attitude | Burnout or personal issue | Have an honest conversation. Offer support. |

---

## 6. Delegation

### The Delegation Matrix

| Task | Urgency | Who Should Do It |
|------|---------|-----------------|
| Critical + only you can do | High | You — now |
| Critical + someone else can do | High | Delegate with clear deadline + check-in |
| Important + develops someone | Medium | Delegate as growth opportunity |
| Routine | Low | Delegate permanently — this isn't your job anymore |
| Shouldn't be done at all | — | Delete it |

### How to Delegate Well

```
1. WHAT: Clear deliverable ("deploy the new API endpoint", not "work on the API")
2. WHY: Context ("this unblocks the mobile team's sprint")
3. WHEN: Deadline ("by Thursday EOD")
4. HOW MUCH AUTONOMY: 
   - Level 1: "Do exactly this" (junior)
   - Level 2: "Research options and recommend" (mid)
   - Level 3: "Decide and tell me what you decided" (senior)
   - Level 4: "Decide and do it" (trusted senior)
5. CHECK-IN: "Let's sync on Wednesday to see how it's going"
```

### Delegation Anti-Pattern: The Boomerang

If every delegated task comes back to you → you're not delegating, you're just creating extra steps.

**Fix:** Give more context upfront. Accept 80% quality. Let them fail (small stakes) and learn.

---

## 7. Remote Team Management

### The Remote Playbook

| Challenge | Solution |
|-----------|---------|
| **Isolation** | Weekly team social (non-work). 15 min. Optional but encouraged. |
| **Miscommunication** | Write it down. "If it wasn't written, it wasn't said." |
| **Time zones** | Define overlap hours (4h minimum). Async for everything else. |
| **Trust** | Focus on output, not online status. Judge by results. |
| **Onboarding** | Over-document. Assign a buddy. First week = 100% guided. |
| **Camera fatigue** | Cameras on for 1:1s and team meetings. Off for focus time. |

### Async Communication Guidelines

```
For your team, establish:
1. Response time expectations: Slack = 2h, Email = 24h
2. "Urgent" channel for real emergencies only
3. Meeting-free blocks (e.g., no meetings before 11 AM)
4. Friday = low-meeting day
5. Document decisions in shared doc, not chat (chat is ephemeral)
```

---

## 8. First 90 Days as New Manager

### Day 1-30: Listen

```
- 1:1 with every team member (learn their goals, frustrations, strengths)
- 1:1 with your manager (understand expectations)
- 1:1 with adjacent team leads (understand dependencies)
- Read all existing docs (architecture, runbooks, retro notes)
- Don't change anything yet. Earn trust first.
```

### Day 31-60: Diagnose

```
- Identify the top 3 problems (team will have told you by now)
- Pick ONE to fix (not three — one)
- Propose your plan to the team (not decree — propose)
- Start weekly 1:1 rhythm if not already happening
- Begin giving feedback (both positive and constructive)
```

### Day 61-90: Act

```
- Ship the ONE fix you proposed
- Measure: did it actually improve things?
- Start on problem #2
- By now: team trusts you, you understand the system, you've earned credibility
```

**The #1 mistake:** Changing everything in week 1. You don't have context yet. Listen first.

---

## 9. Performance Reviews

### Review Template (Quarterly or Semi-Annual)

```
## Performance Review: [Name] — [Period]

### Summary (2-3 sentences)
[Overall assessment: exceeding / meeting / below expectations]

### Key Accomplishments
1. [Shipped X, resulting in Y impact]
2. [Led Z initiative]
3. [Grew in area W]

### Areas for Growth
1. [Specific skill/behavior to improve]
2. [With concrete next steps]

### Goals for Next Period
1. [Measurable goal #1]
2. [Measurable goal #2]
3. [Development goal — skill to build]

### Compensation (if applicable)
[Raise / promotion / no change — with clear reasoning]
```

### The No-Surprises Rule

**Nothing in a performance review should be a surprise.** If you've been doing weekly 1:1s with
regular feedback, the review is just a summary of conversations already had.

If someone IS surprised → you failed at giving ongoing feedback, not them.

---

## Output Standards

When giving management advice:
- **Be practical**: Templates and scripts, not theory
- **Be direct**: "Fire them" when that's the answer, not "consider realignment"
- **Acknowledge discomfort**: Management is emotionally hard. It's OK to feel uncomfortable.
- **Context-aware**: Startup with 3 people ≠ scale-up with 50
- **Reference frameworks**: SBI, Radical Candor, RACI — but explain, don't just name-drop
- **Defend IC time**: Managers who never code lose technical credibility. Protect some maker time.

---

*Because the hardest bugs to fix aren't in the code — they're in the team.*

**Contributing:** Engineering managers, tech leads, CTOs with battle scars — your playbooks are welcome.
Open an issue or PR at [github.com/sanada123/openclaw-skills](https://github.com/sanada123/openclaw-skills).
