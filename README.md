# lilybug58

**Work in progress.** lilybug58 is a split keyboard derived from
[Bug54](https://github.com/ogruendel/bug54-zmk-config) by ogruendel, and this
repository is a fork of the Bug54 repository. It keeps Bug54's
compact, column-staggered layout and adds two keys per half taken from
[Lily58](https://github.com/kata0510/Lily58), for 58 keys in total:

- an index-finger key beside the innermost column, centred between its two
  lowest keys, in the position of the Lily58 extra key;
- a fifth key below the ring-finger column, where a Super key typically sits.

## Status

The design is at an early stage, and nothing in this repository has been
manufactured or tested yet. The PCB is being redesigned in KiCad, starting
from Bug54's ergogen-generated boards, and the firmware moves from ZMK to
QMK.

## Design

- **PCB:** KiCad 10, one project per half in `kicad/`.
- **Microcontroller:** Adafruit Feather RP2040 in the first revision. A later
  revision is planned to stack footprints for several controller boards, so
  that builders can use the board they already own.
- **Firmware:** QMK.
- **Layout sandbox:** ergogen, in `ergogen/`, used to try key positions and
  outlines. `npm install && npm run generate` writes its output to
  `ergogen/output/`; the KiCad projects remain the master copy of the PCB.
- **Case:** `mech/Case.FCStd` is Bug54's FreeCAD case, kept as the starting
  point for the lilybug58 case.

## Credits and license

Based on Bug54 by ogruendel, with key positions taken from Lily58 by
kata0510. Licensed under CC BY 4.0, as inherited from Bug54; see `LICENSE`.
