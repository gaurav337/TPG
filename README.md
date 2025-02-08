# Helicopter Detection using PyTorch

This repository contains code for detecting military helicopter models using computer vision techniques, particularly bounding box detection with deep learning. The dataset used consists of images of various helicopters, with each image annotated with bounding boxes that correspond to the helicopter's location.

The goal of this project is to train a model that can classify and detect different types of helicopters in an image, including both friendly and enemy models.

## Table of Contents

- [Technologies Used](#technologies-used)
- [Dataset](#dataset)
- [Setup Instructions](#setup-instructions)
- [Code Explanation](#code-explanation)
  - [1. Installing Dependencies](#1-installing-dependencies)
  - [2. Configuration](#2-configuration)
  - [3. Data Preprocessing](#3-data-preprocessing)
  - [4. Data Augmentation](#4-data-augmentation)
  - [5. Model Setup](#5-model-setup)
  - [6. Training](#6-training)
- [How to Run](#how-to-run)
- [License](#license)

## Technologies Used

- **Python**: Programming language used.
- **PyTorch**: Deep learning framework for model training.
- **Pandas**: Used for reading and manipulating CSV files.
- **OpenCV**: Used for image processing.
- **Matplotlib**: Used for data visualization and plotting images.
- **Albumentations**: For data augmentation during training.
- **Kaggle**: For downloading the dataset from Kaggle.

## Dataset

The dataset used in this project is the **Military Aircraft Detection Dataset**, which can be found on Kaggle. It contains images of different types of military helicopters, with annotated bounding boxes indicating the position of helicopters in the image. The dataset can be accessed using the Kaggle API.

### Downloading Dataset

1. Create a Kaggle account and generate an API token from the [Kaggle website](https://www.kaggle.com).
2. Place the `kaggle.json` file in the root directory of the project.
3. Run the following command to download the dataset:
   
   ```bash
   !kaggle datasets download -d a2015003713/militaryaircraftdetectiondataset
   !unzip militaryaircraftdetectiondataset.zip -d dataset
   ```

## Setup Instructions

1. Clone the repository to your local machine:
   ```bash
   git clone <repo_url>
   cd <repo_folder>
   ```

2. Install the required dependencies:
   ```bash
   pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu117
   pip install pandas opencv-python matplotlib seaborn albumentations
   ```

3. Set up Kaggle API credentials:
   ```bash
   mkdir ~/.kaggle
   cp kaggle.json ~/.kaggle/
   chmod 600 ~/.kaggle/kaggle.json
   ```

4. Download and unzip the dataset as mentioned above.

## Code Explanation

### 1. Installing Dependencies

The project uses several libraries for model training, data preprocessing, and data augmentation. They are installed using `pip`:

```bash
!pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu117
!pip install pandas opencv-python matplotlib seaborn albumentations
```

- `torch`, `torchvision`, and `torchaudio` are PyTorch libraries for deep learning, computer vision, and audio processing, respectively.
- `pandas` is used for handling data in CSV format.
- `opencv-python` is used for image processing.
- `matplotlib` is used for visualization.
- `albumentations` is used for data augmentation during model training.

### 2. Configuration

Configuration settings are loaded from a `config.yaml` file. If the file is not found, default settings are used. The configuration contains paths, model parameters, learning rates, and other hyperparameters.

Example configuration:
```yaml
dataset_path: '/content/dataset'
model_save_path: 'models/best_model.pth'
checkpoint_path: 'models/checkpoint_epoch_{epoch}.pth'
detection_threshold: 0.8
friendly_models: ['AH64', 'CH47', 'SH60']
enemy_models: ['Mi28', 'Ka52', 'другие']
num_epochs: 10
batch_size: 4
learning_rate: 0.005
step_size_lr_scheduler: 3
gamma_lr_scheduler: 0.1
```

### 3. Data Preprocessing

- The CSV files containing the bounding box annotations are read into a DataFrame using `pandas`.
- Missing images are checked and logged into a file called `missing_images.txt`.
- The class distribution is visualized as a bar chart using `matplotlib`.

### 4. Data Augmentation

Data augmentation is performed using the **Albumentations** library to improve model generalization. These augmentations can include random rotations, flips, and color adjustments.

```python
transform = A.Compose([
    A.Resize(224, 224),
    A.RandomBrightnessContrast(),
    A.HorizontalFlip(),
    ToTensorV2()
])
```

### 5. Model Setup

The model setup part of the code is missing in this notebook, but typically it would involve setting up a convolutional neural network (CNN) architecture using `torchvision.models` for object detection tasks like Faster R-CNN, SSD, or YOLO. The final model would include a classification head to detect different helicopter models.

### 6. Training

The training process would involve:
- Splitting the data into training and validation sets.
- Defining a loss function (e.g., `CrossEntropyLoss` for classification).
- Using an optimizer like `Adam` to update the model's weights.
- Implementing a learning rate scheduler to decrease the learning rate over time.

```python
train_df, val_df = train_test_split(combined_df, test_size=0.2, random_state=42, stratify=combined_df['class'])
```

## How to Run

1. After setting up the environment, downloading the dataset, and configuring the paths, run the following commands to preprocess the data, visualize the samples, and begin model training.

   ```python
   # Plotting random samples with bounding boxes
   plot_random_samples(combined_df, num_samples=10)
   
   # Start model training here (not implemented in the provided code)
   ```

2. The model will train based on the provided configuration, saving the best model and checkpoints periodically.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
