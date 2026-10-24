# Exploratory Testing Charters

These charters complement the scripted test cases by targeting state transitions, misuse and risks that are easy to miss in a fixed checklist.

**Project:** Ashfall Protocol (fictional portfolio case study)  
**Feature:** Inventory & Crafting  
**Build:** `0.7.3-portfolio`

---

## Charter 1 — Inventory integrity under rapid state changes

**Mission:** Explore whether rapid actions can cause item duplication, loss, invalid quantities or UI/game-state desynchronisation.

**Timebox:** 45 minutes

**Areas to explore:**

- pick up items while opening/closing inventory,
- move the same item repeatedly between slots,
- split and immediately recombine stacks,
- drop items while changing selection,
- alternate mouse and controller input,
- spam pickup/drop/craft actions,
- repeat actions at low frame rate if available,
- interact near the inventory capacity limit.

**Oracles:**

- total item quantity should remain explainable,
- no negative or impossible quantities,
- one player action should not create multiple unintended transactions,
- UI state should match actual inventory state.

**Evidence to collect:** video for intermittent issues, before/after inventory screenshots, exact quantity calculations, input method and reproduction frequency.

---

## Charter 2 — Full inventory and boundary behaviour

**Mission:** Explore every important action when inventory is one slot below full, exactly full, or able to accept only partial stack quantities.

**Timebox:** 40 minutes

**Areas to explore:**

- pick up stackable and non-stackable items,
- fill an existing partial stack,
- pick up more than remaining stack capacity,
- craft stackable output,
- craft non-stackable output,
- split stacks with no empty slot,
- drop and immediately repick an item,
- receive an item from a scripted reward if available.

**Questions:**

- Is the action blocked before destructive changes occur?
- Does feedback explain why an action failed?
- Can any item disappear because no destination slot exists?
- Are partial pickups handled consistently?

---

## Charter 3 — Save/load and persistence

**Mission:** Explore whether inventory, crafting resources and slot state survive persistence boundaries correctly.

**Timebox:** 60 minutes

**Areas to explore:**

- save with multiple stacks and moved items,
- save immediately after pickup,
- save immediately after craft,
- save after stack split,
- load after changing inventory substantially,
- use several save slots,
- load after returning to main menu,
- load after restarting the game,
- compare slot positions, quantities and equipped state.

**High-risk failures:**

- item duplication,
- item loss,
- quantities from an older save state,
- equipped item not matching inventory,
- saved inventory differing after repeated load cycles.

---

## Charter 4 — Controller-only usability

**Mission:** Complete the full inventory/crafting loop without touching mouse or keyboard.

**Timebox:** 30 minutes

**Flow:**

1. Pick up resources.
2. Open inventory.
3. Move and split a stack.
4. Open crafting.
5. Craft an item.
6. Equip or select the crafted item.
7. Close and reopen menus.

**Explore:**

- focus order,
- modal open/cancel/confirm behaviour,
- wraparound navigation,
- focus after an item disappears,
- focus after crafting changes available recipes,
- switching tabs rapidly,
- disconnect/reconnect controller if supported.

**Oracle:** Every required action should be reachable and current focus should always be visible. A controller user should not need a mouse to recover from normal interactions.

---

## Session Note Template

Use this lightweight format during exploratory work:

```text
Charter:
Build / environment:
Start time / duration:
Data/setup:

Coverage:
- 

Interesting observations:
- 

Defects / questions:
- 

Follow-up ideas:
- 
```

## Example Session Notes — Charter 2

**Duration:** 35 minutes  
**Setup:** Inventory alternated between 15/16 and 16/16 occupied slots; Scrap stack limits exercised around 9/10 and 10/10.

**Coverage:**

- stackable pickup with full slots,
- non-stackable pickup with full slots,
- craft output that can stack,
- craft output requiring a free slot,
- split stack with no free slot.

**Observations:**

- Stackable pickup correctly used remaining space in an existing stack.
- Non-stackable world pickup stayed in the world and displayed full-inventory feedback.
- Stackable craft output fitted an existing stack.
- Non-stackable craft output exposed a high-impact item-loss scenario documented as BUG-001.

**Follow-up:**

- repeat full-inventory craft checks for every recipe output category,
- verify behaviour after save/load while inventory is exactly full,
- check reward/quest items separately because they may use a different delivery path.
