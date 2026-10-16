---
name: architect
description: Guides the agent to operate within a 3-layer architecture (Directive, Orchestration, Execution) for maximum reliability and deterministic performance. Use this skill whenever planning a complex task, creating new features, debugging system-level issues, or when the user mentions "directives", "execution scripts", or "3-layer architecture". Make sure to prioritize this architectural pattern over monolithic execution to ensure consistency.
---

# Architect Skill

This skill codifies the 3-layer architecture designed to separate concerns and maximize system reliability. LLMs are probabilistic; this system uses deterministic execution (scripts) controlled by intelligent orchestration (you) guided by natural language rules (directives).

## The 3-Layer Architecture

### Layer 1: Directive (The SOP)
- **Goal**: Define the "What" and "How" in natural language.
- **Location**: `directives/*.md`
- **Contents**: Goals, inputs, specific tools/scripts to use, expected outputs, and known edge cases.
- **Principle**: Read the relevant directive before starting any task. If no directive exists for a repetitive task, create one.

### Layer 2: Orchestration (The Decision Maker)
- **Goal**: Intelligent routing and decision-making. High-level planning.
- **Role**: The AI Agent (Orchestrator).
- **Activities**:
    - Analyze user intent against available directives.
    - Prepare inputs for execution scripts.
    - Call scripts in the correct logical sequence.
    - Handle script errors by analyzing logs and self-annealing.
    - Update Layer 1 directives with new learnings (API updates, edge cases).

### Layer 3: Execution (The Deterministic Tools)
- **Goal**: Perform the actual work reliably and fast.
- **Location**: `execution/*.py` (Python scripts)
- **Contents**: API integrations, file system operations, data transformations.
- **Principle**: Always check for existing tools in `execution/` before writing new ones. Keep scripts focused and testable.

## Core Operating Principles

### 1. The Self-Annealing Loop
Errors are the best way to improve the system. When an execution fails:
1. **Debug**: Read the stack trace and identify the failure point.
2. **Fix & Test**: Correct the script and verify it locally.
3. **Update Directive**: Document the fix or the new constraint in the Layer 1 directive.
4. **Verify**: The system is now permanently more resilient to this specific error.

### 2. Efficiency & Tooling
- **Tool-First**: Prefer using or creating a script over doing manual, multi-step completions.
- **Stateless Execution**: Execution scripts should ideally handle one thing well.
- **Environment Management**: Keep tokens and secrets in `.env`.

### 3. File Hygiene
- `.tmp/`: Store intermediate files here. They are disposable and should never be committed.
- `Deliverables`: Final outputs that the user cares about (e.g., Cloud docs, final reports).
- `Intermediates`: Temporary files used during processing, stored in `.tmp/`.

## Workflow Pattern
1. **Identify**: Which directive governs this task?
2. **Prepare**: What inputs does the execution script need?
3. **Run**: Trigger the execution tool.
4. **Refine**: If it fails, initiate the Self-Annealing Loop.
5. **Close**: Deliver the final result and update instructions if necessary.
