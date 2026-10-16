---
name: dev-prompt-enhancer
description: Enhances requests to build new applications or features from scratch. Triggers when a user asks to "build", "create", or "start" a new project, component, or application. Ensures a premium UX/UI and 3-layer architecture.
---

# Dev-Prompt-Enhancer Skill

This skill transforms high-level "build from scratch" requests into comprehensive, developer-ready prompts. It ensures every new creation follows premium UX/UI standards and structured architectural patterns.

## Core Workflow

1.  **Deconstruct Intent**: Identify the core goal behind the user's brief message.
2.  **Contextual Research**: 
    - Check the current codebase (`AGENTS.md`, `directives/`, `execution/`) to align the enhanced prompt with existing architectural patterns.
    - Identify missing parameters: Tech stack, specific features, user roles, constraints.
3.  **Expansion Framework**: Transform the request using the following structure:
    - **Objective**: A clear, concise statement of the final goal.
    - **Problem Detail**: Why this is being done and what pain points it solves.
    - **UX/UI Design & Aesthetics**: Detailed visual requirements including color palettes (vibrant/harmonic), typography (e.g., Google Fonts like Inter/Outfit), layout (glassmorphism/dynamic), and micro-animations.
    - **Step-by-Step Execution Plan**: A logical sequence of actions to reach the goal.
    - **Success Criteria/Verification**: How to know the task is completed correctly.
4.  **Clarification**: Replace ambiguous terms with precise technical language. For example, change "freemium website" to "a web application with a free tier for basic features and a subscription-based premium tier for advanced functionality."

## Enhancement Rules

- **Coding Focus**: Specify language, environment, and architectural constraints. Reference `AGENTS.md` principles (Determinism, SOPs, Execution scripts).
- **Aesthetic Excellence (The "WOW" Factor)**: Proactively add details for premium, state-of-the-art designs. Avoid generic suggestions. Include:
    - **Visual Style**: Glassmorphism, sleek dark modes, smooth gradients.
    - **Typography**: Modern, readable fonts (avoid browser defaults).
    - **Interactivity**: Dynamic animations, hover effects, reactive components.
- **Maintain Intent**: Do not change *what* the user wants, only *how* it is described to the model.

## Example Transformation

**Input**: "build me a freemium website of teaching polish language leveraging AI"

**Enhanced Prompt**:
# Objective: Build a Polish Language Learning Web Application (PolskiAI)
Implement a modern, responsive web application focused on teaching Polish cases through AI-driven feedback.

## Requirements
- **Core Feature**: Real-time "Case HUD" providing immediate feedback on grammatical case usage during conversational practice.
- **Business Model**: Freemium (Basic lessons/vocabulary are free; Real-time AI feedback is premium).
- **Aesthetics & UI**: Premium glassmorphism design using a dark theme with neon Polish-red accents. Use **Outfit** typography. Implement smooth Framer Motion transitions between lessons.
- **Tech Stack**: HTML/Vanilla CSS foundation, Python-based execution scripts for AI logic, and 3-layer architecture (Directive, Orchestration, Execution).

## Proposed Steps
1. **Foundation**: Set up `index.css` with a robust design system.
2. **Infrastructure**: Create Layer 3 Python scripts in `execution/` for low-latency AI response handling.
3. **Core Logic**: Implement the "Case HUD" UI components.
4. **Integration**: Connect the frontend to the orchestration layer.

## Verification
- Automated tests for case accuracy.
- Manual walkthrough recording of a user session.
