# Product Owner — AI Instructions

> **Role:** The user is acting as the **Product Owner**. This folder contains all the planning and tracking artifacts for the project. AI must read and follow the structure described below to keep every file interconnected and in sync.

---

## 1. Entry Point

This file (`index.md`) is the starting point. Whenever the user works in Product Owner mode, AI must:

1. Read this file first to understand the file structure and rules.
2. Read [context.md](context.md) to understand the project's scope, tech stack, and references to all other files.

---

## 2. File Map & Relationships

```
index.md          ← You are here. Instructions for AI.
   │
   └─► context.md        ← Project context (name, description, tech stack).
          │                  Links to all files below.
          │
          ├─► backlog.md      ← Master table of user stories & incidents.
          │      │                Columns: ID | Type | Name | Status
          │      │                Each ID links to its detail in requirements.md or incidents.md.
          │      │
          │      ├──── requirements.md  ← Detailed description of each user story (US-XXX).
          │      │
          │      └──── incidents.md     ← Detailed description of each incident (I-XXX).
          │
          └─► sprint.md       ← Current sprint work items (pulled from backlog.md by ID).
                                 Columns: ID | Type | Name | Owner | Status
```

---

## 3. File Descriptions

| File                               | Purpose                                                      | Key Fields                                        |
| ---------------------------------- | ------------------------------------------------------------ | ------------------------------------------------- |
| [context.md](context.md)           | Project overview and links to every other file.              | Project Name, Description, Tech Stack, References |
| [requirements.md](requirements.md) | One section per user story with a very detailed description. | ID (`US-XXX`), Name, Description                  |
| [incidents.md](incidents.md)       | One section per incident with a very detailed description.   | ID (`I-XXX`), Name, Description                   |
| [backlog.md](backlog.md)           | Single source of truth for all items and their status.       | ID, Type (`US` / `I`), Name, Status               |
| [sprint.md](sprint.md)             | Items actively being worked on in the current sprint.        | ID, Type, Name, Owner, Status                     |

---

## 4. ID Conventions

| Type       | Prefix | Example            |
| ---------- | ------ | ------------------ |
| User Story | `US-`  | `US-001`, `US-002` |
| Incident   | `I-`   | `I-001`, `I-002`   |

---

## 5. Status Values

### Backlog Status (used in backlog.md)

| Status          | Meaning                                             |
| --------------- | --------------------------------------------------- |
| **Defined**     | Item has been written and is ready to be picked up. |
| **In Progress** | Item is currently being worked on in the sprint.    |
| **Completed**   | Item is finished and accepted.                      |
| **Canceled**    | Item has been dropped and will not be worked on.    |

### Sprint Status (used in sprint.md)

| Status          | Meaning                                                                             |
| --------------- | ----------------------------------------------------------------------------------- |
| **To Do**       | Item is in the sprint but work has not started yet.                                 |
| **In Progress** | Item is actively being worked on.                                                   |
| **Done**        | Item is finished — update backlog to **Completed** and remove the item from sprint. |

---

## 6. Owner Values (used in sprint.md)

The **Owner** field determines which role the AI should adopt when working on a task:

| Owner         | Responsibility                                                                                           |
| ------------- | -------------------------------------------------------------------------------------------------------- |
| **Architect** | System design, data models, project structure decisions.                                                 |
| **Developer** | Implementation, testing (TDD), services, data persistence, views, components, user interaction, styling. |

---

## 7. Workflow Rules

### Adding a new User Story

1. **Read the Architect files first** — review [index.md](../Architect/index.md), to understand the current system design, architecture, diagrams, conventions, patterns, and constraints.
2. Write the detailed requirement in [requirements.md](requirements.md) with the next `US-XXX` ID, ensuring it aligns with the existing architecture.
3. Add a row in [backlog.md](backlog.md) with Status = **Defined**.

### Adding a new Incident

1. **Read the Architect files first** — review [index.md](../Architect/index.md), to understand the affected layers and components.
2. Write the detailed incident in [incidents.md](incidents.md) with the next `I-XXX` ID, referencing the impacted architectural areas.
3. Add a row in [backlog.md](backlog.md) with Status = **Defined**.

### Starting work (Sprint)

1. Move the item's status to **In Progress** in [backlog.md](backlog.md).
2. Add the item to [sprint.md](sprint.md) with its full details, acceptance criteria, and owner.

### Completing work

1. Update the item's status to **Completed** in [backlog.md](backlog.md).
2. Remove the item from [sprint.md](sprint.md) so it is clean for the next sprint.

### Canceling an item

1. Update the item's status to **Canceled** in [backlog.md](backlog.md).
2. Remove it from [sprint.md](sprint.md) if it was there.

---

## 8. AI Responsibilities

- **Always consult the Architect** — before writing any new user story or incident, read the [Architect folder](../Architect/index.md) (`architecture.md`, `conventions.md`, `diagrams.md`) to write requirements that align with the system design.
- **Always** keep all files in sync when making changes (backlog ↔ requirements/incidents ↔ sprint).
- **Never** leave orphan IDs — every ID in the backlog must have a matching entry in requirements.md or incidents.md.
- **Auto-increment** IDs based on the last used ID in the corresponding file.
- When the user says a task is done, **update backlog status** and **clear sprint.md** automatically.
