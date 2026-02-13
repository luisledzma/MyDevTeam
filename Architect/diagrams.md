# Diagrams

> Visual / text-based diagrams describing the system structure and flows.
> Referenced by [architecture.md](architecture.md).

---

## System Overview Diagram

```
┌────────────────────────────────────────────┐
│             [Your System Name]             │
│                                            │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐     │
│  │ Module 1 │ │ Module 2 │ │ Module 3 │     │
│  └────┬────┘ └────┬────┘ └────┬────┘     │
│       │          │          │            │
│       └──────────┬──────────┘            │
│                  │                       │
│       ┌──────────┴─────────┐             │
│       │ Shared / Common   │             │
│       └──────────┬─────────┘             │
│                  │                       │
│       [External Systems / Services]     │
└─────────────────┬──────────────────────────┘
                  │
        ┌─────────┴────────┐
        │ [Persistence /  │
        │   Database]     │
        └─────────────────┘
```

---

## Layer Diagram

```
┌──────────────────────────────────────────────────┐
│            [Presentation Layer]                   │
│  (UI, Views, Controllers, Presenters, etc.)     │
├──────────────────────────────────────────────────┤
│            [Business Logic Layer]                 │
│  (Services, Use Cases, Domain Logic, etc.)      │
├──────────────────────────────────────────────────┤
│            [Data Layer]                           │
│  (Repositories, Data Sources, Models, etc.)     │
├──────────────────────────────────────────────────┤
│         [Platform / Frameworks]                   │
│  (Operating System, Libraries, APIs, etc.)      │
└──────────────────────────────────────────────────┘
```

---

## Component / Module Diagram

```
┌─────────── [Component/Module Name] ─────────────┐
│                                                 │
│  ┌─────────────┐    ┌──────────────────┐       │
│  │ [SubComp A] │───▶│  [SubComp B]     │       │
│  │             │◀───│                  │       │
│  └─────────────┘    └───────┬──────────┘       │
│                             │                   │
│                     ┌───────▼────────┐          │
│                     │  [Data/Model]  │          │
│                     └────────────────┘          │
│                                                 │
│  [Brief description of data/control flow]       │
└─────────────────────────────────────────────────┘
```

---

## Data Flow Diagram

```
┌──────────┐         ┌──────────────┐         ┌──────────┐
│  [User/  │  input  │ [Component]  │  data   │ [Data]  │
│  Client] │ ──────▶│ [Logic/      │ ─────▶│ [Store] │
│          │◀──────│  Controller] │◀─────│         │
└──────────┘ output └──────────────┘  data   └──────────┘
```

---

## Folder Structure Diagram

```
[YourProjectName]/
├── [Directory 1]/
│   └── [File or Subdirectory]
├── [Directory 2]/
│   ├── [Subdirectory A]/
│   │   ├── [Files...]
│   │   └── [Files...]
│   └── [Subdirectory B]/
│       ├── [Files...]
│       └── [Files...]
├── [Shared or Common]/
│   ├── [Models or Entities]/
│   ├── [Services or Utils]/
│   └── [Components or Helpers]/
└── [Assets or Resources]/
```

---

## Navigation / Flow Diagram

```
         ┌──────────────────────────┐
         │   [Entry Point/Home]     │
         └───────────┬──────────────┘
                     │
        ┌────────────┴────────────┐
        │                         │
   ┌────┴────┐    ┌────┴────┐    […]
   │ Screen  │    │ Screen  │
   │   A     │    │   B     │
   └─────────┘    └─────────┘
```

---

## State Diagram (Optional)

```
        ┌─────────┐
        │ [State1]│
        └────┬────┘
  [event]   │
        ┌────┴────┐
   ┌───▶│ [State2]│──── [event] ────┐
   │    └────┬────┘                 │
   │ [event] │        [event]       │
   │    ┌────┴────┐                 │
   │    │ [State3]│                 │
   │    └────┬────┘                 │
   │ [event] │                      │
   └─────────┘                      ▼
                   ┌─────────────────────┐
        [reset]    │  [Final State]      │
   [State1] ◀──────┴────────┬────────────┘
                            │
                            ▼
```
