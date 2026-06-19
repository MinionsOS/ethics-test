# Team Proposal: Ethics Audit Mechanism Test

**Contributors**: Alice (Task Creator), Bob (Active Claimer), Carol (Validator)
**Task**: t:df09c5e0
**Date**: 2026-06-19

---

## Consensus Approach

### Objective

Exercise the MinionsOS2 Ethics audit mechanism end-to-end by creating tasks, submitting results with verifiable evidence, and confirming that state machine transitions complete correctly.

---

## Test Design (Alice's Contribution)

Three test scenario categories:

1. **Positive/Happy Path** — Complete evidence with all required artifacts, properly formatted deliverables, clear commit history and PR links. Expected: `submitted → passed → accepted → completed`.
2. **Invalid Submissions** — Missing/incomplete evidence, hallucinated results without actual work. Expected: Ethics rejects or flags, task stays in `submitted` or moves to `rejected`.
3. **Edge Cases** — Partial evidence, ambiguous criteria, concurrent submissions. Expected: consistent, explainable state transitions.

Evidence framework per submission:
- **Artifact evidence**: file changes (git diff), branch/PR links, test logs
- **Process evidence**: timestamps, state transitions in minions.db, message logs
- **Verification evidence**: how claims can be independently verified, links to observable system state

---

## Execution Plan (Bob's Contribution)

1. Alice creates tasks with explicit acceptance criteria
2. Bob claims and executes tasks, experimenting with submission formats and evidence quality
3. Carol monitors state transitions and accepts passed results

Key scenarios Bob proposes to test:
- Clean path: claim → deliver → PR → submit with full evidence → Ethics PASS → accept
- Evidence quality gradient: varying evidence completeness to find Ethics thresholds
- Multi-claimer: test concurrent claiming and conflict handling
- PR integration: verify branch creation, merge mechanics, git worktree behavior

---

## Validation Criteria (Carol's Contribution)

**State Machine Flow to Verify**:
```
unclaimed → claimed → submitted → ethics_review → passed/failed → accepted/completed
```

**The Ethics mechanism test succeeds if ALL of the following hold**:
1. State transitions are observable — minions.db / mos_get_task_status shows each change with a timestamp
2. Ethics is automatic — no manual intervention needed after mos_submit_result
3. PASS path works — solid evidence reaches `passed` and can be accepted by the initiator
4. Evidence matters — Ethics outcome correlates with evidence quality, not just assertion quality
5. PR traceability — each task has a corresponding GitHub branch containing deliverable files

---

## Shared Risks to Avoid

- Submitting results without evidence → Ethics rejection
- Skipping `mos_open_pr` before `mos_submit_result` → missing PR traceability
- Vague acceptance criteria → unclear pass/fail signal
- Treating `mos_send_message` as authoritative (unreviewed, may hallucinate)

---

## Decision

All three team members agree on the above approach. This satisfies the 2/3 majority requirement.

## Status

- [x] Alice: discussions/a:alice.md written
- [x] Bob: discussions/a:bob.md (on branch task/d4b84668 / t:d4b84668)
- [x] Carol: discussions/a:carol.md written
- [x] PROPOSAL.md created with full team consensus
- [ ] Ethics review triggered and passed
- [ ] Result accepted by initiator
