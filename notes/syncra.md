# Syncra: orchestration with evidence

By Igor Grigoryev · Design note

Syncra is my work on orchestration for AI-assisted software and research workflows. The central question is practical: how do several tools and agents produce one result that a person can inspect and trust?

This note describes the design approach. It is not a public SDK release or a claim that every component is complete.

## Separate responsibility from activity

A task has an owner, a scope and an acceptance condition. A running process does not prove progress. A successful tool call does not prove that the requested outcome exists.

The orchestration layer should connect these records:

| Record | Purpose |
| --- | --- |
| Task | Requested outcome, scope and acceptance condition |
| Assignment | Current owner and allowed actions |
| Attempt | One bounded execution of the task |
| Artifact | Inspectable output with an identifier and digest |
| Review | Decision supported by checks on that output |

Several attempts may serve one task. An artifact may exist before it is accepted. A reviewer may reject an output without losing its history.

## Use durable state

Conversation helps explain intent. Structured state should record ownership, dependencies and accepted results. A replacement session should be able to recover the next action without reconstructing the whole chat.

MCP tools provide an interface to this state and to domain actions. The state model still needs explicit permissions, freshness rules and evidence.

## Bound parallel work

Split independent tasks. Assign one writer per shared resource. Use isolated workspaces when changes can collide. Review the combined result after integration.

The useful measure is accepted work per unit of time and cost. Agent count alone does not establish that measure.

## Public scope

These notes cover general engineering ideas. Product repositories, customer data and deployment details remain private. REE is a separate collaborative product; this note does not assign its ownership or its team's work to Syncra.

[Back to profile](../README.md)
