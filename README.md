# Cura 5.13 profiles for the Anycubic Kobra S1 Combo with ACE Pro (Gen 1)

Multi-color printing (up to 4 colors) with **UltiMaker Cura 5.13** on the **Anycubic Kobra S1 Combo** and the **ACE Pro Gen 1**.

> **Experimental.** This is a community project. It is not affiliated with or supported by Anycubic or UltiMaker. Use it at your own risk and watch the first color changes of every new setup.

## What is included

| Folder | Content |
|---|---|
| `definitions/` | Printer definition **Anycubic Kobra S1 Combo (ACE Pro Gen1)** |
| `definitions-gefilterte-materialien/` | Same definition, but the material list only shows Generic PLA, PETG, ABS, ASA and TPU (optional, use *instead of* the file above) |
| `extruders/` | Four extruder definitions, one per ACE Pro slot |
| `profiles/` | Cura profiles for PLA, PETG, ABS, ASA and TPU |

## How it works

- The four ACE Pro slots are modeled as **four extruders that share one nozzle and one heater**.
- Extruder 1-4 in Cura = ACE slot 1-4 = tool `T0`-`T3` in the G-code.
- The start G-code uses Anycubic's `G9111` macro. Every color change runs Anycubic's flush and wipe sequence (about 2 minutes per change).
- The retraction on nozzle switch is set to 0.8 mm. Cura's default (16 mm) does not fit the ACE Pro, because the firmware unloads and loads the filament itself.

## Installation

Close Cura first. Copy the files into the Cura configuration folder (*Help -> Show Configuration Folder* opens it):

| System | Folder |
|---|---|
| Windows | `%APPDATA%\cura\5.13\` |
| Linux (AppImage) | `~/.local/share/cura/5.13/` |
| Linux (Flatpak) | `~/.var/app/com.ultimaker.cura/data/cura/5.13/` |
| macOS | not tested, use *Help -> Show Configuration Folder* |

1. Copy `definitions/anycubic_kobra_s1_ace.def.json` into the `definitions` folder (or the file from `definitions-gefilterte-materialien/`).
2. Copy the four `extruders/*.def.json` files into the `extruders` folder.
3. Start Cura and add the printer: *Add Printer -> Non-networked printer -> Anycubic -> Anycubic Kobra S1 Combo (ACE Pro Gen1)*.
4. Import the profiles: *Preferences -> Configure Cura -> Profiles -> Import*.
5. Select a material for each of the four extruders.

## Recommended settings

- **Prime tower:** enabled, size 30 mm. Set *Prime Tower Minimum Volume* to 50 mm³ on **every** extruder (it is a per-extruder setting). Move the tower away from the bed edge.
- **Adhesion:** if you use a brim or skirt, choose one extruder for it (*Build Plate Adhesion Extruder*). Otherwise each extruder prints its own skirt.
- **Assign the parts of a model to the extruder that matches the loaded spool.** In Cura the assignment depends on the extruder number, not on the color.
- **Thumbnails (untested on the S1):** add the Cura post-processing script *Create Thumbnail* twice, 400x300 first and then 32x32.

## Profiles

| Profile | Nozzle (first layer) | Bed (first layer) | Fan | Print / outer wall |
|---|---|---|---|---|
| PLA 210 | 210 °C (215) | 55 °C (60) | 100 % | 150 / 100 mm/s |
| PETG 235 | 235 °C (240) | 75 °C (80) | 40 % | 90 / 50 mm/s |
| ABS 250 | 250 °C (255) | 100 °C | 15 % | 80 / 50 mm/s |
| ASA 255 | 255 °C (260) | 100 °C (105) | 20 % | 80 / 50 mm/s |
| TPU 95A | 225 °C (230) | 50 °C (55) | 50 % | 35 / 25 mm/s |

The multi-color profiles enable the prime tower (30 mm, 50 mm³ per extruder) and use a 5 mm brim (8 mm for ABS/ASA).

## Status and known limitations

- **Tested:** PLA with four colors (test cube and a multi-part model) on a Kobra S1 Combo with ACE Pro Gen 1, Cura 5.13 on Linux (Flatpak). **PETG, ABS, ASA and TPU values are untested starting points.**
- **TPU 95A does not work with the ACE Pro.** Use the TPU profile only for single-color prints from an external spool, with the built-in Cura printer *Anycubic Kobra S1*.
- ABS and ASA are only partly suited for the ACE Pro. Use PLA or PETG for multi-color.
- Every color change takes about 2 minutes, and a flush also runs at the start of the print.
- The values are starting points. Tune temperature, flow and speed for your filaments.

## Credits

- The printer definition inherits from the built-in Cura definition *Anycubic Kobra S1* (LGPL-3.0).
- The color-change sequence comes from Anycubic Slicer Next, as contributed to OrcaSlicer in pull request #11650.

## License

GPL-3.0, see `LICENSE`. The printer definition builds on Cura's LGPL-3.0 definition, and the LGPL-3.0 allows GPL-3.0 for derived works.
