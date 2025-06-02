<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🌿 Deforestation Detection Using Satellite Imagery</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f0f4f8;
            color: #334155;
            line-height: 1.6;
        }
        .container {
            max-width: 960px;
            margin: 2rem auto;
            padding: 2rem;
            background-color: #ffffff;
            border-radius: 0.75rem;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
        }
        h1, h2, h3, h4 {
            color: #1e293b;
            font-weight: 700;
        }
        h1 {
            font-size: 2.5rem;
            margin-bottom: 1.5rem;
            text-align: center;
        }
        h2 {
            font-size: 2rem;
            margin-top: 2rem;
            margin-bottom: 1rem;
            border-bottom: 2px solid #e2e8f0;
            padding-bottom: 0.5rem;
        }
        h3 {
            font-size: 1.5rem;
            margin-top: 1.5rem;
            margin-bottom: 0.75rem;
        }
        code {
            background-color: #e2e8f0;
            padding: 0.2em 0.4em;
            border-radius: 0.25rem;
            font-family: 'Fira Code', 'Cascadia Code', monospace;
            font-size: 0.9em;
        }
        pre {
            background-color: #1a202c;
            color: #e2e8f0;
            padding: 1rem;
            border-radius: 0.5rem;
            overflow-x: auto;
            font-family: 'Fira Code', 'Cascadia Code', monospace;
            font-size: 0.9em;
            margin-bottom: 1.5rem;
        }
        a {
            color: #3b82f6;
            text-decoration: none;
        }
        a:hover {
            text-decoration: underline;
        }
        ul {
            list-style-type: disc;
            margin-left: 1.5rem;
            margin-bottom: 1rem;
        }
        ol {
            list-style-type: decimal;
            margin-left: 1.5rem;
            margin-bottom: 1rem;
        }
        .badge {
            display: inline-block;
            padding: 0.25rem 0.75rem;
            border-radius: 9999px;
            font-size: 0.875rem;
            font-weight: 600;
            margin-right: 0.5rem;
            margin-bottom: 0.5rem;
        }
        .badge-python { background-color: #3b82f6; color: white; }
        .badge-pytorch { background-color: #ef4444; color: white; }
        .badge-gis { background-color: #10b981; color: white; }
        .badge-ml { background-color: #8b5cf6; color: white; }
        .header-icon {
            vertical-align: middle;
            margin-right: 0.5rem;
        }
    </style>
</head>
<body class="p-4">
    <div class="container">
        <h1 class="text-blue-700">
            <span class="header-icon">🌿</span> Deforestation Detection Using Satellite Imagery
        </h1>

        <p class="text-center text-lg text-gray-600 mb-8">
            A machine learning project leveraging U-Net for semantic segmentation to identify deforestation from satellite imagery.
        </p>

        <div class="flex flex-wrap justify-center mb-8">
            <span class="badge badge-python">Python</span>
            <span class="badge badge-pytorch">PyTorch</span>
            <span class="badge badge-gis">GIS</span>
            <span class="badge badge-ml">Machine Learning</span>
            <span class="badge badge-ml">U-Net</span>
            <span class="badge badge-ml">Semantic Segmentation</span>
        </div>

        <h2>Project Overview</h2>
        <p>
            This project aims to detect deforestation using satellite imagery, specifically focusing on changes in tree cover over time. It employs a U-Net convolutional neural network (CNN) for semantic segmentation, a powerful technique for pixel-level classification. The project includes data loading, preprocessing, model training, and comprehensive evaluation of the detection performance.
        </p>
        <p>
            The core idea is to compare 'first' and 'last' year tree cover data from satellite images with 'lossyear' data (ground truth) to train a model that can accurately identify areas where tree cover has been lost.
        </p>

        <h2>Features</h2>
        <ul>
            <li><strong>Data Handling:</strong> Efficient loading and processing of large GeoTIFF satellite imagery files using <code>rasterio</code>.</li>
            <li><strong>Streaming Evaluation:</strong> A streaming approach for evaluating deforestation detection across large rasters, minimizing memory usage.</li>
            <li><strong>U-Net Architecture:</strong> Implementation of a U-Net model for robust semantic segmentation of deforestation areas.</li>
            <li><strong>Custom Dataset & DataLoader:</strong> PyTorch <code>Dataset</code> and <code>DataLoader</code> for handling satellite image patches during training.</li>
            <li><strong>Training Loop:</strong> A complete training pipeline with loss calculation (BCEWithLogitsLoss with class weighting) and optimization (Adam).</li>
            <li><strong>Model Evaluation:</strong> Comprehensive evaluation metrics including Accuracy, Precision, Recall, F1-Score, IoU, and Dice Coefficient.</li>
            <li><strong>Threshold Experimentation:</strong> Ability to evaluate U-Net model performance across various prediction thresholds.</li>
        </ul>

        <h2>Getting Started</h2>

        <h3>Prerequisites</h3>
        <p>
            Before running the code, ensure you have the following installed:
        </p>
        <pre><code>
pip install numpy rasterio matplotlib seaborn scikit-learn torch torchvision
        </code></pre>
        <p>
            It is highly recommended to use a virtual environment for dependency management.
        </p>

        <h3>Data Acquisition</h3>
        <p>
            This project uses satellite imagery data. You will need to obtain 'first' year tree cover, 'last' year tree cover, and 'lossyear' GeoTIFF (.tif) files. These files are typically named following a convention like:
        </p>
        <ul>
            <li><code>Hansen_GFC-YYYY-vX.Y_first_NNN_EEE.tif</code> (e.g., <code>Hansen_GFC-2019-v1.7_first_30N_070E.tif</code>)</li>
            <li><code>Hansen_GFC-YYYY-vX.Y_last_NNN_EEE.tif</code> (e.g., <code>Hansen_GFC-2019-v1.7_last_30N_070E.tif</code>)</li>
            <li><code>Hansen_GFC-YYYY-vX.Y_lossyear_NNN_EEE.tif</code> (e.g., <code>Hansen_GFC-2019-v1.7_lossyear_30N_070E.tif</code>)</li>
            <li><code>Hansen_GFC-YYYY-vX.Y_treecover2000_NNN_EEE.tif</code> (for U-Net input, e.g., <code>Hansen_GFC-2019-v1.7_treecover2000_30N_070E.tif</code>)</li>
        </ul>
        <p>
            Place all these <code>.tif</code> files in a single directory.
        </p>

        <h3>Project Structure</h3>
        <p>
            The main logic is contained within the provided Jupyter Notebook:
        </p>
        <pre><code>
.
├── Deforestation_Detection_Using_Satellite_Imagery.ipynb
└── GFC_Files/
    ├── Hansen_GFC-2019-v1.7_first_30N_070E.tif
    ├── Hansen_GFC-2019-v1.7_last_30N_070E.tif
    ├── Hansen_GFC-2019-v1.7_lossyear_30N_070E.tif
    ├── Hansen_GFC-2019-v1.7_treecover2000_30N_070E.tif
    └── ... (other .tif files)
        </code></pre>
        <p>
            <strong>Note:</strong> You will need to create the <code>GFC_Files</code> directory and place your downloaded satellite imagery data inside it.
        </p>

        <h3>Configuration</h3>
        <p>
            Open the <code>Deforestation_Detection_Using_Satellite_Imagery.ipynb</code> notebook.
        </p>
        <p>
            <strong>Update the <code>file_path</code> and <code>data_root_dir</code> variables:</strong>
        </p>
        <pre><code class="language-python">
# For initial evaluation function
file_path = r"C:/Users/Maverick/Downloads/GFC_Files" # &lt;-- Update this path

# For U-Net training and evaluation
data_root_dir = r"C:/Users/Maverick/Downloads/GFC_Files" # &lt;-- Update this path
        </code></pre>
        <p>
            Ensure these paths correctly point to the directory where you have stored your <code>.tif</code> files.
        </p>

        <h3>Running the Code</h3>
        <p>
            Execute the cells in the Jupyter Notebook sequentially:
        </p>
        <ol>
            <li><strong>Import Libraries:</strong> Imports all necessary Python libraries.</li>
            <li><strong>Set File Path and Discover All Relevant Data:</strong> Identifies and pairs the 'first', 'last', and 'lossyear' files for initial evaluation.</li>
            <li><strong>Define Evaluation Function (Streaming Metrics):</strong> Defines a function to evaluate deforestation detection using a streaming approach, suitable for large files.</li>
            <li><strong>Run Evaluation for All Data:</strong> Executes the streaming evaluation and prints aggregated metrics (Accuracy, Precision, Recall, F1-Score) and a confusion matrix plot.</li>
            <li><strong>Define Evaluation Metrics (IoU, Dice):</strong> Defines additional metrics for U-Net evaluation.</li>
            <li><strong>U-Net Architecture:</strong> Defines the U-Net model structure.</li>
            <li><strong>Custom Dataset:</strong> Implements a custom PyTorch Dataset for loading image and mask patches.</li>
            <li><strong>Model Training Setup:</strong> Prepares data loaders, calculates class weights, and initializes the U-Net model, optimizer, and loss function.</li>
            <li><strong>Training Loop:</strong> Trains the U-Net model over a specified number of epochs, including a validation phase. The trained model is saved.</li>
            <li><strong>U-Net Model-Based Evaluation Function:</strong> Defines a function to evaluate the trained U-Net model.</li>
            <li><strong>Run U-Net Model-Based Evaluation:</strong> Loads the trained model and evaluates its performance across various prediction thresholds, printing detailed metrics for each.</li>
        </ol>

        <h2>Results & Metrics</h2>
        <p>
            The notebook will output various metrics at different stages:
        </p>
        <ul>
            <li><strong>Initial Evaluation:</strong> Provides overall Accuracy, Precision, Recall, and F1-Score based on a simple thresholding of 'first' vs. 'last' year tree cover against 'lossyear' data. A confusion matrix plot will also be generated.</li>
            <li><strong>U-Net Training:</strong> Displays training and validation loss, IoU, and Dice scores per epoch.</li>
            <li><strong>U-Net Model Evaluation:</strong> Shows aggregated TP, FP, TN, FN counts, and calculated Accuracy, Precision, Recall, and F1-Score for the U-Net model at different prediction thresholds. This helps in understanding the model's performance trade-offs.</li>
        </ul>

        <h2>Contributing</h2>
        <p>
            Contributions are welcome! If you have suggestions for improvements, new features, or bug fixes, please open an issue or submit a pull request.
        </p>

       
    </div>
</body>
</html>
