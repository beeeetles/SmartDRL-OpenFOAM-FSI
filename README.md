# SmartDRL-OpenFOAM: AI-Driven Aerodynamic Shape Optimization Framework 🚁

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-EE4C2C.svg)
![OpenFOAM](https://img.shields.io/badge/OpenFOAM-v2406-orange.svg)
![SmartSim](https://img.shields.io/badge/Powered%20by-SmartSim-red.svg)
![Status](https://img.shields.io/badge/Status-Research%20Pre--release-yellow.svg)

> **⚠️ 特别声明 (Notice)**
> 鉴于本项目相关的核心学术论文尚未正式发表，本仓库目前仅开源**初级验证版本**与**基础架构代码**（Core Architecture & Initial Release）。
> 完整的超参数配置、最终版奖励函数权重（Reward shaping details）以及高保真网格变形策略，将在论文被接收后进行完整开源，敬请期待。

## 📌 Project Overview | 项目简介
本项目是一个面向 AI4Science 领域的自动化气动外形优化 Agent 框架。通过结合深度强化学习（DRL）与计算流体力学（CFD），旨在解决复杂流场下的翼型/结构外形优化问题。

框架使用 **SmartSim** 作为底层调度与内存交互枢纽，将基于 **Python/PyTorch** 的 PPO 智能体与基于 **C++** 的 OpenFOAM 求解器无缝连接。相比传统依靠磁盘 I/O 的联合仿真，本框架大幅提升了数据吞吐量与训练稳定性。

## ✨ Core Features | 核心特性
1. **轻量化 PPO 智能体 (Custom PPO Agent)**: 针对物理仿真环境设计的保守策略 Actor-Critic 网络，确保在高度非线性的流场环境中动作输出的稳定性。
2. **CST 几何参数化 (CST Geometry Parameterization)**: 摒弃了容易导致网格发散的整体旋转策略，Agent 直接输出 CST (Class Shape Transformation) 函数的 10 维系数增量，实现高维度的局部外形精细调控。
3. **多维物理约束的奖励机制 (Physics-Informed Reward)**: 环境 (`environment.py`) 中内置了包含升阻比 (L/D Ratio)、面积偏差约束、翼型厚度约束 (Thickness constraint) 及平滑度惩罚的多维奖励函数。
4. **SmartSim 自动化调度**: 自动化生成 `blockMeshDict`、处理 OpenFOAM 案例克隆、并行执行与数据后处理提取。

## 🧠 System Architecture | 系统架构

* **State Space**: CST 系数 + 当前气动性能 (升阻比、面积偏差等)。
* **Action Space**: CST 系数的连续增量调整 (-0.01 ~ +0.01)。
* **Environment**: OpenFOAM (`simpleFoam`) 求解器计算稳定后的受力系数。

## 🛠️ Tech Stack | 技术栈
* **AI/DRL**: `PyTorch`, `Gymnasium`
* **CFD Simulation**: `OpenFOAM v2406`
* **Infrastructure**: `SmartSim`
* **Math & Geometry**: `NumPy`, `SciPy` (Bernstein polynomials)

## 🚀 Quick Start | 快速开始

### 1. 环境依赖安装
```bash
# 建议使用 Conda 创建虚拟环境
conda create -n drl-fsi python=3.10
conda activate drl-fsi

# 安装 Python 依赖
pip install -r requirements.txt
