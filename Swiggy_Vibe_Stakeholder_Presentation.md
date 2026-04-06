# Swiggy Vibe — Mood-Based Discovery Stakeholder Presentation

**Author:** Product Manager (Swiggy)  
**Date:** April 6, 2026  
**Audience:** Engineering, Design, Ops, Merchant Success, Marketing, Data/ML

---

## Slide 1 — Title Slide
**Swiggy Vibe: Mood-Based Discovery**  
*Help users find food that matches how they feel*
- Launch Pilot: H2 2026 (2–3 metro cities)
- Expected Impact: +15% discovery-to-cart conversion
- Investment: ~8 weeks engineering

---

## Slide 2 — The Problem
**Choice Overload = Friction**
- Current discovery optimized for cuisine/deals, NOT emotional context
- Users browse > 10 mins on average before ordering
- ~30% abandon after reaching restaurant list
- Merchants miss customers who need "comfort" or "celebration" cues

**The Opportunity:**  
Surface mood-aligned recommendations → reduce friction + increase order conversion

---

## Slide 3 — Vision & User Need
**Vision:** Every user discovers food that matches their mood in one tap.

**User Personas:**
- **Ria (Overworked Corporate):** After long workday, wants "Comforting" meal instantly
- **Karan (Late-Night Student):** Studying late, craves spicy "Late Night" options on budget
- **Meera (Weekend Family):** Plans family meal, browses "Celebration" or "Healthy" for variety

**Insight:** Mood is a powerful signal that drives both engagement and AOV

---

## Slide 4 — Product Overview
**Swiggy Vibe = 3 core components:**

1. **Mood Picker (Mood-O-Meter)**
   - 6–8 mood cards (Comforting, Indulgent, Healthy, Quick & Light, Celebration, Budget Friendly, Exotic)
   - Mobile-first, card-based UI with mood icons
   - Tap to select → instant curated results

2. **Mood Results Page**
   - Hero section: "Season of Celebration" curated picks
   - Ranked restaurants with mood relevance badges
   - Filters: price, delivery time, dietary tags
   - One-tap combos for quick ordering

3. **ML-Powered Tagging System**
   - Heuristic keyword mapping (Phase 1): "comfort," "indulgent" in descriptions/reviews
   - LLM sentiment analysis (Phase 1.5): scan 100k+ SKUs, assign mood probabilities
   - Visual recognition (Phase 2): color, texture → mood (e.g., rich saturation = Indulgent)

---

## Slide 5 — Key Features & UX
**Homepage Integration:**
- Mood cards appear below search bar, above standard discovery
- Horizontal scroll for easy exploration
- First-time users see tooltip: "Discover food that matches how you feel"

**Mood Results Experience:**
- Full-width hero with mood-themed gradient (e.g., orange for Comforting)
- 3–5 featured "Top Picks" cards in carousel
- Below: ranked restaurant list (40–50 results), each with:
  - Mood relevance badge
  - Delivery time, rating, distance
  - One-tap "Order Now" or "View Combos" CTA

**Onboarding:**
- Light modal on first exposure: explain Vibe, ask for contextual signals (time, location)
- No heavy data requests; privacy-first approach

---

## Slide 6 — Business Impact & Monetization
**Conversion Uplift:**
- Target: +15% Discovery-to-Cart for Vibe-engaged users (vs baseline)
- Expected AOV lift: +3% via strategic mood bundling
- Retention: +2 pp for 30-day repeat users

**New Revenue Streams:**
- Premium mood-specific featured slots for merchants
- Sponsored mood collections (e.g., "Celebration Feast by Brand X")
- Merchant bid system for top-5 placements per mood

**Merchant Fairness:**
- Enforce 60% local-favorites minimum in top 10 results
- Rotational exposure for sponsored slots
- transparent analytics dashboard for merchants

---

## Slide 7 — North Star Metric & KPIs
**North Star:** Discovery-to-Cart Conversion Ratio

$$\text{D2C} = \frac{\text{# Vibe Sessions with Add-to-Cart}}{\text{# Vibe Sessions}}$$

**L1 Metrics (Direct Product):**
- Vibe Impression Rate: ≥ 20% of sessions
- Vibe CTR: ≥ 8% (clicks on mood cards)
- Vibe Conversion Rate: ≥ 12%
- Time-to-order: ≤ 5 mins from Vibe entry

**L2 Metrics (Business):**
- AOV (Vibe orders vs baseline): +3%
- Cancellation rate: ≤ baseline + 5%
- 30-day retention lift: +2 pp

**Guardrail Metrics (Must Not Degrade):**
- Overall platform conversion: no negative impact
- Delivery ETA accuracy: ±10% of baseline
- Merchant satisfaction: ≥ 4.0/5.0 from pilot partners

---

## Slide 8 — Pilot Plan & Rollout
**Phase 0 (Weeks 1–2):** Design Finalization, Stakeholder Approvals
- Wireframes review & sign-off
- ML taxonomy definition
- Feature flag + experiment setup

**Phase 1 — Internal Beta & QA (Weeks 3–5)**
- Build backend (Vibe API, ranking service)
- Build mobile frontend components
- Internal QA, ops training
- Merchant onboarding (pilot partners)

**Phase 2 — Pilot Launch (Weeks 6–10)**
- Roll out to 2–3 metro cities (Bangalore, Mumbai, Hyderabad)
- 10% randomized traffic assignment (control vs treatment)
- Daily monitoring of KPIs
- Weekly sync with stakeholders

**Phase 3 — Iterate & Scale (Weeks 11–16)**
- Analyze pilot results (success gates: p < 0.05, +15% conversion uplift)
- Refine ranking, UX, merchant incentives
- Expand to top 20 cities
- Enable full merchant monetization

---

## Slide 9 — Risks & Mitigations
| Risk | Mitigation |
|------|-----------|
| **Mood Misinterpretation** — Wrong mapping → irrelevant suggestions | Editorial oversight; conservative thresholds (conf > 0.6); easy feedback/dismiss UX |
| **Echo Chamber** — Users stuck in unhealthy mood loops | Inject "Surprise Me" card every 5th session; monitor dietary diversity per user |
| **Logistics Surge Pressure** — "Rainy Day" mood surge overloads ops | Real-time ETA-aware ranking; cap featured distant merchants; ops comms to partners |
| **Merchant Fairness** — Sponsored slots crowd out local favorites | Enforce ≥60% local-favorites in top-10; rotational exposure; transparent analytics |
| **Privacy Concerns** — Inferring emotional state feels invasive | Explicit consent copy; session-scoped moods; easy opt-out; no 3rd-party data sharing (Phase 1) |

---

## Slide 10 — Critical Asks by Team
**Engineering (6 FTE-weeks):**
- Vibe API service (REST, feature flag integration)
- Mobile UI components (Mood Picker, Results page)
- Ranking microservice + LLM integration
- A/B testing harness & logging

**Design (2 FTE-weeks):**
- Mood color palette (Swiggy brand alignment)
- Mood icons & illustrations
- Component system updates
- One-tap combo UX flow

**Data/ML (4 FTE-weeks):**
- Heuristic tagging pipeline
- LLM fine-tuning for mood classification
- Feature store setup (mood_affinity per user)
- Offline & real-time ranking model

**Operations & Merchant Success (ongoing):**
- Merchant outreach & education
- Pilot partner FAQ & support
- Promotional calendar alignment

**Marketing (2 FTE-weeks):**
- Pilot launch copy & creative
- Social/in-app teasers
- Merchant comms & incentives

---

## Slide 11 — Timeline Overview
```
Week:    1-2     3-5        6-10          11-16
Task:    Design  Build      Pilot         Scale
         ├─ QA   ├─ FE/BE   ├─ Monitor    ├─ Expand
         ├─ Flags├─ ML       ├─ Analyze    ├─ Monetize
         └─ Ops  └─ Internal └─ Iterate    └─ Market
```

**Key Milestones:**
- **M1 (End Week 2):** Design + requirements sign-off
- **M2 (End Week 5):** Internal beta complete, ready for pilot
- **M3 (End Week 10):** Pilot results analyzed, go/no-go decision
- **M4 (End Week 16):** Scale decision + board readout

---

## Slide 12 — Success Criteria for Broader Rollout
**All of the following MUST be true to expand beyond pilot:**
1. ✓ Discovery-to-Cart conversion uplift ≥ 15% (p < 0.05)
2. ✓ No degradation in overall platform conversion (max -0.5 pp)
3. ✓ Cancellation rate ≤ baseline + 5%
4. ✓ Merchant participation ≥ 70% of active restaurants in pilot cities
5. ✓ User satisfaction (NPS) ≥ 40 on Vibe feature
6. ✓ No major safety/privacy incidents

---

## Slide 13 — Competitive Context & Timing
**Why Now?**
- Personalization expectations rising (Zomato Hyperpure, DoorDash Halls)
- Swiggy is #1 in discovery UX opportunity
- Seasonal/emotional signaling is underutilized in food delivery
- ML/LLM maturity enables low-cost tagging at scale

**Competitive Moat:**
- First-mover advantage in mood-based discovery
- Deep merchant relationships for seamless tagging
- Swiggy's design leadership + brand trust

---

## Slide 14 — Next Steps & Approvals Needed
**By End of This Week:**
- [ ] Product vision approval (CPO, VP Strategy)
- [ ] Engineering resource confirmation (6 FTE-weeks)
- [ ] Pilot city selection (Ops + Analytics)
- [ ] Baseline metrics collection (Analytics)

**By End of Next Week:**
- [ ] Design system updates reviewed
- [ ] API contract finalized
- [ ] Merchant outreach list ready

**First Pilot Partner Onboarding:**
- Week 3 launch

---

## Questions & Discussion
**Contact:** Product Manager (jainashishk@gmail.com)

**Appendix files available:**
- [Swiggy_Vibe_PRD.md] — Full product requirements
- [homepage_vibe_wireframe.svg] — Mobile UI mockup (Homepage)
- [mood_results_wireframe.svg] — Mobile UI mockup (Results)
- [Swiggy_Vibe_Gantt.md] — Detailed 8-week milestone plan
- [vibe_telemetry_schema.json] — Event schema for instrumentation
