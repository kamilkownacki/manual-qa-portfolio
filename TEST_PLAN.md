# Test Plan — Inventory & Crafting

## 1. Purpose

This document presents a **fictional manual QA case study** created for portfolio purposes. The product, build numbers and defects are synthetic and do not represent confidential information from any commercial project.

The case study focuses on the Inventory & Crafting feature of a fictional third-person survival game, **Ashfall Protocol**.

The goal is to demonstrate practical manual QA thinking: risk identification, coverage design, reproducible test cases, exploratory testing, regression scope and defect reporting.

## 2. Test Object

**Game:** Ashfall Protocol (fictional)

**Feature:** Inventory & Crafting

**Sample build:** `0.7.3-portfolio`

**Platform:** PC

**Primary environment:**

- Windows 11 64-bit
- 2560x1440 and 1920x1080
- Keyboard + mouse
- Xbox-compatible controller
- English UI

## 3. Feature Overview

The player can:

- pick up world items,
- store items in a slot-based inventory,
- stack compatible items,
- move items between slots,
- split stacks,
- drop items,
- equip usable items,
- craft recipes from collected resources,
- consume required ingredients,
- receive crafted items,
- save and load inventory state.

The inventory has a fixed slot limit. Some resources are stackable, while weapons and tools occupy individual slots.

## 4. Scope

### In scope

- item pickup,
- inventory capacity,
- stack creation and stack limits,
- drag and drop,
- stack splitting,
- dropping items,
- item quantity updates,
- crafting availability,
- ingredient validation,
- crafting output,
- full-inventory behaviour,
- save/load persistence,
- death/respawn behaviour,
- rapid user input,
- keyboard/mouse and controller navigation,
- basic UI scaling and readability,
- regression of critical inventory flows.

### Out of scope

- multiplayer synchronisation,
- backend services,
- console certification,
- monetisation,
- localisation beyond basic UI layout checks,
- performance profiling outside obvious user-facing stalls,
- accessibility certification.

## 5. Quality Risks

| Risk | Impact | Priority |
| --- | --- | --- |
| Item loss or duplication | Player progression / economy can be corrupted | Critical |
| Save/load inventory mismatch | Persistent progress loss | Critical |
| Crafting consumes wrong quantity | Economy and progression broken | High |
| Full inventory causes crafted item loss | Player loses resources | High |
| Incorrect stack handling | Inventory state becomes inconsistent | High |
| Controller focus becomes trapped | Feature unusable without mouse | High |
| Rapid input creates duplicate actions | Exploitable or state-corrupting behaviour | High |
| UI clips at common resolutions | Reduced usability | Medium |
| Cosmetic slot/highlight issues | Visual quality only | Low |

## 6. Test Approach

Testing combines:

- **scenario-based test cases** for repeatable functional coverage,
- **exploratory charters** for state transitions and unexpected interactions,
- **boundary testing** around capacity and stack limits,
- **negative testing** for missing materials and invalid actions,
- **persistence testing** through save/load,
- **input-method testing** with keyboard/mouse and controller,
- **regression checks** focused on inventory integrity and progression risk.

Critical flows are tested first. Any defect involving item loss, item duplication, save corruption or blocked progression is treated as release-impacting until assessed.

## 7. Entry Criteria

Testing can begin when:

- the build launches reliably,
- inventory can be opened,
- test items and crafting recipes are available,
- save/load is functional,
- the feature is not blocked by a known crash on startup.

## 8. Exit Criteria

The feature is considered ready for this sample test cycle when:

- all P0/P1 test cases are executed,
- no open Critical defects remain,
- High defects are reviewed and accepted or fixed,
- critical regression checklist passes,
- save/load and crafting integrity have been retested after fixes,
- remaining known issues are documented.

## 9. Severity Guide

| Severity | Meaning |
| --- | --- |
| Critical | Crash, save corruption, major item duplication/loss, progression blocker |
| High | Core feature broken or exploitable with no reasonable workaround |
| Medium | Feature partially broken; workaround exists; limited user impact |
| Low | Cosmetic, wording or minor usability issue |

Severity describes product impact. Priority may differ depending on release scope, frequency, affected users and production risk.

## 10. Deliverables

- [Test Cases](TEST_CASES.md)
- [Bug Reports](BUG_REPORTS.md)
- [Exploratory Testing](EXPLORATORY_TESTING.md)
- [Regression Checklist](REGRESSION_CHECKLIST.md)
- [Sample Test Summary](TEST_SUMMARY_REPORT.md)
