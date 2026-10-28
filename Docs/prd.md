# Product Requirements Document (PRD)
**Project:** Living Wardrobe  
**Version:** 1.1  
**Date:** 2026-10-28  
**Status:** Ready for Implementation  
**Change:** Added mandatory 3D wardrobe door interaction and spatial depth requirements  

---

## 1. Vision

Living Wardrobe is a feeling-first digital closet experience.  
It is not a fashion recommendation engine, shopping tool, or productivity app.  

It is a quiet, intimate daily ritual that makes opening a closet feel inspiring again — using only the clothes the user already owns.

The product should feel more like a private room filled with soft morning light than a software application.

**Physical Presence Requirement:**  
Key moments (especially first entry and daily opening) must use subtle 3D spatial interactions so the user feels they are physically opening a wardrobe door and stepping into their own closet. This is not decorative animation — it is the emotional foundation of the product.

---

## 2. Problem Statement

Most people open their closet and feel overwhelmed, bored, or defeated.  
They own clothes they love but forget, repeat the same 5–7 outfits, and slowly lose connection with their personal style.

Existing solutions fall into two categories:
- Human stylists (expensive, slow, not scalable)
- Generic fashion apps (transactional, trend-driven, emotionally cold)

There is no product that restores the simple emotional pleasure of getting dressed using what you already have.

---

## 3. Product Principles (Non-Negotiable)

1. **Feeling over function**  
   Every decision must protect calm, intimacy, and recognition.

2. **Atmosphere over interface**  
   The product should feel like a physical space, not a digital dashboard.

3. **Physical presence**  
   Critical moments must use subtle 3D spatial interactions (especially the wardrobe door opening) so the experience feels tangible rather than flat.

4. **Existing clothes first**  
   New purchases are secondary. Rediscovery is the core value.

5. **Slow is better**  
   Pacing, breathing room, and quiet transitions matter more than speed. 3D movements must feel weighted and real, never flashy.

6. **No human dependency**  
   The entire experience must work without any human stylist, consultant, or support for the core loop.

---

## 4. Target Users

**Primary:**
- Women (and style-conscious men) aged 25–45
- Own a full closet but feel they have “nothing to wear”
- Value calm, quality, and emotional connection over trends
- Comfortable with mobile apps but tired of noisy, gamified products

**Secondary:**
- Minimalists and capsule wardrobe enthusiasts
- People going through life transitions (new job, postpartum, moving cities)
- Anyone who wants to fall back in love with what they already own

---

## 5. Core Experience Goals

When a user opens Living Wardrobe, they should feel:

- The soft click of a closet door
- Recognition (“this knows me”)
- Gentle inspiration without pressure
- Calm confidence about what to wear today

**Success is measured by emotional shift, not feature usage.**

---

## 6. Key User Flows

### 6.1 First-Time Experience (Onboarding)
1. Soft welcome with one quiet sentence
2. Name input
3. Guided photo upload of existing clothes (batch supported)
4. Calm background processing while the digital closet is built
5. **Signature 3D Wardrobe Door Sequence**  
   - User sees a closed wardrobe / closet door in soft light  
   - Gentle invitation to open it (tap or slow swipe)  
   - Realistic 3D door opens with weight, soft shadow, and subtle depth  
   - Interior of the closet is revealed with the user’s actual clothes  
   - This is the emotional arrival moment — the user should feel they have just opened their own wardrobe
6. Arrival at the Threshold screen inside the open closet

### 6.2 Daily Ritual (Core Loop)
1. User opens the app → short, soft 3D door opening (or already-open state with subtle depth) into their closet
2. Soft question appears: “How do you want to feel today?”
3. User selects one feeling (Calm / Soft / Sharp / Radiant / Invisible)
4. Three complete outfits are presented, built only from their clothes
5. User can save, wear, or simply look

The daily entry should still carry a light sense of physically arriving inside the wardrobe, even if the full door animation is shortened after the first few uses.

### 6.3 Rediscovery
- Triggered weekly or on demand
- Soft message: “I found three pieces you’ve barely touched that still look beautiful on you.”
- Emotional framing of forgotten garments
- New combinations shown with quiet care

### 6.4 Soft Gap / Possibility
- When a meaningful missing piece is identified, it is shown as the completion of an almost-perfect outfit
- Never presented as a shopping list or deficiency

---

## 7. Feature Requirements

### Must Have (MVP)
- Threshold / Home screen with personalized closet atmosphere
- **3D Wardrobe Door opening interaction** (signature onboarding + daily entry)
- Feeling selection
- Outfit generation based on selected feeling + user’s garments
- Basic digital closet (upload + view garments)
- Rediscovery flow
- Soft bottom navigation
- Calm page transitions and micro-interactions
- Subtle spatial depth and parallax throughout key screens
- Account creation + persistence

### Should Have (Phase 2)
- Wear tracking (mark as worn)
- Seasonal awareness
- Saved outfits collection
- Simple organization suggestions
- Basic profile / style memory

### Nice to Have (Later)
- Advanced AI try-on
- Travel packing mode
- Seasonal closing ritual
- Family / shared profiles
- Affiliate shopping links (optional and quiet)

---

## 8. Design Requirements

### Visual Language
- Warm ivory and soft neutral palette only
- Elegant serif for emotional moments
- Clean sans-serif for UI
- Extremely generous whitespace
- Soft natural light aesthetic
- No bright colors, hard shadows, or dense card layouts

### Motion & Spatial Interaction
- Slow, weighted transitions (600–900ms)
- Prefer opacity and subtle scale for most UI
- **3D Wardrobe Door:** Must feel physical — proper perspective, soft shadow, slight resistance, and natural easing. Duration ~1.2–1.8 seconds for the full open.
- Subtle parallax and depth on the Threshold screen so clothes feel like they exist in real space
- No playful, bouncy, or exaggerated 3D effects
- All 3D must remain calm and elegant — never “game-like”

### Tone of Voice
- Quiet, observant, warm
- Speaks like someone who has known the user’s style for years
- Forbidden words: optimize, unlock, boost, pro, premium, analyze, maximize

---

## 9. Monetization

| Tier              | Price          | Access                                      |
|-------------------|----------------|---------------------------------------------|
| First Light       | Free           | Limited daily looks + basic closet          |
| The Wardrobe      | $14–17 / month | Full daily ritual + rediscovery             |
| The Mirror        | $27–32 / month | Deeper memory, seasonal intelligence        |
| The Closet        | $349 lifetime  | Everything permanently                      |

Naming must stay emotional. Never use “Pro” or “Premium”.

---

## 10. Success Metrics

**Primary:**
- % of users who complete the daily ritual at least 4 days per week
- Emotional feedback (in-app soft rating after outfits)
- Retention at Day 7 and Day 30

**Secondary:**
- Number of garments uploaded
- Rediscovery engagement rate
- Conversion from free → paid

---

## 11. Out of Scope (v1)

- Social features / sharing
- Live human stylist chat
- Heavy e-commerce integration
- Trend forecasting
- Gamification (streaks, points, badges)
- Dark mode (warm light is intentional)

---

## 12. Open Questions

- Exact AI model strategy for outfit generation (rule-based first vs LLM)
- How aggressively to push photo quality during onboarding
- Whether to support web in v1 or mobile-first only

---

**Document Owner:** Product  
**Last Updated:** 2026-10-28  
