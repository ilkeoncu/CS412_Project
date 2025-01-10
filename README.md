# CS412_Project
OVERVIEW
This repository contains code and deliverables for an Instagram analytics project, focusing on two main tasks:

1. Influencer Category Classification
2. Like Count Prediction
It includes a final report detailing methodologies and results, as well as JSON outputs for multiple rounds of predictions. Below is a summary of each file’s purpose.

Files
CS412_Final Project Report

A comprehensive document explaining the project’s methodologies, experiments, and results. It covers data preparation, model architectures (e.g., MLP vs. Logistic Regression), evaluation metrics, and findings.
cs412_all_rounds_vFinal.ipynb

The main Jupyter notebook containing all relevant code. It spans multiple rounds of experimentation (Rounds 1–3) for both influencer category classification and like count regression. This notebook shows data preprocessing, TF-IDF, SMOTE implementation, modeling steps, and evaluation plots.
prediction-classification-round*.json

JSON files where each key is a username, and the value is the predicted influencer category label. These files are created for Round 1, Round 2, and Round 3 predictions.
prediction-regression-round*.json

JSON files where each key is a post ID, and the value is the predicted like count. Similarly, there are versions for Round 1, Round 2, and Round 3.
Feel free to explore the report for a deeper understanding of the approach, and refer to the notebook for the end-to-end code that generates these JSON outputs.

SUMMARY
1. Influencer Category Classification
The classification task aimed to categorize Instagram users into one of ten predefined categories based on their post captions. Key steps and findings include:

Data Preparation: Text data was preprocessed and transformed into sparse vector representations using Term Frequency-Inverse Document Frequency (TF-IDF), optimizing the feature space with the top 5,000 features.

Class Imbalance Handling: Synthetic Minority Oversampling Technique (SMOTE) was employed to generate synthetic samples for underrepresented categories, improving model balance and decision boundaries.

Model Selection and Performance:

Multi-Layer Perceptron (MLP): Demonstrated strong training performance but encountered overfitting issues, limiting generalization capabilities.

Logistic Regression: Achieved more consistent results, with validation accuracy ranging from 64% to 66%, demonstrating robustness and interpretability.

Challenges: Significant category overlap and variability in user-generated content made classification complex. However, well-defined categories, such as sports, yielded better performance.

2. Like Count Prediction
The regression task focused on predicting post engagement (like counts) while addressing the challenges posed by heavy-tailed distributions and user popularity differences. Key aspects include:

Baseline Approach: A simple yet effective baseline model utilized the historical average likes per user, providing an initial benchmark.

Evaluation Metrics: The model was evaluated using Logarithmic Mean Squared Error (Log MSE), minimizing the impact of extreme outliers and achieving a training error of approximately 1.2156.

Challenges and Insights:

The baseline model effectively captured general patterns but struggled with cyclical spikes and extreme outliers.

Residual analysis revealed systematic under- and over-predictions, particularly for posts at both ends of the popularity spectrum.

Conclusion and Recommendations
This analysis highlights the potential of combining robust preprocessing, class balancing techniques, and tailored evaluation metrics for effective Instagram data analytics. While the models provided promising results, future improvements could focus on:

Expanding feature engineering efforts to incorporate image-based or metadata features for influencer classification.

Exploring advanced ensemble models or deep learning architectures for like count prediction to better handle outliers and capture complex engagement patterns.

The insights derived from this project underscore the importance of adaptability and precision in social media analytics, offering valuable strategies for future applications.

