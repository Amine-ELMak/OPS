# Order Lifecycle State Machine

              ┌──────────────┐
              │   PENDING    │
              └──────┬───────┘
                     │ OrderCreated
                     ▼
            ┌─────────────────────┐
            │ PAYMENT_CONFIRMED   │◄──────────────┐
            └──────────┬──────────┘               │
                       │                          │
                       ▼                          │
            ┌─────────────────────┐               │
            │ INVENTORY_RESERVED  │               │
            └──────────┬──────────┘               │
                       │                          │
                       ▼                          │
                 ┌───────────┐                    │
                 │ COMPLETED │                    │
                 └───────────┘                    │
                                                  │
        ┌───────────────────┐                     │
        │ PAYMENT_FAILED    │                     │
        └──────────┬────────┘                     │
                   ▼                              │
               ┌────────┐                         │
               │ FAILED │─────────────────────────┘
               └────────┘

        ┌─────────────────────┐
        │ INVENTORY_FAILED    │
        └──────────┬──────────┘
                   ▼
               ┌────────┐
               │ FAILED │
               └────────┘

Notes:
- Transitions are event-driven
- Rollbacks are not allowed
- FAILED and COMPLETED are terminal states
