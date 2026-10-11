---
name: wow64-persistent-research-context
description: Preserve and recover research context across long OpenHands sessions, context compression, interruptions, and handoffs in the WoW64 Native AMD64 Client project. Prevent duplicate experiments, stale conclusions, unsupported assumptions, and loss of verified findings by reconciling DEVLogs.txt with the authoritative workspace, implementation, and evidence.
---

# WoW64 Persistent Research Context

## 1. Purpose

Use this skill whenever working on the WoW64 Native AMD64 Client project, especially when:

- Continuing an existing investigation.
- Resuming after context compression, interruption, session restart, or handoff.
- Debugging a previously investigated problem.
- Planning or performing an experiment.
- Changing rendering, animation, model parsing, runtime behavior, or reverse-engineering data.
- Deciding whether an earlier hypothesis, measurement, or implementation remains valid.
- Completing, pausing, or handing off a task.

The objective is to preserve continuity of reasoning and evidence, prevent repeated work, and continue from the latest justified state.

**Core principle: recover before acting, verify before concluding, search before repeating, and record significant findings before context is lost.**

This skill supplements the mandatory project rules. If this skill conflicts with `D:\Workspace\Project Rules.txt`, follow the project rules.

## 2. Authoritative workspace and sources

The only authorized project workspace is:

`D:\Workspace\WoW64`

Before starting project work, read:

`D:\Workspace\Project Rules.txt`

Read the development log:

`D:\Workspace\WoW64\DEVLogs.txt`

The authoritative reverse-engineering database is:

`D:\Workspace\WoW64\docs\re\database\WotLK_base.sqlite`

`WotLK_base` is a permanent name, not a version label. This database is the ONLY
authoritative RE database:

- It MUST be updated in place; all future RE work adds to, corrects, and enriches this
  single file.
- Creating a new database file that supersedes `WotLK_base.sqlite` is forbidden, and no
  `baseline.vNN` generation mechanism may be used to mint one.
- It MUST NOT be renamed.
- No parallel, sibling, "commercial", "consolidated", or "merged" database may be kept
  as a second source of truth.
- An in-place update MUST NOT lose any previously present `functions`, `evidence`, or
  `evidence_v2` row, and MUST leave `PRAGMA integrity_check` = `ok`.

This mirrors the single rule defined in `D:\Workspace\Project Rules.txt` §1.2,
`AGENTS.md` §30R, and `TASK_PROTOCOL.md` §29A. Where this skill and those documents
appear to disagree on database identity, they prevail.

Use only `D:\Workspace\WoW64` for project operations. Do not switch to clones, virtual machines, temporary workspaces, stale copies, or alternate project trees.

Treat the sources according to their distinct roles:

| Source | Purpose |
|---|---|
| `Project Rules.txt` | Mandatory project constraints and governance |
| `DEVLogs.txt` | Chronological research history, experiments, results, corrections, unresolved questions, and handoff state |
| Authoritative RE database | Structured reverse-engineering findings, statuses, evidence, provenance, and lineage |
| Source code and tests | Actual implementation and test state |
| Git state | Current branch, commit, working-tree changes, and implementation history |
| Captures, traces, reports, and evidence artifacts | Supporting evidence for specific claims |

No single source automatically proves everything. The log records what happened; it does not guarantee that an old statement still describes the current source code, database, or runtime behavior.

Never modify `Project Rules.txt` unless the user explicitly authorizes the specific modification. Do not silently rewrite or replace it.

### 2.1 Authority and priority

This skill is a specialized aid. It is subordinate to the project rules and operating
constraints. On conflict, follow this order:

1. explicit safety / system requirements;
2. direct user instructions for the current task;
3. `D:\Workspace\Project Rules.txt` (principal permanent project rules);
4. `AGENTS.md` (mandatory agent operating rules);
5. `TASK_PROTOCOL.md` (operating protocol);
6. this skill.

`DEVLogs.txt` and report artifacts record history and results; they do not establish
normative rules.

## 3. Mandatory context-recovery procedure

### Step 1 — Load the project rules

Read `D:\Workspace\Project Rules.txt` before acting.

Extract the constraints relevant to the current task. Do not rely on remembered summaries when the actual file is available.

### Step 2 — Recover the relevant research history

Read `D:\Workspace\WoW64\DEVLogs.txt`.

Identify the history relevant to the current task, including:

- The investigation's objective and initial conditions.
- Experiments and implementation changes performed afterward.
- The latest relevant results and explicit corrections.
- Superseded conclusions and abandoned approaches.
- Unresolved questions and their dependencies.
- The most recent justified next action.

Do not inspect only the final lines and assume they represent the current state.

If the log is too large to inspect in one operation, search for relevant topics, evidence filenames, function addresses, artifact names, hypothesis identifiers, and subsystem terms. Read enough surrounding entries to reconstruct the sequence. Follow references to earlier experiments when they affect the current decision.

Use existing summaries to navigate the history, not as substitutes for verifying critical facts in the original records.

### Step 3 — Establish the relevant actual project state

Inspect the current workspace only as deeply as the task requires.

When relevant, establish:

- Current Git branch and HEAD.
- Whether the working tree contains changes that must be preserved.
- Which implementation is currently present.
- Whether earlier diagnostic changes were reverted or retained.
- Relevant RE database identity, schema or baseline version, and records.
- Which tests and runtime validations have actually passed.
- Whether evidence referenced by the log still exists and applies to the current state.

**Do not perform a broad audit merely to recover context.** Inspect only the files, records, and evidence that could affect the next decision.

For a narrow task with a well-established history, a targeted review is sufficient. For a major investigation, an ambiguous handoff, or a conflict between sources, perform the additional checks needed to resolve the uncertainty.

If the log and actual workspace disagree, do not silently choose one. Establish what can be verified, record the discrepancy when material, and resolve it before making a dependent change.

### Step 4 — Establish the current research state

Before a significant experiment or implementation change, establish the following:

- **Objective:** The exact behavior or property being investigated.
- **Confirmed:** Findings supported by identifiable evidence.
- **Previously confirmed:** Findings supported by earlier evidence but not revalidated against the current state.
- **Rejected:** Hypotheses contradicted by experiments or evidence.
- **Unresolved:** Questions for which the available evidence is insufficient.
- **Current implementation:** Relevant behavior actually present in the workspace.
- **Do not repeat:** Previous experiments and the conditions under which their results remain applicable.
- **Dependencies:** Missing evidence, prerequisites, or blocked validations.
- **Next justified action:** The smallest useful action supported by the evidence.

Keep this summary internal for routine work. Record or update it in `DEVLogs.txt` when it materially improves continuity, resolves ambiguity, or is needed for a reliable handoff.

Do not turn every task into a new audit report.

## 4. Evidence and knowledge classification

Keep the following categories distinct in reasoning, implementation decisions, and logging.

These categories track the lifecycle of a research conclusion across sessions. They are
complementary to, not a replacement for, the evidence-provenance categories of
`AGENTS.md` §3 / `TASK_PROTOCOL.md` §3 (ORIGINAL_RE, RUNTIME_CONFIRMED,
CONTRACT_CONFIRMED, UNIT_TEST_CONFIRMED, THIRD_PARTY_CONFIRMED, INFERRED, UNKNOWN).
The normative mapping is `AGENTS.md` §3A. In particular, a *previously confirmed* or
*carried-over* finding is NOT thereby newly confirmed and MUST NOT justify a
`functions.status` transition until revalidated.

### 4.1 Confirmed finding

A claim directly supported by appropriate evidence, such as a reproducible runtime trace, binary analysis, validated database record, source inspection, or differential test.

Identify the supporting artifact, function address, evidence ID, source location, or test result whenever available.

The evidence must support the specific claim being made. A successful build does not prove runtime correctness, and a plausible source-level interpretation does not automatically establish original-client behavior.

### 4.2 Previously confirmed finding

A finding supported by earlier experiments or artifacts that has not been revalidated against the current implementation or environment.

Preserve the historical conclusion, but do not describe it as newly verified.

### 4.3 Hypothesis

A plausible explanation that remains unproven.

State the supporting observations, contradictory evidence, and the observation or experiment that would distinguish it from competing explanations.

Do not silently promote a hypothesis to a confirmed finding.

### 4.4 Rejected hypothesis

A hypothesis contradicted under documented test conditions.

Preserve the rejection and its evidence. Do not retry it under materially equivalent conditions merely because the result would be convenient.

Reconsider it only when there is a specific justification, such as:

- A relevant implementation change.
- Corrected experimental conditions.
- New evidence.
- A previously unidentified dependency.
- A demonstrated flaw in the original test.

Document why reconsideration is justified and what new information is expected.

### 4.5 Inconclusive result

An experiment that did not distinguish between competing explanations, lacked necessary instrumentation, used invalid conditions, or produced unreliable measurements.

Do not record an inconclusive result as confirmation or rejection.

### 4.6 Superseded conclusion

A conclusion replaced by stronger evidence, a correction, or a subsequent implementation change.

Preserve the historical sequence and explicitly document the superseding result. Do not erase the original conclusion merely because it was later shown to be incorrect.

### 4.7 Carried-over information

A claim inherited from an earlier summary, session, or task without independent verification in the current investigation.

Label its provenance honestly. Do not claim that binary-level reverse engineering was independently performed if only a prior summary was reviewed.

## 5. Preventing duplicate work

Before proposing or executing an experiment, search the relevant history for previous experiments addressing the same underlying question.

Compare them by:

- The hypothesis being tested.
- The implementation and configuration under test.
- The input, environment, and runtime conditions.
- The observed measurements.
- The evidence and conclusion.
- The limitations of the previous test.

Different names, scripts, parameter values, or output filenames do not necessarily make two experiments meaningfully different.

### If an equivalent experiment already exists

Reuse its result when the conditions and implementation remain applicable. Continue to the next unresolved question.

### If the previous experiment was inconclusive

Identify the exact limitation. Design a test that resolves that limitation rather than repeating the original test unchanged.

### If the implementation has changed

Determine whether the change affects the previous result. Revalidate only the affected property.

Do not invalidate unrelated historical findings merely because some part of the implementation changed.

### If repeating a test is necessary

Document why repetition is justified, what has changed, and what new information the repeat is expected to produce.

### If the history is insufficient

Do not invent a previous result or assume that a test was performed. Search the relevant evidence and inspect the actual implementation. If the result remains unknown, label it as unknown.

**Never repeat an experiment solely because context compression removed its details from the active conversation.**

## 6. Selecting the next action

Choose the next action based on current evidence, not on the age of a task description or the order in which entries appear in the log.

Prefer actions that:

1. Resolve a specific consequential uncertainty.
2. Distinguish between competing explanations.
3. Establish a missing fact required for a safe implementation.
4. Validate an existing change under the conditions that matter.
5. Eliminate a documented blocker.
6. Preserve a verified result in the appropriate authoritative source.

Do not jump from an observed discrepancy directly to an implementation guess when the underlying behavior can be investigated.

For rendering and animation issues, distinguish among reference capture conditions, runtime state, resource identity, shader or fixed-function state, transforms, blending, animation inputs, and implementation defects when relevant.

Do not assume that a plausible explanation represents original-client behavior.

Do not apply broad changes to compensate for a discrepancy demonstrated only in a specific material, pass, texture, model, or runtime state.

When several explanations remain possible, select the smallest experiment that can discriminate between them.

Avoid unnecessary preparation, repeated audits, and redundant validation. However, never skip a check that is required by the project rules or necessary to establish the correctness of the intended change.

## 7. Keeping DEVLogs.txt useful

Preserve the existing chronological log format and established conventions. Do not rewrite the entire log, rename historical entries, or reorganize the history merely to accommodate this skill.

Add a new entry or update the current-state summary when a task produces a meaningful result, changes the implementation or authoritative data, changes the status of an investigation, discovers a material limitation, corrects an earlier conclusion, or establishes a useful handoff state.

Do not create log entries for every trivial command, routine inspection, or insignificant operation.

At the end of a meaningful task, and before an unavoidable interruption when practical, ensure that `DEVLogs.txt` contains enough information to resume without reconstructing the investigation from scratch.

### 7.1 Record the relevant information

**Identification**
- Entry identifier and date, following existing conventions.
- Investigation or subsystem.
- Workspace and relevant Git state when useful.

**Objective and baseline**
- What was being tested or changed.
- Relevant initial conditions, inputs, reference captures, configuration, or build.

**Actions**
- What was actually inspected, changed, executed, or measured.
- Relevant source files, function addresses, scripts, database records, and artifact paths.

**Results**
- Quantitative measurements where available.
- Confirmed, rejected, and inconclusive hypotheses.
- What the results establish and what they do not establish.

**Validation**
- Build and test outcomes.
- Runtime confirmation and differential comparisons when relevant.
- Checks not performed, failures, limitations, and remaining uncertainty.

**Change disposition**
- Which modifications remain in the workspace.
- Which diagnostic changes were reverted.
- Whether database or other authoritative artifacts changed.
- Relevant before/after hashes, commits, evidence IDs, or database versions when available and meaningful.

**Continuation**
- Current implementation state.
- Outstanding questions and dependencies.
- The next justified action.
- Experiments or assumptions that must not be repeated without new justification.

Record only the items relevant to the task. Avoid duplicating long blocks of unchanged information already documented in the history.

### 7.2 Distinguish implementation from validation

Do not report a check as passed unless it was actually executed and its result observed.

Clearly distinguish:

- Source modification completed.
- Build succeeded.
- Unit or integration tests passed.
- Runtime behavior was observed.
- Differential comparison improved or met its criteria.
- Behavioral equivalence was established to the extent supported by the evidence.

These are different levels of validation.

Record checks that were not performed when their absence materially affects the conclusion or handoff.

Never invent hashes, evidence IDs, test results, timestamps, or file paths.

### 7.3 Preserve corrections explicitly

If a previous measurement or conclusion was wrong, document:

1. The original claim.
2. Why it was invalid.
3. The corrected measurement or conclusion.
4. The conditions required for the corrected result.
5. Which downstream decisions are affected.

Do not silently replace a false result with a correct one. The correction is valuable research history and may prevent the same mistake from recurring.

### 7.4 Avoid log noise

Record enough detail to prevent costly repeated work or misinterpretation, but do not turn the log into a transcript of every operation.

When a topic has accumulated many entries and its current state is distributed across them, add a compact, clearly dated `CURRENT RESEARCH STATE` section or entry. Preserve the underlying chronology.

A state summary should reduce recovery effort, not create another large document that must be maintained independently.

## 8. Current Research State format

Use this structure for long-running investigations when the current state is distributed across multiple entries.

Adapt it to the existing log conventions rather than restructuring the entire file.

### CURRENT RESEARCH STATE — [topic]

- **Updated:** Date and time, if known.
- **Scope:** The exact behavior or question being investigated.
- **Current implementation:** What is actually present in the workspace.
- **Confirmed findings:** Conclusions with evidence references.
- **Previously confirmed, not revalidated:** Relevant historical findings.
- **Rejected hypotheses:** Hypothesis, conditions tested, and evidence reference.
- **Open hypotheses:** Competing explanations and the evidence needed to distinguish them.
- **Known limitations:** Instrumentation gaps, untested conditions, missing artifacts, or other constraints.
- **Do not repeat:** Equivalent experiments and why their results remain applicable.
- **Next justified action:** One concrete action and why it is the next step.
- **Acceptance criteria:** The evidence required to consider the immediate action successful.
- **Validation status:** What passed, what failed, and what remains untested.
- **Relevant artifacts:** Exact paths, evidence IDs, database identifiers, and other useful references.

Update this state when a meaningful finding, implementation change, or validation result makes the previous summary stale.

Do not update it after every trivial operation.

Do not treat it as a substitute for detailed experiment records.

Do not maintain multiple conflicting current-state summaries for the same topic without clearly identifying which is current and which has been superseded.

A state summary must not imply that unverified historical findings have been independently revalidated.

## 9. Handling context compression and session interruption

After context compression, interruption, restart, or handoff, do not assume that the active conversation contains the complete project history.

Recover in this order:

1. Read `D:\Workspace\Project Rules.txt`.
2. Read `D:\Workspace\WoW64\DEVLogs.txt`.
3. Locate the current-state summary relevant to the task and its underlying entries.
4. Identify corrections, superseded conclusions, and later experiments affecting the topic.
5. Check the current source, Git state, database, or artifacts where necessary to establish whether historical findings still apply.
6. Identify the last completed action and the first unfinished action.
7. Resume from the latest justified next step.

Do not restart a completed phase merely because its completion details are missing from the active conversation.

Do not assume that the last entry in the log represents the current status of every subsystem. A newer entry about another topic does not supersede an older finding unrelated to it.

If the recovery process discovers contradictory states, resolve the contradiction before making a dependent change.

If a required source is inaccessible, explicitly identify which facts could not be verified. Proceed only when that uncertainty does not invalidate the next action.

Do not fabricate missing history or silently reconstruct an uncertain result as fact.

## 10. Safe implementation and evidence preservation

Context continuity does not override implementation safety or reverse-engineering evidence requirements.

Before modifying code or authoritative data:

- Understand the relevant current implementation.
- Identify the evidence that justifies the change.
- Check whether the proposed change duplicates or reverses an earlier attempt.
- Preserve unrelated user modifications.
- Follow the existing project workflow and validation requirements.
- Avoid unsupported behavior or fabricated reverse-engineering details.

After changing code, data, or configuration, record the actual outcome when the change is significant.

If an experiment fails, do not automatically discard the result. Determine whether the failure is evidence against the hypothesis, evidence of a defective test, or an environmental or build problem.

If a change is reverted, verify the resulting workspace state rather than relying on an earlier intention to revert it.

For RE database work, comply with the project's database, provenance, evidence, lineage, and status-transition rules. A detailed development-log entry does not itself validate an RE claim or authorize a database status transition.

Do not overwrite or discard existing user changes merely to restore a historical baseline. Establish the current state and preserve unrelated modifications.

## 11. Completion and handoff

A task is not complete merely because code was changed or a hypothesis appears plausible.

Before reporting completion:

1. Verify the requested implementation or research action.
2. Execute the relevant required checks that are feasible within the task.
3. Record material checks that were not executed and why.
4. Confirm which changes remain in the workspace.
5. Preserve meaningful findings and validation results in `DEVLogs.txt`.
6. Identify the next action only if further work remains.
7. Report the actual outcome without overstating behavioral equivalence.

For routine tasks that produce no meaningful research result or persistent state change, do not create an unnecessary log entry solely to satisfy a logging ritual.

A useful handoff must let another session answer these questions without repeating the investigation:

- What was the objective?
- What is established by evidence?
- What has already been tried?
- Which explanations were rejected, and why?
- What is implemented now?
- What remains uncertain or unvalidated?
- What is the next justified action?
- Which exact artifacts should be consulted?

If interrupted before completion, preserve the current state and unfinished work when practical. Do not mark the task complete merely to produce a clean handoff.

## 12. Reporting requirements

When summarizing work for the user:

- Lead with the actual result.
- Distinguish implementation progress from verified behavioral equivalence.
- Identify the most important evidence and validation status.
- Mention significant unresolved issues and unexecuted checks.
- Provide the next justified action when further work is needed.
- Avoid repeating the entire historical investigation unless requested.

Do not claim that the skill, project rules, development log, database, or source code was updated unless the corresponding change was actually made and verified.

## 13. Final operating principle

**Recover before acting. Verify before concluding. Search before repeating. Record before context is lost.**

The purpose of persistent context is not to create more paperwork. It is to preserve expensive reasoning, maintain evidence integrity, prevent duplicate experiments, and allow WoW64 development to continue from the last justified state—even after the active context has been compressed or replaced.
