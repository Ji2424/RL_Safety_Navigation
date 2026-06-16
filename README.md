# Safety-Constrained Reinforcement Learning Navigation

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](YOUR_COLAB_NOTEBOOK_LINK_HERE)

A clean, minimal Custom Gymnasium environment built to study the fundamental tension between reward maximization and constraint satisfaction in Reinforcement Learning (RL). This project implements a custom $8 \times 8$ grid world, trains a Proximal Policy Optimization (PPO) agent using Stable-Baselines3, and tracks task performance and safety violations independently to evaluate safety-critical deployment trade-offs.

This problem mirrors real-world AI alignment challenges, such as balancing helpfulness vs. harmlessness via penalty coefficients during RLHF or implementing safe trajectory generation in robotics.

---

## 🚀 Quick Start

You can run this project instantly in your browser via Google Colab by clicking the badge above, or spin it up locally:

```bash
# Clone the repository
git clone [https://github.com/YOUR_USERNAME/safety-constrained-rl.git](https://github.com/YOUR_USERNAME/safety-constrained-rl.git)
cd safety-constrained-rl

# Install dependencies
pip install gymnasium stable-baselines3 matplotlib numpy

---

## 🟦 Environment & Layout Design

The custom environment `SafetyGridEnv` constructs an 8x8 grid layout:
* **Start State:** The agent begins at the top-left coordinate `(0, 0)`.
* **Goal State:** The target is located at the bottom-right coordinate `(7, 7)`.
* **Safety-Constrained Zones:** Configured red zones act as restricted spaces where safety violations are tracked and penalized.

### Reward Structure

| Event | Reward / Penalty | Description |
| :--- | :--- | :--- |
| **Reach Goal** | `+10.0` | Successfully completes the episode. |
| **Safety Zone Entry** | `-2.0` (Configurable) | Penalizes the agent for breaching constraints. |
| **Each Step** | `-0.1` | Constant time penalty to encourage efficiency. |
| **Hit Wall** | `-0.5` | Movement is blocked; incurs a minor penalty. |

---

## 📊 Core Research Experiment & Results

The primary objective of this project is answering a key safety alignment question: **How does the magnitude of the safety penalty coefficient affect the agent's willingness to satisfy constraints vs. maximize reward?**

We sweep across multiple penalty values (`0.0`, `0.5`, `1.0`, `2.0`, `5.0`, `10.0`) to plot a Pareto frontier of the safety-performance trade-off.

### 1. Training Curves
The agent is trained for 150,000 timesteps against a random baseline. 
<p align="center">
  <img src="training_curves.png" width="700" alt="PPO Training Curves">
</p>

### 2. The Safety-Performance Trade-off
As the safety penalty increases, the agent learns to favor longer, safer paths to the goal, mapping out the exact trade-off threshold where the agent shifts behavior.
<p align="center">
  <img src="safety_tradeoff.png" width="850" alt="Safety Performance Trade-off Frontier">
</p>

---

## 🛠️ Extensions & Future Work

This environment serves as a baseline playground for more complex alignment research. Planned extensions include:
1. **True Constrained RL (CMDP):** Separating constraint costs completely from the reward function and optimizing via Lagrangian methods (e.g., CPO) instead of manual reward shaping.
2. **Partial Observability:** Restricting the agent's observation space from a global coordinate view to a localized 3x3 window around its position.
3. **Distributional Shift / Generalization:** Randomizing the placement of safety zones during environment resets to test the agent's robust alignment out-of-distribution.
