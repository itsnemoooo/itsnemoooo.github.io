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
| Date                     | Date of the observation               | Date            | 6 months - 1 year             |
| Current Price            | Current price of the product          | Continuous      | [0, ∞)                        |
| Clicks                   | Number of clicks                      | Discrete        | [0, ∞)                        |
| Number of Competitors    | Number of competitors                 | Discrete        | [0, ∞)                        |
| Competitor Prices        | Prices of competitors                 | Continuous      | [0, ∞)                        |
| Media Campaign (y/n)     | Presence of a media campaign          | Discrete        | {0, 1}                        |
| Decline (y/n)            | Product decline status                | Discrete        | {0, 1}                        |
| Product Category         | Category of the product (tree)        | String          | N/A                           |
| Collection Name          | Name of the collection                | String          | N/A                           |
| Type                     | Type of the product                   | String          | N/A                           |
| Color                    | Color of the product                  | String          | N/A                           |
| Material                 | Material of the product               | String          | N/A                           |
| Holiday (y/n)            | Upcoming holiday indicator            | Discrete        | {0, 1}                        |
| Discount Day (y/n)       | Usual discount day indicator          | Discrete        | {0, 1}                        |

## Data Analysis
The project begins with a comprehensive data analysis to understand the current pricing dynamics and identify key factors influencing sales.

## RL Strategy Development
Seasonality plays a crucial role in pricing strategies. Inspired by the DDQN approach used in HVAC control (refer to project-hvac), the RL agent will consider seasonal patterns and holiday cycles.

### Key Seasonal Insights
- **Spring Holidays:** 14 Feb, 23 Feb, 8 March
- **Gift Cycles:** July to late August, November to New Year

A manually annotated dataset incorporating holiday information will enhance the agent's decision-making capabilities.

### Initial Focus
Start with high-volume, low-priced products to validate the RL agent's effectiveness in real-world scenarios.