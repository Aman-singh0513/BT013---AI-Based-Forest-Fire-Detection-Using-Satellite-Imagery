# AI-Based Forest Fire Detection Using Satellite Imagery

## Project Overview

This project explores deep learning techniques for forest fire detection using satellite imagery.
It includes a ResNet-18 image classification stage and preparation for YOLOv8 fire and smoke detection.

## Project Structure

```text
BT013-Forest-Fire-Detection/
├── weights/
│   ├── best_resnet18.pth
│   └── best_resnet18_v2.pth
├── results/
│   ├── resnet18_baseline/
│   └── resnet18_v2/
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

**Evaluation note:** Test results are based on 50 images and do not guarantee real-world performance.

## Stage 2: YOLOv8 Fire and Smoke Detection

Dataset: D-Fire

| Split | Images |
|---|---:|
| Train | 14,122 |
| Validation | 3,099 |
| Test | 4,306 |
| Total | 21,527 |

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

**Current status:** Dataset preparation and structural validation are complete. YOLOv8 training has not started.

## Results

Evaluation files are stored in:
- `results/resnet18_baseline/`
- `results/resnet18_v2/`

These include test metrics, classification reports, confusion matrices, and other evaluation outputs.

## Dataset Availability

The full datasets are not included in this repository because of their large size.
They are stored separately in Google Drive. The YOLOv8 configuration must point to the prepared `cleaned_v2` dataset before training.

## Development Status
- [x] ResNet-18 baseline training and evaluation
- [x] Hard-negative dataset improvement
- [x] ResNet-18 V2 training and evaluation
- [x] D-Fire dataset preparation
- [x] YOLO annotation structural validation
- [ ] YOLOv8 model training
- [ ] YOLOv8 evaluation
- [ ] Real-time detection integration

## Important

The ResNet-18 checkpoints are PyTorch model weights. Training source code and complete datasets are not currently included in this repository.
