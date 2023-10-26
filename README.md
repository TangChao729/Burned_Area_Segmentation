# Burned Area Computer Vision Model Evaluation

This repository houses the models, data, and utility scripts related to the evaluation of computer vision models for burned area detection.

## 📄 Description

This project delves into the evaluation of various computer vision techniques for the identification and segmentation of burned areas in satellite imagery. The project aims to evaluate the performance of different models and techniques, and to identify the most suitable model for the task. Contribution of this project includes:

- An Australia bushfire burned area data collection pipeline.
- An original 2019 Black Summer Bushfire Burned area dataset.
- A comparison of CNN-based and Transformer-based models for burned area detection.
- A novel U-Net all band model for burned area detection.

The data used for this project is self-sourced from Sentinel-2 database based on 2020 National Operational Bushfire Boundaries [Link Text](https://data.gov.au/data/dataset/2020-operational-bushfire-boundaries).

This original data consists of 13 bands of Sentinel-2 satellite imagery. Later processed in-house for labelling (masking) and extracted the 3 bands (4, 8a, 12) to form a SWIR false color image.

Data spiting and augmenting were done using the scripts in the data_prep folder.

The models used for this project are U-Net, U-Net all band, Mask RCNN, SegFormer and SAM. Each model's code including requirements, configuration and codes are stored in the models folder, ipynb of each model respectively.

## 🚀 Training Results

| **Model**                    | **F1-score** | **IoU**    | **MCC**    | **Average** |
| ---------------------------- | ------------ | ---------- | ---------- | ----------- |
| **Traditional (Baseline)**   |              |            |            |             |
| Index-product                | 0.5300       | 0.4020     | 0.4827     | 0.4716      |
| **CNN-based models**         |              |            |            |             |
| U-net                        | 0.8431       | 0.7343     | 0.8353     | 0.8042      |
| U-net all band               | 0.8800       | 0.7897     | 0.8728     | 0.8475      |
| Mask RCNN                    | 0.6126       | 0.7850     | 0.6110     | 0.6695      |
| YOLO                         | 0.6466       | 0.7765     | 0.6394     | 0.6875      |
| **Transformer-based models** |              |            |            |             |
| SegFormer b0                 | 0.8593       | 0.7638     | 0.8533     | 0.8255      |
| SegFormer b3                 | **0.8977**   | **0.8165** | **0.8904** | **0.8682**  |
| SAM                          | 0.6899       | 0.5631     | 0.6907     | 0.6479      |

## 🔧 Visual Results

![models predications](predications.png)

## 📁 Data

Sample images, masks and tiff files can be found here: [Data Folder](data/)
Full dataset can be downloaded in the G-drive, be aware it is about 10GB in size:
https://drive.google.com/file/d/1FCIWgzuJVufYWUdnPt_cWcW1wu6v_UHh/view?usp=share_link

## Architecture and Training Parameters

| **Main**       | **Backbone** | **Param** | **Flops** | **Model Size** | **Epochs** | **LR** | **Optimizer** |
| -------------- | ------------ | --------- | --------- | -------------- | ---------- | ------ | ------------- |
| U-Net          | Custom       | 31.2M     | 219.7B    | 119.5MB        | 500\*      | 1e-4\* | AdamW         |
| U-Net all-band | Custom       | 31.3M     | 220.1B    | 119.5MB        | 500        | 1e-4   | AdamW         |
| Mask RCNN      | ResNet-50    | 45.6M     | 280.3B    | 175.2MB        | 500        | 1e-4   | AdamW         |
| YOLO           | yolov8m      | 27.3M     | 110.2B    | 52.4MB         | 500        | 1e-4   | AdamW         |
| SegFormer      | MiT-b0       | 3.7M      | 6.76B     | 14.4MB         | 500        | 1e-5   | AdamW         |
| SegFormer      | MiT-b3       | 45.2M     | 71.4B     | 179.1MB        | 500        | 1e-5   | AdamW         |
| SAM            | ViT-base     | 93.7M     | 743.9B    | 375.2MB        | 200\*      | 1e-5   | AdamW         |

**Notes:**

- Model trained with 500 epochs has a 100 epoch patience early stop mechanism.
- All learning rates reduced to 0.1 of the starting rate in linear.
- SAM is trained for 200 epochs with a 50 epoch patience.
- Model parameters and flops are observed by using THOP PyTorch-OpCounter with batch size of 1.

## Contents

- `data/`: Directory containing data query and pre-processing codes, as well as original mask JSON files.
- `sample_dataset/`: Stores a small size sample dataset for testing.
- `models/`: Directory containing each model's training configures, testing results and visualizing ipynb files.

## Prerequisites

- Python 3.x
- Jupyter Notebook
- Libraries: Pytorch, OpenCV, NumPy, Matplotlib (Requirements for each model is in its own ipynb file).

## 🤝 Contributions

This research was conducted by Chaojun (Taylor) Tang, under the supervision of Prof. Richard Sinnott, in Faculty of Engineering and Information Technology of The University of Melbourne.
