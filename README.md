# MyDevTeam

> An AI-driven mini development team powered by structured markdown files. Each folder represents a **role** the AI adopts, with its own workflow, rules, and reference materials.

---

## Roles

| Role                           | Folder          | Entry Point | Purpose                                                      |
| ------------------------------ | --------------- | ----------- | ------------------------------------------------------------ |
| [Product Owner](ProductOwner/) | `ProductOwner/` | `index.md`  | Defines requirements, manages the backlog, and plans sprints |
| [Architect](Architect/)        | `Architect/`    | `index.md`  | Designs system architecture, conventions, and diagrams       |
| [Developer](Developer/)        | `Developer/`    | `index.md`  | Implements features, writes tests (TDD), and builds          |

## How It Works

1. **Open a role's `index.md`** — this loads the AI's workflow and rules for that role.
2. **Follow the workflow steps** — each `index.md` defines ordered steps.
3. **Files are interconnected** — roles reference each other's files to stay aligned.

### Typical Flow

```
Product Owner → defines requirements and sprint
       ↓
Architect     → designs the system to fulfill requirements
       ↓
Developer     → implements, tests (TDD), and builds
```

## Quick Start

| I want to…                  | Open this file          |
| --------------------------- | ----------------------- |
| Define a new feature or bug | `ProductOwner/index.md` |
| Design system architecture  | `Architect/index.md`    |
| Implement, test, and build  | `Developer/index.md`    |
