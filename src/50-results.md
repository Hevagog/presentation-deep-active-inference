# Results

Agents trained in the Animal-AI environment demonstrate **intelligent and adaptive behaviors**:

- **Complex Planning:** Capable of devising multi-step strategies to achieve goals.
- **Navigation & Obstacle Avoidance:** Learn to traverse environments and avoid obstacles, even with sparse rewards.
- **Robustness to Missing Input:** In "lights-off" experiments, agents maintain an internal world model and simulate future plans, despite temporary loss of visual input.


> This is remarkable because the transition model, $P_{\theta_s}(s_{t+1} \mid s_t, a_t)$, is implemented as a *feed-forward network*—it lacks explicit memory of previous states.
