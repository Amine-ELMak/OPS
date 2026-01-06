## Order Lifecycle State Machine

This system uses an event-driven, eventually consistent order lifecycle.
The Order Service is the sole owner of order state.

### Design Principles

- Orders are driven exclusively by events
- No synchronous coordination between services
- State transitions are forward-only
- Every order ends in a terminal state
- Failures are handled via compensation, not rollback

### Order States

| State | Description |
|------|-------------|
| PENDING | Order created, awaiting payment |
| PAYMENT_CONFIRMED | Payment succeeded |
| PAYMENT_FAILED | Payment failed |
| INVENTORY_RESERVED | Inventory successfully reserved |
| INVENTORY_FAILED | Inventory reservation failed |
| COMPLETED | Order successfully completed |
| FAILED | Order failed and will not progress further |

### Terminal States

- `COMPLETED`
- `FAILED`

Once an order reaches a terminal state, no further transitions are allowed.

### Valid State Transitions

| Current State | Event | Next State |
|--------------|-------|------------|
| — | OrderCreated | PENDING |
| PENDING | PaymentConfirmed | PAYMENT_CONFIRMED |
| PENDING | PaymentFailed | PAYMENT_FAILED |
| PAYMENT_CONFIRMED | InventoryReserved | INVENTORY_RESERVED |
| PAYMENT_CONFIRMED | InventoryFailed | INVENTORY_FAILED |
| INVENTORY_RESERVED | OrderCompleted | COMPLETED |
| PAYMENT_FAILED | OrderFailed | FAILED |
| INVENTORY_FAILED | OrderFailed | FAILED |

Any event that does not match a valid transition is ignored.

### Duplicate & Replayed Events

Kafka provides at-least-once delivery.
Duplicate or replayed events do not cause corruption because:

- Order state transitions are validated
- Invalid transitions are ignored
- Event processing is idempotent

This guarantees correctness under retries, crashes, and replays.
