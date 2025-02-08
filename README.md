# Guardians of Skies: Military Aircraft Detection System

## Introduction

### Problem Statement

In this grand endeavour, you embody the role of a revered Egyptian Sentinel, entrusted with the protection of the celestial expanse above the sacred lands of Egypt. With the dawn of advanced aerial technology, the skies have become a critical frontier, demanding vigilant surveillance to identify and monitor military helicopters intruding upon Egyptian territory. Your sacred mission is to ensure that only authorized aircraft gain access while swiftly identifying potential threats to the kingdom.

With the wisdom of Thoth and the precision of a falcon's gaze, you must develop a cutting-edge object detection system. This technology will empower you to identify military helicopters with unerring accuracy, becoming your loyal ally in safeguarding Egyptian airspace. Your efforts will maintain the security and sovereignty of the kingdom, honoring the legacy of the ancient gods and protecting the people beneath the vast, eternal sky.

Embark on this journey, Sentinel, and let the skies sing the praises of your unwavering vigilance and unmatched skill. The fate of Egypt rests upon your shoulders.

### Objective

The core objective of this project is to develop an **object detection system** capable of detecting and localizing military helicopters in aerial images. Specifically, the system should be able to:

1. **Detect helicopters**: Identify helicopters from the images.
2. **Draw bounding boxes**: Locate the helicopter in the image with precise bounding boxes.
3. **Classify helicopters**: Categorize helicopters as either **friendly** or **enemy**.
4. **Alerting system**: Trigger an alert if enemy helicopters are detected.

The dataset provided contains labeled helicopter images, categorized into friendly and enemy aircraft. This project will utilize this dataset to train and evaluate a robust model.

### Bonus Objective:
- **Use advanced architectures** (e.g., Faster R-CNN, YOLO, RetinaNet) to further improve the detection accuracy and performance of the system.

### Dataset:
The dataset for this project is hosted on Kaggle and can be accessed [here](https://www.kaggle.com/datasets/a2015003713/militaryaircraftdetectiondataset).

---

## Table of Contents:
- [Introduction](#introduction)
- [Technology Stack](#technology-stack)
- [Problem Statement and Objective](#problem-statement-and-objective)
- [Project Progress](#project-progress)
- [Setup Instructions](#setup-instructions)
- [Usage](#usage)
- [Data Preprocessing](#data-preprocessing)
- [Model Training](#model-training)
- [Evaluation](#evaluation)
- [Contributors](#contributors)
- [Made at](#made-at)
- [License](#license)

---

## Technology Stack:

The project leverages modern computer vision tools and frameworks to build an efficient object detection pipeline:

- **Programming Language**: Python
- **Libraries**:
  - **PyTorch**: Deep learning framework used for training the object detection model.
  - **OpenCV**: For image processing and manipulation.
  - **Albumentations**: For data augmentation to enhance model robustness.
  - **Scikit-learn**: For dataset splitting and evaluation.
  - **Matplotlib/Seaborn**: For data visualization and plotting.
  - **Pandas**: For handling and preprocessing the dataset.
- **Hardware/Environment**:
  - Google Colab (for cloud-based GPU acceleration during training).

---

## Problem Statement and Objective

### Mission: Guardians of Skies

As a guardian of Egypt's airspace, your mission is to build an intelligent system that can detect and classify military helicopters with high precision. The **primary objectives** of the project are as follows:

1. **Helicopter Detection**:
   - Train a deep learning model to identify and detect military helicopters in aerial imagery.

2. **Bounding Box Localization**:
   - Draw bounding boxes around detected helicopters and classify them into two categories: **friendly** or **enemy**.

3. **Alert Mechanism**:
   - Trigger an alert if enemy helicopters are detected in a given aerial image.

4. **Advanced Detection Architectures (Bonus)**:
   - Implement state-of-the-art architectures such as **Faster R-CNN**, **YOLOv5**, or **RetinaNet** to improve detection speed and accuracy.

The dataset provided has images labeled with bounding boxes and class labels, which will be utilized to train and evaluate the detection model. The training process includes:
- **Friendly models** (e.g., AH64, CH47, SH60)
- **Enemy models** (e.g., Mi28, Ka52, другие)

### Dataset Information:
The dataset contains:
- **Images**: A collection of aerial images of helicopters.
- **Annotations**: Each image is annotated with the following data:
  - **Bounding Box Coordinates**: The precise location of the helicopter in the image.
  - **Class**: The model of the helicopter (friendly or enemy).

---

## Project Progress

### What We've Accomplished So Far:

1. **Dataset Setup**:
   - **Downloaded the Dataset**: We have successfully downloaded the dataset from Kaggle, which contains aerial images of military helicopters. The dataset also includes annotation files in CSV format detailing the bounding box coordinates and the class of each helicopter (either friendly or enemy).
   - **Unzipped Dataset**: The dataset was unzipped and stored in a folder for further use in model training.

2. **Data Preprocessing**:
   - **Combined Annotations**: Multiple CSV files containing helicopter annotations have been merged into a single, comprehensive DataFrame.
   - **File Extension Correction**: We ensured that filenames in the annotations have the `.jpg` extension added to match the actual image filenames.
   - **Missing Images Check**: We implemented a system to check for missing images in the dataset. A list of missing images was generated and saved in `missing_images.txt` for further investigation.
   - **Class Distribution Visualization**: A class distribution graph was generated to visually inspect the number of friendly and enemy helicopter images available for training.

3. **Data Augmentation Setup**:
   - **Albumentations Library**: The project now uses **Albumentations** for data augmentation, allowing us to apply random transformations (such as flipping, rotation, scaling) to the images during training. This enhances the model's ability to generalize to unseen data.

4. **Random Image and Annotation Visualization**:
   - **Visualization of Random Samples**: We implemented a function to visualize random images from the dataset along with their bounding box annotations. This confirms that the annotations are accurate and correctly placed around the helicopters.

---

## Setup Instructions:

### Prerequisites:

Ensure that you have Python 3.x installed along with the following dependencies. You can install the necessary packages using the following commands:

```bash
!pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu117
!pip install pandas opencv-python matplotlib seaborn albumentations
```

### Download Dataset:

1. **Kaggle API Setup**: To download the dataset from Kaggle, you need to authenticate using the Kaggle API key. Follow these steps to get your Kaggle API key and authenticate:

   - Create an account on Kaggle (https://www.kaggle.com/).
   - Download the Kaggle API key (`kaggle.json`).
   - Upload the `kaggle.json` file to your project directory.

2. **Download the Dataset**:

```bash
!mkdir ~/.kaggle
!cp kaggle.json ~/.kaggle/
!chmod 600 ~/.kaggle/kaggle.json
!kaggle datasets download -d a2015003713/militaryaircraftdetectiondataset
!unzip militaryaircraftdetectiondataset.zip -d dataset
```

---

## Usage:

### Data Loading & Preprocessing:

1. **Combining CSV Files**:
   - The project loads all CSV files containing helicopter annotations and combines them into a single DataFrame for easier processing.

2. **Missing Image Check**:
   - The dataset is checked for missing images. Any missing images are logged and saved in `missing_images.txt` for further inspection.

3. **Class Distribution**:
   - The project generates a **bar chart** to visualize the distribution of different helicopter models in the dataset.

4. **Bounding Box Visualization**:
   - Random images from the dataset are plotted with bounding boxes around the detected helicopters to ensure annotations are correct.

### Model Training:

- **Data Augmentation**:
   - The model utilizes **Albumentations** for random data augmentations like flipping, rotation, and scaling, which improve the generalization of the model.

- **Model Architecture**:
   - You can experiment with architectures such as **Faster R-CNN**, **YOLOv5**, or **RetinaNet** for the detection task.

- **Training Configuration**:
   - A configuration file (`config.yaml`) stores model hyperparameters, such as:
     - Batch size
     - Learning rate
     - Number of epochs
     - Paths to save the trained model and checkpoints

### Model Evaluation:

- **Precision and Recall**: Evaluate the model’s precision and recall for friendly and enemy classes.
- **Alert Mechanism**: Implement an alert system if an enemy helicopter is detected in an image.
- **Visualization**: Use Matplotlib to visualize model predictions, showing bounding boxes for each detection.

---

## Data Preprocessing:

1. **CSV Parsing**: The project parses CSV annotation files, extracts image filenames, and appends the `.jpg` extension to filenames where necessary.
2. **Splitting Dataset**: The dataset is split into **training** and **validation** sets using Scikit-learn’s `train_test_split`, ensuring a balanced class distribution across both sets.
3. **Image Loading**: Images are loaded using OpenCV and converted to the RGB color format. They are then processed for model input.

---

## Contributors:

**Team Name**: Aura++

- **Gaurav Kumar Jangid**
- **Piyush Kumar**

---

## Made at:
**SVBH, MNNIT**

---

## License:

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

---

**Note**: Ensure that you have the necessary permissions to access and use the dataset from Kaggle. Follow the Kaggle terms and conditions for dataset usage.
