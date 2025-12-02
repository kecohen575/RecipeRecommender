# Recipe Recommender System

A collaborative filtering and content-based recommendation system for recipes, addressing cold-start problems and handling highly sparse interaction data.

## Project Overview

This project implements a recipe recommendation system that combines collaborative filtering (matrix factorization) with content-based features to address the challenges of sparse user-item interactions and cold-start scenarios.

## Dataset Structure

### Interaction Data
- **`interactions_train.csv`**: Training set (698,901 interactions)
- **`interactions_validation.csv`**: Validation set (7,025 interactions)
- **`interactions_test.csv`**: Test set
- **Columns**: `user_id`, `recipe_id`, `date`, `rating`, `u` (user index), `i` (item index)
- **Rating scale**: 0-5 (continuous)

### Metadata
- **`RAW_recipes.csv`**: Full recipe metadata (ingredients, instructions, tags, nutritional info, etc.)
- **`RAW_interactions.csv`**: Raw interaction data with timestamps
- **`PP_recipes.csv`**: Preprocessed recipe embeddings/features
- **`PP_users.csv`**: Preprocessed user features
- **`ingr_map.pkl`**: Ingredient mapping dictionary

## Key Findings from Exploratory Data Analysis

### 1. Rating Distribution Bias
- **Average rating: 4.57** (highly skewed toward positive)
- Heavy concentration of 5-star ratings
- 0-star ratings more common than 1-2 stars (bimodal distribution)
- **Implication**: Users only rate recipes they've tried and enjoyed, creating selection bias

### 2. User Activity Distribution
- **Extreme long-tail pattern**: Most users rate <10 recipes, few power users rate 1000+
- Some users rate 6000+ recipes
- **Implication**: Sparse user histories require collaborative approaches; power users may dominate gradient updates without regularization

### 3. Recipe Popularity Distribution
- **Strong long-tail**: Most recipes receive few ratings, few recipes accumulate 1000+
- **Implication**: Severe item cold-start problem; metadata-based features essential

### 4. Matrix Sparsity
- **99.8% sparsity** (1 - interactions / (users × items))
- **Implication**: Matrix factorization and latent factor models are well-suited

## Planned Approach

### Baselines (To Implement)
1. **Popularity Recommender**: Recommend most-rated recipes globally
2. **User Mean Predictor**: Predict user's average rating for all items
3. **Item Mean Predictor**: Predict recipe's average rating for all users

### Advanced Models
- **Matrix Factorization / Latent Factor Models**: Exploit 99.8% sparsity
- **BPR (Bayesian Personalized Ranking)**: Well-suited for low negative ratings
- **Hybrid Content + Collaborative**: Address cold-start with metadata

### Content-Based Features (Difficulty Scoring)
Incorporate recipe difficulty using:
- **Instruction length**: Longer instructions → more difficult
- **Ingredient count**: More ingredients → more complex
- **Ingredient rarity**: Rarer ingredients → harder to source/prepare
- **Estimated time**: Already available in metadata

### Temporal Features (Low Priority)
- Timestamps available on ratings
- **Note**: Taste changes occur over years, not months
- Most users won't be lifetime raters
- **Decision**: Likely skip temporal modeling for now

## Design Decisions

### Evaluation Metrics
- **Avoid MSE**: Misleading due to high rating bias (predicting 4.57 always looks good)
- **Use ranking-based metrics**:
  - Precision@K
  - Recall@K
  - MRR (Mean Reciprocal Rank)
  - NDCG (Normalized Discounted Cumulative Gain)
- **Caution**: Don't assume normal distribution

### Regularization
- **L2 regularization**: Prevent strong user bias from power users dominating gradient updates
- Balance between learning from active users and generalizing to sparse users

### Model Architecture
- **Latent factors**: Well-suited for sparse user vectors
- **Content-based features**: Address cold-start for niche recipes
- **Hybrid approach**: Combine collaborative filtering with metadata

## Challenges

1. **Cold Start Problem**
   - Most recipes haven't been rated many times
   - Hard to recommend niche recipes
   - **Solution**: Metadata-based content recommendations

2. **User Sparsity**
   - Most users don't rate many recipes
   - Power users dominate updates
   - **Solution**: L2 regularization, latent factor models

3. **Rating Bias**
   - Average 4.57 suggests positive selection bias
   - Low negative ratings (BPR advantage)
   - **Solution**: Ranking metrics, not regression metrics

4. **Data Distribution**
   - Not normally distributed
   - Bimodal (0 and 5 stars)
   - **Solution**: Ranking-based evaluation, not MSE

## Setup Instructions

### Prerequisites
```bash
pip install pandas numpy matplotlib scikit-learn
# Add additional dependencies as models are implemented
```

### Data Loading
```python
import pandas as pd

# Load interaction splits
train_df = pd.read_csv("dataset/interactions_train.csv")
val_df = pd.read_csv("dataset/interactions_validation.csv")
test_df = pd.read_csv("dataset/interactions_test.csv")

# Load metadata
raw_recipes = pd.read_csv("dataset/RAW_recipes.csv")
raw_interactions = pd.read_csv("dataset/RAW_interactions.csv")

# Preprocessed features (if available)
pp_users = pd.read_csv("dataset/PP_users.csv")
pp_recipes = pd.read_csv("dataset/PP_recipes.csv")
```

### Running Analysis
Open `recipe_recsys.ipynb` in Jupyter Notebook to view exploratory data analysis.

## Project Structure

```
RecipeRecommender/
├── dataset/
│   ├── interactions_train.csv
│   ├── interactions_validation.csv
│   ├── interactions_test.csv
│   ├── RAW_recipes.csv
│   ├── RAW_interactions.csv
│   ├── PP_recipes.csv
│   ├── PP_users.csv
│   └── ingr_map.pkl
├── recipe_recsys.ipynb    # EDA and model development
└── README.md
```

## Next Steps

1. **Implement Baselines**
   - Popularity recommender
   - User mean predictor
   - Item mean predictor

2. **Build Matrix Factorization Model**
   - Implement BPR or standard MF
   - Add L2 regularization
   - Tune hyperparameters

3. **Extract Content Features**
   - Recipe difficulty scoring (instructions, ingredients, rarity, time)
   - Feature engineering pipeline

4. **Hybrid Model**
   - Combine collaborative filtering with content features
   - Address cold-start scenarios

5. **Evaluation Framework**
   - Implement ranking metrics (Precision@K, Recall@K, MRR, NDCG)
   - Compare baselines vs. advanced models

## Notes

- **99.8% sparsity** makes matrix factorization ideal
- **BPR** may outperform standard MF due to low negative ratings
- **Metadata** is crucial for cold-start recipes
- **Ranking metrics** are essential due to rating bias
- **Regularization** needed to prevent power user dominance

