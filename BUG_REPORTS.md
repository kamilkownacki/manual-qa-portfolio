# Sample Bug Reports

All defects below are **fictional portfolio examples** based on the synthetic Ashfall Protocol case study. They are written to demonstrate bug-reporting structure and QA reasoning, not to claim findings from a real commercial product.

---

## BUG-001 — Crafted tool is lost while ingredients are consumed when inventory is full

**Severity:** High  
**Priority:** P1  
**Reproduction Rate:** 5/5  
**Build:** `0.7.3-portfolio`  
**Platform:** PC / Windows 11  
**Input:** Keyboard + mouse

### Preconditions

- Inventory is full.
- Player has the required materials for a non-stackable Improvised Axe.
- No existing slot can accept the crafted output.

### Steps to Reproduce

1. Open Crafting.
2. Select Improvised Axe.
3. Press Craft.
4. Open Inventory.

### Actual Result

Required materials are removed, but no Improvised Axe is added to inventory or spawned nearby.

### Expected Result

Crafting should be blocked before ingredients are consumed when the output cannot fit, or the crafted item should be delivered through an intentional fallback defined by design.

### Notes

Potential player progression/economy loss. Retest should include full inventory with stackable and non-stackable outputs.

---

## BUG-002 — Rapid Craft input creates two tools from materials for one

**Severity:** Critical  
**Priority:** P0  
**Reproduction Rate:** 3/5  
**Build:** `0.7.3-portfolio`  
**Platform:** PC / Windows 11  
**Input:** Xbox-compatible controller

### Preconditions

- Player has materials for exactly one Improvised Axe.
- At least two inventory slots are free.

### Steps to Reproduce

1. Open Crafting using the controller.
2. Highlight Improvised Axe.
3. Press the Craft button rapidly several times.
4. Open Inventory.

### Actual Result

Two Improvised Axes can be added while ingredients are consumed only once.

### Expected Result

Only one craft transaction should complete when the player has materials for one item.

### Notes

Economy/exploit risk. Investigate whether input is accepted before inventory/material state refresh completes. Also test keyboard input, low frame rate and other recipes.

---

## BUG-003 — Inventory state can revert after loading a manual save

**Severity:** Critical  
**Priority:** P0  
**Reproduction Rate:** 2/5  
**Build:** `0.7.3-portfolio`  
**Platform:** PC / Windows 11  
**Input:** Keyboard + mouse

### Preconditions

- Inventory contains multiple stacks and at least one moved item.
- Manual saving is available.

### Steps to Reproduce

1. Move Knife from slot 2 to slot 7.
2. Pick up 4 Scrap, resulting in a known quantity.
3. Create a manual save.
4. Drop the Knife and consume one resource.
5. Load the manual save.
6. Open Inventory.

### Actual Result

On affected attempts, item quantities match an earlier state and the Knife returns to its previous slot instead of the saved slot.

### Expected Result

Inventory contents, quantities and slot positions should match the exact state stored in the loaded save.

### Notes

Intermittent data-integrity issue. Capture save timestamp, slot state and logs when available. Retest after clean launch and across multiple save slots.

---

## BUG-004 — Controller focus becomes trapped after closing Split Stack dialog

**Severity:** High  
**Priority:** P1  
**Reproduction Rate:** 5/5  
**Build:** `0.7.3-portfolio`  
**Platform:** PC / Windows 11  
**Input:** Xbox-compatible controller

### Preconditions

- Inventory contains a stack of at least 2 Scrap.
- Controller is active input device.

### Steps to Reproduce

1. Open Inventory with controller.
2. Select Scrap.
3. Open Split Stack.
4. Cancel the dialog.
5. Attempt to move focus to another inventory slot.

### Actual Result

Focus remains on the previously selected slot and directional input no longer changes the selected slot. Mouse input restores navigation.

### Expected Result

After cancelling Split Stack, focus should return to the source slot and normal controller navigation should continue.

### Notes

Feature remains usable with mouse, but controller-only players cannot continue without changing input method.

---

## BUG-005 — Item quantity text overlaps slot icon at 1920x1080 with 125% UI scale

**Severity:** Low  
**Priority:** P2  
**Reproduction Rate:** 5/5  
**Build:** `0.7.3-portfolio`  
**Platform:** PC / Windows 11  
**Resolution:** 1920x1080  
**UI Scale:** 125%

### Preconditions

- Inventory contains a stack with a two-digit quantity.

### Steps to Reproduce

1. Set resolution to 1920x1080.
2. Set UI scale to 125%.
3. Open Inventory.
4. Inspect a stack with quantity 10 or higher.

### Actual Result

Quantity text overlaps the lower-right part of the item icon and becomes harder to read.

### Expected Result

Quantity text should remain readable without overlapping important item artwork or clipping outside the slot.

### Notes

Cosmetic/usability issue. Verify additional UI scales and ultrawide layouts before fixing assumptions are made.

---

## Bug Report Checklist Used

Before submitting a defect, verify that the report contains:

- a concise, searchable title,
- tested build and platform,
- reproduction rate when known,
- required preconditions,
- minimal reproducible steps,
- observed result,
- expected result based on design or reasonable product behaviour,
- severity based on user/product impact,
- notes for useful follow-up investigation,
- evidence such as video, screenshot, save or logs when available.
