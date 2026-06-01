# Product Requirements Document (PRD)

## Project Title: The Attention Sanctuary (Working Title)

**Document Version:** 1.0

**Target:** Web MVP (Minimum Viable Product) with Scaling Pathways to Browser Extensions & Mobile/Desktop Apps.

---

## 1. Executive Summary & Value Proposition

Modern social media feeds exploit cognitive vulnerabilities through infinite scroll mechanisms, locking users into involuntary dopamine loops (doomscrolling). **The Attention Sanctuary** is a minimalist digital intervention platform designed to act as an "emergency brake" for the brain.

Unlike traditional screen-time apps that rely on punitive, hard blocking (which often triggers user frustration), this product leverages **mindful friction** and **attention rehabilitation**. It gently transitions users from a passive, highly fractured state of awareness back into a focused, deliberate state of digital autonomy, offering an actionable way to regain control.

---

## 2. The User Journey & Funnel Architecture

### Phase 1: The Intercept (Ad Campaign)

* **Mechanism:** Highly targeted, low-sensory ads deployed on high-distraction platforms (Instagram, TikTok, YouTube).
* **Creative Assets:** 10-to-15 second silent videos featuring smooth, rhythmic geometric animations (e.g., an expanding/contracting soft circle) overlaid against deep, organic muted backdrops.
* **Copy Angle:** Dynamic pattern interrupts: *"Stop scrolling. Match your breath to this circle for 5 seconds."* or *"You didn't actually want to open this app. Pause. Breathe."*
* **Call-to-Action (CTA):** Redirects directly to the web application.

### Phase 2: The Gateway Dashboard

Upon clicking the ad, the user lands on a screen entirely devoid of traditional web clutter (no header, no footer, no nav bars). They are greeted with a warm, empathetic prompt: *"What does your mind need right now?"* and presented with three clear, low-friction choices:

1. **Calm My Body** (Breathing Module)
2. **Reset My Focus** (Daily Micro-Reading Challenge)
3. **Clear My Head** (The Thought Dissolver)

### Phase 3: The Conversion Hook

Once any of the three exercises are successfully completed, the user is presented with a success state ("Control Regained") followed immediately by the acquisition wall:

* **The Pitch:** *"Your mind is back in your control. Want to automatically protect your attention before you start scrolling tomorrow?"*
* **Gated Value:** Access to the automated browser extension, desktop companion app, and native mobile apps requires a user account registration (Email Sign-up / OAuth).

---

## 3. Core Feature Specifications

### Feature A: The Dashboard

* **UI Components:** A centralized, vertically aligned card container.
* **Interaction:** Three large, elegantly rounded action panels displaying the exercises. High-contrast but low-luminescence states when hovered.

### Feature B: "Calm My Body" (Breathing Exercise)

* **Objective:** Lower the user's heart rate and trigger the parasympathetic nervous system.
* **Mechanism:** A singular, softly glowing geometric circle positioned in the dead center of the screen.
* **Behavior:** The circle uses CSS/JS keyframe animations to guide the user through a box-breathing or a 4-7-8 rhythmic cycle:
* *Expand:* 4 seconds (Inhale)
* *Sustain/Hold:* 2 seconds
* *Contract:* 4 seconds (Exhale)


* **Text Guidance:** Dynamically changing micro-copy centered below the circle syncing perfectly with the animation timing.

### Feature C: "Reset My Focus" (Daily Micro-Reading)

* **Objective:** Shift brain activity from the passive *Default Mode Network* to the active *Central Executive Network*.
* **Mechanism:** A highly legible typographic layout presenting a premium, curated paragraph of exactly 60–80 words.
* **Content Pillars:** Insights on neuroscience, stoic philosophy, or cognitive psychology.
* **Friction Guard:** To prevent habitual fast-skimming, the comprehension question below the paragraph remains locked or invisible until a timer (15–20 seconds) expires, ensuring a deliberate read rate.
* **The Validation Check:** A single, intuitive multiple-choice or reflective question checking comprehension.
* *If correct:* Proceed to the conversion screen.
* *If incorrect:* Show a supportive message (*"Not quite, your brain is still buzzing from social media. Let's take a deep breath and try another approach."*).



### Feature D: "Clear My Head" (The Thought Dissolver)

* **Objective:** Provide cognitive grounding and kinesthetic release for mental anxiety or frantic multi-tasking thoughts.
* **Mechanism:** A clean, unadorned typography input field (`textarea`) stating: *"Type the exact thought, distraction, or worry pulling your attention away right now."*
* **User Action:** The user types out their internal monologue and clicks a "Release It" button.
* **The Animation:** Upon submission, the text element detaches, scales downward, reduces opacity, and drifts upward into a subtle pixelated particle effect until it vanishes completely from the viewport.

---

## 4. UI/UX & Visual Design Guidelines

To contrast sharply with the overstimulating, neon-lit ecosystems of modern social media, the design system must prioritize sensory decompression.

* **Color Palette (Low-Dopamine Dark Mode):**
* *Primary Canvas (Background):* Midnight Charcoal (`#121212` or deep organic forest greens).
* *Typography:* Rich Cream / Off-White (Harsh white `#FFFFFF` is banned to avoid eye fatigue).
* *Accent/Interactive Elements:* Soft Muted Sage, Terracotta, or Pale Amber.


* **Typography:**
* *Headers & Reading Paragraphs:* Editorial Serif (e.g., *Lora*, *Merriweather*). Serif typefaces inherently slow down cognitive reading speeds, promoting retention.
* *UI Controls & Buttons:* Clean, highly spacing-optimized Sans-Serif (e.g., *Inter*, *Plus Jakarta Sans*).


* **Layout Rules:**
* **Absolute Minimalist Constraints:** Strictly NO infinite scrolling, NO gamified sound effects, NO aggressive animations, NO pop-ups, and NO "points/badges" metrics.
* **Geometry:** All containers and interactive inputs must feature generous padding and heavily rounded corners (`border-radius: 16px+`) to communicate physical safety and organic design.



---

## 5. Validation & Proof-of-Concept Strategy

Before initiating full-stack engineering, the product thesis will be stress-tested through a three-staged validation framework using zero-to-low budget inputs.

| Phase | Test Vector | Target Objective | Success Metric (Green Light) |
| --- | --- | --- | --- |
| **Test 1** | **The Pattern Interrupt Ad Loop** | Deploy a $15 ad budget on Meta/TikTok featuring the minimalist breathing circle ad concept. | **Click-Through Rate (CTR) > 2.5%** and a video retention rate indicating users are pausing to watch. |
| **Test 2** | **The No-Code Prototype** | Build the entire 3-step loop using a zero-code logic-forward form builder (e.g., Typeform or Tally) and share it to organic niche communities (`r/nosurf`, `r/ProductivityApps`). | **Completion Rate > 60%** of users finishing an exercise once they initiate it. |
| **Test 3** | **The Acquisition Demand Check** | Place a waitlist form at the tail end of the no-code prototype offering early access to the upcoming browser extension/desktop app. | **Email Conversion Rate > 15%** of total page traffic opting into the database. |
