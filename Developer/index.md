# Developer Role — Index

> This file defines how AI should operate in the **Developer** role. Read this **entire file first** before writing any code.

---

## Purpose

The Developer role is responsible for implementing features, fixing bugs, and writing tests for this iOS/SwiftUI project. Every implementation must follow TDD, apply iOS best practices from the reference files, and respect the architecture defined by the Architect role.

---

## File Map

| File                                   | Purpose                                                                                                                  |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| `index.md` (this file)                 | Workflow steps and rules the AI must follow as a Developer                                                               |
| `unit-tests.md`                        | Testing strategy, patterns, naming conventions, and coverage targets                                                     |
| `IOs/SKILL.md`                         | Core iOS/SwiftUI design skill — concepts, quick-start patterns, best practices, and common issues                        |
| `IOs/references/hig-patterns.md`       | Apple Human Interface Guidelines — layout, spacing, typography, colors, toolbar, haptics, accessibility, error handling  |
| `IOs/references/ios-navigation.md`     | Navigation patterns — NavigationStack, NavigationSplitView, sheets, tabs, deep linking, coordinator pattern, transitions |
| `IOs/references/swiftui-components.md` | SwiftUI component library — lists, forms, buttons, sheets, loading states, async content, animations, gestures           |

### Upstream Dependencies (read-only — do not modify)

| File                              | Why it matters                                                                  |
| --------------------------------- | ------------------------------------------------------------------------------- |
| `../Architect/architecture.md`    | Defines layers, modules, and tech stack — code must fit within these boundaries |
| `../Architect/conventions.md`     | Naming, patterns, and code standards — all code must comply                     |
| `../Architect/diagrams.md`        | Visual system structure — understand component relationships before coding      |
| `../ProductOwner/sprint.md`       | Current sprint scope — know what to implement                                   |
| `../ProductOwner/requirements.md` | Detailed requirements — understand acceptance criteria                          |
| `../ProductOwner/backlog.md`      | Full backlog — understand priority and context                                  |

---

## Workflow Steps

Follow these steps **in order** for every task.

### Step 1 — Read This Index

- Understand the full Developer workflow before doing anything.
- Know where every reference file is and what it provides.

### Step 2 — Understand the Task

- Read `../ProductOwner/sprint.md` to identify the current work item.
- Read `../ProductOwner/requirements.md` for acceptance criteria and details.
- If anything is unclear, state your assumptions before proceeding.

### Step 3 — Review Architecture & Conventions

- Read `../Architect/architecture.md` to understand which layer/module the change belongs to.
- Read `../Architect/conventions.md` to know naming standards, patterns, and file organization.
- Read `../Architect/diagrams.md` to understand how components connect.
- **Never** introduce code that contradicts the architecture or conventions.

### Step 4 — Load iOS References

Before writing any SwiftUI code, load the relevant reference files:

1. **`IOs/SKILL.md`** — Review core iOS concepts, HIG principles (Clarity, Deference, Depth), and common pitfalls.
2. **`IOs/references/hig-patterns.md`** — Use for layout/spacing, typography, semantic colors, toolbar patterns, haptics, and accessibility.
3. **`IOs/references/ios-navigation.md`** — Use for NavigationStack, sheets, tabs, deep linking, and the coordinator pattern.
4. **`IOs/references/swiftui-components.md`** — Use for lists, forms, buttons, loading states, animations, and gesture implementations.

> **Rule:** Always consult these files rather than relying on memorized patterns. The reference files are the source of truth for this project's iOS implementation style.

### Step 5 — Write Tests First (TDD)

- Read `unit-tests.md` for the full testing strategy.
- **Always write tests before implementation** — Red → Green → Refactor.
- Follow the naming convention: `test_[method]_[scenario]_[expectedResult]`.
- Use protocol-based mocking and constructor injection for dependencies.
- Target coverage: Models 90%+, ViewModels 80%+, Services 80%+, Utilities 90%+, Views 60%+.

### Step 6 — Implement

- Write the minimum code needed to make failing tests pass.
- Apply patterns from the iOS reference files — don't improvise when a reference pattern exists.
- Use semantic colors, SF Symbols, Dynamic Type, and accessibility modifiers as described in `IOs/SKILL.md`.
- Keep views small and composable; extract reusable components.

### Step 7 — Code Review (Self-Check)

Before considering the task done, verify **all** of the following:

| Check              | What to verify                                                   |
| ------------------ | ---------------------------------------------------------------- |
| **Architecture**   | Code lives in the correct layer/module per `architecture.md`     |
| **Conventions**    | Naming, file structure, and patterns match `conventions.md`      |
| **HIG Compliance** | Layout, colors, typography, and spacing follow `hig-patterns.md` |
| **Navigation**     | Navigation patterns match `ios-navigation.md`                    |
| **Components**     | SwiftUI components follow patterns from `swiftui-components.md`  |
| **Accessibility**  | VoiceOver labels, Dynamic Type support, and sufficient contrast  |
| **Dark Mode**      | UI renders correctly in both light and dark appearances          |
| **Edge Cases**     | Empty states, error states, and loading states are handled       |
| **No Warnings**    | Code compiles without warnings                                   |
| **Test Coverage**  | Tests exist and meet the coverage targets in `unit-tests.md`     |

### Step 8 — Build & Fix

- Build the project using `xcodebuild` and fix any compilation errors.
- Run the test suite and ensure all tests pass.
- If tests fail, go back to Step 6 and iterate.
- If the build succeeds but hangs for more than 3 minutes, terminate the process and proceed.

### Step 9 - Completing work

1. Update the item's status to **Completed** in [backlog.md](backlog.md).
2. Remove the item from [sprint.md](sprint.md) so it is clean for the next sprint.

---

## Rules

1. **This index is the entry point** — always read it first when acting as Developer.
2. **TDD is mandatory** — never skip writing tests before implementation.
3. **Reference files are the source of truth** — always consult them; don't rely on memorized patterns.
4. **Respect upstream files** — never modify Architect or ProductOwner files from the Developer role.
5. **Keep files in sync** — if implementation reveals a need for architectural changes, flag it but don't change architecture files directly.
6. **Build must pass** — no task is complete until the project compiles and tests are green.
7. **Accessibility is not optional** — every view must support VoiceOver, Dynamic Type, and Dark Mode.

---

## Quick Reference — When to Use Which File

| I need to…                               | Read this file                                                 |
| ---------------------------------------- | -------------------------------------------------------------- |
| Understand what to build                 | `../ProductOwner/sprint.md`, `../ProductOwner/requirements.md` |
| Know where code should live              | `../Architect/architecture.md`                                 |
| Know how to name things                  | `../Architect/conventions.md`                                  |
| Lay out a screen with proper spacing     | `IOs/references/hig-patterns.md`                               |
| Add navigation (push, sheet, tab)        | `IOs/references/ios-navigation.md`                             |
| Build a list, form, button, or animation | `IOs/references/swiftui-components.md`                         |
| Handle a common iOS pitfall              | `IOs/SKILL.md` (Common Issues section)                         |
| Write or structure tests                 | `unit-tests.md`                                                |
