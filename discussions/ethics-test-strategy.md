# Ethics Test Strategy Document

**Task ID**: t:db1addc8  
**Created by**: a:bob (Bob - Active Claimer)  
**Date**: 2026-06-19  
**Status**: Draft - awaiting team review

---

## Project Goal

Test the Ethics audit mechanism by creating tasks, submitting results, and triggering headless Ethics review to verify the state machine flow works correctly.

---

## Test Scenarios

### Scenario 1: Clean Success Path
**Task Type**: Simple documentation task with clear acceptance criteria  
**Evidence Format**:
- File created at specified path
- Content meets all acceptance criteria points
- Git commit shows the work
- PR created with clear description

**Expected Ethics Behavior**:
- Review should pass automatically
- Result should move to "passed" state
- Initiator should be able to accept
- Task should complete successfully

**Test Implementation**: This current task (t:db1addc8) serves as the first test case

---

### Scenario 2: Code Implementation with Testing
**Task Type**: Implementation task requiring code + tests  
**Evidence Format**:
- Code files created/modified in task branch
- Test files demonstrating functionality
- Test execution output showing passing tests
- PR with implementation details

**Expected Ethics Behavior**:
- Should verify presence of test evidence
- Should check for code quality indicators
- May flag if tests are missing or incomplete
- Should pass if evidence is comprehensive

**Test Implementation**: Create a follow-up task for simple feature implementation

---

### Scenario 3: Collaborative Multi-Agent Task
**Task Type**: Task requiring input from multiple agents  
**Evidence Format**:
- Multiple commits from different agents (if possible in same task)
- Discussion/coordination artifacts
- Final deliverable synthesizing multiple perspectives
- Clear audit trail of collaboration

**Expected Ethics Behavior**:
- Should handle multiple contributors
- Should verify collaborative evidence
- Should check final deliverable completeness
- Review process should be transparent

**Test Implementation**: Create a task explicitly inviting multiple agents to contribute

---

### Scenario 4: Edge Case - Minimal Evidence
**Task Type**: Simple task with bare minimum evidence  
**Evidence Format**:
- Minimal file meeting exact acceptance criteria
- No extra documentation or polish
- Basic PR description

**Expected Ethics Behavior**:
- Should determine if minimal evidence is sufficient
- May request additional evidence
- Should have clear pass/fail threshold
- Provides insights into Ethics tolerance levels

**Test Implementation**: Create a deliberately minimal submission to test boundaries

---

## Success Criteria for Overall Project

### Core Functionality
1. ✓ All three agents successfully registered (Alice, Bob, Carol)
2. ✓ Task creation works (t:db1addc8 created successfully)
3. ⏳ Task claiming works (Bob claimed t:db1addc8, status pending)
4. ⏳ Result submission triggers Ethics review
5. ⏳ Ethics review completes and returns verdict
6. ⏳ Passed results can be accepted by initiator
7. ⏳ Task state machine completes full cycle

### State Transitions Verified
- `unclaimed` → `claimed` (via mos_claim)
- `claimed` → `submitted` (via mos_submit_result)
- `submitted` → `passed` or `failed` (via Ethics review)
- `passed` → `accepted` (via mos_accept_result)
- `accepted` → `completed` (via mos_complete_task)

### Evidence Trail
- Each task has corresponding GitHub branch
- All submissions have PRs
- Ethics verdicts are recorded
- State transitions are auditable in minions.db

### Collaboration Patterns
- Agents coordinate via mos_send_message
- Formal work uses mos_create_task
- Task invitations work correctly
- Multi-agent collaboration is smooth

---

## Implementation Plan

### Phase 1: Basic Flow (Current)
1. ✓ Create initial coordination task (this document)
2. ⏳ Submit result with PR
3. ⏳ Observe Ethics review
4. ⏳ Accept result (Carol as validator)
5. ⏳ Complete task

### Phase 2: Code Implementation
1. Alice creates implementation task
2. Bob claims and implements with tests
3. Submit with comprehensive evidence
4. Verify Ethics handles code review appropriately

### Phase 3: Edge Cases
1. Test minimal evidence scenario
2. Test ambiguous completeness
3. Test error handling
4. Document Ethics behavior patterns

### Phase 4: Analysis
1. All agents document findings in discussions/<agent-id>.md
2. Team reviews all scenarios
3. Converge findings to proposals/PROPOSAL.md
4. Submit final proposal with evidence

---

## Team Review Section

### Alice's Input
*Awaiting review from a:alice*

### Bob's Input (Task Creator & Claimer)
- Created this strategy document as initial coordination artifact
- Structured test scenarios to cover different evidence types
- Defined clear success criteria for the overall project
- Ready to execute and submit this as first test case

### Carol's Input
*Awaiting review from a:carol*

---

## Next Actions

1. Alice and Carol review this document
2. Team provides input in their respective sections
3. Bob creates PR for this task branch
4. Bob submits result via mos_submit_result
5. Observe Ethics review process
6. Carol accepts if passed
7. Proceed to Phase 2 scenarios

---

*This document satisfies the acceptance criteria for task t:db1addc8*
