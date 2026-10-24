# Regression Checklist — Inventory & Crafting

Use this checklist after fixes affecting inventory, crafting, save/load, item transactions or UI input handling.

The checklist is intentionally shorter than the full test suite. It targets high-risk flows that should remain stable after changes.

## Build / Environment

- [ ] Correct build installed
- [ ] Clean launch completed
- [ ] Test save/data prepared
- [ ] Keyboard + mouse available
- [ ] Controller available when input-related changes are included

## Inventory — Critical Flow

- [ ] Pick up a non-stackable item into a free slot
- [ ] Pick up a stackable resource into an existing stack
- [ ] Exceed stack limit and verify overflow creates the correct additional stack
- [ ] Pick up stackable resource while all slots are full but existing stack has capacity
- [ ] Reject non-stackable pickup when inventory is full without deleting the world item
- [ ] Move an item to an empty slot
- [ ] Swap two occupied slots
- [ ] Split a stack and verify total quantity is unchanged
- [ ] Drop part of a stack and verify world/inventory quantities match

## Crafting — Critical Flow

- [ ] Craft with exact required ingredients
- [ ] Reject craft with one ingredient missing
- [ ] Craft multiple items sequentially and verify each material deduction
- [ ] Craft stackable output into an existing stack while inventory slots are full
- [ ] Reject or safely handle non-stackable output when inventory is full
- [ ] Rapidly repeat Craft input and verify no duplicate output or negative quantities

## Persistence

- [ ] Save with known item quantities and slot positions
- [ ] Change inventory after saving
- [ ] Load save and verify exact saved state is restored
- [ ] Repeat load once more to check for state drift
- [ ] Restart game and load the same save if the change may affect persistence

## Input / UI

- [ ] Open, navigate and close inventory with keyboard + mouse
- [ ] Open, navigate and close inventory using controller only
- [ ] Open and cancel Split Stack dialog; verify focus recovers
- [ ] Craft using controller and verify focus remains usable after inventory changes
- [ ] Check quantities/tooltips at 1920x1080

## Fix Verification

For each fixed defect:

- [ ] Reproduce on the original affected build if available
- [ ] Confirm the same steps no longer reproduce on the fix build
- [ ] Test one or more nearby scenarios, not only the exact reported path
- [ ] Confirm no new item loss, duplication or state mismatch
- [ ] Record build, result and evidence

## Stop / Escalation Conditions

Pause normal regression and escalate if any of the following occurs:

- item duplication,
- persistent item loss,
- save corruption or inventory rollback,
- crash in a core inventory/crafting flow,
- progression blocker,
- fix introduces a new Critical/High defect in the same system.
