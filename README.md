# CS412_Project
CS412 Machine Learning 
Final Project Report (Fall 2024)


Group Members: Kerim Taşkıran (29520), Eren Yamak (31283), İlke Öncü (28930)

Introduction

This report examines two key tasks in Instagram Influencer : influencer category classification and like count prediction. We address class imbalance with SMOTE, extract textual features using TF-IDF, and compare MLP and logistic regression models. Finally, we explore a simple baseline to estimate like counts despite their heavy-tailed distribution.

Part 1: Influencer Category Classification

1.1. Data Preparation and TF-IDF Feature Extraction
We began by collecting Instagram user data—each user’s profile and their posts. For classification, each user is labeled with one of ten categories in the data annotation part of the project (e.g., food, fashion, entertainment, etc.):
 
Table 1. Influencer Classification Label Counts

We extracted each user’s post captions, cleaned them (lowercasing, removing URLs, punctuation, digits, etc.), and filtered out Turkish stopwords from NLTK. Then, we concatenated all captions belonging to a single user into one document, which we transformed using TF-IDF. TF-IDF provided a sparse vector representation, capturing how important each term is relative to the rest of the corpus. We limited ourselves to 5,000 top features for the computational cost.
Compared to raw word counts, TF-IDF downweights widespread terms and increases the importance of less common but more category-specific terms.


Table 2. TF-IDF Text Vector Representation for the Dataset


Figure 1. Word Cloud Chart for the Most Frequent TF-IDF Words

1.2. Addressing Class Imbalance with SMOTE

One of the foremost issues was class imbalance. Certain categories—like “health and lifestyle” or food—had hundreds of labeled users, while others—such as “gaming”—had fewer than 50. Without mitigation, a classifier might be heavily biased toward the dominant classes and neglect the minority classes. To counteract this, we employed SMOTE (Synthetic Minority Oversampling Technique). SMOTE synthesizes additional samples for minority categories by interpolating between existing points in feature space, helping the classifier learn a more balanced decision boundary.

SMOTE forces the model to “see” enough examples from minority categories, improving recall and precision in classes that were previously overshadowed. However, it can lead to slight overfitting on synthetic data if not carefully validated, hence it was controlled carefully during the project.

1.3. Comparing MLP vs. Logistic Regression Models
This project progressed through three rounds, with different models used at each stage. Initially, a Multi-Layer Perceptron (MLP) classifier was employed in the first two rounds, followed by Logistic Regression with hyperparameter tuning in the final round.
Multi-Layer Perceptron (MLP): Rounds 1 and 2
The MLP was selected for its ability to capture non-linear relationships and learn complex patterns.
Advantages:
Non-linear modeling: MLP can model intricate relationships.
Flexibility: With proper tuning, MLP can achieve high accuracy.
Challenges:
Overfitting: MLP is prone to overfitting, especially with imbalanced data, requiring careful tuning.
Computational cost: Training MLP, particularly with SMOTE, is resource-intensive.
Performance variability: Cross-validation showed moderate variability, particularly with minority classes.
Despite these challenges, MLP performed reasonably well in the early rounds, handling high-dimensional TF-IDF features.
Logistic Regression: Round 3
In the final round, we switched to Logistic Regression, which offered better interpretability, reduced computational needs, and robust performance with imbalanced data.
Advantages:
Simplicity and interpretability: Logistic Regression is easier to interpret.
Efficiency: Fewer hyperparameters to tune, making it faster to train.
Stability on imbalanced data: Consistent performance during cross-validation.
Challenges:
Limited non-linear capability: Logistic Regression is linear and may not capture complex relationships unless feature engineering is applied.
Using GridSearch, we optimized the regularization parameter (C) and solver type. The best configuration—C=10 and solver='liblinear'—was chosen based on cross-validation results. The MLP had moderately strong training accuracy, but logistic regression was more consistent across folds and simpler to tune.
While MLP has the potential for higher accuracy with larger and more balanced datasets, its complexity and resource demands made it less suitable for this task. Logistic Regression provided a simpler and more practical solution, delivering stable and interpretable results aligned with the project’s conditions.

1.4. Cross-Validation and Potential Overfitting

To avoid relying solely on a single train/validation split, we used cross-validation (5-fold) on the training data. By using different data chunks for validation, we can detect overfitting in the model’s performance. Indeed, our cross-validation results for logistic regression hovered around ~64–66% mean accuracy.

Signs of Overfitting:

Logistic regression’s training accuracy and the validation accuracy had significant discrepancies.
This gap hints at some overfitting, where the model memorizes training patterns but cannot replicate that success on unseen data.
Still, the cross-validation approach kept that overfitting in check, ensuring we recognized the realistic performance limit.

1.5. Classification Results and Visualizations
After training and tuning our Logistic Regression model (and comparing it to the previously used MLP), we generated a variety of detailed reports and plots to fully understand how well the classifier performed and where it struggled.

Table 3. Training Classification Report


Table 4. Validation Classification Report

Training vs. Validation Performance
As indicated by the classification report on the training set (see Table 3), the model achieves an exceptionally high accuracy (close to 98–99%) and near-perfect precision, recall, and F1-scores across most categories. This signals that the classifier is highly capable of memorizing or fitting the training data, especially after SMOTE has artificially balanced the categories. However, on the validation set, the accuracy drops to around 64–66%. This discrepancy suggests overfitting, since the model performance on unseen data does not match the near-perfect training metrics.
Nonetheless, 64–66% accuracy across ten categories shows a good model, given the presence of overlapping content across categories (e.g., users who occasionally post about both food and health and lifestyle, or art and fashion). It also reflects the uneven nature of real-world Instagram data, where some classes inherently have more varied text or fewer samples (e.g., gaming).
