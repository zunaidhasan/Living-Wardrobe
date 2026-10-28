# Technical Requirements Document (TRD)
**Project:** Living Wardrobe  
**Version:** 1.1  
**Date:** 2026-10-28  
**Companion Document:** prd.md  
**Change:** Added full 3D wardrobe door technical specifications and updated stack + phases  

---

## 1. Purpose

This document defines the technical architecture, data models, stack recommendations, and implementation guidelines required to build Living Wardrobe according to the emotional and product requirements in the PRD.

The system must support a calm, atmosphere-first experience while remaining realistic and maintainable for an AI coding agent or small team.

---

## 2. High-Level Architecture

**Recommended Approach:**  
Mobile-first Progressive Web App (PWA) or React Native, with a clean separation between presentation and data.

```
Client (Next.js / Expo)
    ↓
API Layer (Next.js Route Handlers or Supabase Edge Functions)
    ↓
Database (Supabase PostgreSQL)
    +
Storage (Supabase Storage or Cloudinary)
    +
Auth (Supabase Auth)
```

**Core Principles:**
- Prefer server components and light client interactivity
- Keep animation and atmosphere on the client
- Avoid heavy real-time complexity in v1
- Design for graceful offline viewing of the closet

---

## 3. Recommended Tech Stack

### Option A – Best Balance (Recommended for most AI agents)
- **Framework:** Next.js 15 (App Router)
- **Styling:** Tailwind CSS + custom design tokens
- **Animation & 3D:** Framer Motion + React Three Fiber (R3F) + Drei
- **Database + Auth + Storage:** Supabase
- **Image Handling:** Cloudinary or Supabase Storage + sharp
- **Deployment:** Vercel
- **Language:** TypeScript

### Option B – Stronger Native 3D Feel
- Expo (React Native) + NativeWind + React Native Reanimated + React Three Fiber (via expo-gl)
- Same backend (Supabase)

**3D Decision Guidance:**  
For the signature wardrobe door, React Three Fiber is the preferred approach on web. Keep the 3D scene extremely lightweight and focused only on the door + immediate interior. Do not build a full 3D room.

**AI Coding Agent Note:** Start with Framer Motion for all 2D transitions. Introduce React Three Fiber only for the door sequence and subtle depth on the Threshold screen.

---

## 4. Design Tokens (Must Be Implemented Exactly)

```ts
// tailwind.config.ts or design-tokens.ts

colors: {
  background: "#F7F3EE",
  surface: "#F1EBE3",
  soft: "#E8DFD4",
  text: {
    primary: "#3C3530",
    secondary: "#8A7E74",
  },
  highlight: "#D6C8B8",
  border: "#EDE6DC",
}

fontFamily: {
  display: ["Cormorant Garamond", "serif"],
  body: ["Inter", "system-ui", "sans-serif"],
}
```

**Spacing:** Use generous scale (prefer 8, 12, 16, 24, 32, 48, 64).  
**Border radius:** Soft only (rounded-2xl or rounded-3xl). Never sharp.

---

## 5. Data Models

### Users
```ts
users {
  id: uuid (PK)
  email: text
  name: text
  created_at: timestamptz
  style_notes: text (nullable) // free-form memory
}
```

### Garments
```ts
garments {
  id: uuid (PK)
  user_id: uuid (FK)
  image_url: text
  thumbnail_url: text
  category: text          // top, bottom, dress, outerwear, shoes, accessory
  color: text
  material: text (nullable)
  tags: text[]            // ["linen", "neutral", "soft"]
  wear_count: integer default 0
  last_worn: date (nullable)
  season: text[]          // ["spring", "summer"]
  notes: text (nullable)
  created_at: timestamptz
  is_archived: boolean default false
}
```

### Outfits
```ts
outfits {
  id: uuid (PK)
  user_id: uuid (FK)
  name: text              // "Quiet Grey"
  feeling: text           // "calm" | "soft" | "sharp" | "radiant" | "invisible"
  garment_ids: uuid[]
  is_saved: boolean default false
  created_at: timestamptz
}
```

### Feeling Sessions
```ts
feeling_sessions {
  id: uuid (PK)
  user_id: uuid (FK)
  feeling: text
  date: date
  created_at: timestamptz
}
```

---

## 6. Core Screens – Technical Notes

### Threshold (Home)
- Full-viewport soft background (user’s closet collage or generated calm image)
- Greeting text with fade-in
- Bottom navigation appears after short delay (opacity animation)
- No heavy data fetching on first paint

### Feeling Selection
- Static list of five feelings
- Selection triggers soft scale + underline
- Auto-advance after 700–900ms using a controlled timeout
- Store selected feeling in session or short-lived state

### Outfit Response
- Fetch or generate 3 outfits based on feeling + available garments
- Display as clean flat-lay style cards or image compositions
- Framer Motion staggered entrance
- Tap expands to detail view

### Rediscovery
- Query garments with low wear_count + older last_worn
- Present with emotional copy (can be template-based in v1)
- Soft list or card layout with large imagery

---

## 7. Animation & 3D Guidelines

### 2D Motion
| Interaction              | Duration | Easing          | Notes                          |
|--------------------------|----------|-----------------|--------------------------------|
| Page transitions         | 700ms    | easeOut         | Opacity + slight y-translate   |
| Feeling selection        | 400ms    | easeOut         | Scale 0.98 → 1 + underline     |
| Outfit card entrance     | 600ms    | stagger 100ms   | Opacity + y                    |
| Expand outfit            | 500ms    | easeInOut       | Layout animation preferred     |
| Bottom nav appearance    | 800ms    | easeOut         | Delayed opacity                |

Avoid spring animations. Prefer tween with custom cubic-bezier if needed.

### 3D – Signature Wardrobe Door (Critical)

**Purpose:** Create the feeling of physically opening a real wardrobe.

**Technical Requirements:**
- Use React Three Fiber + Drei for the door scene
- Door should be a simple but realistic model (or carefully crafted geometry + texture)
- Soft natural lighting (warm key light from the side + subtle fill)
- Proper perspective camera
- Door opens with realistic hinge behavior and slight easing resistance
- Soft contact shadow under the door as it opens
- Interior of the closet (user’s garments) is revealed as the door swings open
- Duration of full open: 1.2 – 1.8 seconds
- User can trigger by tap or slow horizontal swipe
- After first few sessions, the animation can be shortened or skipped to an already-open state while preserving subtle depth

**Performance Rules:**
- Keep polygon count very low
- Prefer baked lighting / simple materials over real-time heavy effects
- Preload the door scene
- Fallback to a high-quality 2D animated door if WebGL is unavailable or performance is poor

**Daily Entry:**
- After onboarding, use a lighter version of the same 3D door or a subtle parallax depth effect so the user still feels they are entering a physical space.

---

## 8. Image Handling Requirements

- Support batch upload during onboarding
- Generate thumbnails on upload
- Store original + optimized versions
- Prefer soft, slightly desaturated presentation
- Lazy load all garment images
- Provide graceful placeholders that match the warm palette

---

## 9. Authentication

- Email + magic link (preferred for calm onboarding)
- Optional Google / Apple later
- Allow limited anonymous exploration before forcing account creation
- Protect all garment and outfit data with Row Level Security (Supabase)

---

## 10. Outfit Generation Strategy (v1)

**Phase 1 (Realistic & Fast):**
- Rule-based system
- Filter garments by category + color harmony + feeling tags
- Assemble valid combinations (top + bottom + shoes, etc.)
- Rank by wear_count (prefer less worn) and recency

**Phase 2:**
- Introduce lightweight LLM or embedding-based ranking for better feeling alignment
- Keep generation under 1.5 seconds

Never block the UI on generation. Show calm skeleton or previous results if needed.

---

## 11. Non-Functional Requirements

- **Performance:** First contentful paint < 1.8s on mid-range mobile
- **Accessibility:** Sufficient contrast on warm palette, keyboard navigable, reduced-motion support
- **Offline:** Cached closet images and last outfits should be viewable offline
- **Privacy:** All clothing images are private by default
- **Scalability:** Designed for single-user heavy usage first (closet of 80–200 items)

---

## 12. Implementation Phases

### Phase 1 – Atmosphere MVP (Priority)
1. Design system + global styles
2. Threshold screen with subtle spatial depth
3. **3D Wardrobe Door opening sequence** (signature moment)
4. Feeling selection
5. Static / mocked outfit response
6. Soft page transitions
7. Basic bottom navigation

### Phase 2 – Real Closet
1. Auth
2. Garment upload + storage
3. Digital closet view
4. Real outfit generation (rule-based)
5. Save outfit

### Phase 3 – Memory & Depth
1. Wear tracking
2. Rediscovery flow
3. Feeling history
4. Seasonal logic
5. Profile & style notes

---

## 13. Folder Structure Suggestion (Next.js)

```
/app
  /(experience)
    /page.tsx                 → Threshold
    /feeling/page.tsx
    /outfits/page.tsx
    /rediscover/page.tsx
    /closet/page.tsx
  /api
    /garments
    /outfits
    /upload
/components
  /ui
  /wardrobe
  /motion
/lib
  /supabase
  /outfit-engine
  /design-tokens
/styles
```

---

## 14. Coding Agent Instructions

- Follow the design tokens exactly. Do not introduce new colors.
- Prefer server components unless interactivity or animation requires client.
- Keep components small and focused.
- Name variables and components with calm, clear language (avoid “Card”, “Widget”, “Modal” when possible — prefer “Look”, “Piece”, “Moment”, “Door”).
- The 3D wardrobe door is a core emotional feature, not a nice-to-have. Treat it with the same priority as the main screens.
- Keep the 3D scene minimal and performant. Do not build an entire 3D room.
- When in doubt between adding a feature and protecting atmosphere, protect atmosphere.
- Write comments only when the “why” is not obvious from the code.

---

## 15. Open Technical Decisions

- Exact image optimization pipeline
- Whether to use React Server Components for outfit generation or edge functions
- Long-term strategy for advanced virtual try-on (out of scope for v1)

---

**Document Owner:** Engineering  
**Last Updated:** 2026-10-28  
**Status:** Ready for development  
