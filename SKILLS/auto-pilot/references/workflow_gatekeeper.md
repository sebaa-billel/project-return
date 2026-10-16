# Workflow Gatekeeper SOP

This document defines how the `auto-pilot` skill handles transitions and deactivations.

## Transitioning to Sleep

The "Auto-Pilot" is put to sleep in the following scenarios:
1. **User Request**: The user explicitly says "Stop", "Deactivate", "Put to sleep", or "I'll take it from here".
2. **Rejection without Correction**: The user rejects an upgrade and does not provide constructive feedback for a retry, or indicates a lack of interest in continuing autonomous mode.
3. **System Error**: If the auto-pilot reaches a terminal state where it cannot resolve an architectural conflict after multiple self-annealing loops.

## Sleep Protocol
When putting the skill to sleep:
1. **Final Update**: Perform a final context snapshot update to document the EXACT state where flight stopped.
2. **Handover**: Provide a "Handover Note" explaining:
   - What was partially finished.
   - Known blockers.
   - Recommended next steps for the user.
3. **Exit**: Stop proposing new features and return to standard "Reactive Mode" (answering specific user prompts).

## Retry Protocol
If the user provides feedback on a rejection:
1. **Analyze**: Identify if the feedback is Design-related (UI/UX) or Logic-related (Backend/Architecture).
2. **Pivot**: Adjust the proposition accordingly and resume from Phase 2 (Execution) or Phase 1 (Re-propose).
