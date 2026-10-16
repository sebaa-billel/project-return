---
name: research-ai-solution
description: Research a pain point/problem and assess the feasibility of an AI solution. This skill analyzes the problem, evaluates AI potential using a SWOT framework, identifies the best business model, researches market competition, and estimates implementation ease.
---

# Research AI Solution Skill

This skill helps users evaluate whether a specific problem can be solved with AI and what the business/technical implications are.

## Core Workflow

1.  **Identify Pain Point**: The user provides a specific problem or pain point.
2.  **Conduct Research**: The agent uses the `ai_solution_research` directive to perform deep research.
3.  **Feasibility Analysis**: Assess the feasibility using the **SWOT framework** (Strengths, Weaknesses, Opportunities, Threats).
4.  **Market Analysis**: Identify primary market **competitors** and existing solutions.
5.  **Strategic Assessment**: Determine the best business model and estimate "Ease of Implementation".
6.  **Report Generation**: Results are saved to a file named `research-<solution-name>.md` in the project root.

## How to use

When a user asks to "research an AI solution for [problem]", "assess if AI can solve [pain point]", or "evaluate the business model for an AI [solution]", activate this skill and follow the [ai_solution_research directive](file:///c:/Users/Booyaah/agtest/directives/ai_solution_research.md).

## Output Expectations

The output must be a detailed Markdown file (`research-<solution-name>.md`) containing sections for:
- Executive Summary
- SWOT Analysis
- Competition & Market Landscape
- Proposed Business Model
- Challenges
- Ease of Implementation (Score & Rationale)
