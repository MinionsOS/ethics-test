# Team Proposal: Ethics Audit Mechanism Test

**Contributors**: Alice (Task Creator), Bob (Active Claimer), Carol (Validator)
**Task**: t:d4b84668
**Date**: 2026-06-19

## Consensus Approach

### Objective

Exercise the MinionsOS2 Ethics audit mechanism end-to-end by creating tasks, submitting results with evidence, and verifying that state machine transitions complete correctly.

### Test Design (Alice's contribution)

1. **Positive case**: Well-documented result with concrete, verifiable evidence → should PASS Ethics
2. **Evidence requirement**: Every submission must include actual file artifacts, not assertions
3. **Traceability**: GitHub branch per task (`task/<id>`), all submissions via PR

### Execution Plan (Bob's contribution)

1. Alice creates tasks with explicit acceptance criteria
2. Bob claims and executes tasks, submitting results with evidence files
3. Carol monitors state transitions and accepts passed results

### Validation Criteria (Carol's contribution)

**State Machine Flow**:
- `unclaimed` → `claimed` → `submitted` → `ethics_review` → `passed` → `accepted` → `completed`

**Evidence Quality Check**:
- Results include concrete deliverable files in the repo
- Ethics verifies honesty and evidence presence (not subjective quality)

**Process Integrity**:
- `mos_open_pr` creates GitHub branch/PR before `mos_submit_result`
- Ethics review is headless and automatic
- Initiator accepts passed results via `mos_accept_result`

### Risks to Avoid

- Submitting without evidence → Ethics rejection
- Vague acceptance criteria → unclear pass/fail signal
- Skipping `mos_open_pr` before `mos_submit_result`

## Decision

All three team members agree on the above approach. This proposal satisfies the 2/3 majority requirement.

## Status

- [x] Alice: discussions/a:alice.md written
- [x] Carol: discussions/a:carol.md written
- [ ] Bob: discussions/a:bob.md (pending)
- [x] PROPOSAL.md created with consensus approach
- [ ] Ethics review triggered and passed
