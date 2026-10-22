# Setup and reproducibility

## Recommended workflow

1. Use an isolated Python environment with a CUDA-capable PyTorch installation, or a GPU notebook runtime such as Colab/Kaggle.
2. Install the dependencies from the repository root with `python -m pip install -r requirements.txt`.
3. Open `notebooks/PatRec_Project_Code_Group4.ipynb`.
4. Treat the historical installation/debug cells at the beginning of the notebook as records of the original environment rather than a portable setup script.
5. Set `MONAI_DATA_DIRECTORY` to a persistent writable directory before dataset initialization.
6. Run data preparation, model construction, training, sampling, counterfactual generation, and evaluation sequentially.

## Historical setup notes

The original notebook mixes CUDA/PyTorch installation commands, Ubuntu package management, MONAI development installs, and a pinned `monai-generative` package. These reflect the original experimentation environment.

In particular:

- `!python` can enter an interactive process and block execution.
- `!cd GenerativeModels/` does not persist into a following notebook shell cell.
- A GitHub `blob` URL is not the same as a raw source URL.
- Development/weekly MONAI installs can replace a stable environment.

## Reproducibility limitations

- The code downloads Medical Segmentation Decathlon `Task01_BrainTumour`; the slides refer to BraTS, so the exact dataset/release naming should be stated carefully.
- Samples are 3D volumes followed by random slice extraction rather than a fixed exported 2D slice dataset.
- Validation uses random cropping transforms, so a selected validation index is not guaranteed to correspond to one fixed slice.
- Dice evaluation in the notebook is demonstrated on a selected slice rather than a complete benchmark aggregation.
- No trained weights, full-run metric archive, or package lockfile was supplied.
- GPU execution and metric reproduction were not rerun during repository organization.
