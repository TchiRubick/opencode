# Frontend Explore Investigator

## Description
This skill performs read-only investigation of frontend applications, browser flows, and Figma designs during Spec-Driven Development exploration work.

Its purpose is to gather evidence-based findings about:
- UI structure and layout composition
- interaction and navigation flows
- responsive behavior across viewports
- UX inconsistencies and friction points
- implementation-to-design alignment
- frontend runtime behavior in the browser

This skill complements `sdd-explore`. It does not replace that phase, does not implement fixes, and does not orchestrate the broader workflow. Use it to deepen frontend-specific discovery inside an existing exploration effort.

## Trigger
Activate this skill only when all of the following are true:
1. The task is in an exploration, investigation, discovery, or analysis context
2. The subject is a frontend application, browser behavior, user flow, or Figma design
3. The requested outcome is findings, observations, alignment analysis, or architecture understanding rather than implementation

Strong activation signals:
- “investigate the frontend”
- “explore this browser flow”
- “analyze the UI”
- “compare implementation to Figma”
- “inspect responsive behavior”
- “review runtime frontend behavior”
- “during sdd-explore, look into the app/design”
- “gather evidence about this user flow”
- “understand how this screen works”

Activate alongside `sdd-explore` when:
- the user explicitly requests `/sdd-explore` and the exploration requires browser, UI, or Figma evidence
- an existing SDD exploration needs frontend-specific analysis
- a spec or proposal depends on validating real UI behavior or design alignment

Do not activate when:
- the user asks to implement, refactor, or fix code
- the task is purely backend, CLI, API-only, or infrastructure-only
- the user asks to create new specs, tasks, or designs instead of investigating existing ones
- the task is to manage SDD phases rather than contribute exploration evidence

## Instructions
1. Confirm the task is read-only investigation.
   - Treat the goal as evidence gathering, not solutioning.
   - If the request mixes investigation with implementation, perform only the investigation portion unless explicitly told otherwise.

2. Establish the investigation target.
   - Identify the relevant frontend app, route, feature, user flow, component area, or Figma frame.
   - Identify whether the primary evidence source is code structure, browser behavior, design artifacts, or a combination.

3. Coordinate with `sdd-explore` without replacing it.
   - If `sdd-explore` is already active, contribute frontend findings that help proposals, specs, and decisions.
   - If not explicitly in SDD, still follow the same exploration discipline: observe first, conclude second.
   - Do not create or manage SDD artifacts unless another skill or direct instruction requires it.

4. Inspect implementation structure.
   - Locate the frontend entry points, routes, screens, major components, state boundaries, and styling/layout systems.
   - Map how the target screen or flow is assembled.
   - Note architectural patterns relevant to the requested investigation.

5. Investigate runtime browser behavior using browser tools.
   - Reproduce the target user flow step by step.
   - Capture evidence about navigation, state transitions, loading states, errors, empty states, and interaction feedback.
   - Inspect console output, network activity, and visible UI behavior when relevant.
   - Test realistic paths, not just the happy path.

6. Investigate responsive behavior.
   - Check the target UI at meaningful viewport sizes.
   - Identify layout shifts, overflow, clipped content, unreadable states, hidden controls, or broken interaction patterns.
   - Distinguish between expected adaptive behavior and likely defects.

7. Investigate Figma alignment when design artifacts exist.
   - Inspect the relevant Figma node, frame, or design context.
   - Compare structure, spacing, hierarchy, states, copy, controls, and interaction intent against the implementation.
   - Report concrete mismatches and confirmed alignments.
   - Do not redesign the interface unless explicitly requested.

8. Produce structured findings.
   - Separate observations from interpretations.
   - For each meaningful finding, include:
     - what was observed
     - where it was observed
     - how it was verified
     - why it matters
   - Label uncertainty clearly when evidence is incomplete.

9. Recommend next exploration steps only when useful.
   - Suggest focused follow-up checks, not fixes.
   - Keep recommendations within investigation scope.

10. Persist important learnings with Engram for cross-session continuity.
   - After completing significant work triggered by this skill, call `mem_save`.
   - Save durable findings using the Engram persistent memory protocol.
   - Prefer saving non-obvious discoveries, validated mismatches, frontend architecture insights, and reusable investigation context.

PROACTIVE SAVE TRIGGERS
- Confirmed root cause or mechanism behind frontend runtime behavior
- Non-obvious UI architecture mapping that will help future sessions
- Verified implementation-to-Figma mismatch with clear scope
- Verified responsive breakpoint issue pattern
- Reusable navigation or state-flow understanding
- Important investigation setup details needed to reproduce the analysis later
- Durable UX inconsistency pattern observed across multiple screens
- Any frontend exploration result likely to affect future spec or proposal work

Suggested Engram save shape:
- **What**: concise finding or investigation result
- **Why**: why the investigation was performed
- **Where**: routes, components, files, frames, or flows involved
- **Learned**: non-obvious behavior, constraints, or caveats

## Rules
- Stay read-only unless the user explicitly requests a separate implementation task.
- Do not implement fixes.
- Do not modify source code.
- Do not modify Figma files or designs.
- Do not orchestrate SDD phases.
- Do not replace `sdd-explore`; only augment it with frontend-specific evidence.
- Do not invent behavior; verify claims through code, browser evidence, design evidence, or both.
- Do not report design misalignment without naming the specific implementation area and design reference.
- Do not generalize from one viewport when responsive behavior is in scope.
- Do not assume console silence means correct behavior; inspect visual and interaction evidence too.
- Do not redesign interfaces unless explicitly requested.
- Do not produce speculative root-cause statements as facts.
- Must clearly separate:
  - direct observation
  - inferred explanation
  - open question
- Must call `mem_save` after significant work completed under this skill, following the Engram persistent memory protocol.

## Examples
Example 1: SDD exploration with browser flow
- User: “During /sdd-explore, investigate the checkout frontend flow and tell me where users get stuck.”
- Skill behavior:
  - Activate because the task is explicit exploration within SDD and concerns a browser flow.
  - Reproduce the checkout flow in the browser.
  - Inspect route transitions, form validation, loading states, and error handling.
  - Report evidence-based friction points and unclear transitions.
  - Save durable findings with `mem_save`.

Example 2: Figma alignment check
- User: “Compare the implemented settings page against the Figma design and note mismatches.”
- Skill behavior:
  - Activate because the task is design-to-implementation investigation, not implementation.
  - Inspect the implemented page structure and the Figma frame.
  - Compare spacing, section hierarchy, labels, control states, and responsiveness.
  - Report confirmed mismatches with exact locations.
  - Do not propose a redesign unless asked.

Example 3: Responsive behavior investigation
- User: “Explore how the dashboard behaves on tablet and mobile.”
- Skill behavior:
  - Activate because the task is frontend exploration focused on responsive behavior.
  - Test meaningful viewport sizes.
  - Capture overflow, wrapping, clipped controls, and hidden navigation issues.
  - Separate expected adaptive changes from probable defects.
  - Save the breakpoint behavior pattern if it is durable and reusable.

Example 4: Should not activate
- User: “Fix the nav drawer bug on mobile.”
- Skill behavior:
  - Do not activate this skill because the task is implementation, not investigation.
  - Another build or fix-oriented skill is more appropriate.

Example 5: Mixed request edge case
- User: “Investigate why the login modal feels broken, then patch it.”
- Skill behavior:
  - Activate only for the investigation portion.
  - Analyze modal behavior, transitions, focus handling, and console/runtime signals.
  - Report findings clearly.
  - Do not patch the code under this skill unless a separate implementation step is explicitly requested.

Example 6: SDD interaction boundary
- User: “Use /sdd-explore to understand the onboarding experience and prepare observations for the proposal.”
- Skill behavior:
  - Activate alongside `sdd-explore`.
  - Investigate screens, navigation steps, and runtime behavior.
  - Provide structured observations that feed the proposal.
  - Do not create or manage the proposal itself unless another skill or instruction requires it.