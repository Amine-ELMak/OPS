# Event Schemas – Version 1

This directory defines the immutable event contracts used for
inter-service communication.

Rules:
- Events are immutable facts
- Events are versioned
- Backward compatibility is mandatory
- Breaking changes require a new version directory

This version defines the initial order processing flow.

## Event-Driven Communication Model

All inter-service communication is performed via Kafka events.
Services never call each other synchronously.

Each event:
- Represents a business fact
- Is immutable
- Is owned by a single service
- Can be safely replayed

This model enables:
- Eventual consistency
- Independent deployment
- Failure recovery via replay
