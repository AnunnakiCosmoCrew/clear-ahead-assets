# Export Automation Guide

This document describes the asset export pipeline for ClearAhead!

## Directory Structure

```
source/          → Editable source files
  blender/       → 3D models, rendered sprites (.blend)
  psd/           → Photoshop/GIMP layered files (.psd, .xcf)
  svg/           → Vector source files (.svg)
exports/         → Final game-ready assets (committed, used by clear-ahead)
  sprites/       → Vehicle sprites, road tiles, character sprites
  ui/            → Buttons, icons, HUD elements
  animations/    → Sprite sheets, frame sequences
references/      → Mood boards, style guides, concept sketches
scripts/         → Export automation scripts
```

## Export Specifications

### Sprites
- **Format**: PNG with transparency
- **Resolution**: 2x base (designed at 80px per world unit, exported at 160px)
- **Naming**: `<category>_<name>_<variant>.png` (e.g., `vehicle_ambulance_default.png`)

### Sprite Sheets
- **Format**: PNG + JSON atlas
- **Tool**: TexturePacker or equivalent
- **Max sheet size**: 2048x2048

### UI Elements
- **Format**: PNG or 9-patch PNG
- **Sizes**: Export at 1x, 2x, 3x for different DPIs

## Manual Export Steps

### From Blender
1. Open the `.blend` file in `source/blender/`
2. Set render resolution to target size (160px per world unit)
3. Render with transparent background (Film > Transparent)
4. Save to `exports/sprites/` with correct naming convention
5. Optimize PNG: `pngquant --quality=80-100 --strip <file>.png`

### From Photoshop/GIMP
1. Open the `.psd` file in `source/psd/`
2. Hide background layers
3. Export as PNG with transparency
4. Save to appropriate `exports/` subdirectory
5. Optimize PNG: `pngquant --quality=80-100 --strip <file>.png`

### From SVG
1. Open the `.svg` file in `source/svg/`
2. Export as PNG at target resolution
3. Or use CLI: `inkscape --export-type=png --export-dpi=192 <file>.svg`
4. Save to appropriate `exports/` subdirectory

## Automation Scripts (Future)

Planned scripts for `scripts/`:
- `export_blender.py` — Blender Python script to batch-render all .blend files
- `export_svg.sh` — Shell script to batch-convert SVGs via Inkscape CLI
- `build_atlas.sh` — Pack sprites into sprite sheets
- `optimize_pngs.sh` — Run pngquant on all exports
- `sync_to_game.sh` — Copy final exports to `clear-ahead/assets/images/`

## Syncing to Game Repo

Final exported assets are copied to the main game repo:

```bash
# From this repo root
cp -r exports/sprites/* ../clear-ahead/assets/images/sprites/
cp -r exports/ui/* ../clear-ahead/assets/images/ui/
cp -r exports/animations/* ../clear-ahead/assets/images/animations/
```

This is intentionally a manual step to keep the game repo's asset set deliberate.
