# 05. Reinforcement Learning

## 1. Overview
Reinforcement Learning (RL) involves an agent learning a **policy**—a sequence of actions—through trial-and-error interactions with an environment. Rather than mapping isolated inputs to outputs, RL optimizes for long-term cumulative reward.

## 2. Core Dynamics
- **Sequential Decision Making:** Action quality is evaluated by its contribution to a long-term goal. A move that appears locally suboptimal may be globally optimal within the broader policy context (e.g., sacrificing a piece in chess).
- **Feedback Mechanism:** The agent improves its policy based on trajectory outcomes and delayed rewards, rather than immediate, explicit corrections.
- **Exploration vs. Exploitation:** A fundamental challenge where the agent must balance exploring new states to discover better strategies and exploiting known strategies to maximize current reward.

## 3. Operational Challenges
- **Credit Assignment:** Determining which specific action within a long sequence was responsible for an ultimate delayed reward or penalty.
- **Partial Observability:** The agent may only perceive local, noisy cues rather than the exact global state of the environment. *Example:* A robot might only know there is a wall to its left, rather than knowing its exact coordinates in the room.
- **Generalization:** Robust policies must generalize across environmental variations and unforeseen states.
- **Safety Constraints:** In physical applications like robotics, exploration must be bounded to prevent catastrophic hardware damage.

## 4. Applications
RL naturally bridges ML with classical AI planning and control systems. It is particularly dominant in:
- Game playing (e.g., Chess, Go) with massive sequential search spaces.
- Autonomous robotics (e.g., obstacle avoidance, dynamic navigation).
- **Multi-agent systems** requiring cooperation toward shared objectives (e.g., a team of robots playing soccer).

## 5. Mathematical Formulation

**Return (Discounted Cumulative Reward):**
The total return $G_t$ from time step $t$ is the sum of discounted future rewards:
$$ G_t = \sum_{k=0}^{\infty} \gamma^k r_{t+k+1} $$
*(Where $\gamma \in [0,1]$ is the discount factor and $r$ is the reward.)*

**Optimal Policy ($\pi^*$):**
The learning objective is to find a policy $\pi$ that maximizes the expected return:
$$ \pi^* = \arg\max_\pi \mathbb{E}_\pi [G_t] $$

## 6. RL Interaction Loop

```text
           +-----------------------+
           |      Environment      |
           |   (State Transition)  |
           +-----------------------+
             /                   ^
    (State S_t)                  |
    (Reward R_t)            (Action A_t)
           \                     |
           v                     |
           +-----------------------+
           |         Agent         |
           |  (Policy: π(A_t|S_t)) |
           +-----------------------+
```

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](04_unsupervised_learning.md) | [Next](06_applications_of_ml.md)
