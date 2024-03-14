# Real-Time Cameraman Segmentation with YOLOv8 in Football Video Broadcasts

'Abstract here'

Dataset: [cameraman-segmentation](https://universe.roboflow.com/cv-wc4ti/cameraman-segmentation/)

## Experiments

The following table describes the experiments performed in this research.

#### YOLOv8 hyper-parameter tuning:

| Experiment No. | Batch Size | LR     | Optimizer | Momentum | Epochs | Model | Backbone Frozen Layers |
| -------------- | ---------- | ------ | --------- | -------- | ------ | ----- | ---------------------- |
| 1              | 16         | 0.01   | SGD       | 0.937    | 15     | nano  | N/A\*                  |
| 2              | 16         | 0.001  | Adam      | 0.9      | 15     | nano  | N/A\*                  |
| 3              | 16         | 0.02   | AdamW     | 0.9      | 15     | nano  | N/A\*                  |
| 4              | 16         | 0.02   | AdamW     | 0.9      | 15     | small | N/A\*                  |
| 5              | 8          | 0.0001 | SGD       | 0.9      | 15     | nano  | N/A\*                  |
| 6              | 28         | 0.1    | SGD       | 0.99     | 15     | nano  | N/A\*                  |
| 7              | 16         | 0.01   | SGD       | 0.937    | 15     | nano  | 15                     |
| 8              | 16         | 0.01   | SGD       | 0.937    | 15     | nano  | 20                     |

`(*)`: Modification was not applied.

#### Comparison with other models:

| Model            | Epochs | Batch Size | LR     | Optimizer | Momentum |
| ---------------- | ------ | ---------- | ------ | --------- | -------- |
| YOLOv5n-seg      | 50     | 16         | 0.01   | SGD       | 0.937    |
| YOLOv7n-seg      | 50     | 16         | 0.01   | SGD       | 0.937    |
| YOLACT           | 50     | 16         | 0.001  | SGD       | 0.9      |
| Mask R-CNN       | 50     | 16         | 0.02   | SGD       | 0.9      |
| OneFormer        | 50     | 16         | 0.0001 | AdamW     | 0.9      |
| SSD              | 50     | 16         | 0.001  | SGD       | 0.9      |
| Proposed YOLOv8n | 50     | 16         | 0.01   | SGD       | 0.937    |

## Results

This table provides a summary of the results obtained in the experiments described above.

'Table here'

## Files

All the experiments perfomed in this research are available in the following files:

1. `YOLOv7` experiments - `./yolov7/train.ipynb`
2. `YOLOv5` experiments - `./yolov5/train.ipynb`
3. `YOLACT` experiments - `./yolact/train.ipynb`
4. `Mask R-CNN` experiments - `./maskrcnn/train.ipynb`
5. `SSD` experiments - `./ssd/train.ipynb`
6. `OneFormer` experiments - `./oneformer/train.ipynb`
7. `Proposed YOLOv8` experiments - `./proposed-yolov8/*`

## Reproducing the Experiments

All the experiments performed in this research were executed in the environment described below:

| Name                    | Version                              |
| ----------------------- | ------------------------------------ |
| CPU                     | Intel Core i7-12700KF                |
| GPU                     | Nvidia RTX 3080 Ti, 12 GB            |
| Memory                  | 64 GB                                |
| Operation System        | Ubuntu 22.04, 64-bit                 |
| Deep Learning Framework | Python 3.8, Pytorch 2.2.1, CUDA 12.1 |

To replicate the experiments described in the [Experiments](#experiments) section, follow the steps below:

Before starting the experiments, make sure to edit the `cfg.ymal` file and set the credentials to download the dataset from the Roboflow platform

```
api_key: <>
workspace: <>
project: <>
version: <>
```

#### Comparison with other models

### `YOLOv7` experiments

To reproduce the experiments of the `YOLOv7` model, follow the steps below:

1. Adjust the hyperparameters in `./yolov7/hyp.yaml` file if needed.
2. Run the `./yolov7/train.ipynb` notebook to train the model.
3. After model training, all the results will be available in the `./yolov7/yolov7/seg/runs/train-seg` directory.

### `YOLOv5` experiments

To reproduce the experiments of the `YOLOv5` model, follow the steps below:

1. Adjust the hyperparameters in `./yolov5/hyp.yaml` file if needed.
2. Run the `./yolov5/train.ipynb` notebook. to train the model
3. After model training, all the results will be available in the `./yolov5/yolov5/runs/train-seg` directory.

### `YOLACT` experiments

1. Run the `./yolact/setup.ipynb` notebook.
2. Insert the following code to the `./yolact/data/config.py` file:

```
# ----------------------- DATASETS ----------------------- #
...
cameramen_dataset = dataset_base.copy({
    'name': 'cameramen_dataset',
    'train_info': './cameraman/train/coco_annotations.json',
    'train_images': './cameraman/train/images/',
    'valid_info': './cameraman/val/coco_annotations.json',
    'valid_images': './cameraman/val/images/',
    'class_names': ('cameraman'),
    'label_map': {1:  1}
})
```

3. Adjust the hyperparameters in `./yolact/train.ipynb` file if needed.
4. Run the `./yolact/train.ipynb` notebook to train the model.
5. After model training, all the results will be available in the `./yolact/results` directory.

### `Mask R-CNN` experiments
