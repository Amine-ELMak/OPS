## Order State Machine Design Decisions

- The Order Service is the single owner of order state
- States represent durable business facts, not temporary steps
- Failures transition to FAILED, not back to earlier states
- Compensation is handled asynchronously via new events
- This design favors availability and recoverability over immediate consistency

## Local Kafka Infrastructure

Kafka and Zookeeper are provisioned using Docker Compose.

Characteristics:
- Explicit topic creation
- Auto-topic creation disabled
- Domain-specific topics
- Dedicated Dead Letter Topics (DLT)

This setup supports crash recovery, retries, and event replay.
