# LUMINAR — Sub-Pixel Lunar Image Registration

COSMOSIGHT

Aligns a Chandrayaan-2 lunar image to an LRO / QuickMap reference image, with honest accuracy metrics and a dashboard.

## Pipeline

auto-trim → scale sweep + simulated viewpoints → SuperPoint + LightGlue + RootSIFT candidates → Lunar Structural Graph → uniform selection → MAGSAC++ / spread-RANSAC / optional manual seed → Huber refinement → non-rigid TPS (only if held-out error improves) → honest metrics → dashboard → exports.

## Outputs

`registered.png`, `checkerboard.png`, `match_points.csv`, `report.json`, `dashboard.png`, a ZIP of all results.

Verdicts: **HIGH / MEDIUM / LOW / FAILED**, or **MANUAL** (hand-picked points, not independently verified).

## How to run

1. Open `LUMINAR_v6.ipynb` in Google Colab (File → Upload notebook, or open from GitHub).
2. Runtime → Change runtime type → **T4 GPU** (faster, optional).
3. Run cells top to bottom in this order:
   **0** install → **0b** imports + config → **I0** input library → **I1** source image → **I2** reference image → **I3** trim lines → **I4** apply trim → **3–8b** pipeline definitions → **8c** run.
4. **9** is a synthetic self-test (needs only 0, 0b and 3–8b).

Inputs accept PNG / JPG / TIF / WebP, PDS4 `.img` + `.xml`, zips containing either, Google Drive links, or a file path.

## Reserved stage hooks

`METADATA_ALIGNMENT` · `DEM_RENDER_RELIGHT` · `PROPOSE_ALIGNMENTS` · `CHANCE_VERIFICATION` · `DENSE_TIE_POINTS`

Each is a no-op today. Install one with `HOOKS['NAME'] = your_function`. The dashboard shows which are installed.

## Requirements

Google Colab (torch and torchvision are preinstalled). Cell 0 installs LightGlue, scikit-image, scipy, matplotlib and opencv-python-headless.
