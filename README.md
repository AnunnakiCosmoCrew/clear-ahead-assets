# clear-ahead-assets

Asset pipeline for **ClearAhead!** — source files, exports, and automation scripts.

## Structure

```
source/
  blender/       → 3D models (.blend)
  psd/           → Layered image files (.psd, .xcf)
  svg/           → Vector source files (.svg)
exports/
  sprites/       → Vehicle sprites, road tiles
  ui/            → Buttons, icons, HUD elements
  animations/    → Sprite sheets, frame sequences
references/      → Mood boards, style guides, concepts
scripts/         → Export automation & documentation
```

## Workflow

1. Create/edit source files in `source/`
2. Export game-ready PNGs to `exports/` (see [export guide](scripts/export-guide.md))
3. Copy final assets to the [clear-ahead](https://github.com/AnunnakiCosmoCrew/clear-ahead) game repo

## Related

- Game repo: [AnunnakiCosmoCrew/clear-ahead](https://github.com/AnunnakiCosmoCrew/clear-ahead)
