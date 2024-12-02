---
title: "Sold by RL"
categories: [Projects]
---

# Sold by RL - Freelance Project

## Project Overview

### Problem Statement
Small Direct-to-Consumer (D2C) businesses struggle to adapt pricing strategies at scale, leading to wasted inventory, financial losses, and inefficiencies.

### Objective
Develop a Reinforcement Learning (RL) agent to dynamically adjust product prices based on environmental factors, aiming to increase sales on the website.

### Approach
- Assign a dedicated RL agent to each product.
- Utilize a continuous action space, granting the agent full control over pricing decisions.

### State Variables

| **State Variable**       | **Description**                       | **Data Type**   | **Range**                     |
|--------------------------|---------------------------------------|-----------------|-------------------------------|
| Match Type               | Type of match                         | Integer         | N/A                           |
| Category 1               | Primary category of the product       | String          | N/A                           |
| Category 2               | Secondary category of the product     | String          | N/A                           |
| Category 3               | Tertiary category of the product      | String          | N/A                           |
| Category 4               | Quaternary category of the product    | String          | N/A                           |
| Category 5               | Quinary category of the product       | String          | N/A                           |
| SKU                      | Stock Keeping Unit                    | String          | N/A                           |
| Brand                    | Brand of the product                  | String          | N/A                           |
| Our Price                | Our price for the product             | Continuous      | N/A                           |
| Price                    | Current price of the product          | Continuous      | N/A                           |
| Price Before Discount    | Price before any discount             | Continuous      | N/A                           |
| Date                     | Date of the observation               | Date            | N/A                           |
| City                     | City identifier                       | Integer         | N/A                           |
| Status                   | Status of the product                 | Integer         | N/A                           |
| Competitor               | Competitor identifier                 | String          | N/A                           |


## Data Analysis & Feature Engineering
The project begins with a comprehensive data analysis to understand the current pricing dynamics and identify key factors influencing sales.

I used a Jupyter notebook to perform feature engineering. It includes:

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



## RL Strategy Development
Seasonality plays a crucial role in pricing strategies. Inspired by the DDQN approach used in HVAC control (refer to project-hvac), the RL agent will consider seasonal patterns and holiday cycles.

### Key Seasonal Insights
- **Spring Holidays:** 14 Feb, 23 Feb, 8 March
- **Gift Cycles:** July to late August, November to New Year

A manually annotated dataset incorporating holiday information will enhance the agent's decision-making capabilities.

### Initial Focus
Start with high-volume, low-priced products to validate the RL agent's effectiveness in real-world scenarios.


