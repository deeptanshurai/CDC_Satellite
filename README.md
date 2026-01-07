Satellite Imagery-Based Property Valuation
A multimodal deep learning system that predicts property market values by combining tabular features with satellite imagery to capture environmental context and neighborhood characteristics.

Overview
This project enhances traditional property valuation by incorporating visual environmental context through satellite imagery. The system captures factors like green cover, road networks, proximity to water bodies, and urban density patterns.

Dataset
Tabular Data
Training Set: train.xlsx
Test Set: test.xlsx
Key Features: price (target), bedrooms, bathrooms, sqft_living, lat, long
Visual Data
Satellite images acquired using Mapbox Static API
Image specifications: 256x256 pixels, zoom level 18
Coverage: Satellite view for each property location
Project Structure
GitHub Repository:
├── data_fetcher.py              # Script to download satellite images
├── preprocessing.ipynb          # Data cleaning, image acquisition, feature engineering
├── model_training.ipynb         # Model training and evaluation
└── README.md                    # Project documentation

Google Drive Structure:
Property_Valuation_Project/
├── data/                        # Raw and processed datasets
├── images/                      # Satellite imagery
│   ├── train/
│   └── test/
├── models/                      # Saved model files
└── results/                     # Outputs and visualizations
    ├── predictions.csv
    ├── all_models_comparison.csv
    └── visualizations/
Setup
Google Colab Environment
This project runs entirely in Google Colab. No local installation required.


Step 1: Data Preprocessing
Open and run preprocessing.ipynb:

Load training and test datasets
Fetch satellite images using Mapbox Static API
Clean data and handle missing values
Perform exploratory data analysis
Create train/validation split (80/20)
Scale numerical features
Save all processed data and images to Drive
Step 2: Model Training
Open and run model_training.ipynb:

Load preprocessed data and images from Drive

Train baseline models:

Linear Regression
Random Forest
XGBoost
Extract image features using pre-trained CNN (VGG16/ResNet50)

Train multimodal models:

Early Fusion: Concatenate features before processing
Late Fusion: Separate pathways merged at end
Hybrid Fusion: Multiple fusion points
Evaluate and compare all models using RMSE, R2, MAE

Generate Grad-CAM visualizations for explainability

Save trained models, predictions, and visualizations to Drive

Since all progress is stored in Drive, you can:

Resume from any checkpoint
Skip already completed steps
Load pre-trained models for quick predictions
Access results from previous runs
Model Architectures
Baseline Models
Use only tabular features (bedrooms, bathrooms, sqft, location, etc.)

Multimodal Models
Combine tabular features with image features

Early Fusion: Concatenate all features at input level

Late Fusion: Process separately, combine at output

Hybrid Fusion: Multiple fusion points in network

Drive Structure
data/
train.xlsx: Original training data
test.xlsx: Original test data
train_processed.csv: Cleaned training data
test_processed.csv: Cleaned test data
images/
train/: Training property images
test/: Test property images
models/
early_fusion_model.h5
late_fusion_model.h5
hybrid_fusion_model.h5
random_forest_model.pkl
xgboost_model.pkl
results/
predictions.csv: Final predictions (id, predicted_price)
all_models_comparison.csv: Performance metrics
visualizations/: Training history, comparisons, Grad-CAM
Technologies
Google Colab: Development environment
TensorFlow/Keras: Deep learning
Scikit-learn: Baseline models
XGBoost: Gradient boosting
Pandas, NumPy: Data processing
Matplotlib, Seaborn: Visualization
OpenCV, PIL: Image processing
Mapbox Static API: Satellite image acquisition

