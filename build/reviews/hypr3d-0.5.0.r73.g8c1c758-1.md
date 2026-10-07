# hypr3d 0.5.0.r73.g8c1c758-1, x86_64

- What it is: 0.5.0.r71.g371300b-1 (see hypr3d-0.5.0.r71.g371300b-1.md and
  the reviews it names) plus two commits on the fork's branch larch/main:
  AfrobamaYT/Hypr3D `9f3fc76` and `8c1c758ad51611c97575e32782abc629de6d15f7`.
  The GitHub archive of 8c1c758 has SHA-256
  `7cf9c1dac722d6629507e0375d769dab5c4305bc74fb1782ab873f6fc4400c74`
  ("Passed" in the build log) and holds exactly that commit's tree (compared
  file by file against `git archive`).
- Why: the owner wants an AI teammate that walks beside him in the room
  (research/ki-mitspieler-2026-10-06.md). This is the room's side of it, as
  agreed with the AI side in research/ki-mitspieler-aktionen.md; the AI talks
  to it through `larch-room-bridge`, a separate process in the larch package.
- The commits, written in this session and read in full: 596 lines added
  and 13 changed in `main.cpp`, 48 in `GLScene`, 36 in the README.
  - `9f3fc76`: a second avatar, the companion. `hl.plugin.hypr3d.companion`
    takes `go_to` and `look_at` with a target (`player`, `spawn`, or a window
    in the room by app class in lower case, `foot`, `foot 2`), `stop` and
    `state`. It walks a straight line as a second Jolt capsule and stops
    short of the player and of the floor's edge rather than push either. A
    refused call is a Lua error with the reason, which `hyprctl eval` prints
    with exit status 7. Events go out on Hyprland's own event socket (socket2)
    as `hypr3d>>{json}`: the room opening and closing and windows coming and
    going, with the window names and titles; and the walk's first step,
    arrival, block or abort. The body setup of the player's capsule moved
    into a function both use, unchanged. The F3 capsule outline and the
    companion share one drawing routine with a colour; the companion's lines
    are depth-tested and write depth.
  - `8c1c758`: the companion appears on the first call, not in every room.
  - No file, process, thread, library or network call is added. The events
    reach only clients of the session's socket2, which already carries every
    window's title (`activewindow`). A Lua error is raised with lua_error
    after the C++ objects of the call are gone. Window names only ever hold
    `[a-z0-9._-]` and a number, so a bridge can pass one back safely.
- The recipe at `8f9af733` differs from r71's in the header, `_commit`,
  `pkgver` and the checksum. Built with `tools/larch-packages build hypr3d` in
  the clean chroot against hyprland 0.56.2-4; its `.BUILDINFO` records the
  committed PKGBUILD's SHA-256 `2d2476c30584...`, which matches. The
  `-debug` package is not published.
- Measured. The owner's PC runs as Larch-B, where no VM may start, so
  everything ran in `larch-rice try --offscreen caelestia`, a nested Hyprland
  0.56.2 on his RTX 3080.
  - Built from the fork by cmake, with two foot windows:
    - `go_to foot`: first step 46 ms after the command, arrival 0.80 s later,
      0.29 m from the point 1.5 m in front of the window, facing it.
    - `go_to player`: it stopped 1.497 m from the player, facing him.
    - `look_at "FOOT 2"` turned it to that window.
    - `go_to spawn` with the player standing there: blocked, "The player is
      in the way", 1.7 s after the start.
    - `stop` held it still. Closing the room mid-walk aborted the walk and
      posted the room closed. After re-entry it stood where it had stopped,
      and `reset()` put it beside the spawn.
    - Closing "foot" left "foot 2" its name; a new terminal became "foot".
    - A fullscreen window aborted a walk and refused commands until it left.
  - Through the bridge against VedalAI's test server Randy (neuro-sdk
    `0cad33a`, bound to 127.0.0.1): every case of the action list, a target
    carrying Lua (refused by the bridge), malformed data, an unknown action,
    reconnection. Action received to result sent 5-11 ms, result to first
    step 28-34 ms.
  - 100 calls in 1.09 s, all taken; unloading the plugin mid-walk posted the
    abort and the closed room, and Hyprland lived on (same PID); loaded
    again, it walked.
  - Before any call no companion is drawn: no pixel of its colour where it
    would stand. After `companion("state")` there are 929.
  - This exact archive's `hypr3d.so` with three headless outputs in the
    owner's layout (1920x1080 at 0,0; 3840x2160 at scale 2 at 1920,45;
    1920x1080 at 675,-1080), through bridge and Randy:
    - `go_to player` arrived after 0.43 s, and `look_at player` turned it.
    - A walk was aborted by leaving the room, then the room was entered again.
    - It is drawn on the main monitor and, where it crosses, on the right one.
- Seen, but not caused by the plugin as far as measured:
  - At 01:03:14 the sandbox's Quickshell (caelestia) aborted with a FATAL in
    its screencopy ("buffer_constraints failure, however the buffer matches
    the last sent size"). This was in a sandbox that had run 35 minutes with
    many plugin reloads, while grim captured the three outputs.
  - The same sequence in fresh sandboxes did not abort, twice with r71's
    archive and twice with this one.
  - Earlier, at 00:38:58, that sandbox's caelestia tried to suspend the host
    through logind after ten idle minutes. An active sleep inhibitor refused
    it. That is larch-rice try's, not the plugin's, and is being fixed there.
- Not measured: the owner's real session; an AI at the other end; a window
  standing between the companion and its target.
- License: unchanged, MIT (Hypr3D, Jolt; both installed), stb_image and
  font8x8 public domain, cgltf MIT; libjpeg-turbo is linked, not included.
- Exact approved archive:
  `hypr3d-0.5.0.r73.g8c1c758-1-x86_64.pkg.tar.zst`, SHA-256
  `6d70efe3622a4037330b11572acf1026a6fae4f08a1870cc56aad4673a3797c8`.
  This approval covers no other version or build; it replaces the approval
  of 0.5.0.r71.g371300b-1.
