# Ethics Testing Strategy Proposal

**Task**: t:df09c5e0 - Initial Ethics Testing Strategy Discussion  
**Status**: Draft (awaiting Bob and Carol's input)  
**Date**: 2026-06-19

---

## Executive Summary

This proposal outlines a systematic approach to testing the MinionsOS2 Ethics audit mechanism. The strategy focuses on exercising key state machine transitions, validating evidence-based decision making, and ensuring the Ethics review process correctly distinguishes valid from invalid submissions.

---

## I. Testing Philosophy

### Core Principles
1. **Evidence-Driven**: Every claim must be backed by verifiable artifacts
2. **Systematic Coverage**: Test all critical state transitions and edge cases
3. **Progressive Complexity**: Start simple, gradually increase scenario complexity
4. **Objective Verification**: Success criteria must be independently verifiable

### Ethics Role
- Ethics is an **automatic verification mechanism**, not a quality judge
- Reviews evidence completeness and honesty, not implementation quality
- Decisions must be explainable and traceable
- Operates headlessly without human intervention

---

## II. Test Scenario Categories

### A. Valid Submissions (Happy Path)

**Objective**: Verify Ethics correctly passes legitimate work with complete evidence

**Test Cases**:
1. **Simple Task Completion**
   - Single agent claims and completes task
   - All acceptance criteria met
   - Complete evidence: commits, PR, verification logs
   - Expected: Pass → Accept → Complete

2. **Multi-Agent Collaboration**
   - Multiple agents contribute to shared deliverables
   - Each contribution traceable via git history
   - Expected: Pass → Accept → Complete

3. **Subtask Aggregation**
   - Parent task with multiple subtasks
   - Each subtask individually verified
   - Parent completion requires all subtasks done
   - Expected: Hierarchical pass → Accept → Complete

**Success Metrics**:
- 100% of valid submissions pass Ethics review
- State transitions complete within expected timeframes
- No false rejections

---

### B. Invalid Submissions (Failure Cases)

**Objective**: Verify Ethics correctly rejects incomplete or dishonest submissions

**Test Cases**:
1. **Missing Evidence**
   - Claim task completion without commits
   - No PR or branch reference
   - Expected: Reject with clear feedback

2. **Incomplete Deliverables**
   - Some but not all acceptance criteria met
   - Partial evidence provided
   - Expected: Reject or request revision

3. **Unverifiable Claims**
   - Claims without supporting artifacts
   - Hallucinated results (no actual work in repo)
   - Expected: Reject, flag honesty concern

**Success Metrics**:
- 100% of invalid submissions rejected
- Rejection reasons are clear and actionable
- No false acceptances

---

### C. Edge Cases (Boundary Testing)

**Objective**: Verify robust handling of complex or ambiguous scenarios

**Test Cases**:
1. **Concurrent Submissions**
   - Multiple agents submit results simultaneously
   - Test race condition handling
   - Expected: Consistent, ordered processing

2. **Ambiguous Acceptance Criteria**
   - Criteria open to interpretation
   - Partial compliance scenarios
   - Expected: Context-aware, explainable decisions

3. **Revision After Rejection**
   - Submit → Reject → Fix → Resubmit
   - Test state recovery and revalidation
   - Expected: Accept revised submission if evidence complete

**Success Metrics**:
- No deadlocks or inconsistent states
- Clear handling of ambiguous cases
- State machine remains stable under edge conditions

---

## III. Evidence Requirements Framework

For every test submission, document:

### 1. Artifact Evidence
- **Git commits**: Specific SHA, author, timestamp
- **Branch reference**: task/<id> or subtask branch
- **Pull request**: PR number, diff, review status
- **File changes**: Specific files created/modified with line counts

### 2. Process Evidence
- **State transitions**: Timestamps from minions.db
- **Task status**: Audit trail of status changes
- **Agent actions**: Claim, submit, accept events with timestamps
- **Communication logs**: Relevant mos_send_message exchanges

### 3. Verification Evidence
- **Test results**: Pass/fail status of test suites
- **Manual verification steps**: How claims can be independently checked
- **Screenshots/logs**: For UI or runtime behavior claims
- **External validation**: CI runs, deployment logs, etc.

---

## IV. Test Progression Plan

### Phase 1: Baseline Validation (Current Task)
- **Goal**: Establish that basic valid submission passes
- **Scope**: This discussion task (t:df09c5e0)
- **Success**: All three agents contribute, Ethics passes, task completes

### Phase 2: Intentional Failure Test
- **Goal**: Verify Ethics rejection mechanism
- **Scope**: Create task, submit without evidence
- **Success**: Ethics rejects, provides clear feedback

### Phase 3: Edge Case Testing
- **Goal**: Test robustness under complex scenarios
- **Scope**: Concurrent claims, ambiguous criteria
- **Success**: Consistent behavior, no crashes

### Phase 4: Multi-Level Task Testing
- **Goal**: Validate subtask handling and aggregation
- **Scope**: Parent task with 2-3 subtasks
- **Success**: Hierarchical verification works correctly

---

## V. Success Metrics

### Coverage Metrics
- **State Transitions**: % of FSM states and transitions exercised
- **Code Paths**: % of Ethics decision branches tested
- **Scenario Types**: Valid/Invalid/Edge all represented

### Correctness Metrics
- **True Positives**: Valid submissions correctly passed
- **True Negatives**: Invalid submissions correctly rejected
- **False Positives**: Invalid submissions incorrectly passed (target: 0%)
- **False Negatives**: Valid submissions incorrectly rejected (target: 0%)

### Quality Metrics
- **Feedback Clarity**: Can rejectees understand what to fix?
- **Decision Traceability**: Can we audit why Ethics decided X?
- **Consistency**: Same evidence → same decision across runs

---

## VI. Open Questions for Team Resolution

1. **Malicious Testing**: Should we test deliberately deceptive evidence?

2. **Ethics Transparency**: How do we validate Ethics reasoning without direct access to decision logs?

3. **Stopping Criteria**: What threshold for "enough testing" before declaring production-ready?

4. **Bug vs Feature**: If Ethics behaves unexpectedly but consistently, bug or feature?

5. **Performance**: Should we test Ethics under load (10 concurrent submissions)?

---

## VII. Team Contributions Needed

### Bob's Input (Execution & Submission)
- [ ] Claimer perspective on evidence gathering during work
- [ ] Practical challenges in preparing complete submissions
- [ ] Suggestions for streamlining result submission workflow

### Carol's Input (Validation & Verification)
- [ ] Validator perspective on acceptance criteria clarity
- [ ] How to verify state machine correctness
- [ ] Metrics for measuring Ethics effectiveness

### Convergence
- [ ] Review and refine this proposal based on all perspectives
- [ ] Resolve open questions
- [ ] Finalize test progression plan
- [ ] Assign ownership for Phase 2+ test tasks

---

## VIII. Next Steps

1. **Await Bob and Carol's contributions** to discussions/
2. **Integrate their perspectives** into this proposal
3. **Resolve open questions** through team discussion
4. **Finalize and submit** this task result with complete evidence
5. **Execute Phase 2** based on agreed strategy

---

**Current Status**: Draft proposal based on Alice's perspective. Awaiting Bob and Carol's input to finalize.
