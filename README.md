# JFDFusion

This repository provides the source code for the manuscript:

**Infrared–Visible Image Fusion with Joint Frequency Decomposition and Deep Feature Learning (JFDFusion)**

JFDFusion is an infrared and visible image fusion framework based on joint frequency decomposition and deep feature learning. The method mainly includes:

- **N-DEWT**: Non-downsampling Enhanced Discrete Wavelet Transform for frequency-domain feature decomposition.
- **GCMam**: Gating Convolutional Mamba module for long-range dependency modeling.
- **DWAF**: Dynamic Weight Adjustment Fusion module for adaptive infrared-visible feature fusion.

## Repository Structure

```text
Fre_code/
├── main.py                  # Training and testing entry
├── config.py                # Configuration loading and model/dataset initialization
├── dataset.py               # Dataset loading and preprocessing
├── metric.py                # Evaluation metrics
├── metrics_test*.py         # Metric calculation scripts
├── summary.py               # FLOPs and parameter calculation
├── config/
│   └── model2.yaml          # Model and training configuration
├── models/
│   ├── models2.py           # Main JFDFusion network
│   ├── E_NDWT.py            # N-DEWT module
│   ├── CMblock.py           # GCMam-related module
│   ├── fusionlayer.py       # Dynamic fusion layer
│   ├── filters.py           # Filtering operators
│   ├── loss.py              # Loss functions
│   └── utils.py             # Utility functions
└── result/
    └── *.xlsx / loss.png    # Example experimental records
```

If this repository only contains `Fre_code.zip`, please download and unzip it before running the code.

## Requirements

The code was implemented with Python and PyTorch. Recommended environment:

```text
Python >= 3.8
PyTorch >= 1.12
torchvision
numpy
Pillow
PyYAML
matplotlib
pandas
openpyxl
pytorch-msssim
einops
mamba-ssm
thop
```

Install the main dependencies with:

```bash
pip install torch torchvision numpy pillow pyyaml matplotlib pandas openpyxl pytorch-msssim einops thop
pip install mamba-ssm
```

The installation of `mamba-ssm` may depend on the CUDA/PyTorch version. Please follow the official installation instructions of `mamba-ssm` if installation fails.

## Dataset Preparation

The datasets used in this work are publicly available infrared-visible image fusion datasets, including:

- MSRS
- Road-Scene
- TNO

Please download these datasets from their original public sources.

The expected dataset structure is:

```text
DatasetName/
├── ir/
│   ├── image_001.png
│   ├── image_002.png
│   └── ...
├── vi/
│   ├── image_001.png
│   ├── image_002.png
│   └── ...
└── labels.txt   # Optional for MSRS/Road/M3FD testing
```

The filenames in `ir/` and `vi/` should correspond to each other.

Before training or testing, modify the dataset paths in:

```text
config/model2.yaml
main.py
```

For example, update the following fields in `config/model2.yaml`:

```yaml
dataset:
  url:
    MSRS: /path/to/MSRS
    Road: /path/to/Road
    TNO: /path/to/TNO
```

## Training

After modifying the dataset paths and configuration file, run:

```bash
python main.py --train
```

The default training configuration is provided in:

```text
config/model2.yaml
```

The trained model checkpoint is saved by default to:

```text
result/Fre2
```

If needed, please modify the checkpoint saving path in `main.py`.

## Testing

After training, update the pretrained model path and test dataset paths in `main.py`, then run:

```bash
python main.py --test
```

The fused images will be saved to the corresponding output folder defined in the testing function.

## Evaluation

Evaluation metric scripts are provided as:

```text
metrics_test.py
metrics_test2.py
metrics_test3.py
```

Before running them, modify the following paths inside the scripts:

```python
ir_folder = "/path/to/ir"
vis_folder = "/path/to/vi"
fuse_folder = "/path/to/fused_results"
results_path = "/path/to/save/results.xlsx"
```

Then run:

```bash
python metrics_test.py
```

The results will be saved as an Excel file.

## FLOPs and Parameters

To calculate FLOPs and model parameters, run:

```bash
python summary.py
```

Please ensure that the model import path in `summary.py` is consistent with the actual model file.

## Notes

1. Some paths in the released code are local paths used during experiments. Please replace them with your own dataset, checkpoint, and result paths before running.
2. Large datasets and trained weights are not included in this repository.
3. This code is released for academic research and reproducibility purposes.

## Citation

If this code is useful for your research, please cite our paper:

```text
Infrared–Visible Image Fusion with Joint Frequency Decomposition and Deep Feature Learning (JFDFusion)
```

## License

This project is released for academic research use only.
