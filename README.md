# Amazon SageMaker ML Project

An end-to-end machine learning project using **Amazon SageMaker** to train and deploy a **Random Forest classification model** for mobile price range prediction.

The project follows a code-driven approach using Python, AWS SDKs, and SageMaker.

## Project Workflow

Data  
↓  
Data Preparation  
↓  
Upload to Amazon S3  
↓  
SageMaker Training  
↓  
Model Artifact  
↓  
SageMaker Endpoint  
↓  
Prediction  
↓  
Endpoint Cleanup  

## Technologies Used

- Python
- Amazon SageMaker
- Amazon S3
- AWS CLI
- Boto3
- Scikit-learn
- Pandas
- Conda
- VS Code

## Project Steps

### 1. AWS Setup

Configure the AWS CLI with appropriate IAM credentials and create an S3 bucket for storing datasets and model artifacts.

### 2. Data Preparation

The project uses a **mobile price classification dataset**.

The data is:

- Loaded using Pandas
- Checked for missing values
- Split into features (`X`) and target (`Y`)
- Divided into training and testing datasets
- Saved as CSV files

Example:
train_v1.csv
test_v1.csv

### 3. Upload Data to S3

The processed datasets are uploaded to Amazon S3 using Boto3 and SageMaker.

Example S3 prefix:
sagemaker/mobile_price_classification/sklearn_container/

### 4. Model Training

A script.py training script reads the data from S3 and trains a Random Forest Classifier using Scikit-learn.

The SageMaker SKLearn estimator is configured with:
Training instance: ml.m5.large
Number of estimators: 100
Random state: 0

The training job is started using:
estimator.fit(...)
The trained model artifact is automatically stored in S3.

### 5. Model Deployment

The trained model is deployed as a SageMaker real-time endpoint.

Predictions can be generated using:
predictor.predict(input_data)

### 6. Cleanup

SageMaker endpoints can incur costs while running. After testing, delete the endpoint:
predictor.delete_endpoint()

### Requirements

Install the required Python packages:
pip install -r requirements.txt