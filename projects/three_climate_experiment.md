# The Three Climate Experiment
**May 2024 - September 2024**  
*London, UK*


### We can do better than rule-based control.

---
![Figure 1: Illustration of the World](https://itsnemoooo.github.io/assets/images/world.png)


HVAC systems account for up to 40% of total energy consumption in commercial buildings and exhibit nonlinear behavior under varying weather conditions, making RBC insufficient for optimisation in modern, changing environments. With the increasing impact of climate change, these challenges are becoming even more pronounced.

To tackle this, I spent my summer exploring the potential of Deep Reinforcement Learning (DRL) to develop more adaptive and efficient control strategies.

The executive summary of my work is available [here](https://itsnemoooo.github.io/ExecutiveSummary.pdf).

---

### Research Question

**How can a deep reinforcement learning agents efficiently manage HVAC systems across diverse and rapidly changing climate conditions?**

---
![Figure 1: Illustration of the Three Climate Experiment framework](https://itsnemoooo.github.io/assets/images/RAE.png)
*Figure 1: Replay across Experiments (RaE) framework.*
### My Contributions

1. **Three Climate Experiment Framework**
   - **Description:** Leveraged a novel training framework that reuses data and continually improves DRL agents as they train across experiments. I transferred this the domain of HVAC control, training agents across diverse climate conditions using the Replay across Experiments (RaE) methodology. [Read more about the Replay across Experiments (RaE) methodology](https://arxiv.org/abs/2311.15951).
   - **Impact:** Enhanced robustness and performance in both normal and extreme weather scenarios.

2. **Novel Global Weather Dataset**
   - **Description:** Created a unique dataset from seven countries, modified to reflect current climate variability, providing a realistic and challenging evaluation environment.
   - **Impact:** Provided a more realistic and challenging evaluation environment for the generalization and resilience of DRL models against real-world climate variations.

### The Challenges
I embarked on my first research project, beginning with a structured literature review. Finding relevant research was challenging, as much of the existing documentation focused on short timeframes or variables that lacked real-world significance. I began the summer, initially inspired by the potential of DRL to improve HVAC control (thanks to articles like [this](https://deepmind.google/discover/blog/deepmind-ai-reduces-google-data-centre-cooling-bill-by-40/)), but quickly realised that the scale of the task was far greater than I initially anticipated.

There were so many decisions to make: selecting frameworks, deciding whether to use HPC or run experiments locally, understanding how dataset choices might bias results, considering the creation of a new reward function, and evaluating the real-world impact and performance of my model.

Significant achievements start with small, focused choices. 

By organizing my schedule at the UCL AI centre, setting achievable goals, and learning from my colleagues, I managed to navigate these challenges with relative success.

### Methodology

I chose to build upon a baseline algorithm: Deep Double Q-Network (DDQN). I refactored it to incorporate the Three Climate Experiment framework. The choice of algorithm was motivated by my previous experience with off-policy algorithms, and coursework in Reinforcement Learning at UCL (taught by Prof Hado van Hasselt).

There were several improvements to the baseline algorithm that I experimented with: decaying epsilon-greedy exploration, prioritised experience replay, and a new reward function. However, the most significant improvement came from the Three Climate Experiment framework, as discussed in the previous section. This was inspired from discussions with my co-supervisor, Dhruva. It is a simple, but powerful idea that I would recommend to anyone looking to improve the data efficency of their Deep Reinforcement Learning models. The results are discussed in the next section.

## Environment
The environment is simulated using EnergyPlus, a building energy simulation program from the Department of Energy. The environment includes various thermal zones, each with its own temperature, humidity, and HVAC settings. The simulation is run with different weather data files to evaluate the performance of the DRL agent under diverse climate conditions.

The building used in this experiment is a six-zone office building.

## Action space
The action space consists of binary actions for each HVAC unit in the building's thermal zones. Each action can either turn the heating or cooling on or off for a specific zone. The action space is represented as a list of binary values, where each value corresponds to the state of the HVAC unit in that zone.

For example, the action below indicates that the second zone is active, and depending on the current temperature, it will be cooled or heated (towards the pre-defined comfort range).

```python
action = [0, 1, 0, 0, 0, 0]  # zone 2 active
```

## State space
The state space includes various environmental and system parameters such as:
- Outdoor temperature and humidity
- Wind speed and direction
- Solar angles
- Zone temperatures and humidity levels
- HVAC heating and cooling setpoints
- Time-related features like hour, day, and month

The state is explicitly defined as a normalized vector (of length 15). This vector contains the following features: 
- Outdoor temperature,
- Worktime (1/0 for working hours or not),
- The temperature and humidity of each zone.

```python
state_0 = [O0/100,W0,T_30/100, T_10/100,T_20/100,T_30/100,T_40/100,T_50/100,T_60/100, H_10/100,H_20/100,H_30/100,H_40/100,H_50/100,H_60/100]
```

## Reward function
The reward function is designed to balance energy consumption and thermal comfort. It includes:
- A penalty for energy consumption (`reward_E`), which is negative and proportional to the HVAC energy usage.
- A comfort reward (`reward_T`), which penalizes deviations from a comfortable temperature range (68°F to 77°F) in each zone.
- An optional penalty for frequent changes in HVAC actions (`reward_signal`), which discourages instability in the system.

The total reward is a combination of these components, encouraging the agent to minimize energy use while maintaining comfort.

## Results and Impact
The model unexpectedly focused on the building's centroid zone, a behavior not explicitly programmed but emerging from the data. This indicates the model's ability to understand the problem's structure rather than just exploiting dataset specifics.

The baseline control solution balances all zones:
![Figure 2: Baseline Control](https://itsnemoooo.github.io/assets/images/base.png)
*Figure 2: Baseline Control.*

The solution learned from the three climate experiment focuses on the centroid for efficiency gains:
![Figure 3: Three Climate Experiment](https://itsnemoooo.github.io/assets/images/3ce.png)
*Figure 3: Three Climate Experiment.*

The results of the experiments are summarised in the table below:
   - **Summary Table:**
     ```markdown
     | Category             | Performance          | Impact                      |
     |----------------------|----------------------|-----------------------------|
     | Baseline             | +/- 6.4% accuracy    | Open-source refactored code |
     | Three Climate (10k)  | 13.34% improvement   | 162,014 kWh p.a. savings    |
     | Three Climate (100k) | 53.02% improvement   | 378,458 kWh p.a. savings    |
     | Modified Climate     | 54.11% improvement   | 523,616 kWh p.a. savings    |
     | **Total Impact**     |                      | **1.064 million kWh p.a.**  |
     ```
---

- **Energy Efficiency Improvement:** The Three Climate Experiment Framework achieved a **53.02%** improvement in energy efficiency over baseline methods.
- **Energy Savings:** Total annual energy savings amounted to **1.064 million kWh**.
- **Robustness to Climate Variability:** Models validated with the modified weather dataset demonstrated resilience to extreme conditions, outperforming baselines by an average of **39.057 percentage points**.

- **Sustainable Development Goals (SDGs) Contribution:**
  - **SDG 7:** Affordable and Clean Energy.
  - **SDG 11:** Sustainable Cities and Communities.
  - **SDG 13:** Climate Action.





## Next Steps
- Work submitted to Neurips 2024 Workshop on Tackling Climate Change with AI
- Implement a more sophisticated reward function to encourage energy-efficient behavior.
- Explore the integration of other control strategies to further enhance performance.
- Expand the experiment to include more diverse climate conditions and scenarios.
