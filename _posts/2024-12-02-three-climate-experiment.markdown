---
layout: post
title:  "Three Climate Experiment"
date:   2024-12-02 19:00:00 +0000
categories: jekyll update
---



### The world deserves better than rule-based control.

---
![Figure 1: Illustration of the World](https://itsnemoooo.github.io/assets/images/world.png)


**HVAC systems account for up to 40%** of total energy consumption in commercial buildings and **exhibit nonlinear behavior** under varying weather conditions.

I devoted my Masters thesis to this exploring this problem, spending my summer days in the UCL AI centre. The potential of **Deep Reinforcement Learning** to attack this problem is tremendous, and developing more adaptive and efficient control strategies is an crucial area of research in building operations.

The executive summary of my work is available [here](https://itsnemoooo.github.io/ExecutiveSummary.pdf).

---

## Research Question

**"How can a deep reinforcement learning agents efficiently manage HVAC systems across diverse and rapidly changing climate conditions?"**

---
![Figure 1: Illustration of the Three Climate Experiment framework](https://itsnemoooo.github.io/assets/images/RAE.png)
*Figure 1: Replay across Experiments (RaE) framework.*
### My Contributions

1. **Three Climate Experiment Framework**
   - **Description:** I used a novel training framework that reuses data and continually improves DRL agents as they train across experiments. I **transferred this to the domain of HVAC control**, training agents across diverse climate conditions using the Replay across Experiments [(RaE) methodology](https://arxiv.org/abs/2311.15951).
   - **Impact:** Enhanced robustness and performance in both normal and extreme weather scenarios.

2. **Novel Global Weather Dataset**
   - **Description:** Created a unique dataset from seven countries, modified to reflect **current climate variability**, providing a realistic and **challenging evaluation environment** for our agent 🤖.
   - **Impact:** Provided a more realistic and **challenging evaluation environment** for the generalization and resilience of DRL models against real-world climate variations.

## Challenges
### Non-technical
1. I started this research project with a structured literature review. Finding relevant research was challenging, as much of the existing documentation focused on short timeframes or variables that lacked real-world significance. 

![Figure 2: Literature Review](https://itsnemoooo.github.io/assets/images/venn.png){: .half}

2. I began the summer, initially inspired by the potential of DRL to improve HVAC control (thanks to articles like [this](https://deepmind.google/discover/blog/deepmind-ai-reduces-google-data-centre-cooling-bill-by-40/)), but quickly realised that the scale of the task was far greater than I initially anticipated.
3. Representation. I wanted to ensure the solution I designed could be used in the real-world. This meant I had to make several choices about how to represent the state and action spaces. Also, with weather data, there are many different ways to preprocess the data to make it more representative of the real-world.

### Technical
1. Environment setup. EnergyPlus is powerful, but the documentation on the API is lacking.
2. Training time. Training time is dominated by the environment simulation, specifically the number of timesteps per hour in the 'run.idf' file. I originally focused on speeding it up by scaling my compute. I built a Docker container with a multi-GPU setup, but the image had to contain the entire EnergyPlus installation, which was too large to be practical. I ended up running the experiments locally, which was time-consuming.
3. Bugs in the starter codebase. The code I began to use was set up for evaluation and plotting as that research stream had ended. I found several hardcoded values, breaking the training loops and making it difficult to reuse the code for my project. It was a monolithic train/test/eval file with 1634 lines, most of which was API handling.
4. There were so many decisions to make: selecting frameworks, deciding whether to use HPC or run experiments locally, understanding how dataset choices might bias results, considering the creation of a new reward function, and evaluating the real-world impact and performance of my model.
5. Measuring performance. This was crucial to understand and very difficult to do comprehensively. Off-policy algorithms are notoriously difficult to evaluate, and I had to make several ad-hoc decisions about how to measure the performance of the model.

“Quality is more important than quantity. One home run is much better than two doubles.” - Steve Jobs

I knew we had to start with small, focused choices. I set up a schedule at the UCL AI centre, and focused on achievable goals. I learned a lot from my colleagues, and we had some great discussions about how to improve the project.

## Methodology

I chose to build upon a baseline algorithm: Deep Double Q-Network (DDQN). I refactored it to incorporate the Three Climate Experiment framework. The choice of algorithm was motivated by my previous experience with off-policy algorithms, and coursework in Reinforcement Learning at UCL (taught by Prof Hado van Hasselt).

There were several improvements to the baseline algorithm that I experimented with: decaying epsilon-greedy exploration, prioritised experience replay, and a new reward function. However, the most significant improvement came from the Three Climate Experiment framework, as discussed in the previous section. This was inspired from discussions with my co-supervisor, Dhruva. It is a simple, but powerful idea that I would recommend to anyone looking to improve the data efficency of their Deep Reinforcement Learning models. The results are discussed in the next section.
### Training
Initial training was conducted for 20 epochs in each climate. This was sufficient to train an agent that was able to generalize to new climates. The model weights were saved after each epoch for both the action and target networks.


### Environment
The environment is simulated using EnergyPlus, a building energy simulation program from the Department of Energy. The environment includes various thermal zones, each with its own temperature, humidity, and HVAC settings. The simulation is run with different weather data files to evaluate the performance of the DRL agent under diverse climate conditions.

The building used in this experiment is a six-zone office building.

### Action space
The action space consists of binary actions for each HVAC unit in the building's thermal zones. Each action can either turn the heating or cooling on or off for a specific zone. The action space is represented as a list of binary values, where each value corresponds to the state of the HVAC unit in that zone.

For example, the action below indicates that the second zone is active, and depending on the current temperature, it will be cooled or heated (towards the pre-defined comfort range).

```python
action = [0, 1, 0, 0, 0, 0]  # zone 2 active
```

### State space
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

### Reward function
The reward function is designed to balance energy consumption and thermal comfort. It includes:
- A penalty for energy consumption (`reward_E`), which is negative and proportional to the HVAC energy usage.
- A comfort reward (`reward_T`), which penalizes deviations from a comfortable temperature range (68°F to 77°F) in each zone.
- An optional penalty for frequent changes in HVAC actions (`reward_signal`), which discourages instability in the system.

The total reward is a combination of these components, encouraging the agent to minimize energy use while maintaining comfort.
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Optimising HVAC Control</title>
</head>
<body>
    <p>The reward function is given as:</p>
    <p>R = L<sub>total</sub> = -(L<sub>T</sub> + L<sub>E</sub> + L<sub>S</sub>)</p>
    
    <p>The first term, L<sub>T</sub>, represents the temperature loss, defined as:</p>
    <p>
        L<sub>T</sub> = 
        <ul>
            <li>0, if T<sub>min</sub> ≤ T<sub>i</sub> ≤ T<sub>max</sub></li>
            <li>&nu;<sub>T</sub>(T<sub>i</sub> - T<sub>min</sub>)<sup>2</sup>, if T<sub>i</sub> ≤  T<sub>min</sub></li>
            <li>&nu;<sub>T</sub>(T<sub>i</sub> - T<sub>max</sub>)<sup>2</sup>, if T<sub>i</sub> ≥ T<sub>max</sub></li>
        </ul>
    </p>
    <p>Here, T<sub>i</sub> is the temperature of zone i, T<sub>min</sub> and T<sub>max</sub> are the minimum and maximum desired temperatures, and &nu;<sub>T</sub> is a tunable temperature loss factor.</p>

    <p>The second term, L<sub>E</sub>, is the energy consumption loss:</p>
    <p>L<sub>E</sub> = &nu;<sub>E</sub>E<sub>t</sub></p>
    <p>Here, E<sub>t</sub> is the energy consumption at time t, and &nu;<sub>E</sub> is the energy loss factor.</p>

    <p>The final term, L<sub>S</sub>, is the smoothness loss:</p>
    <p>L<sub>S</sub> = &nu;<sub>S</sub> ∑ (A<sub>t</sub> ⊕ A<sub>t-1</sub>)</p>
    <p>Here, A<sub>t</sub> is the action of the VAV unit at time step t, ⊕ denotes the XOR operation, and &nu;<sub>S</sub> is the smoothness loss factor. This term penalizes frequent ON/OFF transitions to reduce mechanical wear.</p>
</body>
</html>


## 📊 How'd we do?
The model unexpectedly acted mainly on **the building's centroid zone**, a behavior not explicitly programmed but emerging from the data. This indicates the model's ability to understand the problem's structure rather than just exploiting dataset specifics.

We compared the performance of the Three Climate Experiment Framework to a baseline control solution:
![Figure 3: Baseline Control](https://itsnemoooo.github.io/assets/images/base.png)
*Figure 3: Baseline Control.*

![Figure 4: Three Climate Experiment](https://itsnemoooo.github.io/assets/images/3ce.png)
*Figure 4: Three Climate Experiment.*

The results were outstanding, and the Three Climate Experiment Framework outperformed the baseline control solution by a significant margin. To ensure there was no leakage on the evaluation dataset, we created and used a separate, modified version of the dataset for evaluation. On this climate, the results were consistent with the training results.

- **Energy Efficiency Improvement:** The Three Climate Experiment Framework achieved a **53.02%** improvement in energy efficiency over baseline methods.
- **Energy Savings:** Total annual energy savings amounted to **1.064 million kWh**.
- **Robustness to Climate Variability:** Models validated with the modified weather dataset demonstrated resilience to extreme conditions, outperforming baselines by an average of **39.057 percentage points**.


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







## Next Steps
- Work submitted to Neurips 2024 Workshop on Tackling Climate Change with AI
- Encourage the use of the Three Climate Experiment Framework in the research community to further the following goals:
  - **SDG 7:** Affordable and Clean Energy.
  - **SDG 11:** Sustainable Cities and Communities.
  - **SDG 13:** Climate Action.
- Implement a more sophisticated reward function to encourage energy-efficient behavior.
- Explore the integration of other control strategies to further enhance performance.
- Expand the experiment to include more diverse climate conditions and scenarios.
