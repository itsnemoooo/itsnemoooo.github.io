# The Three Climate Experiment

## Project Summary

### Optimising HVAC Control Across Diverse Climates: A Replay-Enhanced Deep Reinforcement Learning Approach

This project addresses the inefficiencies of traditional rule-based control (RBC) methods for managing Heating, Ventilation, and Air Conditioning (HVAC) systems. HVAC systems account for up to 40% of total energy consumption in commercial buildings and exhibit nonlinear behavior under varying weather conditions, making RBC insufficient for optimization in modern, changing environments. To tackle these challenges, we explore the potential of Deep Reinforcement Learning (DRL) to develop more adaptive and efficient control strategies.

---

### Research Question

**How can a deep reinforcement learning agent efficiently manage HVAC systems across diverse and rapidly changing climate conditions?**

---

### Key Contributions

1. **Three Climate Experiment Framework**
   - **Description:** Developed a novel framework that trains DRL agents across diverse climate conditions using the Replay across Experiments (RaE) methodology.
   - **Impact:** Enhanced robustness and performance in both normal and extreme weather scenarios.

2. **Novel Global Weather Dataset**
   - **Description:** Created a unique dataset from seven countries, modified to reflect current climate variability, providing a realistic and challenging evaluation environment.
   - **Impact:** Improved the generalization and resilience of DRL models against real-world climate variations.
   - **Code Snippet:**
     ```python
     # Example of dataset perturbation
     modified_weather_data = original_weather_data + np.random.normal(mean, std_dev, size)
     ```

3. **Performance and Energy Savings**
   - **Description:** Achieved significant improvements in energy efficiency and substantial annual energy savings.
   - **Impact:** Demonstrated a 53.02% improvement in energy efficiency over baseline methods, leading to up to 1.064 million kWh annual energy savings.
   - **Summary Table:**
     ```markdown
     | Category             | Performance          | Description                          | Impact                       |
     |----------------------|----------------------|--------------------------------------|------------------------------|
     | Baseline             | +/- 6.4% accuracy    | Solid foundation for comparisons     | Open-source refactored code  |
     | Three Climate (10k)  | 13.34% improvement   | Energy efficiency in non-extreme climates | 162,014 kWh p.a. savings     |
     | Three Climate (100k) | 53.02% improvement   | Significant gains in all conditions  | 378,458 kWh p.a. savings     |
     | Modified Climate     | 54.11% improvement   | Resilient to extreme climates        | 523,616 kWh p.a. savings     |
     | **Total Impact**     |                      |                                      | **1.064 million kWh p.a.**  |
     ```

---

### Methodology

The project builds upon a baseline Deep Double Q-Network (DDQN) algorithm, refactoring it to incorporate the Three Climate Experiment framework. By training DRL agents across three distinct climate conditions and leveraging the RaE approach, the models demonstrate:

- **Improved Stability and Faster Convergence:** Enhanced learning efficiency and reliability.
- **Enhanced Performance in Varied Conditions:** Better adaptability to both typical and extreme weather scenarios.

## Results and Impact

- **Energy Efficiency Improvement:** The Three Climate Experiment Framework achieved a 53.02% improvement in energy efficiency over baseline methods.
- **Energy Savings:** Total annual energy savings amounted to 1.064 million kWh.
- **Robustness to Climate Variability:** Models validated with the modified weather dataset demonstrated resilience to extreme conditions, outperforming baselines by an average of 39.057 percentage points.
- **Sustainable Development Goals (SDGs) Contribution:**
  - **SDG 7:** Affordable and Clean Energy.
  - **SDG 11:** Sustainable Cities and Communities.
  - **SDG 13:** Climate Action.



[Thesis PDF](https://itsnemoooo.github.io/ExecutiveSummary.pdf)


## Next Steps
- Work submitted to Neurips 2024 Workshop on Tackling Climate Change with AI
- Implement a more sophisticated reward function to encourage energy-efficient behavior.
- Explore the integration of other control strategies to further enhance performance.
- Expand the experiment to include more diverse climate conditions and scenarios.
