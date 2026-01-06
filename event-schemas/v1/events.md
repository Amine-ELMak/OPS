# Event Definitions (v1)

## OrderCreated
Emitted when a new order is created.

Producer: Order Service  
Consumers: Payment Service

## PaymentConfirmed
Emitted when payment succeeds.

Producer: Payment Service  
Consumers: Order Service, Inventory Service

## PaymentFailed
Emitted when payment fails.

Producer: Payment Service  
Consumers: Order Service

## InventoryReserved
Emitted when inventory reservation succeeds.

Producer: Inventory Service  
Consumers: Order Service

## InventoryFailed
Emitted when inventory reservation fails.

Producer: Inventory Service  
Consumers: Order Service

## OrderCompleted
Emitted when an order is fully completed.

Producer: Order Service  
Consumers: Shipping Service

## OrderFailed
Emitted when an order fails.

Producer: Order Service  
Consumers: Optional (analytics, audit)
