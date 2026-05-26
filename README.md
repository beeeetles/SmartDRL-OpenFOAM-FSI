# SmartDRL-OpenFOAM-FSI

# SmartDRL-OpenFOAM: An AI-Driven Autonomous Agent for FSI Shape Optimization 🚀

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![OpenFOAM](https://img.shields.io/badge/OpenFOAM-v2012+-orange.svg)
![SmartSim](https://img.shields.io/badge/Powered%20by-SmartSim-red.svg)

## 📌 Project Overview
This project presents an advanced **AI4Science framework** that couples Deep Reinforcement Learning (DRL) Agents with Computational Fluid Dynamics (CFD). By integrating **SmartSim** and **SmartRedis**, it achieves high-throughput, in-memory data exchange between a Python-based DRL agent and an OpenFOAM C++ simulation environment, specifically designed for complex Fluid-Structure Interaction (FSI) and aerodynamic shape optimization.

## 🎯 Core Pain Points Solved
In traditional CFD-DRL coupling, data exchange (states, rewards, actions) heavily relies on disk I/O, which creates a massive bottleneck during the millions of iterations required for Reinforcement Learning. 
* **The Solution:** We deploy an in-memory database using SmartRedis, allowing the OpenFOAM solver to act as an active environment that streams runtime flow-field data directly to the DRL agent in milliseconds.

## 🧠 Core Logic & Architecture

The architecture consists of three main cooperating components:
1.  **The Environment (OpenFOAM):** Solves the Navier-Stokes equations and evaluates the aerodynamic performance (e.g., $C_d$, $C_l$).
2.  **The Memory Layer (SmartRedis):** Acts as the high-speed communication bridge, completely bypassing disk I/O.
3.  **The Agent (DRL in Python):** Observes flow states and outputs optimization actions.

### ⚠️ Key Technical Innovation: Robust Mesh Deformation
Unlike standard implementations that rely on simple "airfoil rotation" (which frequently leads to mesh divergence and solver crashing in extreme conditions), this framework's Agent outputs specific mesh adjustment vectors. Combined with robust topology-preserved mesh deformation techniques, it ensures strict numerical convergence even under highly non-linear boundary shape alterations.

## 🛠️ Tech Stack
* **Simulation:** `OpenFOAM`
* **AI/DRL:** `Python`, `PyTorch` (or equivalent), Custom Agent architectures.
* **Infrastructure:** `SmartSim`, `SmartRedis`
* **Data Processing:** `NumPy`, `SciPy`, `Matplotlib`

## 🚀 Quick Start
*(Provide brief instructions on how to start the Redis server, launch the OpenFOAM solver with the SmartRedis linked library, and start the Python DRL training script.)*

```bash
# 1. Start the SmartRedis Database
smart node --port 6379

# 2. Launch the DRL Agent
python train_agent.py

# 3. Run the OpenFOAM Environment
./Allrun
