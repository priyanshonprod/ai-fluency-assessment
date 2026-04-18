# AI Fluency Assessment Tool — Internal Brief

**Date:** April 18, 2026
**Owner:** Priyansh
**Status:** Live. MTP in progress with Palash.

---

## What This Is

An AI Fluency Assessment built for the Scaler Online PGP in Business & AI program. A 10-question, 3-minute web-based quiz that evaluates how AI-ready a working professional is — specific to their current role, their actual daily workflows, and the tools they should be using but aren't.

This isn't a generic "do you know what an LLM is" quiz. Every question is deeply role-specific. A Product Manager gets asked whether they've built AI-powered PRD workflows, prompt chains for spec generation, or multi-agent research systems. A Marketing person gets asked whether they're using AI for ad copy generation at scale, creative benchmarking, or CRO automation. An Ops Manager gets asked about AI demand forecasting, supplier intelligence, and logistics optimization.

**7 roles supported:**
- Product Manager
- Business / Strategy Consultant
- Operations / Supply Chain Manager
- Marketing / Growth Manager
- Tech Professional transitioning to Business
- Founder / Entrepreneur
- Finance / Commercial Manager

**How it works:**
- User logs in with name, email, phone number
- Selects their current role
- Answers 10 skill-area questions, each with 5 levels — from "I haven't touched this" to "I've built systems my entire org runs on"
- Each level has tangible, specific descriptions. Level 3 for a PM might say: "You have a go-to prompt that generates PRD sections — problem statement, user stories, success metrics, edge cases. You iterate with the model until the spec is tight. Your PRDs come out 2x faster." Level 5 says: "Your team's spec process runs through AI. New PMs use your prompt templates. Output quality is indistinguishable from a senior PM's manual work."
- Score out of 50, bucketed into 4 bands: **AI Curious** (10-18), **AI Aware** (19-28), **AI Capable** (29-38), **AI Leader** (39-50)

**Results screen shows:**
- Score with animated ring chart + stage thermometer (4 stages with visual indicator of where they land)
- Plain-English explanation of what their score means (written so anyone can understand it, no jargon)
- Full skill breakdown — all 10 skills with colored bars, grouped into "Where you're strong," "Other skills," and "Where you need work"
- Career transition path: Current Role → AI-Upgraded Role (e.g., "Operations Manager → AI-Driven Operations Leader")
- Specific skills they need to build for this transition — with label + short description per skill
- Coverage callout: "95% of these skills are covered in the Scaler Online PGP in Business & AI curriculum"
- CTA: Request a Callback (popup with phone confirmation) + Explore Curriculum link

**Live URL:** https://golden-kashata-1a0ebe.netlify.app
**GitHub:** https://github.com/priyanshonprod/ai-fluency-assessment

---

## The Problem This Solves

Two root problems have been killing OPGP conversion:

**1. Cold intent.** Leads arrive from ads without understanding why AI fluency matters for their specific role. BDAs spend the first half of every call just trying to establish "AI is important and you're behind." That's a losing position — you're pitching instead of consulting.

**2. No self-awareness of the gap.** Even leads who are somewhat interested don't know WHAT they're missing. They think "I use ChatGPT, I'm fine." They have no framework for understanding that there are 5 levels of AI fluency, that they're at Level 1-2 on most skills, and that Level 5 professionals are building systems that make them irreplaceable.

**What the assessment does:**
- Creates self-awareness of the gap BEFORE the sales conversation. The lead sees their score, sees the 5 levels, and realizes on their own: "I'm barely scratching the surface."
- Makes the gap specific and role-relevant. It's not abstract "AI is the future" — it's "you should be using AI to generate PRDs, build competitive intelligence pipelines, and automate stakeholder communication, and you're doing none of that."
- Pre-establishes the OPGP value prop. The results show exactly what skills they need, and that 95% of those skills are covered in the curriculum. By the time the BDA calls, the lead already knows what the program offers.
- Flips the call dynamic. Instead of "let me convince you AI matters," the conversation becomes "you already know the gap — let's talk about how you close it in 12 months."

---

## How It's Built

End-to-end, no backend dependency. Entirely client-side with a Google Apps Script webhook for data.

- **Frontend:** Single HTML file + data.js. Deployed on Netlify (CDN, instant loads). Inter font. Scaler brand design — dark navy login panel, white content areas, blue accents.
- **Data tracking:** Every user action fires an event to a Google Sheet via Apps Script webhook. Events tracked: `started`, `role_selected`, `question_answered` (per question, with question name and answer level), `completed` (with full score + all 10 skill names and levels), `requested_callback`, `clicked_curriculum`, `retook_test`.
- **Google Sheet has 3 tabs:**
  - **Raw Events:** Every single action logged with timestamp and user UUID
  - **Users:** One row per user, deduplicated. Shows: name, email, phone, role, status (started / in_assessment / completed), score, band, last question reached, whether they completed, requested callback, clicked curriculum, or retook the test
  - **Dashboard:** Live metrics with auto-calculating formulas — total started, % completed, % requested callback, % clicked curriculum, % retook test, average score, score distribution by band, drop-off analysis, role breakdown
- **No server, no database, no authentication backend.** Everything runs in the browser. Google Sheets is the data layer. Can be swapped to a proper backend later if needed.

---

## GTM Plan

**Phase 1 — Floor Distribution (active)**
- Palash is onboard and has shared the tool with BDAs
- BDAs send the assessment link to leads ON the call — the lead fills it out while the BDA is talking to them
- As the lead progresses through the questions, they see 5 levels per skill and realize they're at Level 1-2 on most. This creates the aha moment without the BDA having to pitch it
- After completion, the results screen shows their gaps, the transition path, and the curriculum coverage. The BDA can now reference specific skills: "You scored 2 out of 5 on AI-powered analytics — that's exactly what Module 7 of the program covers"
- The call shifts from convincing to consulting. Pain point is self-discovered, not imposed.

**Phase 2 — MTP with Palash (active)**
- Running as a managed test pilot
- Palash monitors: completion rate, callback request rate, and qualitative BDA feedback on whether it's changing call dynamics
- Collecting feedback from BDAs after the first 50 calls — what's working, what's confusing, are leads engaging or bouncing?
- Will adjust questions, copy, or flow based on BDA feedback

**Phase 3 — Paid Distribution (requested, pending approval)**
- Run the assessment link in a small paid ad set (Meta/Google)
- Measure: assessment start rate, completion rate, callback rate, and most importantly — VSL views and payments from assessment completers vs. non-completers
- If completers convert at a meaningfully higher rate, this becomes a top-of-funnel tool for paid campaigns, not just a sales enablement tool

---

## What We're Tracking

| Metric | Target | Why it matters |
|---|---|---|
| Total users started | Volume | Are BDAs actually sharing the link? |
| Completion rate | >70% | If people drop off, the questions are too hard or too long |
| Drop-off by question | Flag any Q losing >15% | Identifies which specific questions need rework |
| Callback request rate | >30% of completers | Direct signal of intent generated by the tool |
| Curriculum click rate | Track | Secondary intent signal |
| Retake rate | Track | Engagement signal — people re-engaging is good |
| BDA call quality shift | Qualitative, after 50 calls | The actual measure — is this changing conversations? |
| Completers → enrolled | Tracked downstream | The money metric |
| Role distribution | Track | Which roles engage most — informs ad targeting |
| Score distribution | Track | If everyone scores 40+, questions are too easy. If everyone is 10-15, too hard. |

---

## What's Next

- Monitor MTP results for 2 weeks
- Collect BDA feedback after first 50 calls — adjust questions/copy if needed
- If Phase 2 shows signal, push for Phase 3 paid approval
- Potential future: WhatsApp version of the same assessment (conversational format)
- Potential future: Personalized PDF report emailed to the lead after completion
