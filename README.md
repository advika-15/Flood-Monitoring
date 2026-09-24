# Flood Monitoring Using Satellite Imagery

A machine learning and deep learning based flood monitoring project using **Sentinel-1 and Sentinel-2 satellite imagery**. The project performs flood classification and segmentation by combining spectral indices, radar-based features, texture information, and multiple machine learning models.

## Overview

Flood detection from satellite imagery can help identify flooded regions over large geographical areas. This project uses the **Sen1Floods11 dataset** containing Sentinel-1 SAR imagery, Sentinel-2 optical imagery, and corresponding flood masks.

The project explores different approaches for identifying flooded and non-flooded regions, ranging from traditional machine learning models to deep learning-based image segmentation.

## Dataset

The project uses the **Sen1Floods11** dataset.

The data contains:

* **Sentinel-1 (S1)** SAR imagery

  * VV polarization
  * VH polarization
* **Sentinel-2 (S2)** multispectral imagery

  * Multiple spectral bands
* **Flood masks**

  * Ground-truth labels indicating flooded and non-flooded regions

The dataset is downloaded and processed in the notebook rather than stored directly in this repository because of its large size.

## Features

### Sentinel-2 Spectral Indices

The following indices are calculated from Sentinel-2 bands:

* **MNDWI** — Modified Normalized Difference Water Index
* **NDWI** — Normalized Difference Water Index
* **NDVI** — Normalized Difference Vegetation Index

These indices provide information about water and vegetation characteristics and help distinguish flooded areas from non-flooded areas.

### Sentinel-1 Texture Features

A local texture feature is extracted from the **VH band of Sentinel-1** using a 5×5 window.

This helps capture spatial variations in the SAR imagery that can be useful for distinguishing flooded and non-flooded regions.

### Separability Analysis

A Separability Index is calculated to examine how effectively different features distinguish between flooded and non-flooded pixels.

## Machine Learning Models

The project experiments with multiple approaches:

### 1. Support Vector Machine (SVM)

SVM is used as a baseline supervised classification model using Sentinel-2 spectral indices.

### 2. K-Means Clustering

K-Means is explored as an unsupervised approach for separating image pixels into different clusters based on their feature values.

### 3. Random Forest

Random Forest is used as a supervised classification approach using combinations of satellite-derived features.

### 4. U-Net

A **U-Net convolutional neural network** is implemented for pixel-level flood segmentation.

The U-Net architecture contains:

* Encoder/downsampling blocks
* Bottleneck layer
* Decoder/upsampling blocks
* Skip connections
* Final 1×1 convolution for flood-mask prediction

The model is trained using **Dice Loss** and optimized using **Adam**.

## Workflow

```text
Sentinel-1 + Sentinel-2 Images
             │
             ▼
       Data Pairing
             │
             ▼
        Preprocessing
             │
      ┌──────┴──────┐
      ▼             ▼
Spectral Indices   S1 Texture
      │             │
      └──────┬──────┘
             ▼
      Feature Analysis
             │
             ▼
     ┌───────┼────────┐
     ▼       ▼        ▼
    SVM   K-Means  Random Forest
             │
             ▼
          U-Net
             │
             ▼
      Flood Segmentation
             │
             ▼
        Evaluation
```

## Data Preprocessing

The notebook performs the following preprocessing steps:

1. Downloads the required Sentinel-1, Sentinel-2, and label data.
2. Pairs corresponding S1, S2, and flood-mask files.
3. Calculates Sentinel-2 spectral indices.
4. Extracts texture features from Sentinel-1 VH imagery.
5. Visualizes sample satellite images.
6. Splits the paired data into training and validation sets.
7. Prepares the data for machine learning and U-Net training.

## Evaluation

The models are evaluated using classification metrics such as:

* Precision
* Recall
* F1-score
* Classification report

For U-Net, predictions are converted into binary flood masks and compared against the ground-truth masks on the validation dataset.

## Technologies Used

* Python
* NumPy
* Pandas
* Matplotlib
* Scikit-learn
* PyTorch
* Rasterio
* SciPy
* scikit-image
* Google Colab
* Sentinel-1
* Sentinel-2

## Project Structure

```text
Flood-Monitoring/
│
├── Flood.ipynb
├── README.md
└── .gitignore
```

## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/Flood-Monitoring.git
cd Flood-Monitoring
```

### 2. Open the notebook

The project is designed to run in **Google Colab**.

Open:

```text
Flood.ipynb
```

### 3. Install required dependencies

Install the required Python libraries in the notebook environment before running the cells.

### 4. Download the dataset

The notebook contains the dataset download and setup steps for the Sen1Floods11 data.

### 5. Run the notebook

Run the cells sequentially to perform:

* Data preparation
* Feature extraction
* Separability analysis
* Model training
* Flood segmentation
* Model evaluation

## Results

The project compares traditional machine learning approaches with a deep learning based U-Net segmentation model for flood detection.

The final evaluation includes classification reports comparing predicted flood regions with the corresponding ground-truth masks.

## Future Improvements

* Add IoU and Dice Score as explicit segmentation metrics.
* Compare model performance across different geographic regions.
* Improve U-Net architecture using attention mechanisms or pretrained encoders.
* Add a visualization interface for uploading satellite images and generating flood masks.
* Optimize preprocessing and inference for near-real-time flood monitoring.

## Author

**Advika**

B.Tech Computer Science and Engineering
