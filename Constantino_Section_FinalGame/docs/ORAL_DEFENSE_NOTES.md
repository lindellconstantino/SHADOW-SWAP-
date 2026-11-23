# Oral Defense - simple explanations

- **Processes and Programs:** A `.tscn` scene is like a program file. `instantiate()` makes a new running copy, like launching a process. I do it for the player, shards, wisps, effects. (`level.gd: _spawn_shards`)
- **CPU Scheduling:** The engine schedules my code. `_physics_process` runs at a fixed 60/s (movement); `_process` runs every drawn frame (animation). `delta` is the time since the last call so speed is the same on slow and fast computers.
- **Interrupts:** A signal is a software interrupt: something happens (shard touched) and the connected function runs automatically. Custom signals: `collected`, `realm_changed`, `touched_player`... connected with `.connect()` in `level.gd`.
- **I/O Management:** Polling = ask the keyboard every tick (`Input.get_vector`, movement). Event-driven = the OS tells me when a key is pressed (`_unhandled_input`, SPACE/E/ESC).
- **Memory Management:** Objects I create must be freed. `queue_free()` via `GameState.dispose()`. Sound effects use a pool of 8 players re-used instead of creating new ones. F4 turns cleanup off to show the leak; compare in Debugger > Monitors.
- **File Systems:** `user://` is a folder the OS gives the game for saving. I save JSON and validate it when loading, so missing/corrupt files give defaults instead of a crash.
- **Threads:** The loading screen asks Godot to load the next stage on another thread (`load_threaded_request`) so the screen stays responsive; I poll the status in `_process` and switch scene when it is LOADED.
- **OS as a Platform:** The game asks the OS for its name, folders and can open the file explorer. Exporting packages the game as a standalone program for the OS.

**Be honest in the defense:** say which parts you tested in Godot (see QA_CHECKLIST).
