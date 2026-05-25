# GFP Analysis

A Python script for automated analysis of GFP experiments performed on the **Incucyte live-cell imaging system**. It takes raw export files, normalises the GFP signal to cellular confluence, and generates a publication-ready multi-panel figure together with a CSV summary.

---

## What it does

- Loads raw Incucyte TSV export files (GFP count, confluence, and optionally GFP intensity)
- Aligns time points across files and filters selected conditions
- Normalises GFP signal by confluence to account for differences in cell number
- Computes per-condition summary metrics:
  - **Growth index** - confluence at end / confluence at start (proliferation / cytotoxicity check)
  - **GFP synthesis fold** - GFP density relative to control at the end of the experiment
  - **GFP count accumulation slope ** - rate of GFP increase above control within a user-defined time window
- Generates a **multi-panel figure** (PNG, 300 dpi) ready for a paper or presentation
- Exports metrics to **CSV**

Works both in **Google Colab** and as a **local Python script**.

---

## Panels generated

| Panel | Content | Always shown |
|-------|---------|:---:|
| A | Raw GFP+ object count per well | ✅ |
| B | Cell confluence | ✅ |
| C | GFP count normalised to confluence | ✅ |
| D | Summary metrics table (count-based) | ✅ |
| E | Raw GFP total integrated intensity (GCU) | optional |
| F | GFP intensity normalised to confluence | optional |
| G | Summary metrics table (intensity-based) | optional |

---

## Requirements

- Python ≥ 3.9
- See `requirements.txt` for dependencies

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Usage

### Google Colab (recommended for first use)

1. Open a new Colab notebook
2. Upload `analysis.py`
3. Run it - the script will prompt you to upload your data files via the Colab file picker

### Local environment

```bash
python analysis.py
```

The script will prompt you step by step:
1. Whether to show captions below plots
2. The name (or fragment) of your control condition
3. Any conditions to exclude
4. Which optional panels to generate (E, F, G)
5. Paths to your input files

---

## Input files

The script expects standard **Incucyte TSV export files**:

| File | Content |
|------|---------|
| File 1 (required) | GFP object count |
| File 2 (required) | Confluence (%) |
| File 3 (optional) | GFP total integrated intensity (GCU) |

Files are automatically aligned by elapsed time points; minor column name differences between files are handled by fuzzy matching.

---

## Output files

| File | Description |
|------|-------------|
| `<input_name>_gfp_delivery_analysis.png` | Multi-panel figure (300 dpi) |
| `<input_name>_gfp_count_metrics.csv` | Summary metrics - count-based |
| `<input_name>_gfp_intensity_metrics.csv` | Summary metrics - intensity-based (if panels E/F/G selected) |

---

## Configuration

Key parameters can be adjusted at the top of the script:

```python
FONT_SIZE_BASE = 20       # tick labels and body text
FONT_SIZE_TITLE = 24      # panel title (A, B, C …)
SLOPE_T_MIN = 0           # start of accumulation slope window (hours)
SLOPE_T_MAX = 24          # end of accumulation slope window (hours)
```

---

## Citation

If you use this script in your work, please cite the repository:

```
GitHub. https://github.com/martynakor/analysis
```
