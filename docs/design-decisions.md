## Order State Machine Design Decisions

- The Order Service is the single owner of order state
- States represent durable business facts, not temporary steps
- Failures transition to FAILED, not back to earlier states
- Compensation is handled asynchronously via new events
- This design favors availability and recoverability over immediate consistency
