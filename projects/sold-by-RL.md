---
title: "Sold by RL"
date: YYYY-MM-DD
categories: [Blogs]
---

# Sold by RL - a freelance project

## Problem: 
Small D2C businesses have failed to adapt to pricing at scale. This wastes inventory, money, and time.

## Goal: 
Sell more product on the website by allowing an RL agent to change prices based on the environment.

Each product gets its own agent. The agent has continuous action space with full control over pricing. 

| State Variable       | Description                       | Data Type   | Range - TBD              |
|----------------------|-----------------------------------|-------------|--------------------------|
| date                 | Date of the observation           | Date        | 6mo - 1 year             |
| current price        | Current price of the product      | Continuous  | [0, ∞)                   |
| clicks               | Number of clicks                  | Discrete    | [0, ∞)                   |
| # of competitors     | Number of competitors             | Discrete    | [0, ∞)                   |
| competitor prices    | Prices of competitors             | Continuous  | [0, ∞)                   |
| media campaign (y/n) | Whether there is a media campaign | Discrete    | {0, 1}                   |
| decline (y/n)        | Whether product is in decline     | Discrete    | {0, 1}                   |
| product category     | Category of the product (tree)    | String      | N/A                      |
| collection name      | Name of the collection            | String      | N/A                      |
| type                 | Type of the product               | String      | N/A                      |
| color                | Color of the product              | String      | N/A                      |
| material             | Material of the product           | String      | N/A                      |
| holiday (y/n)             | Is there a holiday coming up?           | String      | N/A                      |
| discount day (y/n)             | Do we discount pricing usually?          | String      | N/A                      |
## Data Analysis
Like any good engineering challenge, it starts with data analysis.


## RL Brainstorming
Time of year is very significant here. I am thinking of doing something similar to a DDQN for controlling building temperatures (seen in project-hvac) since seasonality is at play there also.

The spring cycle includes the following holidays:
23 Feb
14 Feb
8 March

With gift cycles in:
July-Late august
November-New Year

I am thinking it would be valuable to have a manually annotated environment dataset with this holiday information. 

We should start simple, with products that get sold a lot with lowish prices.