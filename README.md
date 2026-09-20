# MS1 RT Region Localization

Code accompanying **Localizing Discriminative Retention-Time Regions in LC-MS MS1 Signals via Contrastive Representation Learning** (ICTAI 2026).

The repository implements preprocessing of minimally processed LC-MS MS1 chromatograms, window-level contrastive representation learning, frog-level linear-probe evaluation, retention-time ablation, and figure generation.

## Repository structure

```text
notebooks/
  preprocessing/   mzML inspection and conversion to resampled NPZ files
  training/        contrastive training for the two classification tasks
  evaluation/      linear probes, threshold analysis, and supervised baselines
  ablation/        RT-bin masking and region-only analyses
  plotting/        scripts used to generate paper figures
data/              expected data layout (data are not distributed)
results/           generated checkpoints, metrics, and figures
```

## Environment

Python 3.10 or later is recommended.

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Data availability

The LC-MS dataset is not publicly distributed. The notebooks expect the following local structure:

```text
data/
  raw/mzML/
  processed/mzML_npz_45/
  processed/metadata_with_frog.csv
```

The metadata file must provide the sample identifiers, frog identifiers, and treatment labels used by the evaluation notebooks. Raw and processed data are excluded from version control.

## Running the notebooks

Run notebooks from their respective subdirectories so that `Path("../..").resolve()` points to the repository root. A typical workflow is:

1. `notebooks/preprocessing/`
2. `notebooks/training/`
3. `notebooks/evaluation/`
4. `notebooks/ablation/`
5. `notebooks/plotting/`

The two notebooks whose names end in `_sensitivity` reproduce the additional temperature comparison requested during review. Generated checkpoints and intermediate result files are not included.

## Evaluation scope

The encoder was pretrained once using all unlabeled chromatograms and then frozen. Leave-one-frog-out splitting was applied to the downstream linear probes. The reported evaluation is therefore transductive and does not measure fully inductive generalization to frogs unseen during representation learning.
