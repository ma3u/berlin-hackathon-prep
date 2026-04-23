# Big Berlin Hack 2026 - Team Prep & Idea Shortlist

**Event:** Big Berlin Hack by {Tech: Europe} × CODE University × The Delta Campus
**Dates:** 25-26 April 2026
**Location:** The Delta Campus, Berlin-Neukölln
**Prize pool:** €50K+
**Team size:** up to 5 (we plan for 2-4)
**Our real build window:** Saturday night → Sunday ~14:00 submission deadline ≈ **~14-16h of actual coding**

> ⚠️ We are **not** working the full 36h. This single constraint drives every decision in this document.

---

## Table of Contents

1. [Why this repo exists](#why-this-repo-exists)
2. [What the jury actually rewards](#what-the-jury-actually-rewards)
3. [Case study: why MedAccura won in January 2026](#case-study-why-medaccura-won-in-january-2026)
4. [Our strategic filter: the 15-hour rule](#our-strategic-filter-the-15-hour-rule)
5. [Partner tech stack - what's on the table](#partner-tech-stack--whats-on-the-table)
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

Because the rules require a **brand-new project started at the event**, we cannot pre-write code. But we absolutely can (and should) pre-write **decisions** - the team that shows up with fuzzy intent and 14h of coding time loses to the team that shows up with a sharp wedge and the same 14h.

---

## What the jury actually rewards

From the January 2026 edition at Delta Campus (source: Gründerszene / Business Insider coverage by Leandra Finke), the jury scored 27 submitted projects on three things:

| Criterion | What it actually means | How we target it |
|---|---|---|
| **Creativity** | A non-obvious angle on a real problem. Not "another chatbot." | Pick a problem the team has *lived experience* with. MedAccura won because a practicing doctor was on the team. |
| **Technical complexity** | Real plumbing visible under the hood - not just a Lovable front-end calling one API. | Mandatory: at least one non-trivial data/retrieval/agent layer (RAG, multi-step agent, tool-calling, voice pipeline, etc.) |
| **Effective use of partner tech** | Bonus points for using partner tools *well*, not decoratively. | Use 3+ partner techs where each one is **load-bearing** - if you remove it, the demo breaks. |

The judges' literal praise for MedAccura: *"This project stands out for its great technical depth, realized in a very short time, with really great results that can make the world a better place - especially hospitals."* Memorize the shape of that sentence. That's what we're aiming to trigger.

---

## Case study: why MedAccura won in January 2026

**The team:** Led by Tim Schwarz, a practicing doctor. Second hackathon for him.

**The product:** An AI agent for hospital clinicians. Doctors face hundreds of pages of medical guidelines (PDFs) and have to stay current while juggling patients. MedAccura ingested all the guideline PDFs and let clinicians query them via ChatGPT / OpenAI, returning the exact relevant passages on demand.

**Why it won - decomposed:**

### 1. Creativity score: high, but not because it was flashy

It wasn't a novel AI technique. RAG over PDFs is a solved pattern in 2026. The creativity was in the **problem selection**: picking a domain where the asymmetry between "information available" and "information accessible during a stressful shift" is enormous, and where the wow moment ("I found the right protocol in 4 seconds instead of 20 minutes") is immediately legible to non-experts on the jury.

**Takeaway for us:** Creativity != novelty of tech. Creativity = a problem framing the jury hasn't heard 8 times that same day.

### 2. Technical complexity score: high, for pragmatic reasons

A working RAG pipeline in 36h (and we only have ~15h) that actually returns correct, cited passages from long PDFs is harder than it looks:

- PDF parsing of medical guidelines (tables, footnotes, multi-column layouts)
- Chunking strategy that preserves clinical context
- Embedding + vector search
- Prompt engineering that forces citation of source passage
- A UI that surfaces the source so a doctor can verify

That's 5 real engineering decisions, each of which can fail. Demonstrating that *all five work* in a 2-minute video reads as technical depth - even though none of the individual pieces are research-grade.

### 3. Partner tech fit: clean and load-bearing

They used OpenAI (reasoning / synthesis) as the core. The other required 2 of 4 tools were absorbed into the pipeline. Nothing was decorative. **Every partner tech earned its keep in the demo.**

### 4. The hidden 4th criterion: domain credibility in the pitch

A doctor on stage saying "I face this problem every week in the ER" is unbeatable demo framing. The jury's "make the world a better place, especially hospitals" line is a direct response to that framing.

**Takeaway for us:** Whoever pitches must have or convincingly borrow **first-person authority** over the problem. If nobody on the team lives the pain, don't pick that problem.

---

## Our strategic filter: the 15-hour rule

Teams that stay all 36h have a real advantage on depth. We don't have that. So we need to win on **problem selection + ruthless scope**, not stamina.

Every idea in the shortlist below has been stress-tested against five questions:

1. **Can a 2-4 person team ship a *working* demo in 14-16h?** Not a mockup - a demo where the judge watches one input go in and one useful output come out on a real laptop at the demo station.
2. **Does it have one undeniable "wow" moment?** The 2-minute video must have a single shot where the jury audibly reacts.
3. **Can 3+ partner techs be load-bearing, not decorative?** (See table below.)
4. **Does at least one team member have first-person authority on the pain point?** If no, drop it.
5. **Is there a believable "this could be a company" story?** The jury is staffed by sponsors; several are VCs. MedAccura's team said they'd keep working on it post-event. That line matters.

Any idea that fails #1 or #2 is an **automatic reject** regardless of how cool it sounds.

---

## Partner tech stack - what's on the table

From the Big Berlin Hack poster and the Luma event page. The rule is typically "use at least 3 of N partner tools." Here's how we're thinking about each:

### Core model / reasoning layer
| Partner | What it is | How we'd use it |
|---|---|---|
| **Google DeepMind (Gemini 3)** | Frontier multimodal reasoning model | Primary brain for any agent / reasoning task. Long context + vision makes it strong for document-heavy or screenshot-in workflows. |
| **Pioneer by Fastino Labs** | Small models that train themselves on your data | Pairs beautifully with a domain-specific vertical (fine-tune on the specific corpus, let Gemini handle orchestration). |

### Agent / orchestration layer
| Partner | What it is | How we'd use it |
|---|---|---|
| **Entire** | Developer platform for agent ↔ human collaboration | When the agent needs a human in the loop - approvals, edits, handoffs. Excellent for any workflow automation pitch. |
| **Qontext** | Context layer for AI (think: shared memory / structured context) | Any time you need the agent to remember across steps or share state between multiple tools. Load-bearing in multi-agent setups. |

### Data / retrieval / search
| Partner | What it is | How we'd use it |
|---|---|---|
| **Tavily** | Real-time web search, extraction, research API | Essential for any "up-to-date info" angle - news, regulations, competitor data, market signals. |

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
| **Aikido** | Secure everything | Only load-bearing if our pitch is explicitly security/compliance. Otherwise skip - don't tack it on. |

### Vertical track partners (bonus prize categories)
| Partner | Domain | Strategic value |
|---|---|---|
| **Buena** | Property / real-estate operations | Dedicated track prize. Huge opportunity if we pick a property-ops idea. |
| **Inca** | Agentic AI for insurance | Dedicated track. Insurance claims / underwriting automation is a natural fit. |
| **Reonic** | AI OS for renewable installers | Dedicated track. Great for solar/heat-pump installer workflow automation. |
| **Peec AI** | AI search analytics (how your brand shows up in ChatGPT/Perplexity) | Dedicated track. Marketing / SEO angle. |

> **Strategic observation:** Picking an idea that aligns with a **vertical track partner** gives us two shots - the main prize AND the track-specific prize. This is probably the single highest-EV move available to us.

---

## Shortlisted ideas (analyzed in detail)

Each idea is scored 1-5 on the five strategic filters. Anything below 4/5 average is cut. These 12 ideas are the survivors of a larger filter, now rebuilt around a single lens: **urgent daily problems where AI can create visible impact AND a credible business**.

The jury at Big Berlin Hack is staffed by sponsors, several of whom are active investors. The ideas below are picked so that the 2-minute video doubles as an investor teaser: each one names a specific paying customer, a wedge, and a clean partner-tech composition.

Legend for difficulty dots: green = feasible in 15h, yellow = tight but doable with discipline, red = only if a teammate has prior art in the exact stack.

### Idea 1 - HireSignal: Job description -> realistic skills interview in 5 minutes

> Recruiter or hiring manager pastes a job description. Agent generates a *specific*, *hands-on*, adaptively difficult interview (not generic STAR-question fluff) in the candidate's browser. As the candidate answers via voice, difficulty adjusts live. At the end, recruiter gets a structured signal report - not a yes/no - scoring on the actual skills the JD implied.

**Partner tech (all load-bearing):**
- **Gemini 3** - JD decomposition into a skill tree, adaptive question generation, scoring
- **Gradium** - real-time voice for the candidate-facing interview
- **ai|coustics** - clean up home-office audio (this directly affects perceived interview quality)
- **Qontext** - candidate-session memory for adaptive difficulty
- **Lovable** - both dashboards (recruiter + candidate)

**The wow moment:** Paste a real Anthropic or Neo4j job description (both relevant to Ian's network). Two minutes later, a judge takes the live interview themselves on stage. At the end, the dashboard scores them in real time on the specific skills.

**Technical complexity:** High. Adaptive questioning is non-trivial, and doing it in real time over voice is a visible engineering feat.

**Feasibility in 15h:** Tight. We constrain to technical JDs only (narrower question space) to make the adaptive loop tractable.

**First-person authority:** Ian is literally job-hunting right now and is evaluating how to signal skills to hiring managers. This idea has the strongest first-person authority of the list for you specifically, and the pitch writes itself: "I got tired of shallow interviews eight weeks into my job search, so we built the thing we wished existed on both sides."

**Scores:** Creativity 4/5 - Complexity 5/5 - Partner fit 5/5 - First-person authority 5/5 - Company story 5/5
**Average: 4.8/5 (top-ranked)**

---

### Idea 2 - StandUpAgent: The async daily standup that actually writes itself

> Every team member sends a 30-second voice note to a number at any point in the morning. The agent transcribes, deduplicates (yes, you already mentioned the Stripe issue yesterday), cross-references GitHub / Linear / Jira activity, and publishes a single structured standup summary to Slack - with blockers highlighted and @-mentions for anyone whose work is blocking someone else.

**Partner tech (all load-bearing):**
- **Gradium** - the voice interface (STT + optional TTS nudge if you forgot to submit)
- **ai|coustics** - cleans up voice notes recorded on the train
- **Gemini 3** - synthesis + cross-referencing + deduplication
- **Qontext** - week-over-week memory so "still blocked on the thing from yesterday" resolves correctly
- **Tavily** - fetch GitHub/Linear activity for the cross-reference

**The wow moment:** Three team members record voice notes *during the pitch*. Thirty seconds later, a beautifully formatted standup appears in Slack on the big screen, with one blocker correctly flagged and one automatically-resolved "this was fixed yesterday" call-out.

**Technical complexity:** Medium-high. The interesting engineering is the cross-reference + dedup, not the voice part.

**Feasibility in 15h:** Very feasible. Lots of prior art in the voice-to-summary space, which is why we need to make the cross-reference angle the differentiator.

**Risks:** The jury may have seen "AI standup" before. Differentiation has to come from the *specificity* of the output (real PR numbers, real blocker graph) not from the concept.

**Scores:** Creativity 3/5 - Complexity 4/5 - Partner fit 5/5 - First-person authority 5/5 - Company story 4/5
**Average: 4.2/5**

---

### Idea 3 - JobMatch Reverse: for people locked out of the job market, not the other way around

> Most job platforms optimize for employer search. JobMatch Reverse optimizes for the candidate who is unemployed, long-term out of work, or recently migrated. User uploads whatever they have - a CV in Farsi, a photo of a foreign certificate, a voice note describing past work. Agent extracts real skills, translates credentials into German-market equivalents, and produces a ranked list of *specific open roles they have a realistic shot at today*, plus the 1-2 skills that would unlock 10x more roles with a free course link attached.

**Theme:** Employment access, economic exclusion, credential recognition

**Partner tech (all load-bearing):**
- **Gemini 3** - multimodal CV + certificate extraction, skill mapping, long-context matching against live job boards
- **Tavily** - live scrape of Bundesagentur fuer Arbeit, StepStone, LinkedIn public listings
- **Qontext** - stores the candidate's skill graph across sessions so follow-ups get smarter
- **Gradium** - voice interface for users who can't type well in German
- **Lovable** - the candidate dashboard

**The wow moment:** A teammate drops in a photo of a real Ukrainian engineering diploma + a 30-second voice note in broken German describing 8 years of experience. Ninety seconds later: 12 ranked Berlin roles with realistic match scores, one-click CV tailored per role, and "add PostgreSQL in 3 weeks via this free course to unlock 47 more roles."

**Technical complexity:** High. Multimodal + translation + credential-equivalence reasoning + live market scraping + ranking.

**Feasibility in 15h:** Yellow. Pre-scrape 200 live Berlin job listings on Saturday night so the demo is fast. Credential-equivalence logic is the interesting engineering.

**Business potential:** Paid by integration employers (diversity hiring quotas, Bundesagentur contracts), refugee NGOs, corporate CSR budgets. Market parallel: Handshake for students, Welcome.US for refugees. Germany has no equivalent.

**First-person authority:** Maximum for Ian. Currently job-hunting in Berlin, has lived the "my skills don't map cleanly to German job posts" frustration, and WorkScanAI is literally the employer-side inverse of this.

**Scores:** Creativity 5/5, Complexity 5/5, Partner fit 5/5, First-person authority 5/5, Business story 5/5
**Average: 5.0/5**

---

### Idea 4 - MedStockNow: find the medicine you can actually get today

> Patient or caregiver types or voice-dictates a drug name. In under 60 seconds, the agent returns: live stock across nearby pharmacies with distance and price, legal generic equivalents with price delta, insurance-coverage status per option, and - if everything is out - an automated phone call to the top 3 pharmacies asking expected restock time. For high-cost drugs, surfaces patient-assistance programs the patient qualifies for.

**Theme:** Medicine access, care for the chronically ill

**Partner tech (all load-bearing):**
- **Gemini 3** - drug-name parsing (misspellings, brand vs active ingredient), generic-equivalence reasoning, eligibility filtering
- **Tavily** - live pharmacy stock scraping (several German chains publish this), drug shortage feeds from BfArM
- **telli** - places the real phone call to pharmacies to confirm stock / restock
- **Gradium** - voice input for elderly users who won't type long drug names
- **ai|coustics** - cleans the live pharmacy call audio for reliable transcription

**The wow moment:** Live on stage, type "Eliquis 5mg" into the phone. Screen shows 4 nearby pharmacies (2 out, 1 in, 1 unknown), the agent auto-dials the unknown one through telli, and 40 seconds later the pharmacist's answer is transcribed back into the dashboard: "yes, 12 packs in stock." The jury will clap.

**Technical complexity:** High. Drug reasoning + live stock + real phone calls + insurance logic is four non-trivial layers.

**Feasibility in 15h:** Yellow. We curate a drug list of 50 common chronic-illness meds and pre-seed pharmacy data; live phone call is the one piece we demo end-to-end.

**Business potential:** B2C freemium (free lookup, premium subscription for auto-reminders and insurance navigation). B2B: insurers (Krankenkassen reduce claims when adherence goes up), pharmacy chains paying for routing traffic, patient-assistance program orgs paying for qualified referrals.

**Scores:** Creativity 4/5, Complexity 5/5, Partner fit 5/5, First-person authority 3/5, Business story 5/5
**Average: 4.4/5**

---

### Idea 5 - TriageLine: WhatsApp-first multilingual symptom triage

> In Berlin, hundreds of thousands of residents don't have a Hausarzt and can't easily get one. A user sends symptoms to a WhatsApp number in any form - text, voice, or a photo of a rash or eye. Agent runs a safe structured triage in the user's language (Turkish, Arabic, Ukrainian, Russian, English, German), outputs a clear next step - "ER now", "GP within 3 days", "self-care, here's what to watch for" - and for urgent cases calls KV-116117 or finds an open walk-in clinic in real time.

**Theme:** Treatment access, healthcare inequality, language barriers

**Partner tech (all load-bearing):**
- **Gemini 3** - multimodal (text + voice + image) + multilingual safety-critical reasoning
- **Gradium** - voice input/output for users who can't read well in any written language
- **ai|coustics** - cleans symptom voice notes recorded in noisy home conditions
- **telli** - makes the outbound triage booking call to 116117 or walk-in clinics
- **Tavily** - live walk-in clinic availability

**The wow moment:** Send a WhatsApp voice note in Turkish describing chest pain and nausea. Twenty seconds later, the system replies in Turkish: "this is potentially a cardiac event, calling 116117 for you now" - and you hear the agent place the call live.

**Technical complexity:** Very high - safety-critical multilingual medical reasoning with voice + vision + phone dispatch. Jury will respect this.

**Feasibility in 15h:** Yellow. Scope to 3 languages and 5 symptom categories. The safety framing (clear "not a doctor" disclaimer, always defaults to escalation on ambiguity) is critical and must be on-screen in the demo.

**Business potential:** Paid by public health authorities (Senatsverwaltung fuer Gesundheit, equivalents in other cities), by NGOs serving migrant health, by employers providing health benefits. Adjacent market: Babylon Health, Ada Health - both have grown into major businesses.

**Safety note:** The demo must foreground the safety disclaimer; the jury's January winner built in healthcare and the jury rewarded responsibility, not just cleverness.

**Scores:** Creativity 5/5, Complexity 5/5, Partner fit 5/5, First-person authority 3/5, Business story 5/5
**Average: 4.6/5**

---

### Idea 6 - BenefitRecovery: the EUR 3,000 you never claimed

> Billions in German welfare benefits go unclaimed every year because the rules are too complex - Wohngeld, Kinderzuschlag, Bildungspaket, Buergergeld top-ups, energy-relief, city-level programs. User answers 5 questions by voice. Agent figures out which federal, state, and city-level benefits they qualify for, totals the annual sum, pre-fills every form, and books the Termine. Monetization: success-fee cut on the first year's recovered amount.

**Theme:** Income fairness, hidden entitlements, bureaucratic exclusion

**Partner tech (all load-bearing):**
- **Gemini 3** - navigates the decision tree across many overlapping programs; generates pre-filled forms
- **Tavily** - current rule tables for each program (these change every year, hard-coding is a trap)
- **telli** - books the Termine at Jobcenter, Wohngeldstelle, Familienkasse
- **Qontext** - maintains the household state across multiple applications
- **Lovable** - the dashboard with the big "you qualify for EUR 2,860 per year" number front and center

**The wow moment:** A teammate pretends to be a single parent with 2 kids earning EUR 2,100/month. Ninety seconds of voice conversation later: "you qualify for Wohngeld EUR 147/month, Kinderzuschlag EUR 250/month, Bildungspaket annually EUR 380 - total EUR 5,144/year you're not getting." Forms appear pre-filled with placeholders for sensitive fields.

**Technical complexity:** High. The eligibility reasoning across federal + state + city programs is the real engineering.

**Feasibility in 15h:** Green. Most of the work is prompt engineering + a good form-filler. Scope to Berlin residents + 4 programs.

**Business potential:** Very strong. Proven model: UK's "Billy", "Entitledto", US "Benefits.com" all raised serious rounds. German market is even more fragmented (good for a tech wedge) and has no dominant player. Revenue: 10-20% success fee or EUR 9.99/month subscription.

**Scores:** Creativity 5/5, Complexity 4/5, Partner fit 5/5, First-person authority 3/5, Business story 5/5
**Average: 4.4/5**

---

### Idea 7 - RentShield: know exactly what your landlord is overcharging you

> Tenant uploads their Mietvertrag (photo or PDF). Agent extracts Kaltmiete, Nebenkosten, apartment size, year of build, district. Cross-references the official Berlin Mietspiegel and current comparable listings. Returns a one-pager: "your rent is EUR 187/month above the legal Mietspiegel range for your apartment class. Here is the BGB paragraph to cite, a ready-to-send Mietminderung letter, and Berlin tenants win this in court with ~85% success rate."

**Theme:** Income fairness, housing, legal empowerment

**Track fit:** Buena (property track prize)

**Partner tech (all load-bearing):**
- **Gemini 3** - OCR + extraction from messy contract PDFs; legal reasoning against Mietspiegel tables
- **Tavily** - live comparable-listing lookup for sanity check
- **Qontext** - stores the tenant's evidence pack across the multi-week dispute process
- **Lovable** - the dashboard + the letter-generation UI
- **Aikido** - security framing matters when the input is a signed legal contract

**The wow moment:** A teammate uploads a real (anonymized) Mietvertrag. Thirty seconds later, the screen shows the overcharge calculation, the BGB paragraph highlighted, and a complete Mietminderung letter ready for German postal mail.

**Technical complexity:** Medium-high. OCR + legal-rule reasoning against structured Mietspiegel data + letter generation in formal German.

**Feasibility in 15h:** Green. Mietspiegel tables are public, BGB is public, formal letter template is straightforward. The OCR/extraction step is the risk; pre-test with 5 real contracts on Saturday night.

**Business potential:** Strong. Proven model: British "Resolver" and "Flatfair", German "Conny" (formerly wenigermiete.de) - Conny does exactly this and sued landlords on behalf of tenants for tens of millions of EUR. They were acquired by LexFox. A voice-first, AI-native version is a credible wedge into the same market.

**First-person authority:** Universal in Berlin. Every resident of Berlin has an opinion about rent; a Berlin jury will feel this one immediately.

**Scores:** Creativity 5/5, Complexity 4/5, Partner fit 5/5, First-person authority 5/5, Business story 5/5
**Average: 4.8/5**

---

### Idea 8 - CareCall: weekly voice check-ins for elderly chronic-illness patients

> Elderly patients with diabetes, heart failure, or COPD decompensate between GP visits because nobody is watching. CareCall auto-dials the patient weekly (voice-only, no app, no smartphone), runs a 5-minute condition-specific protocol - "how is your breathing today on a scale of 1 to 10; did you take your evening meds; have you weighed yourself" - flags red flags for the GP or community nurse, and just talks warmly for a minute because isolation itself is a health risk.

**Theme:** Chronic illness management, elder care, healthcare cost reduction

**Partner tech (all load-bearing):**
- **telli** - the core product. Places warm, reliable outbound calls at scheduled times.
- **Gradium** - voice conversation with natural cadence (elderly patients hate robotic TTS)
- **ai|coustics** - critical: elderly patients often have poor mics, hearing aids, or background TV
- **Gemini 3** - protocol reasoning + red-flag detection + empathetic conversation
- **Qontext** - tracks the patient's trajectory week over week, surfaces "this is the third week they've mentioned dizziness"

**The wow moment:** Live on stage, trigger a call to a teammate playing an 80-year-old with diabetes. The full natural conversation plays out on speakerphone. At the end, a dashboard lights up: "red flag - patient reports 2kg weight gain in 5 days and increased swelling. Notify GP."

**Technical complexity:** High. Voice naturalness + clinical protocol adherence + red-flag detection + multi-week memory.

**Feasibility in 15h:** Green. telli handles the hard parts; we own the conversation flow and dashboard.

**Business potential:** Very strong and underserved in Germany. Paid by Krankenkassen (insurers), because preventing one hospital readmission saves them EUR 5,000+. US parallels: Papa, Honor - both have raised hundreds of millions. German Krankenkassen have explicit mandates to fund preventive care.

**Scores:** Creativity 4/5, Complexity 5/5, Partner fit 5/5, First-person authority 3/5, Business story 5/5
**Average: 4.4/5**

---

### Idea 9 - WageRadar: know your real market rate before you sign

> Job-seeker pastes an offer letter or job description. Agent pulls live comparable salaries from Kununu, Glassdoor, StepStone, LinkedIn, adjusts for role, years of experience, city, company size, and reports: "your offer is 12% below market median for your profile. Here are the 3 highest-leverage asks for your negotiation, based on what this company has conceded in past hires." Then: voice role-play where the agent plays the recruiter and the user practices the negotiation call live.

**Theme:** Income fairness, wage transparency, hiring asymmetry

**Partner tech (all load-bearing):**
- **Gemini 3** - offer decomposition, comparable synthesis, negotiation coaching reasoning
- **Tavily** - live salary-data scraping + company-specific negotiation signal (Kununu reviews mention "they flex on signing bonus")
- **Gradium** - the voice role-play (this is the demo)
- **ai|coustics** - cleans the role-play audio so the feedback module can score tone
- **Lovable** - the dashboard

**The wow moment:** Live on stage, a teammate takes a 60-second negotiation role-play call. At the end, the dashboard shows a scored transcript: "you conceded too early on base; you missed the signing bonus leverage; here is the sentence you should have said."

**Technical complexity:** Medium-high. The voice role-play with scored feedback is the technical flex.

**Feasibility in 15h:** Green. Salary data scraping + a well-prompted role-play + basic scoring is doable.

**Business potential:** Strong B2C subscription potential (Levels.fyi has proven users pay for salary transparency). B2B: executive coaching firms, career-transition programs, MBA career offices, diversity hiring orgs (closing the gender pay gap starts with knowing the gap).

**First-person authority:** High for Ian as an active job-seeker negotiating offers right now.

**Scores:** Creativity 4/5, Complexity 4/5, Partner fit 5/5, First-person authority 5/5, Business story 5/5
**Average: 4.6/5**

---

### Idea 10 - FoodRescue: redirect tonight's restaurant surplus to the people who need it

> Restaurants, bakeries, and supermarkets throw away roughly a third of their daily stock every evening. Food banks and shelters can't plan around ad-hoc donations. FoodRescue is a two-sided voice agent. At closing time, restaurant staff dictate a 10-second voice note: "8kg bread, 20 pastries, 12 salads, available until 10pm." Agent auto-matches to the nearest food bank or shelter with capacity and the right dietary mix, and dispatches a volunteer driver via phone call. Zero app install on the donor side.

**Theme:** Food access, food waste, urban inequality

**Partner tech (all load-bearing):**
- **Gemini 3** - parses messy voice notes about inventory + matches by dietary mix, capacity, distance
- **Gradium** - voice capture from restaurant staff during closing crunch
- **ai|coustics** - restaurant kitchens are loud; audio cleanup is load-bearing
- **telli** - dispatches volunteer drivers and confirms pickup windows
- **Lovable** - the coordinator dashboard for the food bank

**The wow moment:** A teammate playing a pizzeria owner dictates tonight's surplus into their phone. Twenty seconds later, a volunteer driver's phone rings (live, on stage), the driver accepts, and the food-bank dashboard updates with ETA. Zero friction on the restaurant side.

**Technical complexity:** Medium-high. Voice parsing under real conditions + multi-agent coordination + phone dispatch.

**Feasibility in 15h:** Green. telli does the hard phone part; the matching logic is straightforward.

**Business potential:** Paid by restaurant chains as part of ESG/CSR budget (tax-deductible in Germany), by corporate sponsors wanting impact metrics, by municipalities. Parallels: Too Good To Go (unicorn, Danish), Olio (UK). Neither owns the operational food-bank side; that's the wedge.

**Scores:** Creativity 5/5, Complexity 4/5, Partner fit 5/5, First-person authority 3/5, Business story 5/5
**Average: 4.4/5**

---

### Idea 11 - AidMatch: refugee and migrant credential recognition, done in a day not a year

> A newly-arrived asylum seeker or migrant brings whatever documents they have - diplomas, work references, licensing certificates - often in Arabic, Farsi, Ukrainian, Tigrinya. Germany's official credential-recognition process (Anerkennung) takes 6-18 months. AidMatch does a first-pass equivalence assessment in 5 minutes: "your Syrian medical degree maps to German Approbation requirements as follows; here are the 3 exams you need; here is a specific Landesaerztekammer contact in Berlin; here are 2 pre-Approbation roles you could take today that count as experience." Handles teachers, nurses, electricians, engineers - not just doctors.

**Theme:** Employment access, integration, recognition of foreign qualifications

**Partner tech (all load-bearing):**
- **Gemini 3** - multimodal + multilingual credential parsing + mapping to German professional frameworks
- **Tavily** - live search of Landesaerztekammer, Handwerkskammer, IHK, BQ-Portal resources
- **telli** - books orientation calls at the relevant Kammer
- **Gradium** - voice-first intake for users with low German literacy
- **Qontext** - multi-session memory as the user progresses through the recognition journey

**The wow moment:** A teammate uploads a genuine Syrian nursing diploma (translated) and a work reference. Ninety seconds later: a precise mapping against Krankenpflege requirements, the specific Kenntnispruefung the user needs, the Berlin contact point, and 3 bridging roles they can do right now while waiting.

**Technical complexity:** Very high. Cross-language credential parsing + German professional framework + live Kammer data + journey state.

**Feasibility in 15h:** Yellow. Scope tightly - 3 professions (nursing, engineering, one Handwerk trade), 4 source languages.

**Business potential:** Paid by the German federal government (BQ-Portal has explicit modernization budget), by staffing agencies (the healthcare staffing crisis is acute), by corporate diversity programs, by NGOs. German shortage of skilled workers is a national-priority political issue.

**Scores:** Creativity 5/5, Complexity 5/5, Partner fit 5/5, First-person authority 4/5, Business story 5/5
**Average: 4.8/5**

---

### Idea 12 - AquaAlert: satellite drought early warning for smallholder farms

> Smallholder farmers in drought-prone regions lose harvests because they learn about water stress only when crops visibly fail - too late. AquaAlert takes a farm's coordinates (GPS pin, voice-described landmark, or a photo), pulls Sentinel-2 satellite imagery weekly, combines with local weather and soil data, and sends a voice message in the farmer's language: "your north field will be water-stressed in 8 days; here is your irrigation priority order; here is the subsidy program you qualify for if you install drip irrigation, with the application form pre-filled."

**Theme:** Water access, food security, climate resilience

**Partner tech (all load-bearing):**
- **Gemini 3** - multimodal reasoning over satellite imagery + weather + soil data; generates personalized advice in local language
- **Tavily** - live weather forecasts, subsidy program data, local agricultural extension resources
- **Gradium** - voice message output in local language; voice input from farmers who can't read
- **telli** - optional follow-up call with the farmer to confirm actions; call to subsidy office
- **Qontext** - tracks the farm across seasons, learns which advice the farmer actually acts on

**The wow moment:** Live on stage, drop a coordinate pin on a farm in (say) southern Spain or Kenya. Ten seconds later: a color-coded satellite image of the farm's fields, stress prediction for each parcel, a voice message in Spanish/Swahili, and the subsidy application form pre-filled.

**Technical complexity:** Very high. Vision on satellite imagery is the core technical flex. Combining it with weather data and local subsidies is the product wedge.

**Feasibility in 15h:** Yellow. Satellite imagery is available free via Copernicus. The vision-reasoning step is the wildcard; prototype early on Saturday night with a fallback of "pre-run analysis on 3 demo farms" if live Gemini vision accuracy is insufficient.

**Business potential:** Paid by agri-insurance providers (index insurance pricing), by agricultural input companies (Bayer, BASF, Syngenta have channel budgets for African/Latin American markets), by development finance orgs (KfW, IFC). Real money flows through smallholder agriculture via carbon credits and climate-adaptation grants.

**Scores:** Creativity 5/5, Complexity 5/5, Partner fit 4/5, First-person authority 2/5, Business story 4/5
**Average: 4.2/5**

---

### Summary ranking

| # | Idea | Theme | Score | Why it ranks here |
|---|---|---|---|---|
| 3 | **JobMatch Reverse** - candidate-first job platform | Employment access, Ian's authority | **5.0** | Max first-person authority for Ian; WorkScanAI inverse; huge TAM with no German player. |
| 7 | **RentShield** - Mietspiegel enforcement | Housing fairness, Buena track | **4.8** | Track prize shot + every Berliner feels this + legal-grade output is unforgettable demo + proven business model (Conny). |
| 1 | **HireSignal** - JD to adaptive skills interview | Hiring fairness, Ian's authority | 4.8 | Strongest personal story + voice + adaptive is a genuine technical flex. |
| 11 | **AidMatch** - refugee credential recognition | Employment access, integration | 4.8 | Nationally strategic problem + multimodal + political tailwinds + direct government buyer. |
| 5 | **TriageLine** - multilingual WhatsApp triage | Healthcare access | 4.6 | Safety-critical health tech; multilingual is killer in Berlin; Ada/Babylon precedent. |
| 9 | **WageRadar** - negotiation coach | Income fairness, Ian's authority | 4.6 | Voice role-play is a jury-pleaser; Levels.fyi precedent; Ian's authority. |
| 4 | **MedStockNow** - medicine + pharmacy routing | Medicine access | 4.4 | Dramatic live-call demo; strong B2B2C model. |
| 6 | **BenefitRecovery** - unclaimed welfare | Income fairness | 4.4 | Billy/Entitledto precedent; "we found you EUR 2,860" line is unbeatable. |
| 8 | **CareCall** - elderly chronic-illness check-ins | Disease / elder care | 4.4 | telli's core use case; Papa/Honor precedent; Krankenkassen ready to pay. |
| 10 | **FoodRescue** - restaurant surplus routing | Food access | 4.4 | Two-sided dispatch demo is visible impact; Too Good To Go precedent. |
| 2 | **StandUpAgent** - async voice standup | Universal dev pain | 4.2 | Universal relatability; weaker jury differentiation. |
| 12 | **AquaAlert** - drought early warning | Water / food security | 4.2 | Strong problem, less Berlin-immediate; vision-on-satellite is a technical flex. |

### The meta-observation

**Four ideas now sit in the top tier (5.0 / 4.8 / 4.8 / 4.8):** JobMatch Reverse, RentShield, HireSignal, AidMatch. All four have genuine first-person authority available (Ian as job-seeker, anyone living in Berlin for RentShield, Ian for HireSignal, and the city is full of people living AidMatch's problem who could be pitched to join the team on Saturday morning).

**Business-model quality is the new explicit filter.** Every top-tier idea names a credible customer who will pay. RentShield has Conny as a proven EUR-tens-of-millions reference. BenefitRecovery has Billy. FoodRescue has Too Good To Go. CareCall has Papa and Honor. WageRadar has Levels.fyi. Pitching against a known analog is strategic: the jury does not have to imagine the business, only the wedge.

**Google DeepMind (primary sponsor) publicly backs "AI for good" initiatives** including the Norrsken / Nvidia / Lovable Fixathon. Humanitarian framing is unlikely to be penalized by this specific jury mix; it is plausibly rewarded.

**Tiebreaker rule:** When creativity, complexity, and partner fit are tied at the top, pick the idea whose opening video line the team can tell truthfully in first person. Then: pick the one with the cleanest already-public business analog, so the pitch earns less imagination debt.

**Strong recommendation:** Lock the final call between **JobMatch Reverse** and **RentShield**. JobMatch Reverse if Ian wants the idea most-aligned with his current life and post-hackathon trajectory. RentShield if the team wants a track-prize double shot and a more politically charged pitch.

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
- Matchmake aggressively. If someone at the event has exactly the domain authority our idea needs (a nurse for a health idea, a landlord for TenantTriage), **invite them onto the team**. Teams of 4-5 out-deliver teams of 2 in the final 3 hours.

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
| **Domain / Pitch** | Owns the problem framing, talks to sponsor mentors, writes the pitch deck, narrates the video. Does light frontend or data work as bandwidth allows. | 1 (critical if the pitch needs domain credibility - see MedAccura) |

### Ian's stack fits these slots cleanly

Given Ian's Next.js / FastAPI / Claude-or-Gemini integration experience plus the WorkScanAI muscle memory for ingestion + agent orchestration, **Lead / Architect** is the natural slot - with the option to float into Backend if a teammate has stronger product-design chops.

### Tooling expectations on the day

- Desktop Commander MCP + Claude in Chrome MCP are force multipliers - walk teammates through these in the first hour. File edits, git ops, browser automation for testing all run through them.
- Git repo: one of us creates the repo at 10:30 (right after kickoff briefing), branch = `main`, no PR workflow, just direct commits. Hackathon mode, not production.
- Decision log: pinned Discord thread or a `DECISIONS.md` in the repo - every non-trivial fork gets one line. When the 2am exhaustion hits, this is how we avoid re-litigating.

---

## Timeline: Saturday night → Sunday 14:00

### Saturday (pre-night)

| Time | What's happening | Our move |
|---|---|---|
| 10:00 | Doors open, networking | Arrive, set up, scope out sponsor mentors for the tools we want to use |
| 10:30 | Opening & matchmaking | If our team isn't full, recruit. Target: domain-authority teammate if our idea needs one. |
| 12:30 | Lunch | **Idea locked by now.** Eat fast. |
| 13:00-19:00 | Most teams start building | We're still planning and skeleton-scaffolding. Don't panic. |
| 19:00 | Dinner | Last checkpoint before the real sprint. Eat, then begin the actual build. |
| 20:00 | **Idea lock hard deadline** | If still flip-flopping, commit to the highest-scoring option. No more debate. |

### Saturday night → Sunday (the real ~15h sprint)

| Time | Goal | Output |
|---|---|---|
| 20:00-22:00 | **Skeleton + partner integrations smoke-tested** | Each of the 3+ partner APIs returns a real response. No UI yet. |
| 22:00-00:00 | **Happy-path end-to-end** | One input goes in, one usable output comes out - even if ugly. |
| 00:00-02:00 | **The "wow moment" works** | The single demo-video shot is reliable and reproducible. |
| 02:00-04:00 | Sleep rotation. At least 2 people sleep 3-4h. Nobody codes on no sleep past this point. |
| 04:00-07:00 | **Second pass on core + edge cases** | Demo doesn't break on the second run. |
| 07:00-10:00 | Everyone back. **Polish pass.** | UI cleanup via Lovable, copy polish, error handling on the demo path. |
| 10:00-12:00 | **Record the 2-minute submission video** | Multiple takes. Best take wins. |
| 12:00-13:30 | Buffer for technical issues + upload | Submit **early**, not at 13:59. |
| 14:00 | **Submission deadline** | Don't be the team that missed it. The article noted some teams didn't submit in time. |
| 15:30 | Finalists announced (3 teams) | - |
| 16:00 | Finalist pitches (5 min each) | If we're here, pitch rehearsal happens during the 15:00 wait. |
| 17:30 | Award ceremony | - |

### The 3 rules we will not break

1. **No new features after 02:00.** After 2am we only polish what works.
2. **No debugging during the video recording window (10:00-12:00).** If something breaks at 10:30, we cut it from the demo and record without it.
3. **Submit by 13:30.** One hour of buffer before the 14:00 deadline is non-negotiable.

---

## Submission checklist

Exactly what the jury sees. Nothing more, nothing less.

- [ ] **2-minute video** (hard ceiling). Shows: the problem, the wow moment (single clean shot), partner tools credited visibly, one sentence on "what we'd do next."
- [ ] **Working demo URL** (Lovable / Vercel / wherever). Reliable on Sunday afternoon network conditions.
- [ ] **GitHub repo** public with a README that credits every partner tool used.
- [ ] **One-slide deck** for the optional live pitch if we make finalists.
- [ ] **Team names + contact** on the submission form.
- [ ] **Partner tools list** explicitly listed - judges give bonus points for effective use; make it easy for them to check.

### The 2-minute video skeleton

- 0:00-0:15 - The problem, told as a first-person story. Not "businesses face a challenge in..." - **"Last Tuesday I was..."**
- 0:15-0:30 - What we built, in one sentence. Show the name and logo.
- 0:30-1:30 - The demo. One continuous shot if possible. This is where the wow moment lives.
- 1:30-1:45 - Which partner tools and how each one is load-bearing (one sentence each).
- 1:45-2:00 - What this becomes if we keep building. **Include the "we're keeping going after the hackathon" line.** MedAccura did this, and the jury responded.

---

## Appendix: what we learned from the January 2026 edition

Source: Leandra Finke's coverage in Gründerszene / Business Insider, 27 January 2026.

- **105 participants from 600 applicants** - ~6x oversubscribed. Expect similar at Big Berlin Hack.
- **27 projects submitted** out of ~30 teams - some didn't finish. Being in the "submitted" cohort already filters you into the top 90%.
- The jury evaluated on **creativity + technical complexity**, with **bonus points for effective partner tech use**. This exact rubric is the one we're optimizing for.
- The winner's jury citation emphasized **"great technical depth realized in a very short time"** and **real-world impact** - framing that rewards working software over slideware.
- Organizer Bela Wiertz's on-the-ground philosophy: *"The goal isn't maximum complexity - it's joy in the product. It's allowed to be light as long as it works."* We take this seriously. Don't over-engineer.
- The winning team explicitly said they'd **continue the project after the event**. Jury likes signals of durability.

---

## Contact

Ian - Full-stack / project lead
🌐 [ianworks.dev](https://ianworks.dev)
💼 [linkedin.com/in/avoiann](https://linkedin.com/in/avoiann)
💻 [github.com/ibxibx](https://github.com/ibxibx)

Berlin AI/tech community: GlobalAI Berlin, AgentCon Berlin 2026.

---

**See you at Delta Campus, 25 April. 🚀**
