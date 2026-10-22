# Anomaly Localization with Counterfactual Diffusion

**Pattern Recognition semester project · ECE, National Technical University of Athens · Group 4 · 2024**

Generating healthy counterfactual brain MRI slices with a conditional diffusion model, then comparing them with the input to localize potential lesions. This group project studies and reproduces the approach of **Sanchez et al., “What is Healthy? Generative Counterfactual Diffusion for Lesion Localization” (2022)** using MONAI, and explores hyperparameters and anomaly-map thresholding.

[Notebook](notebooks/PatRec_Project_Code_Group4.ipynb) · [Project report](docs/project_report.pdf) · [Presentation](docs/project_presentation.pdf) · [Setup guide](docs/SETUP.md) · [Original paper](https://arxiv.org/abs/2207.12268)

## Method

1. Load brain MRI volumes through MONAI's Medical Segmentation Decathlon `Task01_BrainTumour` interface and extract 64 × 64 FLAIR slices.
2. Derive a slice-level healthy/unhealthy label from the segmentation mask.
3. Train a conditioned 2D diffusion U-Net with class-conditioning dropout.
4. Encode an input slice with reversed DDIM steps and reconstruct it with classifier-free guidance toward the healthy class.
5. Compute the absolute input–reconstruction difference as an anomaly heatmap.
6. Threshold the heatmap using a percentile or Otsu's method, then calculate Dice overlap with the reference mask.

The network receives scalar class conditioning, not segmentation masks as training targets. Masks are nevertheless used to derive these class labels and to evaluate localization: this is **weakly supervised**, not fully unsupervised.

## Included work

- Jupyter notebook preserving the original notebook workflow.
- Group report and presentation covering theory, reproduction, hyperparameter experiments, and a liver CT extension.
- Experiment figures, their original parameter index, and supporting presentation images.
- Setup notes, dependency list, and explicit reproducibility limitations.

The supplied executable notebook covers the **brain MRI experiment**. The liver extension is documented in the report, slides, and images; its implementation was not included in the supplied files.

## Reported results

| Experiment | Thresholding | Dice reported in presentation |
|---|---|---:|
| Brain MRI reproduction | Percentile / manual | 61.4% |
| Brain MRI reproduction | Otsu | 63.5% |
| Liver CT extension | Not specified in result slide | 51% |

These historical presentation results have not been recomputed. The notebook calculates Dice for a selected validation slice; it does not contain the complete aggregation procedure needed to reproduce the table.

## Repository contents

| Path | Contents |
|---|---|
| `notebooks/` | Original research notebook |
| `docs/` | Report, presentation, figure compilation, setup and experiment notes |
| `assets/experiments/` | Experiment figures and original parameter index |
| `assets/presentation/` | Brain/liver examples and presentation illustrations |
| `references/` | Paper bibliography and attribution |
| `data/README.md` | Dataset acquisition and storage notes; no dataset bundled |
| `requirements.txt` | Dependency starting point; not a verified environment lock |

## Running the notebook

Use a CUDA-capable environment and open `notebooks/PatRec_Project_Code_Group4.ipynb` in Jupyter, Colab, or Kaggle. **Read [SETUP.md](docs/SETUP.md) before executing it**: the original notebook contains historical system-installation cells that should not be run blindly on a managed runtime.

No trained weights, dataset, or fully pinned environment were supplied.

## Team and contributions

| Member | Contribution recorded in the presentation |
|---|---|
| Anthi Vozinaki | Different-dataset experiments, MONAI setup, report, presentation |
| Panagiotis Giadikiaroglou | Hyperparameter experiments, Dice scores, report, presentation |
| Nikolas Karafyllis | Theoretical analysis, paper reproduction, report, presentation |
| Ioannis Litsos | Hyperparameter experiments, Dice scores, report, presentation |
| Panagiotis Michelakis | Theoretical analysis, paper reproduction, report, presentation |

## Acknowledgements

Based on the work of Pedro Sanchez, Antanas Kascenas, Xiao Liu, Alison Q. O'Neil, and Sotirios A. Tsaftaris, and the MONAI Generative Models implementation.

This repository is an educational research project, not a clinically validated diagnostic tool. See `docs/RIGHTS.md` for rights and attribution notes.
