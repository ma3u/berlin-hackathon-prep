# Big Berlin Hack 2026 — Team Prep & Idea Shortlist

**Event:** Big Berlin Hack by {Tech: Europe} × CODE University × The Delta Campus
**Dates:** 25–26 April 2026
**Location:** The Delta Campus, Berlin-Neukölln
**Prize pool:** €50K+
**Team size:** up to 5 (we plan for 2–4)
**Our real build window:** Saturday night → Sunday ~14:00 submission deadline ≈ **~14–16h of actual coding**

> ⚠️ We are **not** working the full 36h. This single constraint drives every decision in this document.

---

## Table of Contents

1. [Why this repo exists](#why-this-repo-exists)
2. [What the jury actually rewards](#what-the-jury-actually-rewards)
3. [Case study: why MedAccura won in January 2026](#case-study-why-medaccura-won-in-january-2026)
4. [Our strategic filter: the 15-hour rule](#our-strategic-filter-the-15-hour-rule)
5. [Partner tech stack — what's on the table](#partner-tech-stack--whats-on-the-table)
6. [Shortlisted ideas (analyzed in detail)](#shortlisted-ideas-analyzed-in-detail)
7. [How we'll pick the final idea](#how-well-pick-the-final-idea)
8. [Team roles & division of labor](#team-roles--division-of-labor)
9. [Timeline: Saturday night → Sunday 14:00](#timeline-saturday-night--sunday-1400)
10. [Submission checklist](#submission-checklist)

---

## Why this repo exists

This repo is our **pre-hackathon war room**. The goal is to walk into the Delta Campus on Saturday already knowing:

- What we're building and why it fits the judging criteria
- Which 3+ partner tools we're using and how they compose
- Who's doing what in the first 2 hours vs the last 2 hours
- What our 2-minute demo video is going to show

Because the rules require a **brand-new project started at the event**, we cannot pre-write code. But we absolutely can (and should) pre-write **decisions** — the team that shows up with fuzzy intent and 14h of coding time loses to the team that shows up with a sharp wedge and the same 14h.

---

## What the jury actually rewards

From the January 2026 edition at Delta Campus (source: Gründerszene / Business Insider coverage by Leandra Finke), the jury scored 27 submitted projects on three things:

| Criterion | What it actually means | How we target it |
|---|---|---|
| **Creativity** | A non-obvious angle on a real problem. Not "another chatbot." | Pick a problem the team has *lived experience* with. MedAccura won because a practicing doctor was on the team. |
| **Technical complexity** | Real plumbing visible under the hood — not just a Lovable front-end calling one API. | Mandatory: at least one non-trivial data/retrieval/agent layer (RAG, multi-step agent, tool-calling, voice pipeline, etc.) |
| **Effective use of partner tech** | Bonus points for using partner tools *well*, not decoratively. | Use 3+ partner techs where each one is **load-bearing** — if you remove it, the demo breaks. |

The judges' literal praise for MedAccura: *"This project stands out for its great technical depth, realized in a very short time, with really great results that can make the world a better place — especially hospitals."* Memorize the shape of that sentence. That's what we're aiming to trigger.

---

## Case study: why MedAccura won in January 2026

**The team:** Led by Tim Schwarz, a practicing doctor. Second hackathon for him.

**The product:** An AI agent for hospital clinicians. Doctors face hundreds of pages of medical guidelines (PDFs) and have to stay current while juggling patients. MedAccura ingested all the guideline PDFs and let clinicians query them via ChatGPT / OpenAI, returning the exact relevant passages on demand.

**Why it won — decomposed:**

### 1. Creativity score: high, but not because it was flashy

It wasn't a novel AI technique. RAG over PDFs is a solved pattern in 2026. The creativity was in the **problem selection**: picking a domain where the asymmetry between "information available" and "information accessible during a stressful shift" is enormous, and where the wow moment ("I found the right protocol in 4 seconds instead of 20 minutes") is immediately legible to non-experts on the jury.

**Takeaway for us:** Creativity ≠ novelty of tech. Creativity = a problem framing the jury hasn't heard 8 times that same day.

### 2. Technical complexity score: high, for pragmatic reasons

A working RAG pipeline in 36h (and we only have ~15h) that actually returns correct, cited passages from long PDFs is harder than it looks:

- PDF parsing of medical guidelines (tables, footnotes, multi-column layouts)
- Chunking strategy that preserves clinical context
- Embedding + vector search
- Prompt engineering that forces citation of source passage
- A UI that surfaces the source so a doctor can verify

That's 5 real engineering decisions, each of which can fail. Demonstrating that *all five work* in a 2-minute video reads as technical depth — even though none of the individual pieces are research-grade.

### 3. Partner tech fit: clean and load-bearing

They used OpenAI (reasoning / synthesis) as the core. The other required 2 of 4 tools were absorbed into the pipeline. Nothing was decorative. **Every partner tech earned its keep in the demo.**

### 4. The hidden 4th criterion: domain credibility in the pitch

A doctor on stage saying "I face this problem every week in the ER" is unbeatable demo framing. The jury's "make the world a better place, especially hospitals" line is a direct response to that framing.

**Takeaway for us:** Whoever pitches must have or convincingly borrow **first-person authority** over the problem. If nobody on the team lives the pain, don't pick that problem.

---

## Our strategic filter: the 15-hour rule

Teams that stay all 36h have a real advantage on depth. We don't have that. So we need to win on **problem selection + ruthless scope**, not stamina.

Every idea in the shortlist below has been stress-tested against five questions:

1. **Can a 2–4 person team ship a *working* demo in 14–16h?** Not a mockup — a demo where the judge watches one input go in and one useful output come out on a real laptop at the demo station.
2. **Does it have one undeniable "wow" moment?** The 2-minute video must have a single shot where the jury audibly reacts.
3. **Can 3+ partner techs be load-bearing, not decorative?** (See table below.)
4. **Does at least one team member have first-person authority on the pain point?** If no, drop it.
5. **Is there a believable "this could be a company" story?** The jury is staffed by sponsors; several are VCs. MedAccura's team said they'd keep working on it post-event. That line matters.

Any idea that fails #1 or #2 is an **automatic reject** regardless of how cool it sounds.

---

## Partner tech stack — what's on the table

From the Big Berlin Hack poster and the Luma event page. The rule is typically "use at least 3 of N partner tools." Here's how we're thinking about each:

### Core model / reasoning layer
| Partner | What it is | How we'd use it |
|---|---|---|
| **Google DeepMind (Gemini 3)** | Frontier multimodal reasoning model | Primary brain for any agent / reasoning task. Long context + vision makes it strong for document-heavy or screenshot-in workflows. |
| **Pioneer by Fastino Labs** | Small models that train themselves on your data | Pairs beautifully with a domain-specific vertical (fine-tune on the specific corpus, let Gemini handle orchestration). |

### Agent / orchestration layer
| Partner | What it is | How we'd use it |
|---|---|---|
| **Entire** | Developer platform for agent ↔ human collaboration | When the agent needs a human in the loop — approvals, edits, handoffs. Excellent for any workflow automation pitch. |
| **Qontext** | Context layer for AI (think: shared memory / structured context) | Any time you need the agent to remember across steps or share state between multiple tools. Load-bearing in multi-agent setups. |

### Data / retrieval / search
| Partner | What it is | How we'd use it |
|---|---|---|
| **Tavily** | Real-time web search, extraction, research API | Essential for any "up-to-date info" angle — news, regulations, competitor data, market signals. |

### Voice / audio
| Partner | What it is | How we'd use it |
|---|---|---|
| **Gradium** | Real-time voice AI (TTS + STT) | Any phone/voice-first interface. Pairs insanely well with telli for inbound/outbound call demos. |
| **ai\|coustics** | Real-time audio intelligence / enhancement | Clean up real-world audio before it hits the model. Useful for any voice demo recorded in a noisy hackathon room. |
| **telli** | AI-handled customer calls | Prebuilt calling infrastructure. Dramatic demos: "watch the AI handle this real phone call live." |

### Frontend / UI
| Partner | What it is | How we'd use it |
|---|---|---|
| **Lovable** | Build apps and websites by chatting with AI | Our frontend lever. Stops the front-end from eating 6h of our 15h. |
| **Hera** | AI motion designer | If we want the demo video itself to look polished without a designer on the team. |

### Security
| Partner | What it is | How we'd use it |
|---|---|---|
| **Aikido** | Secure everything | Only load-bearing if our pitch is explicitly security/compliance. Otherwise skip — don't tack it on. |

### Vertical track partners (bonus prize categories)
| Partner | Domain | Strategic value |
|---|---|---|
| **Buena** | Property / real-estate operations | Dedicated track prize. Huge opportunity if we pick a property-ops idea. |
| **Inca** | Agentic AI for insurance | Dedicated track. Insurance claims / underwriting automation is a natural fit. |
| **Reonic** | AI OS for renewable installers | Dedicated track. Great for solar/heat-pump installer workflow automation. |
| **Peec AI** | AI search analytics (how your brand shows up in ChatGPT/Perplexity) | Dedicated track. Marketing / SEO angle. |

> **Strategic observation:** Picking an idea that aligns with a **vertical track partner** gives us two shots — the main prize AND the track-specific prize. This is probably the single highest-EV move available to us.

---

## Shortlisted ideas (analyzed in detail)

Each idea is scored 1–5 on the five strategic filters. **Anything below 4/5 average is cut.** These eight ideas survived an initial filter of ~20 candidates.

Legend for difficulty dots: 🟢 feasible in 15h · 🟡 tight but doable with discipline · 🔴 only if a teammate has prior art in the exact stack

---

### Idea 1 — ClaimPilot: Voice-first insurance claim intake

> A claimant calls a number, speaks their claim in natural language in any condition (car accident, flooded basement, lost luggage). The agent asks clarifying questions, extracts structured claim data, checks it against policy terms fetched live, and produces a filing-ready claim package + fraud-risk score.

**Track fit:** 🎯 **Inca** (insurance track prize)

**Partner tech (all load-bearing):**
- **Gradium** — real-time voice conversation
- **ai\|coustics** — cleans up claimant audio (they're stressed, it's noisy)
- **Gemini 3** — reasoning + structured extraction + long-context policy doc ingestion
- **Tavily** — for regulatory/policy lookups if the claim is cross-jurisdictional
- **telli** — the actual phone pipe for the demo call

**The wow moment:** Someone on the team literally calls the demo number from their phone in front of the jury, describes a fake fender-bender, and a complete filled-out claim form appears on the screen in 90 seconds.

**Technical complexity:** High. Voice pipeline + STT + structured extraction + RAG over policy docs + fraud heuristics. Five real moving parts.

**Feasibility in 15h:** 🟡 Tight. We skip fraud scoring v1 and make it a placeholder. Core pipeline is absolutely doable.

**Risks:** Audio quality during live demo in a noisy hackathon hall. Mitigation: pre-record the call for the video, live-demo only if the room is quiet.

**Scores:** Creativity 4/5 · Complexity 5/5 · Partner fit 5/5 · First-person authority 3/5 (none of us work in insurance — need to research fast) · Company story 5/5
**Average: 4.4/5 ✅**

---

### Idea 2 — SolarScout: 30-second rooftop quote from a postcode

> Installer or homeowner types in a German postcode + monthly electricity bill. Agent pulls satellite imagery, estimates usable roof area, fetches current electricity tariffs + feed-in rates + regional subsidies, and returns a full solar install quote with payback period — in under 60 seconds. Then it can book a site visit via voice call.

**Track fit:** 🎯 **Reonic** (renewable installers track prize)

**Partner tech (all load-bearing):**
- **Gemini 3** — vision on satellite image (roof area / orientation estimation) + reasoning
- **Tavily** — live tariffs, subsidies, feed-in rates (these change quarterly in Germany)
- **telli** — books the installer site visit via automated call
- **Lovable** — the frontend in 30 minutes instead of 6 hours

**The wow moment:** Postcode → 60 seconds later → full quote with an annotated satellite image of *their actual roof* with panel layout overlaid.

**Technical complexity:** High. Vision + geospatial reasoning + real-time data aggregation + financial calculation + voice booking.

**Feasibility in 15h:** 🟡 Tight but doable. The vision estimation is the wildcard — we'd prototype it early Saturday night and have a fallback of "use a pre-annotated roof dataset" if Gemini vision isn't accurate enough on real imagery.

**Risks:** Satellite imagery licensing. Mitigation: use OpenStreetMap / public aerial tiles for the demo.

**Scores:** Creativity 4/5 · Complexity 5/5 · Partner fit 5/5 · First-person authority 3/5 · Company story 5/5
**Average: 4.4/5 ✅**

---

### Idea 3 — TenantTriage: Property-manager inbox that handles itself overnight

> A small-landlord or property manager forwards their tenant inbox to TenantTriage. The agent reads every message, classifies urgency (leak vs. lightbulb), drafts a reply in the landlord's voice, auto-schedules a handyman via voice call for anything in the "send someone" bucket, and escalates only the ~5% that genuinely need human judgment.

**Track fit:** 🎯 **Buena** (property track prize)

**Partner tech (all load-bearing):**
- **Gemini 3** — classification, drafting in landlord's tone, extraction
- **Qontext** — maintains per-tenant context across conversations (crucial — a "the sink is still leaking" message only makes sense with the prior thread)
- **Entire** — the human-in-the-loop approval flow for the escalated ~5%
- **telli** — makes the actual outbound call to the handyman, schedules the appointment
- **Lovable** — dashboard

**The wow moment:** Scroll through an inbox with 40 real-looking tenant emails. Hit "Run overnight triage." Watch the inbox re-color itself in 20 seconds: 35 auto-replied, 3 handymen dispatched (show the call recording), 2 escalated with summary + recommended action.

**Technical complexity:** High. Multi-agent with memory, tone-conditioned generation, voice dispatch, approval queue.

**Feasibility in 15h:** 🟡 Tight. We cheat by pre-loading a synthetic inbox rather than hooking a real IMAP. That's fine — the demo is about the triage, not the mail plumbing.

**Scores:** Creativity 5/5 · Complexity 5/5 · Partner fit 5/5 · First-person authority 2/5 (unless someone on the team has rented in Berlin 🙃) · Company story 5/5
**Average: 4.4/5 ✅**

---

### Idea 4 — ShipShape: Hands-free QA for e-commerce product copy at scale

> E-commerce brands have thousands of product pages with inconsistent tone, missing details, SEO gaps, and brand-voice drift. ShipShape ingests a product catalog (CSV or Shopify URL), audits every page against the brand's style guide, generates specific rewrites, and — critically — tracks how well the brand currently ranks in ChatGPT/Perplexity answers and predicts the uplift from the fixes.

**Track fit:** 🎯 **Peec AI** (AI search analytics track prize)

**Partner tech (all load-bearing):**
- **Gemini 3** — audit + rewrite at scale with long context (whole style guide in context)
- **Tavily** — scrape competitor pages + live ChatGPT/Perplexity visibility checks
- **Peec AI** — (the track partner itself, if they expose an API credit) — feed their visibility metrics back into the recommendation ranking
- **Lovable** — the audit dashboard

**The wow moment:** Drop in a real Shopify store URL. Ten seconds later: a ranked list of "if you fix these 5 product pages first, you'll show up in 40% more AI answers for your category." One-click apply shows the before/after.

**Technical complexity:** Medium-high. The interesting bit is the modeling of "AI answer visibility as a function of copy features" — which is novel and arguably research-grade in 2026.

**Feasibility in 15h:** 🟢 Very feasible. Most of the work is prompt engineering + a nice dashboard.

**Scores:** Creativity 4/5 · Complexity 4/5 · Partner fit 5/5 · First-person authority 4/5 (Ian's WorkScanAI taste for "audit real artifacts + score them" maps exactly) · Company story 5/5
**Average: 4.4/5 ✅**

---

### Idea 5 — StandUpAgent: The async daily standup that actually writes itself

> Every team member sends a 30-second voice note to a number at any point in the morning. The agent transcribes, deduplicates (yes, you already mentioned the Stripe issue yesterday), cross-references GitHub / Linear / Jira activity, and publishes a single structured standup summary to Slack — with blockers highlighted and @-mentions for anyone whose work is blocking someone else.

**Partner tech (all load-bearing):**
- **Gradium** — the voice interface (STT + optional TTS nudge if you forgot to submit)
- **ai\|coustics** — cleans up voice notes recorded on the train
- **Gemini 3** — synthesis + cross-referencing + deduplication
- **Qontext** — week-over-week memory so "still blocked on the thing from yesterday" resolves correctly
- **Tavily** — fetch GitHub/Linear activity for the cross-reference

**The wow moment:** Three team members record voice notes *during the pitch*. Thirty seconds later, a beautifully formatted standup appears in Slack on the big screen, with one blocker correctly flagged and one automatically-resolved "this was fixed yesterday" call-out.

**Technical complexity:** Medium-high. The interesting engineering is the cross-reference + dedup, not the voice part.

**Feasibility in 15h:** 🟢 Very feasible. Lots of prior art in the voice-to-summary space, which is why we need to make the cross-reference angle the differentiator.

**Risks:** The jury may have seen "AI standup" before. Differentiation has to come from the *specificity* of the output (real PR numbers, real blocker graph) not from the concept.

**Scores:** Creativity 3/5 · Complexity 4/5 · Partner fit 5/5 · First-person authority 5/5 (every developer lives this pain) · Company story 4/5
**Average: 4.2/5 ✅**

---

### Idea 6 — RegRadar: Compliance-change early warning for small startups

> A small founder/operator drops their business URL. Agent figures out what regulated activities they do (payments? health data? AI? cross-border?), subscribes them to the relevant EU/DE regulatory feeds, and every morning produces a 30-second brief: "these 3 things changed this week, here's what's relevant to *you specifically*, here's the action if any."

**Partner tech (all load-bearing):**
- **Tavily** — the core engine. Live crawling of EUR-Lex, BaFin, BfDI, national gazettes
- **Gemini 3** — long-context reasoning over dense legal text + relevance filtering per company
- **Qontext** — the company's regulated-surface profile maintained across weeks
- **Gradium** — optional daily voice brief ("here's what changed while you were sleeping")

**The wow moment:** Drop in a fintech URL. In 60 seconds: a personalized regulatory dashboard showing 2 real changes that happened this month affecting that specific company, with plain-language explanations and concrete action items.

**Technical complexity:** High. Getting the per-company relevance filter right is genuinely hard. But it's exactly the kind of depth judges reward.

**Feasibility in 15h:** 🟡 Tight. We'd have to pre-curate 5–10 regulatory feeds rather than build a general crawler. That's fine for a demo.

**Scores:** Creativity 5/5 · Complexity 4/5 · Partner fit 4/5 · First-person authority 3/5 · Company story 5/5
**Average: 4.2/5 ✅**

---

### Idea 7 — HireSignal: Job description → realistic skills interview in 5 minutes

> Recruiter or hiring manager pastes a job description. Agent generates a *specific*, *hands-on*, adaptively difficult interview (not generic STAR-question fluff) in the candidate's browser. As the candidate answers via voice, difficulty adjusts live. At the end, recruiter gets a structured signal report — not a yes/no — scoring on the actual skills the JD implied.

**Partner tech (all load-bearing):**
- **Gemini 3** — JD decomposition into a skill tree, adaptive question generation, scoring
- **Gradium** — real-time voice for the candidate-facing interview
- **ai\|coustics** — clean up home-office audio (this directly affects perceived interview quality)
- **Qontext** — candidate-session memory for adaptive difficulty
- **Lovable** — both dashboards (recruiter + candidate)

**The wow moment:** Paste a real Anthropic or Neo4j job description (both relevant to Ian's network). Two minutes later, a judge takes the live interview themselves on stage. At the end, the dashboard scores them in real time on the specific skills.

**Technical complexity:** High. Adaptive questioning is non-trivial, and doing it in real time over voice is a visible engineering feat.

**Feasibility in 15h:** 🟡 Tight. We constrain to technical JDs only (narrower question space) to make the adaptive loop tractable.

**First-person authority:** 🔥 **Ian — you are literally job-hunting right now and are evaluating how to signal skills to hiring managers.** This idea has the strongest first-person authority of the list for you specifically, and the pitch writes itself: "I got tired of shallow interviews eight weeks into my job search, so we built the thing we wished existed on both sides."

**Scores:** Creativity 4/5 · Complexity 5/5 · Partner fit 5/5 · First-person authority 5/5 · Company story 5/5
**Average: 4.8/5 ✅✅ — top-ranked**

---

### Idea 8 — PermitPilot: Berlin Anmeldung & bureaucracy agent for internationals

> Paste in your situation (visa type, planned activity, family status). Agent figures out the exact chain of Berlin bureaucratic steps — Anmeldung, Steuer-ID, Krankenversicherung, Freiberufler if relevant, Blue Card transition — books the Termine via phone calls, generates the forms pre-filled, and reminds you what to bring.

**Partner tech (all load-bearing):**
- **Gemini 3** — situation parsing + rule-chain reasoning
- **Tavily** — live availability of Termine across Berlin Bürgerämter
- **telli** — calls the Bürgeramt / Finanzamt / Ausländerbehörde
- **Gradium** — optional voice-first interaction for non-German speakers
- **Qontext** — state maintained across the multi-week process

**The wow moment:** Live demo where a (fake) newly-arrived Brazilian dev gets a complete personalized bureaucracy roadmap + one Termin booked via automated call in under 90 seconds.

**Technical complexity:** Medium-high. The rule-chain is the interesting part. Live booking via phone is the dramatic part.

**Feasibility in 15h:** 🟢 Feasible if we scope tightly to 3 visa types. Berlin-specific, which is thematic catnip at a Berlin hackathon.

**First-person authority:** 🔥 Berlin AI/tech community is *stuffed* with people who lived this. Highly relatable to a Berlin-based jury.

**Scores:** Creativity 5/5 · Complexity 4/5 · Partner fit 5/5 · First-person authority 4/5 · Company story 4/5
**Average: 4.4/5 ✅**

---

### Summary ranking

| # | Idea | Track | Score | Why it ranks here |
|---|---|---|---|---|
| 1 | **HireSignal** — JD → adaptive skills interview | — | **4.8** | Ian's first-person authority is unmatched. Voice + adaptive is a genuinely strong demo. |
| 2 | **ClaimPilot** — voice insurance intake | Inca 🎯 | 4.4 | Track prize shot + dramatic live-call demo. |
| 3 | **SolarScout** — postcode → solar quote | Reonic 🎯 | 4.4 | Track prize + vision demo is visually striking. |
| 4 | **TenantTriage** — property-manager inbox | Buena 🎯 | 4.4 | Track prize + the "overnight magic" framing. |
| 5 | **ShipShape** — e-commerce copy QA | Peec AI 🎯 | 4.4 | Track prize + Ian's WorkScanAI instinct transfers directly. |
| 6 | **PermitPilot** — Berlin bureaucracy agent | — | 4.4 | Berlin-thematic, warm-room appeal, Ian in Berlin. |
| 7 | **StandUpAgent** — async voice standup | — | 4.2 | Universal pain, but lower creativity differentiation. |
| 8 | **RegRadar** — compliance early warning | — | 4.2 | Strong but needs deeper regulatory knowledge than we have. |

### The meta-observation

Five of our eight shortlisted ideas hit a **dedicated track partner** (Inca / Reonic / Buena / Peec / no-track). Track alignment is the single highest-leverage move: same amount of work, two prize shots. **Strongly recommend picking from ideas 2–5 unless HireSignal's personal-story advantage proves decisive in team discussion.**

---

## How we'll pick the final idea

### Pre-event (this week)

1. Share this README with every team member.
2. Each person picks their top 2 and scores on the same five-criterion rubric.
3. **45-minute call** where we converge on top 2.
4. For each of the top 2, do a 30-minute "demo video walkthrough" exercise: one person narrates what the 2-minute submission video shows, shot by shot. **If we can't narrate a compelling video now with no code, we can't make one in 15h with code.**
5. Pick 1 primary + 1 backup.

### At the event (Saturday morning)

- Confirm the sponsor briefings align with our assumptions about what each partner tool can do. If something we assumed is wrong (e.g. telli doesn't support outbound to Germany), pivot to the backup *in the first 90 minutes*, not at hour 8.
- Matchmake aggressively. If someone at the event has exactly the domain authority our idea needs (a nurse for a health idea, a landlord for TenantTriage), **invite them onto the team**. Teams of 4–5 out-deliver teams of 2 in the final 3 hours.

### The irreversible decision deadline

**By Saturday 20:00 (7h before we actually start coding), the idea is locked.** No pivots after that unless something is literally on fire.

---

## Team roles & division of labor

A 2-person team is viable. A 3-person team is ideal. A 4-person team is excellent if the communication overhead is managed. Suggested roles:

| Role | What they own | Headcount |
|---|---|---|
| **Lead / Architect** | Idea coherence, end-to-end demo, submission video script, pitch. Also owns the Gemini / agent reasoning layer. | 1 (Ian suggested) |
| **Backend / Data** | Tavily queries, data pipelines, any RAG, API glue, telli/Gradium integration if voice. | 1 |
| **Frontend / UX** | Lovable-driven UI, demo polish, recording the submission video with Hera if time allows. | 1 |
| **Domain / Pitch** | Owns the problem framing, talks to sponsor mentors, writes the pitch deck, narrates the video. Does light frontend or data work as bandwidth allows. | 1 (critical if the pitch needs domain credibility — see MedAccura) |

### Ian's stack fits these slots cleanly

Given Ian's Next.js / FastAPI / Claude-or-Gemini integration experience plus the WorkScanAI muscle memory for ingestion + agent orchestration, **Lead / Architect** is the natural slot — with the option to float into Backend if a teammate has stronger product-design chops.

### Tooling expectations on the day

- Desktop Commander MCP + Claude in Chrome MCP are force multipliers — walk teammates through these in the first hour. File edits, git ops, browser automation for testing all run through them.
- Git repo: one of us creates the repo at 10:30 (right after kickoff briefing), branch = `main`, no PR workflow, just direct commits. Hackathon mode, not production.
- Decision log: pinned Discord thread or a `DECISIONS.md` in the repo — every non-trivial fork gets one line. When the 2am exhaustion hits, this is how we avoid re-litigating.

---

## Timeline: Saturday night → Sunday 14:00

### Saturday (pre-night)

| Time | What's happening | Our move |
|---|---|---|
| 10:00 | Doors open, networking | Arrive, set up, scope out sponsor mentors for the tools we want to use |
| 10:30 | Opening & matchmaking | If our team isn't full, recruit. Target: domain-authority teammate if our idea needs one. |
| 12:30 | Lunch | **Idea locked by now.** Eat fast. |
| 13:00–19:00 | Most teams start building | We're still planning and skeleton-scaffolding. Don't panic. |
| 19:00 | Dinner | Last checkpoint before the real sprint. Eat, then begin the actual build. |
| 20:00 | **Idea lock hard deadline** | If still flip-flopping, commit to the highest-scoring option. No more debate. |

### Saturday night → Sunday (the real ~15h sprint)

| Time | Goal | Output |
|---|---|---|
| 20:00–22:00 | **Skeleton + partner integrations smoke-tested** | Each of the 3+ partner APIs returns a real response. No UI yet. |
| 22:00–00:00 | **Happy-path end-to-end** | One input goes in, one usable output comes out — even if ugly. |
| 00:00–02:00 | **The "wow moment" works** | The single demo-video shot is reliable and reproducible. |
| 02:00–04:00 | Sleep rotation. At least 2 people sleep 3–4h. Nobody codes on no sleep past this point. |
| 04:00–07:00 | **Second pass on core + edge cases** | Demo doesn't break on the second run. |
| 07:00–10:00 | Everyone back. **Polish pass.** | UI cleanup via Lovable, copy polish, error handling on the demo path. |
| 10:00–12:00 | **Record the 2-minute submission video** | Multiple takes. Best take wins. |
| 12:00–13:30 | Buffer for technical issues + upload | Submit **early**, not at 13:59. |
| 14:00 | **Submission deadline** | Don't be the team that missed it. The article noted some teams didn't submit in time. |
| 15:30 | Finalists announced (3 teams) | — |
| 16:00 | Finalist pitches (5 min each) | If we're here, pitch rehearsal happens during the 15:00 wait. |
| 17:30 | Award ceremony | — |

### The 3 rules we will not break

1. **No new features after 02:00.** After 2am we only polish what works.
2. **No debugging during the video recording window (10:00–12:00).** If something breaks at 10:30, we cut it from the demo and record without it.
3. **Submit by 13:30.** One hour of buffer before the 14:00 deadline is non-negotiable.

---

## Submission checklist

Exactly what the jury sees. Nothing more, nothing less.

- [ ] **2-minute video** (hard ceiling). Shows: the problem, the wow moment (single clean shot), partner tools credited visibly, one sentence on "what we'd do next."
- [ ] **Working demo URL** (Lovable / Vercel / wherever). Reliable on Sunday afternoon network conditions.
- [ ] **GitHub repo** public with a README that credits every partner tool used.
- [ ] **One-slide deck** for the optional live pitch if we make finalists.
- [ ] **Team names + contact** on the submission form.
- [ ] **Partner tools list** explicitly listed — judges give bonus points for effective use; make it easy for them to check.

### The 2-minute video skeleton

- 0:00–0:15 — The problem, told as a first-person story. Not "businesses face a challenge in..." — **"Last Tuesday I was..."**
- 0:15–0:30 — What we built, in one sentence. Show the name and logo.
- 0:30–1:30 — The demo. One continuous shot if possible. This is where the wow moment lives.
- 1:30–1:45 — Which partner tools and how each one is load-bearing (one sentence each).
- 1:45–2:00 — What this becomes if we keep building. **Include the "we're keeping going after the hackathon" line.** MedAccura did this, and the jury responded.

---

## Appendix: what we learned from the January 2026 edition

Source: Leandra Finke's coverage in Gründerszene / Business Insider, 27 January 2026.

- **105 participants from 600 applicants** — ~6x oversubscribed. Expect similar at Big Berlin Hack.
- **27 projects submitted** out of ~30 teams — some didn't finish. Being in the "submitted" cohort already filters you into the top 90%.
- The jury evaluated on **creativity + technical complexity**, with **bonus points for effective partner tech use**. This exact rubric is the one we're optimizing for.
- The winner's jury citation emphasized **"great technical depth realized in a very short time"** and **real-world impact** — framing that rewards working software over slideware.
- Organizer Bela Wiertz's on-the-ground philosophy: *"The goal isn't maximum complexity — it's joy in the product. It's allowed to be light as long as it works."* We take this seriously. Don't over-engineer.
- The winning team explicitly said they'd **continue the project after the event**. Jury likes signals of durability.

---

## Contact

Ian — Full-stack / project lead
🌐 [ianworks.dev](https://ianworks.dev)
💼 [linkedin.com/in/avoiann](https://linkedin.com/in/avoiann)
💻 [github.com/ibxibx](https://github.com/ibxibx)

Berlin AI/tech community: GlobalAI Berlin, AgentCon Berlin 2026.

---

**See you at Delta Campus, 25 April. 🚀**
