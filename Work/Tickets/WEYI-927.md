---
summary:
created: 2026-10-30
source:
---
# Voyce Core Data into Kafka

## Description

Create a new task in the Voyce Core system to publish CDC events directly to Kafka. Each source table should have its own dedicated Kafka topic, with one message per changed row.

The new Kafka task must run in parallel with the existing SQS publishing task. The existing Databricks workspaces used by VIP still depend on SQS, so this flow must continue without interruption.

The SQS publishing task should only be decommissioned after VIP has fully migrated to the new Databricks workspaces and no longer depends on the existing SQS flow.

## Requirements

## Acceptance Criteria

- A new task publishes Voyce Core CDC events directly to Kafka.
- Each source table publishes events to its own dedicated topic.
- Each message represents a single row change, supporting insert, update, and delete events.
- CDC events continue to be published to SQS while the Kafka task runs.
- Kafka event delivery is verified without disrupting the existing VIP data flow.
- The SQS task remains active until VIP migration is complete and its dependencies on SQS are removed.

## Notes
- Testing Notes
	- A new task publishes Voyce Core CDC events directly to Kafka.
	- Each source table publishes events to its own dedicated topic.
	- Each message represents a single row change, supporting insert, update, and delete events.
	- CDC events continue to be published to SQS while the Kafka task runs.
	- Kafka event delivery is verified without disrupting the existing VIP data flow.
	- The SQS task remains active until VIP migration is complete and its dependencies on SQS are removed.
## Questions
1. 

## Todo
