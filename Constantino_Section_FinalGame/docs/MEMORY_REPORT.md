# Memory Management Report - Measurement Worksheet

**Instructor method:** run the game for **2 minutes** without freeing, record Debugger > Monitors values; run **2 minutes** with cleanup and record again.

**Status: NOT MEASURED YET.** The game was written in an environment without Godot, so no numbers exist. **Fill in the table yourself - do not invent numbers.**

## How the "before" and "after" runs work in this project
`GameState.dispose()` frees every temporary object. Pressing **F4** in game switches cleanup OFF, which reproduces the classic leaks:
- player echo trail + burst effects are removed from the tree but never freed -> **Orphan Nodes** grow
- wisps are left hidden in the tree -> **Nodes** grow
Pressing **F10** makes the player walk automatically so both runs are identical.

## Procedure (do it twice)
1. Open the project in Godot 4.4, press **F5** (run). Start **Stage 2** (STAGE SELECT after clearing Stage 1, or PLAY then clear Stage 1).
2. **Before run:** press **F4** (overlay F3 shows "cleanup: OFF - leaking!"), press **F10** (auto-walk). In Godot's bottom panel open **Debugger > Monitors**, tick *Object > Nodes*, *Object > Orphan Nodes*, *Memory > Static*. Optionally press **F9** to record rows into `user://memory_log.csv`.
3. Wait **2 minutes**, take a screenshot of the Monitors, record the three values below. Close the game.
4. **After run:** run again, leave cleanup **ON** (default), press **F10**, wait 2 minutes, screenshot, record.

| Measurement after 2 minutes | Before cleanup (F4 = OFF) | After cleanup (default) |
|---|---:|---:|
| Object > Nodes | ______ | ______ |
| Object > Orphan Nodes | ______ | ______ |
| Memory > Static | ______ | ______ |

## What to expect (a prediction, not a result)
With cleanup OFF the orphan count and node count should climb steadily (the echo trail alone creates about 14 objects per second while moving). With cleanup ON the counts should stay roughly flat. Static memory may fluctuate because of engine caches, so describe what you actually observe.

## Why it matters
Objects that are never freed keep using memory and, if still in the tree, keep running `_process()` every frame. Over a long session this causes growing memory use, slowdowns and eventually crashes - a memory leak.

Note: orphan counts and static memory are only reported in the editor / debug builds (the overlay shows "n/a" in release exports).
