# Network Security ML Project

## Overview

This project aims to develop a machine learning pipeline for network security data analysis. It leverages various tools and frameworks to facilitate data ingestion, model training, evaluation, and deployment. The core functionalities include data extraction, transformation, loading (ETL), model training, and inference, along with integrated logging and error handling mechanisms.

## Table of Contents

- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [ETL Pipeline](#etl-pipeline)
- [Model Training and Evaluation](#model-training-and-evaluation)
- [Deployment](#deployment)
- [MLflow Integration](#mlflow-integration)
- [DagsHub Usage](#dagshub-usage)
- [Usage](#usage)
- [Logging and Error Handling](#logging-and-error-handling)
- [Future Improvements](#future-improvements)

## Technologies Used

- **Python**: The primary programming language for implementing the project.
- **FastAPI**: A modern web framework for building APIs with Python.
- **Pandas**: For data manipulation and analysis.
- **NumPy**: For numerical operations on arrays.
- **PyMongo**: For interacting with MongoDB, the database used to store data.
- **Scikit-learn**: For building and evaluating machine learning models.
- **MLflow**: For tracking experiments, packaging code into reproducible runs, and sharing models.
- **DagsHub**: For version control of datasets, models, and experiments.
- **Certifi**: For SSL certificate verification with MongoDB connections.
- **YAML**: For configuration management.



## Installation

To set up the project, follow these steps:

1. Clone the repository:
   ```bash
   git clone https://github.com/dineshramv13/networksecurity
   cd networksecurity
   ```

2. Create a virtual environment:
   ```bash
   conda create -p venv python==3.10
   conda activate venv  
   ```

3. Install the required packages:
   ```bash
   pip install -r requirements.txt
   ```

4. Set up environment variables:
   - Create a `.env` file in the root directory and add your MongoDB connection string:
     ```plaintext
     MONGODB_URL_KEY=<your_mongodb_connection_string>
     ```

## ETL Pipeline

The project implements an ETL (Extract, Transform, Load) pipeline to handle data efficiently:

1. **Extract**: Data is extracted from CSV files using Pandas. The `push_data.py` script reads the data and converts it into a JSON format suitable for MongoDB.
   
2. **Transform**: The data is preprocessed to remove inconsistencies and prepare it for analysis. This include data cleaning, feature selection, and normalization.

3. **Load**: The transformed data is inserted into MongoDB for further analysis and model training. The `insert_data_mongodb` method in `push_data.py` handles the insertion of records into the specified database and collection.


## Model Training and Evaluation

The machine learning models are trained using the `TrainingPipeline` class found in `pipeline/training_pipeline.py`. Key steps include:

- Splitting the data into training and testing sets.
- Using various models from Scikit-learn for training.
- Hyperparameter tuning is performed using `GridSearchCV` to optimize model performance.
- The models are evaluated using metrics like R² score to assess their accuracy.

## Deployment

The FastAPI application is structured to handle requests for model training and predictions. 

- **Training Route**: 
  The `/train` endpoint triggers the training pipeline, which loads data, trains models, and evaluates their performance.

- **Prediction Route**: 
  The `/predict` endpoint accepts CSV file uploads, preprocesses the data, makes predictions using the trained model, and returns the results in an HTML table format.

## MLflow Integration

MLflow is used to track experiments, log metrics, and manage models throughout the machine learning lifecycle:

- **Tracking Experiments**: 
  MLflow captures parameters, metrics, and artifacts during the model training phase, allowing for easy comparison and reproducibility.

- **Model Registry**: 
  After training, models can be registered in MLflow, making it easier to manage different versions of the models and streamline the deployment process.

### How to Use MLflow

1. **Start the MLflow UI**:
   ```bash
   mlflow ui
   ```
   Navigate to `http://localhost:5000` to view logged experiments.


## DagsHub Usage

DagsHub is utilized for version control of datasets and models, offering a collaborative environment for data scientists:

- **Dataset Versioning**: 
  DagsHub allows tracking changes to datasets, ensuring that all team members work with the latest data.

- **Experiment Tracking**: 
  DagsHub integrates with MLflow, enabling seamless tracking of experiments and model versions, facilitating collaborative development.

- **Collaboration**: 
  Team members can review, comment on, and improve models and datasets through DagsHub's interface.

## Usage

To run the FastAPI application, use the command:

```bash
uvicorn app:app --reload
```

You can access the API documentation at `http://localhost:8000/docs`.

### Training the Model
Send a GET request to the `/train` endpoint to initiate the training process.

### Making Predictions
Send a POST request to the `/predict` endpoint with a CSV file to receive predictions.

## Logging and Error Handling

The project implements logging using Python's logging module to capture important events and errors throughout the application. 

- **Custom Exceptions**: 
  The `NetworkSecurityException` class is defined to handle exceptions uniformly across the application.

- **Logging Levels**: 
  Logs are categorized into different levels (INFO, ERROR) to facilitate debugging and monitoring.

## Future Improvements

- Implement more advanced model evaluation metrics and visualizations.
- Enhance the ETL pipeline to include more data sources and types.
- Develop a user-friendly front-end interface for better interaction with the machine learning models.
- Incorporate more robust error handling and validation checks throughout the application.

## Conclusion

This project serves as a comprehensive example of a machine learning pipeline in the context of network security. By utilizing various tools and frameworks, the project effectively manages data workflows, model training, and deployment, providing valuable insights into network security analytics.
