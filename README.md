# ETGBA revised review code and supporting assets

Version: 2026.10.31-review. This is a confidential peer-review package for *Security Assessment of Energy Forecasting Models under Grey-Box Selective Transfer Ensemble Attacks* (NCOMMS-26-015713-T).

## Start here

The package preserves the original `nc-review-code-main.zip` source files byte-for-byte under `legacy_original/`. Maintained revision workflows, frozen predictions, fitted models, numerical source data and plotting sources are supplied separately. The original README and K-S/non-parametric scripts describe the earlier implementation, not the revised statistical analysis.

From this directory, using Python 3.10 or newer:

```text
python workflow/verify_package.py
python -m pip install -r environment/requirements_quick.txt
python workflow/reproduce_frozen.py
python workflow/reproduce_gefcom09986_frozen.py
python workflow/demo_search.py
python workflow/run_lightweight_tests.py
python workflow/export_current_figures.py --output demo_output/current_figures
```

The first command uses the Python standard library only. The numerical demo uses NumPy; figure export uses Pillow. No GPU is needed. `verification/validation_results.json` records actual commands, runtime and outcomes for this assembled package. These timings are not clean-machine installation timings.

## Scientific scope

- `workflow/reproduce_frozen.py`: 180 metric/SEI checks from the ten retained Panama inputs and twenty S0/S1 conditions. No retraining, attack generation or model inference.
- `workflow/reproduce_operational.py`: 2,400 reserve-stress proxy checks from frozen predictions, three quantiles and both directions. These are not dispatch simulations.
- `workflow/verify_temporal_protocol.py`: training provenance, 20 fitted substitutes, 80 regenerated source-attack sets, target exclusion and frozen-input reconstruction.
- `workflow/reproduce_sei_weighting.py`: component scores, 11 fixed scenarios and 50,000 sampled weight vectors. This does not change the original SEI definition.
- `workflow/reproduce_cosine_threshold.py`: archived threshold sensitivity, input lineages, numerical outcomes and library admission. Exclusion is not an operational detector rate.
- `workflow/reproduce_gefcom2014_frozen.py`: the primary 0.999 GEFCom2014-L assessment.
- `workflow/reproduce_gefcom09986_frozen.py`: all 420 metric/SEI checks for seven frozen conditions across ten GEFCom2014-L targets, including 0.9986.
- `workflow/reproduce_statistical_draws.py` and `workflow/verify_statistical_inference.py`: the revised paired block-bootstrap inference. The 200, 450 and 50 hypothesis families are separate. These longer calculations are not part of the quick demo.

Training and new searches require the full scientific environment. See `INSTALL.md` and the original command documentation retained in `provenance/ASSEMBLY_README_20261029.md`. Running an archived script without reading its settings is not a substitute for choosing the documented entry point.

For exact reproduction of the archived Monte Carlo weighting summaries, use the separate NumPy 2.3.5 environment in `environment/requirements_weighting.txt`. A check with NumPy 1.26.4 reproduced the fixed scenarios but differed in an ancillary FGSM mean-rank summary by 0.00004 because strict rankings are sensitive to floating-point near-ties. The recorded NumPy 2.3.5 environment passed all stored weighting checks. The first compatibility result is retained in `verification/`; no reference values or tolerances were changed.

## Current figure numbering

`figures/current/` contains the exact embedded raster figures from the final main PDF (31 October, 15:47:34) and Supplementary PDF (31 October, 15:55:56): Main Figs. 1-4 and Supplementary Figs. 1-19. `figures/FIGURE_INDEX.csv` maps each to its PDF page, pixel checksum, numerical data and available plotting/design code. The source PDFs themselves are not duplicated in this code archive.

`workflow/export_current_figures.py` exports and checks these frozen files; it is not a new data-to-plot calculation. Original plotting code and available PDF/SVG exports are retained at their versioned paths. Their old figure numbers are historical names: use the index for the current numbering. A design script is not asserted to reproduce later manual edits to the Fig. 4 schematic.

`Source_Data/current_manuscript_tables/` contains labelled display-table exports from the matching Word versions. These rounded display values are distinct from full-precision prediction-derived analysis data. In particular, the retained main clean reference and the paired S0/S1 clean references must not be interchanged.

## Preservation and provenance

- `legacy_original/`: all 51 files from the supplied original ZIP, unchanged, including their original filenames.
- `src/`: original research scripts plus the revision search, scoring, projection and data modules. Current project source supersedes earlier copied source where the two differ; every decision is recorded in the assembly map.
- `workflow/`: small documented verification and demonstration entry points.
- `outputs/`: versioned numerical assets and source code for the current experiments, including the additional GEFCom2014-L threshold.
- `figures/`: exact current figures, available vector exports and original plotting sources.
- `Source_Data/`, `Dataset/`, `data_external/`, `Trained models/`: numerical source data, public-data working copies and trusted local fitted-model artifacts.
- `provenance/`: original ZIP preservation records and earlier audit/assembly records. Earlier progress flags and numbering are historical, not new claims of completion.
- `manifests/files.csv`: SHA256 and size of every packaged payload file. The manifest does not include its own hash.

Generated demo outputs and duplicate cached rerun outputs from the old assembly were not used as source inputs and are omitted. Required archived statistical distributions remain where referenced by the verification workflows. Raw data, predictions, source-attack arrays and model files were not edited.

## Important boundaries

Reproducing a frozen table is different from reproducing a fresh attack search. The current retained Panama selection and the unrestricted terminal-pool runner have different selection conditions; they are not asserted to produce identical candidates. Model-table/H5 and single-time-step attention correspondence remain author-review items. See `KNOWN_LIMITATIONS.md`.

This package is prepared for private review. No repository URL, DOI or new software/data licence is invented. The original archive did not supply a licence. Authors must confirm software licensing and third-party data redistribution conditions before public release. Never load pickle/joblib artifacts from an untrusted source.

Relevant guidance: https://www.nature.com/documents/GuidelinesCodePublication.pdf
