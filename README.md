# Motion Libraries

The catalog the Motion plugin reads for its Libraries tab. Motion fetches `catalog.json` from this
repository; each entry points at a library's own source on GitHub, pinned to a commit, with a
checksum for every file. Motion downloads those files, checks them, and installs them into
`ReplicatedStorage.MotionLibraries`. No library code is stored here.

## Entry format

| Field | Meaning |
| --- | --- |
| `id` | Folder name and style prefix (`spring/Bouncy`). Letters, digits, `-`, `_` |
| `kind` | How Motion uses it: `easing-table` (a module returning `In<Style>` / `Out<Style>` / ... functions of 0..1), `spring` (a module with `new(damping, frequency, position)`, `:setGoal`, `:step(dt)`), `shake` (RbxUtil Shake's API; presets give `strength`, `rotation`, `speed`, `length`, `fadeIn`, `fadeOut`) or `physics` (3dUI_lib: a module with `Presets.Get(name)` giving `Stiffness`, `Ratio`, `Swirl`, `Bank` ranges and an optional `Tuning` table; Motion runs its spring between keys) |
| `entry` | The file Motion requires |
| `files` | `name`, `url` (raw.githubusercontent.com at a full 40-character commit), `hash` (32-bit FNV-1a of the file's bytes), `size`; `text = true` stores the file as a StringValue (licences); `append` may add one `return <Name>` line for modules that do not return themselves; `parent` puts a module inside another one from the same entry (for code that does `script:WaitForChild("Presets")`) |
| `styles` | The styles it adds; spring styles also give `damping` and `frequency` |

Motion ignores any entry that breaks these rules, so a bad entry can never install anything.

## Libraries

| Library | Licence | Source |
| --- | --- | --- |
| BoatTween Easing | MIT | https://github.com/boatbeaker/BoatTween |
| Spring Easing | MIT | https://github.com/Fraktality/Spring |
| Shake | MIT | https://github.com/Sleitnick/RbxUtil |
| 3D UI | none listed | https://github.com/barbiewire/3dUI_lib |

Each library keeps its own licence, which Motion installs alongside it.
