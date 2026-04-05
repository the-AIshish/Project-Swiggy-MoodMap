# Swiggy Vibe — Mood-Based Discovery (PRD)

**Author:** Product Manager — Swiggy

**Last updated:** 2026-04-05

## Executive Summary

Swiggy Vibe is a mood-based discovery feature that helps users discover restaurants, dishes, and experiences aligned with their current mood. Users can select or implicitly signal a mood (e.g., "Comforting", "Celebration", "Healthy", "Indulgent"), and Swiggy surfaces personalized recommendations, curated collections, and contextual offers. The feature aims to increase engagement, reduce decision friction, and improve order conversion and retention.

## Why now
- Increasing choice friction on the app leads to longer decision time and drop-offs.
- Personalization expectations: users expect contextual discovery experiences.
- Monetization: curated mood-based placements open up targeted promotions for merchants and brands.

## Problem Statement
Users spend cognitive effort browsing menus and listings when they just want a vibe-aligned meal quickly. The current search/discovery surfaces are optimized for cuisine or deals, not emotional context. This results in lower engagement and missed conversion opportunities for relevant merchants.

## Non-goals
- Replacing the core search/restaurant listing experience.
- Full voice-based mood detection in phase 1.
- **Direct integration with fitness trackers (Apple Health/Google Fit) for Phase 1.** We will keep mood selection session-based in the initial phase to minimize privacy friction and maintain user trust. Integration with external health ecosystems can be explored in Phase 2 after establishing baseline safety and retention metrics.

## Goals & Success Metrics
**Primary Goals:**

**Success metrics (initial 12 weeks):**

**Success Metrics (KPIs)**

**North Star:**
- Discovery-to-Cart Conversion Ratio (primary product-level indicator for Vibe effectiveness): defined as the fraction of Vibe sessions that result in an Add-to-Cart event.
- Formula (LaTeX):

	$${\text{Discovery\text{-}to\text{-}Cart}} = \dfrac{\text{# Vibe Sessions with Add\_to\_Cart}}{\text{# Vibe Sessions}}$$

**Guardrail Metrics (must not degrade):**
- Overall platform conversion rate (orders/sessions) — no negative impact > 0.5 percentage point.
- Average delivery ETA accuracy — remain within baseline ±10%.
- Cancellation rate for Vibe-attributed orders — must not exceed baseline by > 5%.

**L1 Metrics (direct product):**
- Vibe Impression Rate = Vibe.Impressions / App.Open.Sessions
- Vibe CTR = Vibe.Clicks / Vibe.Impressions
- Discovery-to-Cart (as above)
- Vibe Conversion Rate = Vibe.Orders / Vibe.Sessions

**L2 Metrics (supporting):**
- Time-to-order (median) from Vibe entry
- AOV for Vibe orders
- Retention lift (30-day) for users exposed to Vibe
- Revenue per 1k Vibe impressions

**How to compute Discovery-to-Cart with control comparisons (LaTeX):**

Let $S_{v}$ be Vibe sessions, $A_{v}$ be Vibe sessions with Add-to-Cart. For baseline sessions $S_{b}$ and $A_{b}$:

$$\text{D2C}_{v} = \frac{A_{v}}{S_{v}}, \quad \text{D2C}_{b} = \frac{A_{b}}{S_{b}}$$

Relative uplift:\

$$\text{Uplift\%} = 100 \times \frac{\text{D2C}_{v} - \text{D2C}_{b}}{\text{D2C}_{b}}$$

Statistical significance to be computed via two-proportion z-test on $(A_{v}, S_{v})$ vs $(A_{b}, S_{b})$.

**Go-To-Market (GTM) & Risks**

GTM Plan (high level):
- Pre-launch (2 weeks): internal beta with ops and merchant partners; collect curated collections and merchant tags.
- Pilot (4–6 weeks): rollout to 2–3 metros, marketing banners, merchant incentives for participating partners, measure KPIs.
- Expansion (6–8 weeks): refine ranking, onboard more merchants, introduce sponsored placements and brand partnerships.
- Full launch: national rollout, TV/digital marketing, seasonal mood campaigns.

Risks & Mitigations:
- Mood misinterpretation: Users may find mood suggestions irrelevant → Mitigation: conservative heuristics, clear CTAs, easy dismiss/feedback controls, and rapid model retraining with event labels.
- Logistics pressure during weather events ("Rainy Day" surges): Surges may increase ETAs and cancellations → Mitigation: real-time ETA-aware ranking, limit featured distant merchants, dynamic caps on sponsored exposure during surges, and ops communication to merchants.
- Privacy concerns: inference of emotional state may worry users → Mitigation: explicit consent copy, session-scoped selections, ability to opt-out and remove saved moods.
- Merchant fairness / transparency: sponsored clubs may crowd out local favorites → Mitigation: enforce local-favorite minimums and rotational exposure.

**Wireframes & Figma links**

- I created two lightweight SVG wireframes in the workspace for quick review:
	- [Homepage Vibe Wireframe](homepage_vibe_wireframe.svg)
	- [Mood Results Wireframe](mood_results_wireframe.svg)

*(If you'd like real Figma files, I can prepare a Figma spec and share a link; currently adding SVG mockups for local review.)*

**Stakeholder Presentation (draft)**

I added a slide deck draft in markdown: `Swiggy_Vibe_Stakeholder_Presentation.md` covering problem, goals, UX, business case, metrics, pilot plan, and asks.

**6–8 Week Milestone Gantt**

Added `Swiggy_Vibe_Gantt.md` with a week-by-week milestone plan covering design, build, pilot, iterate, and scale.

**Telemetry Event Schema (JSON)**

I added `vibe_telemetry_schema.json` containing event definitions and fields for instrumentation.

---

If you want, next I can:
- Export the wireframes as PNGs and generate a simple Figma spec.
- Convert the stakeholder markdown into PPTX.
- Start drafting API contracts for the Vibe backend.

## Non-goals
- Replacing the core search/restaurant listing experience.
- Full voice-based mood detection in phase 1.

## User Personas
- **Ria (Busy Professional):** Wants quick, comforting meals after work.
- **Amit (Weekend Planner):** Looks for discovery and novelty on weekends; receptive to suggestions.
- **Neha (Health-Conscious):** Prefers mood suggestions like "Healthy" or "Light" and filters accordingly.

## User Journeys
1. Quick decision: User opens app, taps `Vibe` on homepage, selects "Comforting", sees prioritized restaurants and one-tap combos, places order.
2. Discovery & browsing: User explores curated mood collections, taps individual restaurant, reads highlights, and saves a favorite.
3. Passive personalization: User doesn’t explicitly choose mood; system surfaces a small set of mood cards based on context (time, weather, past orders). User taps one and proceeds.

## Feature Overview
**Core components (phase 1):**
- Mood Picker UI (explicit): a horizontal scroll of mood cards on the homepage and a Vibe entry on category pages.
- Mood Collections: curated lists (restaurants, dishes, combos) per mood with short rationale copy and high-quality thumbnails.
- Ranking & Personalization: ranking pipeline that blends mood affinity, historical user preferences, merchant freshness, and promotion eligibility.
- Quick Actions: one-tap combos or "Order Now" flows for selected mood items.
- Experimentation Layer: server-side flags and A/B targeting to test variants.

## Functional Requirements
**FR-1 — Mood Picker (Homepage):**
- Visible on top of discovery feed as a horizontal scroll.
- Contains 6–8 default moods with icon, label, and short description.
- Tapping a mood opens a Vibe results page (list view + hero carousel).

**FR-2 — Mood Results Page:**
- Top hero carousel with 3–5 curated cards (restaurants or collections).
- Ranked list of restaurant tiles with mood relevance score, estimated delivery time, rating, and mood highlight.
- Filters: price, delivery time, dietary tags.

**FR-3 — Personalization Signals:**
- Accepts explicit mood selection and implicit signals (time of day, weather API, recent orders, saved preferences).
- Stores aggregated mood affinity per user for personalization.

**FR-4 — Merchant Controls:**
- Merchant dashboard integration to tag offerings as mood-appropriate (optional for merchants).
- Promotion targeting API to surface mood-based promotions.

**FR-5 — Analytics & Instrumentation:**
- Track Vibe impressions, clicks, selections, add-to-cart, completed orders, cancellations.
- Log features used by ranking model and treatment assignment for experiments.

## Non-functional Requirements
- Latency: Vibe results must load within 800ms for cached responses; 1.5s for cold responses.
- Availability: 99.9% uptime for core Vibe APIs during business hours.
- Privacy: Explicit opt-out; do not infer or expose sensitive attributes; store only aggregated mood affinity.

## UX Flows & Wireframes (descriptive)
**Homepage placement:**
- A horizontal mood card strip directly under the search bar. Cards show icon + label. First-time users see a short tooltip: "Tap a mood to discover food that matches how you feel." 

**Mood results page:**
- Hero: Full-width carousel with curated picks and a short copy like "Comforting picks for tonight." 
- Below: List of restaurants with a colored mood badge and a short mood rationale (1–2 words). 
- Each restaurant card includes a CTA for one-tap combos when available.

**Onboarding:**
- First exposure includes a brief modal explaining Vibe and asking permission for contextual signals (time/day). No sensitive data requests.

## Ranking & Personalization Design
- Input signals: explicit mood, user order history, time-of-day, day-of-week, weather, user dietary filters, merchant promotions.
- Model: mix of rule-based signals + a learning-to-rank model (phase 1: weighted heuristic; phase 2: LTR using historical Vibe interactions).
- Score = w1 * mood_affinity(user,item) + w2 * relevance(item,mood) + w3 * recency + w4 * promotion_score + w5 * reliability_score.

## ML & Taxonomy Generation

**Heuristic Mapping (Phase 1):**
- Initial mood tagging pipeline using keyword density analysis on dish descriptions and merchant reviews.
- Leverage keywords like "comfort," "guilt-free," "indulgent," "light," "treat," etc., to assign preliminary mood scores to menu items.
- Rule-based scoring: high keyword match confidence → `Comforting`; high-calorie, rich descriptors → `Indulgent`; low-fat, plant-based keywords → `Healthy`.
- Editorial review of top-tagged items to catch errors and refine thresholds.

**LLM Sentiment Analysis (Phase 1.5):**
- Deploy a fine-tuned language model to scan dish descriptions, merchant copy, and aggregated user reviews.
- Assign mood affinity scores across all 100k+ SKUs in our network.
- Model outputs multi-label mood probabilities (e.g., Spicy Ramen: 0.6 Late-Night, 0.3 Comforting, 0.1 Budget Friendly).
- Feedback loop: store user mood selections as implicit labels; periodically retrain model to improve accuracy.

**Visual Search & Image Recognition (Phase 2):**
- Leverage image recognition to analyze food photography in menus and user uploads.
- Detect visual cues: color saturation (rich desserts → `Indulgent`), texture (creamy, cheesy → `Comforting`), presentation (plated beautifully → `Celebration`).
- Combine visual signals with text to improve cross-modal mood predictions, especially for ethnic cuisines where descriptive text may be sparse.

## Data & ML Considerations
- Labeling: negative/positive interactions — clicks, orders, skips, saves. Mood selections serve as weak labels for model training.
- Privacy: store mood interactions as anonymous event logs; avoid storing raw contextual inference without explicit consent.
- Offline training: use batched logs to train LTR models and update mood taxonomy. Real-time ranking via feature-store lookups.
- Taxonomy versioning: maintain historical mood mappings to track model performance and enable A/B testing of new tagging approaches.

## Technical Architecture (high-level)
- Frontend: new Vibe component on mobile app and web; local caching + remote fetch.
- Backend: Vibe API service (REST) that returns mood-curated collections and ranked results.
- Recommender: Ranking microservice that exposes a predict API; uses feature-store and model artifacts.
- CMS: Editorial tool for curated mood collections (for marketing/ops).
- Experimentation: integrate with existing A/B platform and feature flag system.

## Data & Instrumentation
- Events: Vibe.Impression, Vibe.Click, Vibe.SelectMood, Vibe.CollectionClick, Vibe.AddToCart, Vibe.Order, Vibe.Cancel.
- Attributes: user_id (hashed), mood_id, session_id, treatment_id, rank_position, item_id, timestamp, context signals.
- Dashboards: weekly funnel (impression → click → add to cart → order), retention cohorts, revenue uplift.

## Monetization & Merchant Impact
- Premium placements: merchants can bid or enroll for mood-specific featured slots.
- Sponsored mood collections for brand campaigns.
- Merchant uplift metric: Orders attributed to Vibe per merchant and incremental revenue.

## Rollout Plan
Phase 0 — Internal beta (2 weeks)
- Build feature flags, internal QA, limited QA users.

Phase 1 — Pilot (4–6 weeks)
- Launch in 2–3 metro cities (high order density), randomized A/B test with 10% treatment.
- Primary focus: validate engagement and conversion metrics.

Phase 2 — Gradual rollout (6–8 weeks)
- Expand to top 20 cities while iterating on ranking and UX.
- Introduce merchant controls and promo targeting.

Phase 3 — National roll-out
- Full roll-out with advertising/promotional campaigns; merchant monetization enabled.

## Experimentation & Validation
- A/B test: Vibe vs baseline discovery for new/returning users.
- Key A/B metrics: Vibe CTR, conversion rate, AOV, time-to-order, retention.
- Success gates for broader rollout: statistically significant conversion uplift (p<0.05) and no negative effect on overall platform metrics.

## Monitoring & Ops
- Real-time dashboards for impressions, clicks, API latencies, errors, and cancellation rates.
- Alerting on: API latency > 2s, error rate > 1%, cancellations uplift > 10% vs baseline.
- Rollback: server-side flag to disable Vibe; client updates not required for kill switch.

## Risks & Mitigations
- Risk: Wrong mood mapping leads to poor recommendations → Mitigation: editorial oversight + conservative heuristics until model stabilizes.
- Risk: Users feel manipulated by mood inference → Mitigation: clear UX consent, ability to opt-out, transparency copy.
- Risk: Merchant dissatisfaction with placements → Mitigation: early merchant pilot and clear enrollment/analytics.
- **Risk: Echo Chamber Effect** — If we only surface "Comforting" or "Indulgent" foods to users who frequently select stressed/tired moods, we may inadvertently reinforce unhealthy eating patterns and reduce their dietary diversity over time. This could harm long-term user health and create a regulatory/brand reputation risk. → **Mitigation:** Introduce a "Mood Reset" or "Surprise Me" card every 5th Vibe session that breaks the algorithmic loop by surfacing unexpected, health-conscious options. Log diversity metrics (# unique cuisines, # health-tagged items) per user weekly to detect and alert on users showing low dietary diversity. Partner with nutrition experts to establish guardrails on mood-affinity weighting to avoid amplifying unhealthy suggestions.

## Open Questions
- Should mood inputs be saved as part of user preferences for future sessions? (privacy trade-offs)
- Trade-off between editorial curation vs fully automated ML-driven collections for initial launch.
- Pricing model for premium mood placements.

## Appendix
**Mood taxonomy (phase 1 examples):** Comforting, Indulgent, Healthy, Quick & Light, Celebration, Budget Friendly, Exotic.

**Metric definitions:**
- Vibe CTR = Vibe.Clicks / Vibe.Impressions
- Vibe Conversion Rate = Orders attributed to Vibe / Vibe Sessions
- Time-to-order = median(duration from Vibe entry to order placement)

**Sample A/B test plan:**
- Population: active users in pilot cities, randomized 50/50 (control vs Vibe treatment subset during pilot 10%).
- Duration: 4 weeks post-stability.
- Primary metric: Vibe Conversion Rate uplift.

---

If you'd like, I can:
- Add wireframe images or Figma links to the `Mood results page` and `Homepage placement` flows.
- Draft the stakeholder presentation and a 6–8 week milestone Gantt.
- Produce the telemetry event schema (in JSON) for instrumentation.

