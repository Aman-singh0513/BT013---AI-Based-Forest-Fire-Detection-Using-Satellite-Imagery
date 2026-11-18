# AI-Based Forest Fire Detection Using Satellite Imagery

## Project Overview

This project explores deep learning techniques for forest fire detection using satellite imagery. It includes:

- ResNet-18 image classification for fire and non-fire images.
- YOLOv8 object detection for identifying fire and smoke regions.

The project is developed in stages, covering dataset preparation, model training, evaluation, and future real-time detection integration.

## Project Structure

```text
BT013-Forest-Fire-Detection/
├── notebooks/
│   └── WildForest_Fire_Detection.ipynb
├── weights/
│   ├── best_resnet18.pth
│   ├── best_resnet18_v2.pth
│   └── best.pt
├── results/
│   ├── resnet18_baseline/
│   ├── resnet18_v2/
│   └── yolov8n_dfire_v1/
├── .gitignore
└── README.md
```

## Stage 1: ResNet-18 Image Classification

### Baseline Model

- Architecture: ResNet-18
- Input size: 224 x 224
- Optimizer: Adam
- Learning rate: 0.0001
- Loss: Weighted CrossEntropyLoss
- Training: 15 epochs
- Test accuracy: 98% (49/50)
- Checkpoint: `weights/best_resnet18.pth`

### Improved Model (V2)

- Added 92 manually approved hard-negative images to the non-fire training class.
- Training: 15 epochs
- Best validation accuracy: 99.57% (epoch 13)
- Test accuracy: 100% (50/50)
- Test loss: 0.0122
- Checkpoint: `weights/best_resnet18_v2.pth`

**Evaluation note:** Both test results are based on a test set of 50 images. They should not be interpreted as a guarantee of real-world performance.

## Stage 2: YOLOv8 Fire and Smoke Detection

### Dataset

Dataset: D-Fire

| Split | Images |
|---|---:|
| Train | 14,122 |
| Validation | 3,099 |
| Test | 4,306 |
| **Total** | **21,527** |

Class IDs:

- `0`: smoke
- `1`: fire

### Annotation Validation

- Valid bounding boxes: 26,539
- Smoke boxes: 11,854
- Fire boxes: 14,685
- Empty label files preserved: 9,838
- Invalid annotations after repair: 0
- Missing labels: 0
- Orphan labels: 0
- Unreadable images: 0

These figures describe structural validation of the prepared annotations; they do not represent a complete manual audit of every bounding box.

### Training Configuration

- Model: YOLOv8n
- Pretrained weights: `yolov8n.pt`
- Training epochs: 50
- Image size: 640 x 640
- Batch size: 16
- Optimizer: Ultralytics default configuration
- Training seed: 42
- Best checkpoint: `weights/best.pt`

### Validation Results

The following results are from the validation split at epoch 50:

| Metric | Overall |
|---|---:|
| Precision | 77.79% |
| Recall | 70.11% |
| mAP@50 | 77.20% |
| mAP@50-95 | 45.02% |

**Per-class validation mAP@50:**

- Smoke: 83.10%
- Fire: 71.30%

**Important:** These are validation metrics, not independent test-set results. The test split remains reserved for a separate final evaluation.

Training curves, validation plots, confusion matrices, and training metrics are intended to be stored in `results/yolov8n_dfire_v1/`.

## Results

ResNet-18 evaluation files are stored in:

- `results/resnet18_baseline/`
- `results/resnet18_v2/`

YOLOv8 training and validation artifacts are stored in:

- `results/yolov8n_dfire_v1/`

These include training metrics, curves, confusion matrices, and configuration details.

## Dataset Availability

The complete datasets are not included in this repository because of their size.

The prepared D-Fire dataset is stored separately. Users must obtain the dataset from its original source, review and comply with its applicable license and terms, and prepare the expected directory structure before running the YOLOv8 workflow.

The notebook may require changes to dataset paths and environment-specific setup when run outside the original Google Colab environment.

## Development Status

- [x] ResNet-18 baseline training and evaluation
- [x] Hard-negative dataset improvement
- [x] ResNet-18 V2 training and evaluation
- [x] D-Fire dataset preparation
- [x] YOLO annotation structural validation
- [x] YOLOv8n training (50 epochs)
- [x] YOLOv8 validation
- [ ] Independent YOLOv8 test-set evaluation
- [ ] Real-time detection integration

## Important Notes

- The ResNet-18 checkpoints are PyTorch model weights.
- The YOLOv8 checkpoint is a trained model weight file.
- Model performance on validation or small test samples does not guarantee performance in real-world deployment.
- Complete datasets and temporary training files are not included in this repository.
