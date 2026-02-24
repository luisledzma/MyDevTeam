# Architect Role — Index

> This file defines how AI should operate in the **Architect** role. Read this first before touching any code.

---

## Purpose

The Architect role is responsible for defining and maintaining the system's high-level design, enforcing coding conventions, and keeping diagrams up to date. All architectural decisions flow through the files listed below.

---

## File Map

| File                   | Purpose                                                                        |
| ---------------------- | ------------------------------------------------------------------------------ |
| `index.md` (this file) | Steps and workflow the AI must follow as an Architect                          |
| `architecture.md`      | System architecture, layers, modules, and references to conventions & diagrams |
| `conventions.md`       | Code conventions, naming standards, patterns, and best practices               |
| `diagrams.md`          | Visual / text-based diagrams that describe the system structure and flows      |

---

## Workflow Steps

### Step 1 — Read the Index

- Always start here.
- Understand how all Architect files relate to each other before making changes.

### Step 2 — Review Architecture

- Open `architecture.md`.
- Understand the current system layers, modules, and dependencies.
- `architecture.md` references both `conventions.md` and `diagrams.md` — follow those references as needed.

### Step 3 — Follow Conventions

- Open `conventions.md`.
- Apply all listed conventions when writing or reviewing code.
- Propose updates to conventions when new patterns emerge.

### Step 4 — Consult Diagrams

- Open `diagrams.md`.
- Use diagrams to understand component relationships and data flows.
- Update diagrams whenever the architecture changes.

### Step 5 — Make Changes

- When modifying architecture, update **all three files** (`architecture.md`, `conventions.md`, `diagrams.md`) to stay in sync.
- Never change the system design without updating the corresponding diagram.
- Never introduce a pattern that contradicts `conventions.md`.
- If the project uses **Domain-Driven Design (DDD)**, define bounded contexts, aggregates, and ubiquitous language in `architecture.md` — the Developer role depends on these definitions.

---

## Rules

1. **index.md** is the entry point — always read it first.
2. All architectural decisions must be documented in **architecture.md**.
3. All code standards must live in **conventions.md**.
4. All visual representations must live in **diagrams.md**.
5. Keep the three files consistent with each other at all times.

---

## Downstream Dependents

These roles read Architect files and depend on them being accurate and up to date:

| Consumer          | Files they read                                    | Why                                                       |
| ----------------- | -------------------------------------------------- | --------------------------------------------------------- |
| **Product Owner** | `architecture.md`, `conventions.md`, `diagrams.md` | Writes requirements that align with the system design     |
| **Developer**     | `architecture.md`, `conventions.md`, `diagrams.md` | Implements code within the defined layers and conventions |

> **Impact:** Any change to architecture, conventions, or diagrams affects how requirements are written and how code is implemented. Always keep these files accurate.
