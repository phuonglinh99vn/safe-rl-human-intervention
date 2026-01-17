# Safety‑Aware Reinforcement Learning in Grid World

> A portfolio project demonstrating reinforcement learning, risk modelling, and neural networks applied to safe decision‑making.

This project combines **tabular Q‑learning** with a **supervised danger‑prediction model** to create an agent that learns to navigate a hazardous environment while reasoning about risk. The work mirrors real‑world problems such as autonomous navigation, healthcare decision support, and robotics safety.

---

## What This Project Demonstrates

* End‑to‑end RL workflow: environment → agent → evaluation
* Experiment design & comparison of reward shaping
* Feature engineering for state‑action safety representation
* Neural network classification with imbalanced classes
* Writing clean, modular research code

**Skills:** Python · Reinforcement Learning · Neural Networks · Data Engineering · Experiment Analysis

---

## Problem Overview

A 10×10 Grid World contains:

* Start at (0,0), goal at (9,9)
* 15 hazardous cells (terminal failure)
* Actions: UP / DOWN / LEFT / RIGHT

The agent must reach the goal while minimizing:

1. Number of steps
2. Visits to dangerous regions

Two step‑penalty settings were studied:

* Mild: −0.1
* Harsh: −1.0

---

## 1. Environment Design

**Key features**

* Deterministic transitions with boundary checks
* Configurable reward structure
* Text renderer for debugging
* Support for fixed or random safe starts

**Reward function**

* Goal: +10
* Hazard: −10
* Step: configurable penalty

---

## 2. Q‑Learning Agent

**Algorithm**
Q(s,a) ← Q(s,a) + α[r + γ max Q(s',·) − Q(s,a)]

**Training setup**

* 2000 episodes
* ε‑greedy exploration (1.0 → 0.05)
* α = 0.1, γ = 0.99

**Evaluation metrics**

* Episode reward
* Episode length
* Safety violations
* Success rate

**Insights**

* Mild penalty encouraged exploration and higher returns
* Harsh penalty produced risk‑averse but inefficient policies
* Clear trade‑off between speed and safety

---

## 3. Danger Map & Dataset Engineering

To enable safety reasoning, a **distance‑to‑hazard map** was generated using BFS.

**Risk labels**

* 0 – Hazard
* 1 – One step away
* 2 – Two steps away
* 3 – Safe region

**Feature vector (10D)**

* Current position (x,y)
* One‑hot action
* Next position (x',y')
* Normalized danger distances

Dataset split: 70/15/15

---

## 4. Neural Network Risk Predictor

**Architecture**

* Dense 64 → ReLU
* Dense 64 → ReLU
* Softmax (4 classes)

**Outcome**

* Near‑perfect accuracy on unseen states
* Enables pre‑action safety screening

---

## 5. Safety‑Aware RL Concept

The classifier can act as a **shield**:

* Block actions predicted as high‑risk
* Guide exploration without reward hacking

This mirrors techniques used in:

* Safe robotics
* Clinical decision support
* Autonomous vehicles

---

## ▶️ Run

safe_rl_shield.ipynb
complete_dataset.pkl
safety_shield.h5

---

## Future Improvements

* Double Q‑learning / SARSA comparison
* Prioritized replay for rare hazards
* Cost‑constrained RL (CMDP)
* Explainable risk features

---

## 👩‍💻 Author

**Linh**

