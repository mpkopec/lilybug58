# CLAUDE.md — lilybug56

Split keyboard that combines two existing designs. Bug54 provides the compact,
portable, column-staggered base; this repo is a fork of ogruendel's Bug54.
Lily58 provides the additions that Bug54 lacks. The first addition is the
Lily58-style index-finger key. If the Lily58 thumb cluster differs from the
Bug54 one, the Lily58 thumb cluster is the second addition; if the two
clusters are the same or similar, the index-finger key is the only addition.

## Toolchain

- PCB: KiCad. The two halves are separate projects, `kicad/lilybug56_left`
  and `kicad/lilybug56_right`.
- Firmware: QMK.

## Microcontroller

The design proceeds in two phases. The first phase targets the Adafruit
Feather RP2040 only. The second phase replaces its footprint with stacked
footprints for several controller boards, so that builders can use the board
they already own; the set of boards is not yet decided.

## KiCad libraries

Symbols missing from KiCad's official libraries go into the project-local
library `kicad/lilybug56.kicad_sym`, registered in the project
`sym-lib-table` through `${KIPRJMOD}`, so that every clone resolves them
without extra installation.

The Feather RP2040 symbol is a full copy of
`MCU_Module:Adafruit_Feather_Generic` with the pins renamed, not a derived
symbol. KiCad locks the pins of a derived symbol to its parent, which would
prevent the renaming. The footprint is the official generic Feather one.

Once the board is proven, the symbol is submitted as a merge request to
`kicad-symbols` on GitLab, from a separate fork. The project never points at
that fork. This keeps upstream review work, with its per-MR branches, out of
the project's own workflow.

## Firmware (QMK)

QMK supports the RP2040, but the Feather RP2040 is believed to have no
QMK board definition yet. The keyboard definition lives in `qmk/` in this
repo, laid out so that it can be copied unchanged into `keyboards/` of
`qmk_firmware`. A pull request to QMK follows later.

## Inherited Bug54 files

The following files come from Bug54 and do not describe the current design.
They are therefore not edited and not used as a source of current facts.

- `ergogen/`, `boards/shields/bug54/`, `config/`, `zephyr/`, `build.yaml` and
  `.github/` (the ergogen + ZMK setup) are kept as reference until the
  lilybug56 PCB is released and tested.
- `BOM.md`, `README.md` and `docs/` are removed once the KiCad project is
  established.
