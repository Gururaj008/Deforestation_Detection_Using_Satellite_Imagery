# 🌿 Deforestation Detection Using Satellite Imagery

A machine learning project leveraging U-Net for semantic segmentation to identify deforestation from satellite imagery.
Project Overview

This project aims to detect deforestation using satellite imagery, specifically focusing on changes in tree cover over time. It employs a U-Net convolutional neural network (CNN) for semantic segmentation, a powerful technique for pixel-level classification. The project includes data loading, preprocessing, model training, and comprehensive evaluation of the detection performance.

The core idea is to compare 'first' and 'last' year tree cover data from satellite images with 'lossyear' data (ground truth) to train a model that can accurately identify areas where tree cover has been lost.
Features

    Data Handling: Efficient loading and processing of large GeoTIFF satellite imagery files using rasterio.

    Streaming Evaluation: A streaming approach for evaluating deforestation detection across large rasters, minimizing memory usage.

    U-Net Architecture: Implementation of a U-Net model for robust semantic segmentation of deforestation areas.

    Custom Dataset & DataLoader: PyTorch Dataset and DataLoader for handling satellite image patches during training.

    Training Loop: A complete training pipeline with loss calculation (BCEWithLogitsLoss with class weighting) and optimization (Adam).

    Model Evaluation: Comprehensive evaluation metrics including Accuracy, Precision, Recall, F1-Score, IoU, and Dice Coefficient.

    Threshold Experimentation: Ability to evaluate U-Net model performance across various prediction thresholds.

Getting Started
Prerequisites

Before running the code, ensure you have the following installed:

pip install numpy rasterio matplotlib seaborn scikit-learn torch torchvision

It is highly recommended to use a virtual environment for dependency management.
Data Acquisition

This project uses satellite imagery data. You will need to obtain 'first' year tree cover, 'last' year tree cover, and 'lossyear' GeoTIFF (.tif) files. These files are typically named following a convention like:

    Hansen_GFC-YYYY-vX.Y_first_NNN_EEE.tif (e.g., Hansen_GFC-2019-v1.7_first_30N_070E.tif)

    Hansen_GFC-YYYY-vX.Y_last_NNN_EEE.tif (e.g., Hansen_GFC-2019-v1.7_last_30N_070E.tif)

    Hansen_GFC-YYYY-vX.Y_lossyear_NNN_EEE.tif (e.g., Hansen_GFC-2019-v1.7_lossyear_30N_070E.tif)

    Hansen_GFC-YYYY-vX.Y_treecover2000_NNN_EEE.tif (for U-Net input, e.g., Hansen_GFC-2019-v1.7_treecover2000_30N_070E.tif)

Place all these .tif files in a single directory.
Project Structure

The main logic is contained within the provided Jupyter Notebook:

.
├── Deforestation_Detection_Using_Satellite_Imagery.ipynb
└── GFC_Files/
    ├── Hansen_GFC-2019-v1.7_first_30N_070E.tif
    ├── Hansen_GFC-2019-v1.7_last_30N_070E.tif
    ├── Hansen_GFC-2019-v1.7_lossyear_30N_070E.tif
    ├── Hansen_GFC-2019-v1.7_treecover2000_30N_070E.tif
    └── ... (other .tif files)

Note: You will need to create the GFC_Files directory and place your downloaded satellite imagery data inside it.
Configuration

Open the Deforestation_Detection_Using_Satellite_Imagery.ipynb notebook.

Update the file_path and data_root_dir variables:

# For initial evaluation function
file_path = r"C:/Users/Maverick/Downloads/GFC_Files" # <-- Update this path

# For U-Net training and evaluation
data_root_dir = r"C:/Users/Maverick/Downloads/GFC_Files" # <-- Update this path

Ensure these paths correctly point to the directory where you have stored your .tif files.
Running the Code

Execute the cells in the Jupyter Notebook sequentially:

    Import Libraries: Imports all necessary Python libraries.

    Set File Path and Discover All Relevant Data: Identifies and pairs the 'first', 'last', and 'lossyear' files for initial evaluation.

    Define Evaluation Function (Streaming Metrics): Defines a function to evaluate deforestation detection using a streaming approach, suitable for large files.

    Run Evaluation for All Data: Executes the streaming evaluation and prints aggregated metrics (Accuracy, Precision, Recall, F1-Score) and a confusion matrix plot.

    Define Evaluation Metrics (IoU, Dice): Defines additional metrics for U-Net evaluation.

    U-Net Architecture: Defines the U-Net model structure.

    Custom Dataset: Implements a custom PyTorch Dataset for loading image and mask patches.

    Model Training Setup: Prepares data loaders, calculates class weights, and initializes the U-Net model, optimizer, and loss function.

    Training Loop: Trains the U-Net model over a specified number of epochs, including a validation phase. The trained model is saved.

    U-Net Model-Based Evaluation Function: Defines a function to evaluate the trained U-Net model.

    Run U-Net Model-Based Evaluation: Loads the trained model and evaluates its performance across various prediction thresholds, printing detailed metrics for each.

Results & Metrics

The notebook will output various metrics at different stages:

    Initial Evaluation: Provides overall Accuracy, Precision, Recall, and F1-Score based on a simple thresholding of 'first' vs. 'last' year tree cover against 'lossyear' data. A confusion matrix plot will also be generated.

    U-Net Training: Displays training and validation loss, IoU, and Dice scores per epoch.

    U-Net Model Evaluation: Shows aggregated TP, FP, TN, FN counts, and calculated Accuracy, Precision, Recall, and F1-Score for the U-Net model at different prediction thresholds. This helps in understanding the model's performance trade-offs.

Contributing

Contributions are welcome! If you have suggestions for improvements, new features, or bug fixes, please open an issue or submit a pull request.
License

