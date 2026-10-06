### Hi, I'm Kuzuri

I build tools for 3D printing and fix the problems I run into along the way. Most of my work right now is on the **Snapmaker U1**: the slicer, the firmware, and getting projects from other printers onto it.

[kuzuriao.com](https://kuzuriao.com)

## bambu2orca

Converts Bambu Studio, Creality Print and Anycubic Slicer Next `.3mf` projects to Snapmaker U1 / OrcaSlicer, keeping as much of the original print settings as possible.

- **Web app:** [b2o.kuzuriao.com](https://b2o.kuzuriao.com), drag and drop
- **CLI:** [b2o](https://github.com/KuzuriAo/b2o) (`npx @kuzuri.ao/b2o`), MIT licensed, for scripting and batches
- **Privacy:** only the slicer settings ever leave your machine, never the 3D models. Run `--dry-run` to see exactly what would be sent.

## Snapmaker U1 contributions

### Print-by-object collisions

The U1 could crash the toolhead into finished objects in print-by-object jobs in three places: homing at the end of the print, tool changes, and pausing. I reported it to Snapmaker with videos, then fixed each one where it can be fixed.

| Collision | Where it's fixed | PRs |
|---|---|---|
| Homing after the print | Slicer profile | [OrcaSlicer #13854](https://github.com/OrcaSlicer/OrcaSlicer/pull/13854) (merged) |
| Tool changes | Slicer profile | [Snapmaker Orca #958](https://github.com/Snapmaker/OrcaSlicer/pull/958) · [OrcaSlicer #16094](https://github.com/OrcaSlicer/OrcaSlicer/pull/16094) |
| Pausing (the Pause button and spaghetti detection) | Firmware | [u1-klipper #17](https://github.com/Snapmaker/u1-klipper/pull/17) · [Extended Firmware #763](https://github.com/paxx12-snapmaker-u1/SnapmakerU1-Extended-Firmware/pull/763) |

All of them were tested on a U1 with the same collision test file, which is attached to the PRs.

### Sequential printing

The clearance check depended on the order objects were listed in, and flagged material below the gantry rod as a collision.

- [Snapmaker Orca #630](https://github.com/Snapmaker/OrcaSlicer/pull/630) and [#793](https://github.com/Snapmaker/OrcaSlicer/pull/793), also merged into a Snapmaker developer's dev branch ([#10](https://github.com/zackaree-shen/OrcaSlicer/pull/10))
- Upstream: [OrcaSlicer #14987](https://github.com/OrcaSlicer/OrcaSlicer/pull/14987) and [#15544](https://github.com/OrcaSlicer/OrcaSlicer/pull/15544)

### macOS and opening projects

- On macOS, models opened from Snapmaker Space were loaded and then thrown away: [Snapmaker Orca #852](https://github.com/Snapmaker/OrcaSlicer/pull/852) (merged)
- The Home page stopped rendering in builds from `main`; I traced it to the macOS SDK the app was built with: [Snapmaker Orca #853](https://github.com/Snapmaker/OrcaSlicer/issues/853)
- Projects opened from a link now open as projects, with their settings: [Snapmaker Orca #856](https://github.com/Snapmaker/OrcaSlicer/pull/856) · [OrcaSlicer #15652](https://github.com/OrcaSlicer/OrcaSlicer/pull/15652)
- `orcaslicer://` links are no longer ignored when OrcaSlicer isn't already running: [OrcaSlicer #15735](https://github.com/OrcaSlicer/OrcaSlicer/pull/15735)
- The command line no longer rejects every project file: [Snapmaker Orca #839](https://github.com/Snapmaker/OrcaSlicer/pull/839)
