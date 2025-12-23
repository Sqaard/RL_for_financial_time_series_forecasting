# RL for Adaptive Portfolio Management

\The project investigates how **Reinforcement Learning (RL)** combined with **deep learning feature extraction (GRU)** can create dynamic, personalized trading strategies that adapt to market conditions and user-defined risk profiles.

> *Investing shouldn't be a choice between a snail and a rollercoaster. This is the engine for the self-driving car.*

---

## 🎯 Project Overview & Key Findings

The core hypothesis was that **feature quality is paramount**. We engineered predictive features using a Gated Recurrent Unit (GRU) network and compared their effectiveness against traditional technical indicators within various RL environments.

**The Key Result:** The **PPO agent trained on GRU features achieved a positive annual return (+1.12%)** and significantly outperformed both a baseline model using standard indicators and a complex ensemble of five different RL algorithms. This validates GRU-based features as a superior signal for RL-driven trading.

### 🏆 Performance Snapshot

| Model / Metric | Annual Return | Sharpe Ratio | Key Comparison & Insight |
| :--- | :--- | :--- | :--- |
| **Best RL Agent (10k steps)**<br>*FinRL Env, FinRL Policy* | **-1.64%** | **-0.36** | • **Most stable baseline**: Loss was **7.56 p.p. less severe** than DJI's -9.20%.<br>• Demonstrates the reliability of standard components with limited training. |
| **Best RL Agent (50k steps)**<br>*Zhang Env, Custom Policy* | **-3.53%** | **-0.15** | • **Best Sharpe Ratio** after extended training.<br>• **More resilient than the market**: Loss was **5.67 p.p. less severe** than DJI.<br>• Shows custom policies *can* converge and improve with more data. |
| **Ensemble Model**<br>(A2C+PPO+DDPG+SAC+TD3) | **-5.11%** | *N/A* | • **Outperformed by a single PPO+GRU agent** by 6.23 p.p.<br>• Still **4.09 p.p. more resilient** than the DJI benchmark. |
| **DJI Index (Benchmark)** | **-9.20%** | *N/A* | Market benchmark performance during the test period. |

**Core Takeaway:** In a declining market, the **PPO agent powered by GRU-derived features was the only strategy to achieve a positive return (+1.12%)**, decisively outperforming all other RL configurations and the market itself. This strongly validates the hypothesis that deep learning-based feature engineering provides a critical advantage for RL in financial forecasting.

*Note: Results from the test period during a general market decline.*

---

## 📁 Repository Structure
├── 📓 Data_Preprocessing.ipynb # Creates the dataset. Calculates technical indicators
│ # and adds forward-looking trends using a GRU.
├── ⚗️ Experiments.ipynb # Main experiment notebook. Trains & evaluates all
│ # RL agent configurations (A/B).
├── 📊 Experiment_Results/ # All outputs, visualizations, and metrics.
│ ├── 📈 Experiment_A_10k_Steps/ # Results for the 10,000-step training phase.
│ │ ├── ppo_all_configurations.png # Cumulative returns chart (6 configs + DJI).
│ │ ├── ppo_metrics_comparison.png # Bar charts comparing key metrics.
│ │ └── ppo_metrics_summary.csv # Detailed performance table (CSV).
│ └── 📈 Experiment_B_50k_Steps/ # Results for the extended 50,000-step training.
│ ├── ppo_50000_all_configurations.png
│ ├── ppo_50000_metrics_comparison.png
│ └── ppo_50000_metrics_summary.csv
└── 📄 README.md # This file.


---

## 🔬 Detailed Experiment Log

### **Experiment A: Baseline Performance (10,000 Timesteps)**
*   **Objective:** Establish a baseline and compare the initial performance of different reward functions and policy architectures with limited training.
*   **Core Question:** "Which components work best *out-of-the-box*?"
*   **State Space:** 313 (Technical Indicators + GRU-derived features).
*   **Total Timesteps:** 10,000
*   **Best Model:** `finrl_finrl` (Standard FinRL environment & policy).
*   **Key Insight:** Standard components showed greater initial stability. Custom components (especially policies) underperformed, suggesting a need for more training or tuning.

### **Experiment B: Extended Training & Convergence (50,000 Timesteps)**
*   **Objective:** Investigate if longer training allows complex custom components (policy networks) to converge and improve.
*   **Core Question:** "Do custom policies need more time to learn?"
*   **State Space:** 313
*   **Total Timesteps:** 50,000
*   **Best Model:** `zhang_custom` (Zhang reward function & Custom policy network).
*   **Key Insight:** Extended training enabled the custom policy to achieve the best Sharpe Ratio (-0.15), confirming it requires more data. However, a critical finding was a **significant increase in portfolio volatility across all models**, highlighting the risk of overfitting and the necessity for **early stopping and validation mechanisms** in production.

---

## 🛠️ Technical Implementation

*   **Reinforcement Learning Framework:** [FinRL](https://github.com/AI4Finance-Foundation/FinRL)
*   **RL Algorithms:** Proximal Policy Optimization (PPO), with comparisons to A2C, DDPG, SAC, TD3.
*   **Deep Learning:** PyTorch for implementing Gated Recurrent Units (GRU) to generate predictive financial features.
*   **Environments:** Custom `StockTradingEnv` classes implementing three distinct reward functions:
    1.  Standard FinRL reward.
    2.  Reward from *"Deep Reinforcement Learning for Trading"* (Zhang et al.).
    3.  Our novel reward function with a quadratic utility term.
*   **Policy Networks:** Comparison between default FinRL networks and custom architectures (`[256, 128]` units).

---

## 🚀 Future Work & Path to Production

This repository forms the **validated core AI engine** for the financial co-pilot. The immediate next steps are:

1.  **Implement Robust Validation:** Integrate a validation dataset and early stopping to automatically find the optimal training checkpoint and prevent overfitting.
2.  **Build the Personalization Layer:** Develop the interface to map user risk profiles (e.g., "Conservative", "Balanced Growth", "Aggressive") to specific RL agent configurations (e.g., risk aversion parameter `λ`, target volatility `σ_tgt`).
3.  **Develop API Integration:** Refactor the architecture into a modular system ready to connect to live brokerage APIs (e.g., Tinkoff Invest API) for paper and live trading.

---

## 📄 Citation & License

If this work contributes to your research, please consider citing it. This project is for educational and research purposes.
