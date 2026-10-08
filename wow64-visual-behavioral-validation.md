---
name: wow64-visual-behavioral-validation
description: Orchestrate evidence-first visual and behavioral parity validation between the WoW64 Native AMD64 client and the original World of Warcraft 3.3.5a build 12340. Use when investigating UI, rendering, input, state, timing, networking, or other observable client differences where parity with the original is the acceptance criterion.
---

# WoW64 Visual & Behavioral Validation

## Purpose

This is a WoW64-specific orchestration skill for investigating and validating observable behavioral and visual differences between:

- the original World of Warcraft 3.3.5a build 12340 client;
- the WoW64 Native AMD64 client.

The goal is not merely to make a specific screen or symptom appear correct.

The acceptance criterion is observable parity with the Original under equivalent conditions.

This skill determines:

- what evidence must be obtained;
- which specialized skill should obtain it;
- where investigation should proceed;
- when sufficient evidence has been reached;
- when implementation is justified;
- how the result must be differentially validated;
- when the investigation must stop.

This skill does not replace specialized skills such as Ghidra, WinDbg, RenderDoc, pixel-perfect analysis, protocol reverse engineering, performance analysis, or systematic debugging.

---

## Authoritative Workspace

All WoW64 work MUST use:

```text
D:\Workspace\WoW64
```

Before proceeding:

1. Read and comply with:

```text
D:\Workspace\Project Rules.txt
```

2. Preserve existing dirty/uncommitted work.
3. Do not treat clones, VM copies, temporary directories, stale workspaces, or alternate roots as authoritative.
4. Do not silently switch to another copy of the project because it appears cleaner or easier to analyze.
5. Do not perform destructive Git operations unless explicitly required, justified, and safe.

The workspace above is the authoritative implementation, evidence, and validation environment.

---

## Authoritative Original

The Original client is the behavioral reference.

Expected Original:

```text
World of Warcraft 3.3.5a
Build: 12340
SHA-256:
28287CD94E6AB2D6E68865F49314B456D2750DCB5D0B8ECCA12EEDDF72B7BF80
```

When an investigation depends on Original behavior, establish that the observed binary/runtime corresponds to the authoritative Original before treating observations as evidence.

Do not silently substitute another WoW 3.3.5a executable.

---

## Core Principle

Use the following workflow:

```text
OBSERVED DIFFERENCE
        ↓
REPRODUCIBLE DIFFERENCE
        ↓
CLASSIFY DIFFERENCE
        ↓
LOCATE FIRST OBSERVABLE / CAUSAL DIVERGENCE
        ↓
SELECT REQUIRED EVIDENCE
        ↓
ESTABLISH ROOT CAUSE
        ↓
MINIMAL CORRECT FIX
        ↓
REVALIDATE AGAINST ORIGINAL
        ↓
REGRESSION VALIDATION
        ↓
PASS / PARTIAL / FAIL
```

Do not optimize for fixing the latest visible symptom.

Optimize for identifying and correcting the earliest relevant divergence supported by evidence.

---

## First Divergence Principle

When Original and WoW64 differ at multiple downstream points, do not automatically fix the most visible or latest difference.

Trace backward through the causal chain.

Prefer:

```text
Latest visible symptom
        ↑
Downstream state difference
        ↑
Earlier state/input/render difference
        ↑
First observable divergence
        ↑
Potential causal divergence
```

The investigation should attempt to establish the earliest meaningful divergence that explains the downstream behavior.

If the earliest causal divergence cannot yet be proven:

- record the earliest confirmed observable divergence;
- distinguish it from an inferred earlier cause;
- do not present the inferred cause as established fact.

The objective is not to trace arbitrarily far backward.

The objective is to stop at the earliest divergence that is both relevant and sufficiently supported by evidence.

---

## No Endless Tool or Skill Loops

Specialized skills MUST NOT be invoked merely because they are available.

Each investigation branch must have a concrete evidence-based reason.

Before invoking another specialized skill, identify:

- what unanswered question it addresses;
- what evidence it is expected to produce;
- why the current evidence is insufficient.

Stop that branch when sufficient evidence has been obtained.

Do not repeatedly:

- run the same capture without a new hypothesis;
- re-run the same RE pass without a new unresolved question;
- switch between skills without evidence requiring the switch;
- collect evidence that cannot change the diagnosis or implementation decision.

The orchestration goal is:

```text
Question → Required Evidence → Appropriate Skill → Evidence → Decision
```

not:

```text
Available Skill → Run Skill → More Output → Run Another Skill
```

---

## Skill Selection

Select specialized skills according to the actual evidence required.

### Visual Difference

Use:

```text
pixel-perfect
```

when the question is primarily:

- visual output;
- screenshot/framebuffer comparison;
- layout;
- geometry;
- colors;
- typography;
- spacing;
- visual state;
- pixel-level divergence.

### GPU / Rendering Difference

Use:

```text
renderdoc-gpu-debug
```

when evidence requires:

- GPU captures;
- draw-call inspection;
- resource inspection;
- render targets;
- shaders;
- pipeline state;
- graphics API behavior;
- rendering order.

### Native Runtime Difference

Use:

```text
windbg
```

when evidence requires:

- runtime execution;
- native call stacks;
- memory state;
- breakpoints;
- registers;
- exceptions;
- thread behavior;
- Windows runtime state.

### Unknown Original Internal Behavior

Use:

```text
ghidra-iterative-re
binary-analysis-patterns
```

when the behavior or internal mechanism of the Original is not sufficiently established.

Prefer `ghidra-iterative-re` for evidence-first reconstruction.

Use `binary-analysis-patterns` when binary structure, CFG patterns, calling conventions, compiler patterns, or decompilation interpretation materially affects the investigation.

### Dependency / Impact / Architecture

Use:

```text
graph-engineering
```

when the investigation requires:

- dependency mapping;
- caller/callee impact;
- subsystem relationships;
- architecture constraints;
- propagation analysis;
- evidence-backed dependency reasoning.

### Network / Login Protocol

Use:

```text
protocol-reverse-engineering
```

only when the divergence is plausibly related to:

- network protocol;
- authentication;
- session establishment;
- packet structure;
- serialization;
- protocol state.

Do not invoke it for a purely local visual difference.

### Timing / Performance

Use:

```text
performance
```

when timing, CPU, memory, frame pacing, GPU utilization, or performance behavior is materially relevant to the divergence.

### Root-Cause Debugging

Use:

```text
systematic-debugging
```

when the required evidence has been sufficiently established and systematic root-cause debugging is needed.

This skill determines **what evidence is needed and which investigation path should produce it**.

`systematic-debugging` determines **how to conduct the root-cause debugging process once the relevant evidence exists**.

These responsibilities complement rather than replace one another.

---

## Evidence Selection

Evidence must be selected according to the question being answered.

Do not assume that one evidence type is universally stronger than another.

### Preferred Evidence Sources — Depending on the Question

Possible evidence sources include:

1. **Original runtime observation**
   - establishes what the Original actually does under specific conditions;
   - particularly valuable for observable behavior, timing, UI state, input handling, and rendered output.

2. **Original binary / RE evidence**
   - establishes internal implementation logic, relationships, constants, branches, structures, and data flow;
   - particularly valuable when runtime behavior alone cannot explain the mechanism.

3. **WoW64 runtime observation**
   - establishes what the current implementation actually does;
   - particularly valuable for reproducing and localizing the divergence.

4. **Differential observation**
   - establishes the concrete difference between Original and WoW64 under equivalent conditions;
   - particularly valuable for identifying divergence boundaries.

5. **Dependency / call / data-flow evidence**
   - establishes how a confirmed difference propagates through the implementation;
   - particularly valuable for tracing toward an earlier causal divergence.

6. **GPU / rendering evidence**
   - establishes graphics pipeline behavior and rendering-specific differences;
   - particularly valuable when final visual output alone cannot identify the rendering cause.

The appropriate evidence depends on the question.

For example:

```text
"What does the player see?"
→ runtime / framebuffer evidence

"Why does the Original call this internal routine?"
→ Original RE evidence

"Where does WoW64 first diverge from Original?"
→ differential runtime + call/data-flow evidence

"Why is this frame visually different?"
→ visual + GPU evidence

"Which subsystem propagates this state?"
→ dependency / graph evidence
```

Evidence should therefore be evaluated by:

- relevance to the question;
- directness;
- reproducibility;
- provenance;
- consistency with other evidence;
- ability to distinguish competing explanations.

---

## Root-Cause Requirement

Do not implement a fix solely because it makes the visible symptom disappear.

Before implementation, establish:

```text
Observed divergence
        ↓
Relevant causal path
        ↓
Supported root cause
        ↓
Correct implementation change
```

If the root cause remains uncertain, do not claim that it has been established.

When multiple explanations remain plausible:

- obtain discriminating evidence;
- narrow the hypothesis set;
- or explicitly mark the result PARTIAL.

---

## Behavioral Parity

Behavioral parity includes, where applicable:

- initialization;
- input handling;
- state transitions;
- UI interaction;
- timing;
- animation;
- game logic;
- network behavior;
- resource loading;
- error handling;
- persistence;
- subsystem interaction.

A visually similar result is not sufficient if subsequent behavior diverges.

Likewise, identical internal implementation is not required if observable behavior is equivalent.

The project acceptance criterion is behavior, not implementation identity.

---

## Visual Parity

Visual parity must be evaluated under equivalent reproducible conditions.

Relevant conditions may include:

- resolution;
- window mode;
- graphics settings;
- UI scale;
- viewport;
- loaded data;
- character/account state;
- camera;
- timing;
- input state;
- environment;
- rendering state.

A visual comparison must distinguish between:

```text
Observed difference
```

and:

```text
Difference caused by different test conditions
```

Do not declare visual parity from a single convenient screenshot when the same state cannot be reproduced reliably.

---

## Original ↔ WoW64 Differential Validation

When comparing Original and WoW64:

1. Establish the exact test conditions.
2. Reproduce the same observable state.
3. Record the Original behavior.
4. Record the WoW64 behavior.
5. Identify the first meaningful divergence.
6. Trace backward when required.
7. Obtain evidence supporting the causal explanation.
8. Implement the smallest justified correction.
9. Repeat the same comparison.
10. Run regression checks.

The goal is not:

```text
WoW64 looks better
```

The goal is:

```text
WoW64 behavior matches Original
```

under equivalent conditions.

---

## Regression Gate

A fix is not complete merely because the original divergence disappears.

After implementation:

1. Reproduce the original failing scenario.
2. Confirm the divergence is removed.
3. Confirm the intended behavior matches Original.
4. Test adjacent states and transitions.
5. Test relevant downstream behavior.
6. Check for regressions in previously validated functionality.

Use:

```text
qa-methodology
```

when a structured regression strategy, test matrix, quality gate, or regression analysis is required.

A fix that closes one visual difference while breaking later behavior is not accepted as a parity fix.

---

## Evidence Record

For significant investigations, preserve a compact evidence chain:

```text
DIVERGENCE
FIRST CONFIRMED DIVERGENCE
ORIGINAL EVIDENCE
WOW64 EVIDENCE
ROOT CAUSE
FIX
VALIDATION
REGRESSION
```

Each claim should be traceable to concrete evidence where practical:

- executable;
- address/RVA;
- function;
- source file;
- call path;
- runtime observation;
- capture;
- screenshot;
- test;
- log;
- database record;
- relevant commit.

Do not replace evidence with confidence statements.

---

## Evidence Quality

Evidence should be evaluated rather than mechanically ranked.

Prefer evidence that is:

- directly relevant;
- independently reproducible;
- tied to the authoritative Original or current WoW64 implementation;
- sufficiently specific to answer the current question;
- capable of distinguishing competing explanations;
- consistent with other established evidence.

Strong evidence for one question may be weak evidence for another.

For example:

- runtime observation can establish observable behavior but may not establish internal cause;
- RE can establish internal logic but may not prove that the runtime reaches that path in the tested scenario;
- a screenshot can prove a visual difference but usually cannot establish its causal source;
- a GPU capture can explain a rendering divergence but may not explain why the wrong rendering state was selected.

Use the evidence type appropriate to the claim being made.

---

## Fail-Closed

If evidence is insufficient:

```text
Do not guess.
Do not invent Original behavior.
Do not silently reinterpret missing RE.
Do not claim parity.
```

Instead:

- obtain additional evidence;
- reduce the claim;
- mark the result PARTIAL;
- or stop the investigation if the required evidence cannot be established.

Unknown must remain unknown until evidence resolves it.

---

## Minimal Correct Fix

Prefer the smallest implementation change that:

- addresses the established root cause;
- reproduces the Original behavior;
- does not introduce unnecessary architectural changes;
- does not mask downstream symptoms;
- remains consistent with established RE evidence.

Do not rewrite broad areas of the client when a narrow causal correction is sufficient.

Conversely, do not use a narrow patch to conceal a broader architectural divergence when evidence shows that the divergence originates earlier.

---

## Scope Control

The investigation must remain focused on the observable parity problem.

Do not expand scope because:

- another subsystem is interesting;
- another Skill is available;
- unrelated RE debt exists;
- unrelated cleanup appears useful;
- additional metrics can be collected.

Expand scope only when evidence demonstrates that the additional area is causally relevant to the current divergence.

---

## Skill Boundary

This skill is an orchestration layer.

It does not attempt to reproduce the detailed methodology of:

- Ghidra;
- binary analysis;
- WinDbg;
- RenderDoc;
- pixel-perfect analysis;
- protocol reverse engineering;
- performance profiling;
- systematic debugging;
- QA methodology.

Instead it defines:

```text
WHEN
→ WHY
→ WHICH SKILL
→ WHICH EVIDENCE
→ WHEN TO STOP
```

Specialized Skills remain responsible for their own domain methodology.

This prevents meta-skill duplication and keeps the orchestration layer maintainable.

---

## Acceptance Criteria

An investigation can be considered complete when:

1. Original behavior is established from the authoritative reference.
2. WoW64 behavior is reproducibly established.
3. The meaningful divergence is identified.
4. The earliest relevant observable or causal divergence has been investigated.
5. The root cause is supported by evidence.
6. The implementation change addresses the established cause.
7. WoW64 reproduces the required Original behavior.
8. Visual and/or behavioral validation passes as applicable.
9. Relevant regression checks pass.
10. No unsupported 1:1 claim remains.

If one or more of these conditions cannot be established, report:

```text
PARTIAL
```

rather than claiming full parity.

---

## Final Report

A final investigation report should contain, at minimum:

```text
Result:
PASS / PARTIAL / FAIL

Observed divergence:
...

First confirmed divergence:
...

Original evidence:
...

WoW64 evidence:
...

Root cause:
...

Implementation:
...

Validation:
...

Regression:
...

Specialized Skills actually used:
...

Specialized Skills considered but not required:
...
```

Do not list a Skill as used merely because it was available or mentioned.

---

## Operating Rule

Use the right evidence for the question.

Find the earliest relevant divergence.

Stop when the evidence is sufficient.

Do not invoke tools or Skills without a concrete investigative reason.

Fix the cause rather than the symptom.

Never claim 1:1 parity without proving it.
--- 
