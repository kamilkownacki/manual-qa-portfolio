# Test Cases — Inventory & Crafting

**Project:** Ashfall Protocol (fictional portfolio case study)  
**Build:** `0.7.3-portfolio`  
**Platform:** PC / Windows 11

Priority scale: **P0** = progression/data integrity, **P1** = core functionality, **P2** = secondary/usability.

---

## TC-INV-001 — Pick up an item into an empty inventory

**Priority:** P1  
**Preconditions:** Inventory has free slots. A Bandage is present in the world.

**Steps:**
1. Approach the Bandage.
2. Use the interaction key.
3. Open inventory.

**Expected Result:** Bandage disappears from the world and appears once in inventory. No other slot changes.

---

## TC-INV-002 — Stack identical resources

**Priority:** P1  
**Preconditions:** Inventory contains 3 Scrap. Scrap stack limit is 10. Another 4 Scrap is available.

**Steps:**
1. Pick up 4 Scrap.
2. Open inventory.

**Expected Result:** Existing Scrap stack increases from 3 to 7. No additional Scrap stack is created.

---

## TC-INV-003 — Respect stack limit

**Priority:** P1  
**Preconditions:** Inventory contains 8 Scrap. Scrap stack limit is 10. Another 5 Scrap is available. At least one free slot exists.

**Steps:**
1. Pick up 5 Scrap.
2. Open inventory.

**Expected Result:** First stack becomes 10 and a second stack with 3 Scrap is created. Total quantity equals 13.

---

## TC-INV-004 — Reject pickup when inventory is full

**Priority:** P0  
**Preconditions:** Every inventory slot is occupied. A non-stackable Rifle is present in the world.

**Steps:**
1. Attempt to pick up the Rifle.

**Expected Result:** Rifle remains in the world. Player receives clear inventory-full feedback. No item is deleted or replaced.

---

## TC-INV-005 — Fill an existing stack while inventory slots are full

**Priority:** P0  
**Preconditions:** All slots are occupied. One stack contains 7/10 Scrap. 2 Scrap is available in the world.

**Steps:**
1. Pick up 2 Scrap.

**Expected Result:** Pickup succeeds because the existing stack has capacity. Stack becomes 9/10. No item is lost.

---

## TC-INV-006 — Move item between inventory slots

**Priority:** P1  
**Preconditions:** Inventory contains a Medkit in slot 2 and slot 6 is empty.

**Steps:**
1. Drag Medkit from slot 2 to slot 6.

**Expected Result:** Medkit appears in slot 6 and slot 2 becomes empty. Quantity and item state are unchanged.

---

## TC-INV-007 — Swap two occupied slots

**Priority:** P1  
**Preconditions:** Slot 1 contains a Knife. Slot 2 contains a Medkit.

**Steps:**
1. Drag Knife from slot 1 onto slot 2.

**Expected Result:** Knife and Medkit swap slots. Neither item is duplicated, deleted or unequipped unexpectedly.

---

## TC-INV-008 — Split a valid stack

**Priority:** P1  
**Preconditions:** Inventory contains 8 Scrap and at least one empty slot.

**Steps:**
1. Select Split Stack.
2. Split 3 Scrap into a new stack.

**Expected Result:** Original stack becomes 5 and a new stack of 3 is created. Total remains 8.

---

## TC-INV-009 — Prevent invalid stack split

**Priority:** P1  
**Preconditions:** Inventory contains a stack of 5 Scrap.

**Steps:**
1. Open Split Stack.
2. Attempt to enter 0.
3. Attempt to enter 5 or more.

**Expected Result:** Invalid values cannot create a new stack. Inventory quantity remains 5.

---

## TC-INV-010 — Drop part of a stack

**Priority:** P1  
**Preconditions:** Inventory contains 6 Scrap.

**Steps:**
1. Drop 2 Scrap.
2. Close inventory.
3. Inspect the ground near the player.

**Expected Result:** Inventory contains 4 Scrap. A world pickup containing exactly 2 Scrap appears at a valid location.

---

## TC-INV-011 — Save and load inventory state

**Priority:** P0  
**Preconditions:** Inventory contains 4 Scrap, 2 Bandages and one Knife in known slots.

**Steps:**
1. Create a manual save.
2. Change inventory contents by dropping the Knife and using one Bandage.
3. Load the save.

**Expected Result:** Inventory returns exactly to the saved state: quantities, items and slot positions match the save point.

---

## TC-INV-012 — Inventory state after player death

**Priority:** P0  
**Preconditions:** Player carries several resources and one equipped tool. Game design specifies which items are retained after death.

**Steps:**
1. Record inventory contents.
2. Trigger player death.
3. Respawn.
4. Compare inventory to the design rule.

**Expected Result:** Only intended items are retained/lost. No additional items disappear or duplicate.

---

## TC-CRAFT-001 — Craft recipe with exact required materials

**Priority:** P0  
**Preconditions:** Recipe requires 2 Cloth + 1 Alcohol. Player has exactly 2 Cloth + 1 Alcohol and one free slot.

**Steps:**
1. Open Crafting.
2. Select Medkit.
3. Craft once.

**Expected Result:** Required materials are consumed once and one Medkit is added. Ingredient quantities reach zero.

---

## TC-CRAFT-002 — Prevent crafting with missing materials

**Priority:** P1  
**Preconditions:** Recipe requires 2 Cloth + 1 Alcohol. Player has 2 Cloth and 0 Alcohol.

**Steps:**
1. Select Medkit recipe.
2. Attempt to craft.

**Expected Result:** Craft action is unavailable or rejected with clear feedback. Cloth is not consumed and no Medkit is created.

---

## TC-CRAFT-003 — Craft multiple items sequentially

**Priority:** P1  
**Preconditions:** Player has materials for 3 Bandages and sufficient inventory space.

**Steps:**
1. Craft Bandage three times.
2. Inspect inventory after each craft.

**Expected Result:** Exactly three Bandages are created. Materials decrease by the correct amount after each action.

---

## TC-CRAFT-004 — Craft when inventory has no free slots but output can stack

**Priority:** P0  
**Preconditions:** Inventory is full. Existing Bandage stack is 3/5. Player has ingredients for one Bandage.

**Steps:**
1. Craft one Bandage.

**Expected Result:** Craft succeeds and Bandage stack becomes 4/5. Ingredients are consumed exactly once.

---

## TC-CRAFT-005 — Handle crafting when output cannot fit

**Priority:** P0  
**Preconditions:** Inventory is full. Recipe output is a non-stackable Tool. Required ingredients are present.

**Steps:**
1. Attempt to craft the Tool.

**Expected Result:** Crafting is blocked before ingredients are consumed, or output is handled according to design without item loss. The player never loses ingredients without receiving the crafted item.

---

## TC-CRAFT-006 — Rapid repeated craft input

**Priority:** P0  
**Preconditions:** Player has materials for exactly one Tool.

**Steps:**
1. Select the Tool recipe.
2. Rapidly press the Craft action multiple times.

**Expected Result:** Only one Tool is created and ingredients are consumed once. No duplication or negative quantities occur.

---

## TC-INPUT-001 — Navigate inventory using controller only

**Priority:** P1  
**Preconditions:** Xbox-compatible controller connected. Inventory contains several items.

**Steps:**
1. Open inventory with controller.
2. Navigate through every slot and action.
3. Move an item.
4. Close inventory.

**Expected Result:** Focus remains visible and predictable. All required actions are reachable without mouse input. No focus trap occurs.

---

## TC-UI-001 — Inventory at common desktop resolutions

**Priority:** P2  
**Preconditions:** Game available at 1920x1080 and 2560x1440.

**Steps:**
1. Open inventory at 1920x1080.
2. Inspect labels, quantities, tooltips and action prompts.
3. Repeat at 2560x1440.

**Expected Result:** UI remains readable and within screen bounds. No clipped quantities, overlapping text or inaccessible controls.

---

## Coverage Notes

The cases above intentionally prioritise **inventory integrity and progression risk** over exhaustive UI permutations. Additional coverage is handled through exploratory charters and the regression checklist.
