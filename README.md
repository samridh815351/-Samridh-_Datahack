# -Samridh-_Datahack
This method leverages logistic regression within a multioutput classification framework to handle the prediction of two vaccine types simultaneously. The preprocessing steps ensure that the data is clean and properly formatted for model training, and the chunk processing helps manage memory limitations during the prediction phase. 

Problem Overview
The goal is to predict the likelihood of individuals receiving two types of vaccines: the xyz flu vaccine and the seasonal flu vaccine. This is a multilabel classification problem, where each individual can receive both vaccines, just one, or neither. The performance is evaluated using the ROC AUC score for each target variable, and the final score is the mean of these two scores.

Steps to Solve the Problem
Data Loading:

Load the training and test datasets from CSV files.
Data Preprocessing:

Column Separation: Separate the numerical and categorical columns for appropriate processing.
Numerical Transformation: Apply imputation (to fill missing values with the median) and scaling (standardization) to numerical features.
Categorical Transformation: Apply imputation (to fill missing values with the most frequent value) and one-hot encoding (to convert categorical values into binary variables) to categorical features.
Column Transformation: Use ColumnTransformer to apply the transformations to the appropriate columns of the dataset.
Feature Sampling:

Data Reduction: Sample 10% of the training data to reduce memory usage during model training. This step is crucial given the memory constraints observed.
Data Splitting:

Split the sampled training data into training and validation sets to evaluate the model performance.
Model Selection and Training:

Use MultiOutputClassifier with LogisticRegression as the base estimator. This model can handle multiple output labels simultaneously.
Train the model on the training set.
Model Evaluation:

Predict probabilities on the validation set.
Calculate the ROC AUC scores for both target variables.
Compute the mean ROC AUC score as the final evaluation metric.
Prediction on Test Set:

Chunk Processing: Due to memory limitations, process the test data in smaller chunks to avoid memory errors during prediction.
Predict probabilities for each chunk and collect the results.
Submission Preparation:

Combine the predictions for all chunks.
Save the predictions to a CSV file in the required format.
