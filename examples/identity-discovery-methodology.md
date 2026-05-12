# Identity Discovery Methodology — Case Study

> How Gary arrived at a 27-trait + 6-shadow self-portrait through repeated dialogue with Claude Code, and what the agent reads in `about-you.md` every session.
>
> **Reference only.** Don't reproduce Gary's 27 traits — your number will differ. Reproduce the *process*.

---

## Why this exists

The `about-you.md.template` gives you the **structure** (4-Layer, traits, principles, shadows, validation).
This document gives you the **process** — how to fill it without staring at a blank scaffold.

The actual artifact in Gary's vault took ~6 weeks of iterative agent dialogue, ~12 sessions, and converged to a v2.7 document the agent reads as the single entry point before answering anything about Gary.

---

## What a mature `about-you.md` looks like

Gary's lives at `20-wiki/meta/about-gary.md`. Anonymized shape:

```
🪞 One-Line Summary             — single sentence + identity stability note
📍 Current Situation             — job, life phase, 2–3 year horizon
🏛️ 4-Layer Identity              — What / How / Why / Embodied
🧭 27 Traits                     — grouped into the 4 Layers,
                                   each with external validation citations
⭐ Focus 3 Principles             — distilled from 27 for the current era
🌑 6 Shadow Areas                — strengths' other side + conscious learning
🚀 Ongoing Activities            — work, craft, projects, life
🎓 Certifications                — auditable credentials with meaning
🎤 Public Activities             — large/mid/small scale + recommendations
🎯 How to Interact                — communication preferences, what to avoid
🔗 Detail References             — links to thesis / principles / patterns
📝 Update Principles              — what LLM may auto-touch vs. manual-only
🔄 Version History                — v0.1 → v2.7 audit trail
```

Total: ~430 lines after 6 weeks of compounding.

---

## Source material that fed the dialogue

Gary's raw inputs the agent read across sessions:

| Source | What it provided |
|---|---|
| **Personal journal** (`10-raw/personal-journal/`) | Patterns in self-observation — parent relationship, Vipassana volunteer week, what feels effortful vs. natural |
| **CliftonStrengths report** (2022-07, from prior employer) | Top-5 psychometric anchors → became external validation for traits |
| **Recommendation letters** (from past managers and peers) | What others see — translator capability, ownership, shadow areas |
| **Manager NPS data** | Direct report feedback (NPS +100) |
| **Public event feedback** (우아콘 mentoring) | 9/10 satisfaction → validation that mid-scale coaching works |
| **Career certifications** (CSM/PMP/SAFe RTE/ACP-620) | Auditable evolution curve over 6 years |

Common thread: **artifacts already existed**. The agent didn't invent traits — it surfaced patterns Gary couldn't see in isolation.

---

## The 6-step process

### Step 1 — Brain dump phase (sessions 1–2)

Tell the agent: _"I want to build my about-you.md. Read what's in `10-raw/personal-journal/` and `10-raw/external/` and tell me what patterns you see. Don't synthesize yet — just list candidates."_

Output: 30–50 candidate trait fragments, redundant, overlapping.

### Step 2 — Layer scaffolding (session 3)

Pick the **What / How / Why / Embodied** model (or your own). Ask the agent: _"Take the candidate list. Each fragment — which layer does it belong to? Where does it fail to fit?"_

Output: rough grouping. Some fragments split into two; some collapse into one.

### Step 3 — External validation pass (session 4–5)

For every candidate trait, ask: _"What external evidence do I have for this? Is there a recommendation letter, an NPS number, a psychometric score, a public-event feedback that supports it? Cite it inline."_

Traits that survive: ones with at least one external citation. Traits that fail: drop or move to a "candidate" parking lot.

This is the **non-negotiable** step. Without external validation, the doc decays into wishful self-portrait.

### Step 4 — Shadow pass (session 6–7)

Strengths only is half the picture. Ask: _"For each of the surviving traits, what's the shadow side? When does this strength fail or become costly?"_

Gary's 6 shadows all come from this pass:
- Shadow 1 = the cost of trait #10 (Translator) — too quick to enter execution
- Shadow 2 = the cost of trait #24 (Long-form stewardship) — outer-circle fatigue
- ...

Shadows must come from **observed evidence**, not introspective guessing. Use journal entries, manager feedback, or specific incidents.

### Step 5 — Focus 3 distillation (session 8)

From the surviving N traits (Gary's was 27), select 1–3 that matter most *for this era*. Era-bounded: tied to current life phase, age, economic context.

Gary's distillation (2026–2027):
```
Trade-off (#17) — seeing both sides
      ↓
Translator (#10/#11) — connecting both sides
      ↓
Designer-owner separation (#26) — letting go of the connection
```

Three is a ceiling. Two is fine. One can also work. More than three becomes noise.

### Step 6 — Update discipline (ongoing)

Frontmatter rule in `about-you.md`:
- **Manually managed**: trait list, focus principles, shadow definitions
- **Auto-update OK**: "Current situation," "Ongoing activities" — agent can propose at monthly PDCA
- **External validation citations**: append-only when new data arrives (new recommendation, new NPS, new public-event feedback)

Each version bump (v2.1 → v2.7) logs **what changed and what evidence triggered it**. Gary's version history shows Vipassana volunteer week (2026-05-03) triggered v2.2–v2.5 — four traits gained validation citations and Shadow 5 was scope-corrected.

---

## What the agent does with this document

Set in `CLAUDE.md`:
```
User context 필요 시 항상 먼저 → 20-wiki/meta/about-you.md
```

Every session, before answering any question about the user, the agent reads `about-you.md` first. This means:
- "What do I know about X" answers are framed against the user's traits
- Recommendations consider shadow areas (e.g., Gary's Shadow 6 → agent gives more context up front)
- Suggestions check the **Focus 3 adoption criterion** ("does this contribute to at least one principle?")

The 27 traits aren't a vanity exercise. They're the **runtime context** the agent uses to be useful instead of generic.

---

## Common failure modes

| Failure | Why it happens | Fix |
|---|---|---|
| Trait inflation (50+ candidates, never converges) | No external validation gate | Step 3 — drop everything without a citation |
| All strengths, no shadows | Easier to surface | Step 4 — require one observed shadow per major trait cluster |
| Generic "leadership / curiosity" traits | Pulled from job description | Anchor in specific incidents — "did X with Y people for Z duration" |
| Doc decays after 1 month | No update discipline | Frontmatter manual-vs-auto rule + monthly PDCA review |
| Agent doesn't actually use it | `CLAUDE.md` doesn't point here | Add explicit "read this first" line in `CLAUDE.md` |

---

## Reading list (optional)

What Gary was reading while this took shape:
- Cal Newport, *Deep Work* — definition of self-determined work
- Donald Schön, *The Reflective Practitioner* — surface vs. tacit knowledge
- Carol Dweck, *Mindset* — growth vs. fixed framing for shadow areas
- (Not required — your inputs will differ)

---

## Re-running this for your own vault

1. Copy `vault-skeleton/20-wiki/meta/about-you.md.template` → `about-you.md`
2. Drop your raw material into `10-raw/personal-journal/` and `10-raw/external/`
3. Run sessions 1–8 above with Claude Code
4. Commit small. The first version (v0.1) should fit on one screen. Let it compound.

The 27 isn't a target. Yours may converge to 12, 18, 40 — the convergence is what matters.
