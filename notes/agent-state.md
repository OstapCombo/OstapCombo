# Agent activity and completed work

By Igor Grigoryev · Design note

An agent can be assigned a task while its process is offline. It can also be active while making no useful progress. An orchestration interface should make those differences visible.

## Keep three independent dimensions

| Dimension | Example values | Evidence |
| --- | --- | --- |
| Assignment | Unassigned, assigned, released | Ownership record |
| Execution | Running, waiting, stopped, unknown | Recent executor observations |
| Acceptance | Pending, accepted, rejected | Review of a specific output |

Do not turn an assignment into an execution heartbeat. Do not turn a heartbeat into acceptance.

## Make observations expire

Every observation needs a measurement time and a validity window. If a heartbeat is too old, show the observation as stale. Do not silently carry the last green indicator forward.

A blocked task should name the dependency or decision it needs. A retry should refer to the previous attempt and explain what changed.

## Tie acceptance to an exact output

The following is an illustrative record, not a real Syncra run:

```json
{
  "task_id": "example-task",
  "attempt_id": "example-attempt-2",
  "artifact_id": "example-report-v2",
  "acceptance": "pending",
  "checks": [
    {"name": "source_links_present", "result": "passed"},
    {"name": "independent_review", "result": "pending"}
  ]
}
```

A real record also needs the artifact digest, measurement timestamps, actor identity and check provenance. If the artifact changes, its earlier review does not automatically apply to the new bytes.

## Define completion before execution

For a documentation change, acceptance may require correct links and an accurate description of current behavior. For a product change, it may also require a test of the affected user flow on a known build.

A screenshot, a commit and a test report answer different questions. Choose evidence that proves the requested outcome.

[Back to profile](../README.md)
