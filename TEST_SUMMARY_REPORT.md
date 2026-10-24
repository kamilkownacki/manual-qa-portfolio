# Sample Test Summary Report

> **Portfolio note:** This is a fictional execution summary for the synthetic Ashfall Protocol case study. Results and defects are examples created to demonstrate QA reporting and release-risk communication.

## Test Cycle

**Feature:** Inventory & Crafting  
**Build:** `0.7.3-portfolio`  
**Platform:** PC / Windows 11  
**Primary input:** Keyboard + mouse; controller coverage included  
**Scope:** Functional manual testing + focused exploratory testing

## Execution Summary

| Metric | Result |
| --- | ---: |
| Planned test cases | 20 |
| Executed | 20 |
| Passed | 15 |
| Failed | 5 |
| Blocked | 0 |
| Pass rate | 75% |

## Defect Summary

| Severity | Open defects |
| --- | ---: |
| Critical | 2 |
| High | 2 |
| Medium | 0 |
| Low | 1 |

### Key Findings

- **BUG-002 — Critical:** rapid controller input can duplicate a crafted tool while consuming materials only once.
- **BUG-003 — Critical:** loaded inventory can intermittently restore an older state instead of the saved state.
- **BUG-001 — High:** crafting a non-stackable item with full inventory can consume ingredients without delivering output.
- **BUG-004 — High:** controller navigation can become trapped after cancelling Split Stack.
- **BUG-005 — Low:** quantity text overlaps item artwork at 1920x1080 with 125% UI scale.

See [BUG_REPORTS.md](BUG_REPORTS.md) for full reproduction details.

## Areas That Passed

The sample cycle confirmed expected behaviour for:

- normal item pickup,
- stack creation and overflow,
- stackable pickup with full inventory slots,
- moving and swapping items,
- valid and invalid stack splitting,
- partial stack dropping,
- crafting with exact materials,
- preventing craft with missing ingredients,
- sequential crafting under normal input,
- stackable craft output with full slots,
- baseline inventory rendering at standard UI scale.

## Exploratory Testing Notes

Exploratory coverage focused on:

- rapid inventory state changes,
- full-inventory boundaries,
- save/load persistence,
- controller-only navigation.

The highest-risk findings came from **state transition and boundary testing**, rather than the happy path. This reinforces the need to test transaction integrity around crafting, persistence and full-capacity inventory states.

## Risk Assessment

### Release-impacting risks

1. **Item duplication** can damage game economy and progression balance.
2. **Inventory rollback after load** risks loss of player progress and trust.
3. **Ingredient loss during full-inventory crafting** can create unrecoverable player loss.
4. **Controller focus trap** blocks a core feature for controller-only players until input method is changed.

### Lower-risk issue

The UI-scale overlap is visible and should be corrected, but it does not block core gameplay.

## Recommendation

**Sample QA recommendation: NOT READY for release candidate approval.**

The build should not pass this feature gate while the two Critical defects remain open. BUG-001 should also be resolved before release because it causes deterministic resource loss.

Recommended next steps:

1. Fix BUG-002 and BUG-003 first.
2. Verify each fix on the original reproduction path.
3. Run nearby transaction/persistence scenarios, not only the exact steps.
4. Fix and retest BUG-001.
5. Run the focused [Regression Checklist](REGRESSION_CHECKLIST.md).
6. Reassess controller-only usability after BUG-004.
7. Track BUG-005 separately if schedule requires lower-risk visual issues to be deferred.

## Retest Template

For a follow-up build, record:

| Defect | Fix build | Original repro result | Nearby regression | Status |
| --- | --- | --- | --- | --- |
| BUG-001 | — | — | — | Open |
| BUG-002 | — | — | — | Open |
| BUG-003 | — | — | — | Open |
| BUG-004 | — | — | — | Open |
| BUG-005 | — | — | — | Open |
