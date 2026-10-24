# Manual QA Portfolio — Game QA Case Study

A practical manual QA portfolio based on a **fictional third-person survival game** called **Ashfall Protocol**.

The case study focuses on the **Inventory & Crafting** feature and demonstrates how I approach manual testing beyond simple happy-path test cases: risk analysis, boundaries, exploratory testing, bug reporting, regression scope and release-risk communication.

> All product names, builds, defects and execution results in this repository are synthetic portfolio examples. They do not contain confidential information from any commercial project.

## What This Portfolio Includes

| Document | What it demonstrates |
| --- | --- |
| [Test Plan](TEST_PLAN.md) | Scope, risks, entry/exit criteria, severity model and test strategy |
| [Test Cases](TEST_CASES.md) | 20 functional and boundary-focused manual test cases |
| [Bug Reports](BUG_REPORTS.md) | 5 realistic defects with severity, priority, repro rate and investigation notes |
| [Exploratory Testing](EXPLORATORY_TESTING.md) | 4 charters covering integrity, boundaries, persistence and controller usability |
| [Regression Checklist](REGRESSION_CHECKLIST.md) | Focused post-fix regression around high-risk gameplay flows |
| [Test Summary Report](TEST_SUMMARY_REPORT.md) | Sample execution metrics, risk assessment and release recommendation |

## Test Scenario

**Game:** Ashfall Protocol *(fictional)*  
**Genre:** Third-person survival/action  
**Platform:** PC  
**Feature:** Inventory & Crafting  
**Sample build:** `0.7.3-portfolio`

The player can collect resources, manage a slot-based inventory, stack/split/drop items, craft recipes and save/load their state.

The highest-risk areas are intentionally centred around **item loss, duplication, persistence and blocked progression** rather than cosmetic-only checks.

## Coverage Highlights

The portfolio includes examples of:

- functional testing,
- regression testing,
- exploratory testing,
- boundary and negative testing,
- save/load and persistence checks,
- keyboard/mouse and controller coverage,
- inventory capacity and stack-limit testing,
- item transaction integrity,
- reproducible bug reporting,
- severity vs priority assessment,
- release-risk communication.

## Example QA Reasoning

A normal successful craft is useful coverage, but it is not enough on its own. I also test what happens when:

- inventory is completely full,
- output could fit only by stacking,
- the player has almost enough materials,
- Craft is pressed repeatedly before state refreshes,
- the game is saved or loaded around the transaction,
- input method changes or controller focus is interrupted.

Those transitions are where item duplication, item loss and state inconsistencies are more likely to appear.

## Sample Cycle Outcome

The fictional sample execution contains **20 executed cases: 15 passed and 5 failed**. Two synthetic Critical findings lead to a **Not Ready** recommendation for the sample build until item duplication and save/load rollback risks are resolved.

The goal is not to create a perfect fake product history. It is to show how I structure testing, communicate evidence and prioritise risk.

## Related Portfolio Projects

- [QA Playwright Automation](https://github.com/kamilkownacki/qa-playwright-automation) — Playwright + TypeScript browser automation with smoke/regression coverage and CI.
- [QA Bug Report Assistant](https://github.com/kamilkownacki/qa-bug-report-assistant) — AI-assisted QA tool for turning tester notes into structured Jira-ready reports without inventing missing facts.
