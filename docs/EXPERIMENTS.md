# Experiments

The project investigates anomaly localization in brain MRI using diffusion models, inspired by the paper *What is Healthy? Generative Counterfactual Diffusion for Lesion Localization*.

The main implementation is kept in notebook form in `notebooks/PatRec_Project_Code_Group4.ipynb`.

## Main workflow

1. Prepare and preprocess BraTS MRI slices.
2. Train or load the diffusion model used to model healthy anatomy.
3. Generate counterfactual/healthy reconstructions from anomalous inputs.
4. Compare the original and reconstructed images.
5. Produce anomaly maps that highlight likely pathological regions.
6. Visualize representative examples and qualitative results.

## Repository figures

- `assets/presentation/` contains figures used in the course presentation.
- `assets/experiments/` contains experiment figures and additional qualitative outputs.

## Reproducibility notes

This was a semester group project, so some cells may reflect the original Google Colab/runtime setup. Before running the notebook, review paths, dataset locations, and package versions described in `docs/SETUP.md`.
