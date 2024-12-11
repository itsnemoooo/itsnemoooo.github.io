---
layout: default
---

### Sold-by-RL

### problem statement
small Direct-to-Consumer (D2C) businesses struggle to adapt pricing strategies at scale, leading to wasted inventory, financial losses, and inefficiencies.

a manually annotated dataset incorporating holiday information will enhance the agent's decision-making capabilities.

### objective
develop a Reinforcement Learning agent to dynamically adjust product prices based on environmental factors, aiming to increase sales on the website.

### approach
- assign a dedicated RL agent to each product.
- use a continuous action space, granting the agent full control over pricing decisions.

### state variables
will update this section when the project is complete if permitted

### data analysis & feature engineering

the project begins with a comprehensive data analysis to understand the current pricing dynamics and identify key factors influencing sales.

I used a Jupyter notebook to perform **feature engineering**, specifically:

- **Imports**: Loads necessary libraries such as pandas, sklearn, and transformers.
- **Data Loading**: Reads data from parquet files into pandas DataFrames.
- **Feature Engineering**:
  - **Category Filtering**: Filters data for specific categories of interest.
  - **Lag Features**: Creates lag features for price data to capture temporal dependencies.
  - **Encoding**: Encodes categorical variables using one-hot encoding and target encoding.
  - **Translation and Embedding**: Translates category names and computes embeddings using pre-trained models.
  - **Date Features**: Extracts date-related features such as year, month, and day of the week.
  - **Dimensionality Reduction**: Applies PCA to reduce the dimensionality of embedding features.
- **Model Training**: Trains machine learning models using scikit-learn, including hyperparameter tuning with Optuna.
- **Feature Importance**: Extracts and visualizes feature importances from trained models.

## this is an in-progress private project for a client

## will update this page when the project is complete if permitted