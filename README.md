# Book Recommender System

A collaborative filtering-based book recommendation system developed using Python and the [goodbooks-10k](https://github.com/zygmuntz/goodbooks-10k) dataset.

This academic group project compares **K-Nearest Neighbors (KNNBasic)** and **Singular Value Decomposition (SVD)** for predicting user ratings and generating personalized book recommendations. It also evaluates recommendation accuracy, popularity bias, and diversity-aware re-ranking.

**Developed by:** Mico, Dani, Gids, and Drea

## Project Objectives

The project aims to:

1. Develop a book recommendation system using collaborative filtering techniques.
2. Compare KNNBasic and SVD in terms of rating prediction accuracy and recommendation relevance.
3. Identify patterns and potential biases in the generated recommendations.
4. Explore methods for improving recommendation diversity without sacrificing relevance.

## Dataset

The project uses the publicly available **goodbooks-10k** dataset, which contains:

- 53,424 users
- 10,000 books
- Approximately 6 million user-book ratings
- Ratings ranging from 1 to 5

The dataset includes user ratings, book metadata, and book tags.

To improve computational efficiency, the dataset was filtered to retain sufficiently active users and frequently rated books.

**Final modeling dataset:**

| Metric | Count |
|---|---:|
| Users | 52,546 |
| Books | 320 |
| Ratings | 1,947,038 |

## Methodology

### 1. Data Preparation and Exploratory Analysis

- Performed data quality checks and preprocessing.
- Examined rating distributions, user activity, and book popularity.
- Analyzed the sparsity of the user-item rating matrix.
- Filtered users and books based on rating activity.

### 2. Collaborative Filtering Models

Two recommendation algorithms were implemented:

**KNNBasic (Item-Based Collaborative Filtering)**

Identifies similarities between books based on users' rating patterns. Hyperparameters such as neighborhood size and similarity measure were optimized.

**Singular Value Decomposition (SVD)**

Uses matrix factorization to learn latent user and book characteristics for predicting ratings and generating personalized recommendations.

### 3. Model Training and Evaluation

The models were evaluated using:

- **Root Mean Squared Error (RMSE):** Measures rating prediction accuracy.
- **Hit Rate@10:** Measures how frequently a held-out book appears in a user's Top-10 recommendations.
- **Cross-validation:** Assesses model performance across different data splits.

Hyperparameter tuning was performed to improve model performance.

### 4. Recommendation Bias and Diversity

The project also examined how frequently individual books appeared in recommendation lists.

An experimental SVD re-ranking approach was implemented to reduce excessive recommendation concentration and improve catalog coverage.

## Results

### Rating Prediction Performance

| Model | Mean RMSE |
|---|---:|
| KNNBasic (Default) | 0.9180 |
| KNNBasic (Tuned) | 0.8854 |
| SVD (Default) | 0.8648 |
| **SVD (Tuned)** | **0.8612** |

The tuned SVD model achieved the lowest RMSE, indicating better rating prediction accuracy than KNNBasic.

### Top-10 Recommendation Performance

| Evaluation | KNNBasic | SVD |
|---|---:|---:|
| Hit Rate@10 (All Ratings) | 7.06% | **8.28%** |
| Hit Rate@10 (Ratings 4–5) | 8.37% | **10.71%** |

SVD demonstrated stronger recommendation relevance based on the Hit Rate@10 results.

### Diversity-Aware Re-Ranking

Although SVD performed better in rating prediction, its recommendations were concentrated among a smaller set of popular books.

Applying a diversity-aware re-ranking approach improved:

- Catalog coverage from approximately **65% to 99%**
- Recommendation diversity across users
- Hit Rate@10 for positively rated books from **10.43% to 15.39%** on the held-out evaluation group

These findings demonstrate that improving recommendation diversity can also improve relevance under the evaluated conditions.

## Technologies Used

- **Programming Language:** Python
- **Data Processing:** Pandas, NumPy, SciPy
- **Machine Learning:** Scikit-learn, Scikit-Surprise
- **Visualization:** Matplotlib
- **Text Matching:** FuzzyWuzzy
- **Development Environment:** Google Colab / Jupyter Notebook

## Repository Structure

```text
book-recommender-system/
│
├── README.md
├── requirements.txt
├── notebooks/
│   └── book_recommender_system.ipynb
├── outputs/
└── images/
```

## Installation and Usage

1. Clone the repository:

   ```bash
   git clone https://github.com/<your-username>/book-recommender-system.git
   ```

2. Install the required libraries:

   ```bash
   pip install -r requirements.txt
   ```

3. Open `notebooks/book_recommender_system.ipynb` using Jupyter Notebook or Google Colab.

4. Run the notebook cells to reproduce the analysis, train the models, and generate recommendations.

The notebook downloads the required goodbooks-10k datasets from their public source.

## Key Findings

1. **SVD outperformed KNNBasic** in both rating prediction accuracy and Top-10 recommendation relevance.
2. **Higher prediction accuracy does not necessarily guarantee diverse recommendations.** The original SVD model favored a relatively small set of books.
3. **Popularity bias is an important consideration** when developing collaborative filtering systems, particularly when filtering books based on rating frequency.
4. **Re-ranking can improve recommendation diversity** while maintaining or improving recommendation relevance.

## Limitations and Future Improvements

The project was constrained by computational resources, resulting in a reduced catalog of frequently rated books.

Potential improvements include:

- Expanding the recommendation system to the complete dataset.
- Incorporating book genres, authors, and descriptions.
- Exploring hybrid recommendation approaches.
- Evaluating additional ranking metrics such as Precision@K, Recall@K, and NDCG.
- Developing a user-facing application for personalized book recommendations.

## Contributors

This project was collaboratively developed as part of an academic requirement by:

- **Mico**
- **Dani**
- **Gids**
- **Drea**

All contributors participated in the development and completion of the project.

## Acknowledgments

**Dataset:** [goodbooks-10k](https://github.com/zygmuntz/goodbooks-10k)

The project was developed for academic purposes using publicly available data and open-source Python libraries.
