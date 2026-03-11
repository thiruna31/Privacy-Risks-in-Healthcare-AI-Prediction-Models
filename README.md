Secure Private AI – Healthcare Prediction System

Team 8 – The Secure Minds
Thirunavukkarasu Palaniappa & Victor Lam

Project Overview

This project focuses on building a healthcare risk prediction system using machine learning while studying the privacy risks associated with machine learning models. Healthcare datasets often contain sensitive patient information, and models trained on such data may unintentionally leak information about individuals.

The goal of our project is to first build a baseline AI prediction system that estimates the likelihood of heart disease based on patient health features. In later stages of the project, we will investigate how machine learning models may leak information through membership inference attacks, and evaluate defense strategies to mitigate these privacy risks.

This repository contains the initial AI system foundation used for Checkpoint 1 of the project.

Dataset

The system uses the UCI Heart Disease Dataset, which contains clinical health measurements from patients.

Example features in the dataset include:

Age

Sex

Chest pain type

Resting blood pressure

Cholesterol level

Maximum heart rate achieved

Exercise-induced angina

ST depression induced by exercise

Number of major vessels colored by fluoroscopy

The original dataset contains a diagnosis column called num, where:

num value	Meaning
0	No heart disease
1–4	Presence of heart disease

For the purposes of this project, the diagnosis was converted into a binary classification problem:

target = 0 → No heart disease
target = 1 → Heart disease present
System Architecture

The current system implements a machine learning prediction pipeline for healthcare risk prediction.

Heart Disease Dataset
        ↓
Data Preprocessing
        ↓
Feature Encoding (categorical variables)
        ↓
Handling Missing Values
        ↓
Train/Test Dataset Split
        ↓
Feature Scaling
        ↓
Logistic Regression Prediction Model
        ↓
Heart Disease Prediction
        ↓
Prediction Probabilities

This architecture forms the foundation of the final secure AI system.

Data Preprocessing

Before training the machine learning model, several preprocessing steps were applied to prepare the dataset.

1. Handling Missing Values

Some columns in the dataset contain missing values. These were handled by replacing missing entries with default values to allow the model to train properly.

2. Encoding Categorical Features

Certain features such as chest pain type or sex are categorical. These were converted into numerical features using one-hot encoding.

Example transformation:

sex	cp
Male	asymptomatic

becomes

sex_Male	cp_asymptomatic
1	1

This ensures the machine learning model can process all features numerically.

3. Train-Test Split

The dataset was divided into two subsets:

80% Training Data – used to train the model

20% Testing Data – used to evaluate the model

This ensures that the model is evaluated on unseen data, which better reflects real-world performance.

4. Feature Scaling

Different medical features have different ranges. For example:

Feature	Example Value
Age	63
Cholesterol	250

To ensure consistent learning, the features were normalized using StandardScaler, which standardizes the data distribution.

Prediction Model

The prediction model used in this baseline system is Logistic Regression.

Logistic regression is widely used in healthcare prediction tasks because:

It performs well for binary classification problems

It provides interpretable results

It outputs prediction probabilities, which are important for later security analysis

The model learns relationships between patient health features and the presence of heart disease.

Example concept:

Patient Health Features → Disease Risk Probability
Model Output

The trained model produces two outputs:

1. Predicted Class

The model predicts whether a patient is likely to have heart disease.

Example prediction output:

[0 0 1 1 0 0 1]

Where:

0 → No heart disease
1 → Heart disease predicted
2. Prediction Probabilities

The model also outputs probability scores for each prediction.

Example:

[[0.96 0.03]
 [0.92 0.07]
 [0.06 0.93]]

This represents:

Probability No Disease	Probability Disease
0.96	0.03
0.92	0.07
0.06	0.93

These probabilities are important for the next stage of the project, where we will evaluate whether attackers can infer if a specific data record was used during training.

Baseline Results

Using the current preprocessing pipeline and logistic regression model, the system achieved the following baseline performance:

Model Accuracy: ~84.8%

This result aligns with reported performance for the UCI Heart Disease dataset and provides a strong baseline for future experimentation.

Current Working Components

The following components of the system are currently implemented and functional:

Dataset loading

Data preprocessing pipeline

Categorical feature encoding

Missing value handling

Train-test dataset split

Feature scaling

Logistic regression model training

Prediction generation

Model evaluation using accuracy

Probability output generation

Future Work

The current system represents the baseline AI prediction system. Future project stages will extend this work by focusing on machine learning security and privacy.

Planned additions include:

Membership Inference Attack

Implement an attack model capable of predicting whether a specific data record was used in the training dataset.

Attack Evaluation

Measure how vulnerable the prediction model is to membership inference attacks.

Defense Mechanisms

Implement defense strategies such as:

Regularization

Model robustness techniques

Privacy vs Performance Analysis

Evaluate the trade-off between model accuracy and privacy protection.

Technologies Used

Python

Scikit-learn

Pandas

NumPy

Google Colab
