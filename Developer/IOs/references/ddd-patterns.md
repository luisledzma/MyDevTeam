# DDD Patterns Reference

> Domain-Driven Design patterns and rules for this project. Consult this file before modeling any domain concept or placing business logic.

---

## Core Principles

| Principle                | Description                                                                                                                                                                          |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Ubiquitous Language**  | All code symbols (types, methods, variables) must use the same terminology as the domain experts and product requirements. Never use generic names like `data`, `info`, or `object`. |
| **Bounded Context**      | Each major module owns its own domain model. Never share mutable domain objects across bounded context boundaries — use mappings or domain events instead.                           |
| **Layered Architecture** | Domain logic must not depend on infrastructure or UI layers. Dependencies always point inward toward the domain.                                                                     |

---

## Building Blocks

### Entity

An object defined by its **identity**, not its attributes. Two entities with the same attributes but different IDs are different objects.

```swift
// ✅ Entity — has a stable identity
struct Order: Identifiable {
    let id: UUID           // identity
    var status: OrderStatus
    var lineItems: [LineItem]
}
```

**Rules:**

- Always carry a stable, unique `id`.
- Mutable state is allowed.
- Equality is based on `id`, not attribute values.

---

### Value Object

An object defined entirely by its **attributes**. Two value objects with the same attributes are equal and interchangeable.

```swift
// ✅ Value Object — no identity, fully described by its properties
struct Money: Equatable {
    let amount: Decimal
    let currency: Currency
}
```

**Rules:**

- Must be `struct` (value type).
- Must be immutable — `let` properties only.
- Equality is based on all property values.
- Never assign an `id` to a value object.

---

### Aggregate

A **cluster of entities and value objects** treated as a single unit. One entity is the **Aggregate Root** — the only entry point for external modifications.

```swift
// ✅ Aggregate Root — Cart owns its items
struct Cart: Identifiable {
    let id: UUID
    private(set) var items: [CartItem]

    mutating func addItem(_ item: CartItem) {
        // enforce invariants here
        items.append(item)
    }

    mutating func removeItem(id: UUID) {
        items.removeAll { $0.id == id }
    }
}
```

**Rules:**

- External objects may only reference the **aggregate root** by ID.
- All mutations go through the aggregate root's methods.
- The aggregate root is responsible for enforcing **business invariants**.
- Keep aggregates small — include only what is needed to enforce invariants.

---

### Repository

Abstracts **persistence** behind a protocol. Domain code works with the protocol; infrastructure provides the concrete implementation.

```swift
// ✅ Repository protocol lives in the domain layer
protocol OrderRepository {
    func fetchAll() async throws -> [Order]
    func fetch(id: UUID) async throws -> Order?
    func save(_ order: Order) async throws
    func delete(id: UUID) async throws
}

// Concrete implementation lives in the infrastructure/data layer
final class SwiftDataOrderRepository: OrderRepository { ... }
```

**Rules:**

- Repository protocols belong in the **domain layer**.
- Concrete implementations belong in the **infrastructure/data layer**.
- ViewModels inject repositories via constructor injection.
- Never call persistence APIs (SwiftData, CoreData, network) directly from a ViewModel or domain service.

---

### Domain Service

Stateless logic that **doesn't naturally belong to a single entity or value object**.

```swift
// ✅ Domain Service — operates across multiple aggregates
struct PricingService {
    func calculateTotal(for cart: Cart, applying coupon: Coupon?) -> Money {
        // business logic here
    }
}
```

**Rules:**

- Must be **stateless** — no stored properties that change over time.
- Use when an operation spans multiple aggregates or requires coordination.
- Do not put infrastructure concerns (networking, persistence) in a domain service.

---

### Application Service

Orchestrates **use cases** — coordinates domain objects and repositories without containing domain logic itself.

```swift
// ✅ Application Service (ViewModel in MVVM-DDD hybrid)
@MainActor
final class CheckoutViewModel: ObservableObject {
    private let cartRepository: CartRepository
    private let pricingService: PricingService
    private let orderRepository: OrderRepository

    init(cartRepository: CartRepository,
         pricingService: PricingService,
         orderRepository: OrderRepository) {
        self.cartRepository = cartRepository
        self.pricingService = pricingService
        self.orderRepository = orderRepository
    }

    func placeOrder() async { ... }
}
```

**Rules:**

- Contains **no domain logic** — delegates to domain objects and services.
- Handles transaction boundaries and error translation.
- Maps domain objects to view models / DTOs at this layer.

---

### Domain Event

Represents something **significant that happened in the domain**. Used to decouple parts of the system.

```swift
// ✅ Domain Event
struct OrderPlaced {
    let orderId: UUID
    let placedAt: Date
    let total: Money
}
```

**Rules:**

- Named in the **past tense** (something that already happened).
- Immutable value types (`struct`).
- Published/consumed via a domain event bus or Combine publisher — not via direct calls across bounded contexts.

---

## Layer Dependency Rules

```
UI (Views)
    ↓ depends on
Application (ViewModels / Application Services)
    ↓ depends on
Domain (Entities, Value Objects, Aggregates, Domain Services, Repository Protocols)
    ↑ implemented by
Infrastructure (Repositories, Network, Persistence)
```

- **Domain layer has zero external dependencies.**
- **Infrastructure depends on Domain** (implements its protocols).
- **Application depends on Domain** (uses its types and protocols).
- **UI depends on Application** (binds to ViewModels).

---

## Common Mistakes to Avoid

| Mistake                                        | Fix                                                                    |
| ---------------------------------------------- | ---------------------------------------------------------------------- |
| Putting business rules in a ViewModel          | Move rules into an Entity, Aggregate, or Domain Service                |
| Using raw primitives for domain concepts       | Wrap in a Value Object (e.g., `Email`, `Money`, `PhoneNumber`)         |
| Directly calling SwiftData from a ViewModel    | Inject a Repository protocol; implement it in the infrastructure layer |
| Sharing mutable domain objects across contexts | Map to a DTO or raise a Domain Event at the context boundary           |
| Naming types `Manager`, `Helper`, `Handler`    | Use domain vocabulary; name types after what they _are_ in the domain  |
| Fat aggregates with dozens of properties       | Split into smaller aggregates; cross-aggregate access by ID only       |

---

## Quick Checklist Before Committing

- [ ] Every domain concept is modeled as an entity, value object, or aggregate — not a raw primitive or dictionary.
- [ ] Business invariants are enforced inside the aggregate root, not in the ViewModel or View.
- [ ] All persistence access goes through a repository protocol.
- [ ] Domain services are stateless.
- [ ] ViewModels contain no domain logic.
- [ ] All type/method names use the ubiquitous language from the product requirements.
- [ ] Domain events are raised (not direct cross-context calls) when bounded contexts need to communicate.
