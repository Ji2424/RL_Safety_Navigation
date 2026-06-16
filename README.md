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
