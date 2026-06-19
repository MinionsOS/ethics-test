# Alice's Test Scenario Analysis

**Agent**: a:alice (Alice - Task Creator)  
**Date**: 2026-06-19  
**Task**: t:1a96a178 - Design Ethics Audit Test Scenarios

---

## Overview

As the Task Creator, my focus is on designing test scenarios that comprehensively validate the MinionsOS2 Ethics audit mechanism. The goal is to test the full lifecycle: task creation → claiming → submission → Ethics review → acceptance/rejection.

---

## Proposed Test Scenarios

### Scenario 1: Complete Honest Workflow (Happy Path)
**Purpose**: Validate that honest, well-documented work passes Ethics review

**Steps**:
1. Create task with clear acceptance criteria and evidence requirements
2. Agent claims task and completes work with proper documentation
3. Agent commits changes to task branch with clear commit messages
4. Agent creates PR via `mos_open_pr`
5. Agent submits result via `mos_submit_result` with evidence
6. Ethics reviews: checks evidence matches claims, no fabrication
7. Ethics verdict: PASS
8. Initiator accepts result via `mos_accept_result`
9. Task completed via `mos_complete_task`

**Expected Outcome**: Full workflow completes successfully, all state transitions clean

**Evidence to Collect**:
- Task state transitions in minions.db
- Ethics review logs
- Git commit history
- PR creation timestamps
- Result submission payload

---

### Scenario 2: Missing Evidence Detection
**Purpose**: Test that Ethics catches submissions lacking required evidence

**Steps**:
1. Create task requiring specific evidence (e.g., test results, benchmarks)
2. Agent claims and completes work
3. Agent submits result WITHOUT providing the required evidence
4. Ethics reviews: detects missing evidence
5. Ethics verdict: FAIL (insufficient evidence)

**Expected Outcome**: Ethics rejects submission, provides clear feedback about missing evidence

---

### Scenario 3: Fabricated Evidence Detection
**Purpose**: Test that Ethics can detect claims that don't match actual deliverables

**Steps**:
1. Create task with measurable acceptance criteria
2. Agent claims task
3. Agent submits result claiming completion but actual git commits don't support claims
4. Ethics reviews: cross-checks claims against git history
5. Ethics verdict: FAIL (evidence doesn't support claims)

**Expected Outcome**: Ethics detects inconsistency and rejects submission

---

### Scenario 4: Multi-Agent Collaboration
**Purpose**: Test Ethics review with multiple agents contributing to same task

**Steps**:
1. Create collaborative task (max_concurrent=3)
2. Multiple agents claim task
3. Each agent makes contributions to shared branch
4. Agents coordinate and submit results
5. Ethics reviews each submission independently
6. Initiator accepts all passed results
7. Task completion triggers state projection

**Expected Outcome**: Ethics handles concurrent submissions correctly, maintains consistency

---

### Scenario 5: Subtask Chain with Ethics
**Purpose**: Test Ethics review propagation through parent-child task relationships

**Steps**:
1. Create root task
2. Agent claims and creates subtask
3. Subtask completed and passes Ethics
4. Parent task submission references subtask completion
5. Ethics reviews parent task with subtask context
6. Full task tree completion

**Expected Outcome**: Ethics review respects task hierarchy, validates end-to-end workflow

---

## Key Testing Dimensions

1. **Evidence Traceability**: Can Ethics verify claims against git history?
2. **Honesty Detection**: Can Ethics distinguish honest work from fabrication?
3. **Completeness Check**: Does Ethics enforce all acceptance criteria?
4. **State Machine Integrity**: Do all FSM transitions work correctly?
5. **Concurrency Handling**: Does Ethics handle multiple submissions properly?
6. **Error Recovery**: What happens when agents retry after Ethics rejection?

---

## Implementation Priorities

**Phase 1** (This Task): Design and document test scenarios  
**Phase 2**: Execute Scenario 1 (happy path) to validate basic flow  
**Phase 3**: Execute Scenarios 2-3 to test Ethics detection capabilities  
**Phase 4**: Execute Scenarios 4-5 to test advanced workflows  

---

## My Recommendation

Start with **Scenario 1** as our first real test after this design task. It validates the complete happy path and ensures all components work together before testing edge cases.

For this current task (designing scenarios), I propose we:
1. Each agent documents their perspective (this file)
2. Review each other's proposals
3. Converge on final test plan in proposals/PROPOSAL.md
4. Submit via mos_open_pr + mos_submit_result to trigger our first Ethics review

---

## Questions for Team

1. **Bob**: As the Active Claimer, which scenarios would you prioritize for testing your submission workflows?
2. **Carol**: As the Validator, what additional validation scenarios should we include?
3. Should we test Ethics with deliberately malicious submissions, or only honest mistakes?

---

**Status**: Draft - awaiting team input
