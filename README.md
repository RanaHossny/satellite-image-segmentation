# Satellite Image Segmentation

## Overview

This project involves segmenting satellite images using various neural network architectures. The dataset consists of satellite images with 12 spectral bands in TIFF format. The aim is to preprocess these images and apply different segmentation models to evaluate their performance.

## Dataset

The dataset includes satellite images with 12 bands in TIFF format. It is structured as follows:

- **`train/images`**: Training images.
- **`train/labels`**: Corresponding training labels.
- **`val/images`**: Validation images.

## Preprocessing

The preprocessing steps include:
- Converting RGB channels to a single grayscale band.
- Reducing the total number of bands from 12 to 10.

## Dataset Class

The `SatelliteDataset` class handles the loading and preprocessing of images and labels. It supports data augmentation using the `albumentations` library.

### Dataset Class Details

- **`SatelliteDataset`**: Handles images and labels with preprocessing, filtering, normalization, and band selection.
- **`SatelliteDataset_2`**: An alternative class that uses the entire dataset without band selection. It includes normalization and optional filtering.

## Encoder-Decoder Architectures

Encoder-Decoder architectures are particularly well-suited for image segmentation tasks. They are designed to learn and predict pixel-level segmentation maps. Here’s a detailed breakdown of how they work:

1. **Encoder**:
   - **Purpose**: Extracts features from the input image.
   - **Structure**: Consists of convolutional layers that capture low-level features and pooling layers to downsample the feature maps.
   - **Output**: Produces increasingly abstract representations of the input image.

2. **Bottleneck**:
   - **Purpose**: Contains the deepest layer of the network, capturing the most abstract features of the image.

3. **Decoder**:
   - **Purpose**: Reconstructs the spatial dimensions of the feature maps.
   - **Structure**: Uses transposed convolutions (upsampling) to increase spatial dimensions and generate high-resolution output maps.
   - **Output**: Produces segmentation maps from abstract features learned by the encoder.

4. **Skip Connections**:
   - **Purpose**: Preserve fine details and improve segmentation quality by transferring information from the encoder to the decoder.

### Models Evaluated

Various segmentation models, including encoder-decoder architectures, were evaluated. Here are the results:

| Model                          | Training Loss | Validation Loss | Pixel Accuracy | Jaccard Index | Dice Loss |
|--------------------------------|---------------|-----------------|----------------|---------------|-----------|
| **U-Net**                      | 0.3204        | 0.4330          | 0.8568         | 0.4900        | 0.1043    |
| **U-Net++**                    | 0.2258        | 0.3454          | 0.8850         | 0.5198        | 0.0517    |
| **PAN**                        | 0.1392        | 0.3283          | 0.8653         | 0.4949        | 0.0474    |
| **DeepLabV3**                  | 0.1814        | 0.2608          | 0.9002         | 0.6005        | 0.1261    |
| **DeepLabV3+**                 | 0.7743        | 0.3941          | 0.8864         | 0.5348        | 0.0799    |

### Encoder-Decoder Architectures Results

| Model                          | Training Loss | Validation Loss | Pixel Accuracy | Jaccard Index | Dice Loss |
|--------------------------------|---------------|-----------------|----------------|---------------|-----------|
| **U-Net Encoder-Decoder**      | 0.1875        | 0.2830          | 0.9148         | 0.6787        | 0.3574    |
| **U-Net++ Encoder-Decoder**    | 0.1334        | 0.2631          | 0.9183         | 0.6890        | 0.3780    |
| **PAN Encoder-Decoder**        | 0.6389        | 0.4001          | 0.8764         | 0.5776        | 0.1551    |
| **DeepLabV3 Encoder-Decoder**  | 0.1769        | 0.3259          | 0.8996         | 0.6211        | 0.2422    |
| **DeepLabV3+ Encoder-Decoder** | 0.1819        | 0.2228          | 0.9235         | 0.6999        | 0.3998    |
