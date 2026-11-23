# QA Checklist - fill in while testing in Godot 4.4

**Nothing below has been tested in Godot yet** (the authoring environment had no Godot). `tools/static_check.py` (script/resource references) and `tools/check_levels.py` (all 3 stages are solvable, computed by search) were run and passed. Tick each box only after you try it.

- [ ] Project opens with no errors in the Output panel (first open imports fonts/audio)
- [ ] Main menu shows; PLAY, CONTINUE, STAGE SELECT, HOW TO PLAY, SYSTEM INFO, QUIT work
- [ ] Loading screen shows a progress bar and arrives in the stage
- [ ] WASD/arrows move; SPACE shifts realm; barriers change; blocked shift shows a message
- [ ] Stage 1 caged shard can be collected; all shards collected -> gate opens with E
- [ ] ESC pauses, RESUME, RESTART STAGE, MAIN MENU, SOUND toggle work; R restarts
- [ ] Stage 2 wisps appear only in Shadow realm and send you back to the anchor
- [ ] Stage 3 can be completed and shows the ending screen
- [ ] NEXT STAGE / REPLAY / MAIN MENU / PLAY AGAIN work
- [ ] Save survives closing the game; erasing the save does not crash
- [ ] F3 overlay shows all concepts; F4/F9/F10 work
- [ ] Memory report measured (docs/MEMORY_REPORT.md)
- [ ] Exported .exe runs outside Godot (Project > Export)
