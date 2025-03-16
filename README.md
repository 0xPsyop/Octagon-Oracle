# Octagon-oracle

## Overview

The dataset used is `ufc_fights.csv`, which includes various features related to fighters, fight statistics, and betting odds. The goal is to predict the winner of a fight (Red or Blue) based on these features.

## How to Use

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/octagon-oracle.git
   cd octagon-oracle
   ```

2. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the Jupyter Notebook**:
   ```bash
   jupyter notebook oracle.ipynb
   ```

## Repository Structure

- **`ufc_fights.csv`**: The raw dataset containing UFC fight data.
- **`processed_fighting_data.csv`**: The cleaned and processed dataset after handling missing values and feature engineering.
- **`winner_balanced_ufc_dataset.csv`**: The dataset after balancing the class distribution of the target variable (Winner).
- **`final_ufc_dataset.csv`**: The final dataset after additional feature engineering and standardization.
- **`oracle.ipynb`**: Jupyter notebook containing the code for data preprocessing, feature engineering, and model training.

## Data Preprocessing

### 1. **Handling Missing Values**
   - **Analysis**: The dataset contains a significant number of missing values. Some columns have more than 95% missing data, while others have less than 23%.
   - **Decisions**:
     - **Dropping Unnecessary Columns**: Columns like `Country`, `Location`, `FinishRoundTime`, `EmptyArena`, `RedFighter`, and `BlueFighter` were dropped as they were deemed irrelevant or had too many missing values.
     - **Creating Indicator Variables**: For columns with more than 95% missing values, binary indicators were created to denote the presence or absence of data.
     - **Imputation**: For columns with less than 23% missing values, missing data was imputed using the median for numerical columns and the mode for categorical columns.

### 2. **Balancing the Dataset**
   - **Analysis**: The target variable `Winner` was imbalanced, with more instances of the "Red" fighter winning compared to the "Blue" fighter.
   - **Decision**: The dataset was balanced using Random Under-Sampling to ensure equal representation of both classes.

### 3. **Feature Engineering**
   - **New Features**: Several new features were created to capture additional insights:
     - **Odds Ratio**: Ratio of RedOdds to BlueOdds.
     - **Experience Metrics**: Total fights, wins, losses, and draws for both fighters.
     - **Win Percentages**: Win percentages for both fighters.
     - **Form Metrics**: Current win/loss streaks.
     - **Fighting Style Indicators**: Scores for striking and grappling based on fight statistics.
     - **Finish Rate**: Rate at which fighters finish fights by KO or submission.
     - **Age-Adjusted Performance**: Performance metrics adjusted for fighter age.
     - **Betting Confidence**: Confidence in betting odds based on expected values.
     - **Composite Indicators**: Combined performance scores for fighters.
     - **Outcome Prediction Probabilities**: Implied probabilities from betting odds.

### 4. **Standardization**
   - **Decision**: Numerical features were standardized using `StandardScaler` to ensure that all features contribute equally to the model.

### 5. **Encoding Categorical Features**
   - **Decision**: Categorical features were one-hot encoded to convert them into a format suitable for machine learning models.

## Model Training

### 1. **Feature Selection**
   - **Decision**: The top features were selected based on their importance using `SelectKBest` with `f_classif`.

### 2. **Model Selection**
   - **Decision**: After evaluating various models, including RandomForestClassifier, LogisticRegression, XGBoost, and LightGBM, it was determined that the XGBoost model provided the best accuracy. Additionally, an ensemble model created using the Stacking Classifier with LightGBM, XGBoost, and RandomForest as estimators, and Logistic Regression as the meta-classifier, also achieved similar high accuracy. Therefore, both the XGBoost model and the ensemble model were considered for the final implementation to ensure optimal prediction performance.

### 3. **Evaluation**
   - **Metrics**: The model was evaluated using accuracy, classification report, and confusion matrix.

The Evaluation for the XGBoost Classifier
![Capture](https://github.com/user-attachments/assets/245eba21-c2b7-46a5-80ec-61545176f4fd)

![image](https://github.com/user-attachments/assets/5e1f635b-bb60-4354-9a14-33b843af1a8b)
