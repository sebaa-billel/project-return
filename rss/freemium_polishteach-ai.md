# PolskiAI - The Case Master: Project Specification

## 1. Project Overview & Vision
Develop a freemium, AI-driven language learning platform that revolutionizes Polish language acquisition by solving its most significant pain point: the 7-case grammatical system. The platform will use real-time AI feedback and an immersive "Case HUD" (Heads-Up Display) to provide immediate improvement and reduce learner cognitive load.

## 2. Technical Architecture & Coding Efficiency
- **Core Engine**: Low-latency (sub-200ms) voice-to-text and LLM processing pipeline.
- **Tech Stack**:
    - **Frontend**: Next.js 14 (App Router), Tailwind CSS, Framer Motion (for HUD animations).
    - **Backend**: FastAPI (Python) for high-performance AI inference and WebSocket management.
    - **Real-time Comms**: WebSockets for streaming audio and receiving HUD updates.
    - **AI/LLM**: GPT-4o-realtime or fine-tuned Llama-3 models.
- **Deterministic Validation**: Integrate a morphological dictionary (e.g., Morfeusz) to cross-reference LLM output for 100% case accuracy.

## 3. UX/UI Design & Aesthetics
**Visual Theme**: "Midnight Scholar" – Dark mode (background: `#0f172a`) with vibrant, neon-coded grammar highlights.

### A. The "Case HUD" Interface
- **Persistent Overlay**: A holographic HUD highlighting nouns and adjectives as they are spoken or typed.
- **Color-Coding Strategy**:
    - **Nominative**: `#3b82f6` (Sky Blue) - The "Subject" anchor.
    - **Genitive**: `#22c55e` (Emerald Green) - Possession/Negation.
    - **Dative**: `#eab308` (Sunlight Yellow) - Direction/Target.
    - **Accusative**: `#f97316` (Neon Orange) - Direct Action.
    - **Instrumental**: `#a855f7` (Electric Purple) - Tools/Means.
    - **Locative**: `#14b8a6` (Deep Teal) - Position/Context.
    - **Vocative**: `#ef4444` (Vulcanic Red) - Direct Address.

### B. "Shadow Teacher" Mode
- **Real-time Assistance**: AI suggests correct case endings via "ghost text" before the user finishes their sentence.
- **Interactive Feedback**: Hovering over words show the grammatical "Why."

### C. Progress & Gamification
- **3D Mastery Hexagon**: A rotatable visualization of progress across all 7 cases.
- **High-Contrast Typography**: Optimized for reduced cognitive load during intense grammar study.

## 4. Implementation roadmap
1. **Infrastructure**: Setup WebSocket server and Whisper-v3.
2. **Contextual HUD Logic**: Middleware to extract and color-code grammatical metadata.
3. **UI Implementation**: Build the "Midnight Scholar" theme and dynamic CSS classes.
4. **Freemium Integration**: Stripe setup for Basic (Free) vs. Mastery HUD ($12.99/mo).
5. **Testing**: Automated benchmarks for declension accuracy and voice latency.
