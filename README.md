# DSA 4060 Personalized Movie Recommender

## Student Details
* **Student Name:** Yahya Mohamed
* **Student ID:** 669622
* **Assigned User ID:** 23 (Calculated via $(22 \bmod 40) + 1 = 23$)

## Project Objective
The goal of this project is to build a personalized content-based movie recommendation system for a streaming service. By analyzing the historical movie ratings of an assigned user, the recommender identifies key genre preferences and suggests five unseen, highly relevant movies using TF-IDF feature extraction and cosine similarity.

## Datasets
* **`movies.csv`**: Contains 36 movies with unique `movie_id`, `title`, and pipe-separated `genres`.
* **`ratings.csv`**: Contains 440 historical rating records across 40 users with fields `user_id`, `movie_id`, and `rating`.

## Method / Approach
1. **Data Inspection:** Verified shape and checked for missing values across both datasets.
2. **User Profiling:** Filtered historical ratings for User 23 to analyze rating distribution and top-rated titles (*The Grand Budapest Hotel* rated 5.0, *Moneyball* rated 4.0).
3. **Feature Vectorization:** Converted pipe-separated movie genres into numerical vector representations using `TfidfVectorizer`.
4. **Preference Vector & Cosine Similarity:** Formed a User 23 preference vector by averaging the TF-IDF feature vectors of positively rated movies ($\ge 4.0$) and calculated cosine similarity against all movies in the catalogue.
5. **Filtering:** Excluded the 12 movies already rated by User 23 and extracted the top 5 unseen recommendations.

## How to Run the Notebook
1. Open Google Colab or a local Jupyter Notebook environment with Python 3.x.
2. Ensure `pandas`, `numpy`, and `scikit-learn` are installed (`pip install pandas numpy scikit-learn`).
3. Place `movies.csv` and `ratings.csv` in the same directory as the notebook.
4. Run all notebook cells sequentially from top to bottom.

## Recommendation Results

| Rank | Recommended Movie | Genres | Reason |
| :---: | :--- | :--- | :--- |
| **1** | Creed | Sports\|Drama | Exact genre overlap (`Sports\|Drama`) with *Moneyball* (rated 4.0). |
| **2** | Remember the Titans | Sports\|Drama | Exact genre overlap (`Sports\|Drama`) with *Moneyball* (rated 4.0). |
| **3** | The Shawshank Redemption | Drama | Shares core `Drama` genre present in user's top-rated choices. |
| **4** | The Hangover | Comedy | Matches `Comedy` genre present in user's top film, *The Grand Budapest Hotel* (5.0). |
| **5** | The Notebook | Romance\|Drama | Combines preferred `Drama` theme with `Romance` (similar to *Titanic* rated 3.5). |

## Limitation and Suggested Improvement
* **Limitation:** The recommender suffers from overspecialization and coarse feature granularity. Because it relies purely on genre tags, movies with identical genres receive identical similarity scores, ignoring directors, cast, plot nuance, or release era.
* **Suggested Improvement:** Develop a hybrid recommender system combining collaborative filtering (such as Matrix Factorization/SVD) with rich content embeddings (e.g., TF-IDF or SBERT on full plot synopses) to improve accuracy and introduce serendipitous recommendations.
