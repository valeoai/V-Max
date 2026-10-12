<div align="center">
  <img src="docs/assets/png/logo.png" alt="Demo" width="100%" />
</div>

# V-Max

![Python version](https://img.shields.io/badge/Python-3.11-blue) [![Paper](https://img.shields.io/badge/arXiv-2503.08388-b31b1b.svg)](https://arxiv.org/abs/2503.08388)


**V-Max** is a plug-and-play extension of the [Waymax](https://github.com/waymo-research/waymax) simulator for autonomous driving research. It provides a learning-based motion planning framework for benchmarking, training, and evaluation of path planners from bird-eye view to control.

This framework integrates simulation pipelines, observation wrappers, and realistic metrics, making it easy to experiment with RL/IL algorithms, custom networks, and new features.


<div align="center">
<table>
  <tr>
    <th>Expert</th>
    <th>RL Policy</th>
  </tr>
  <tr>
    <td><img src="docs/assets/trajectories/expert/scene1.gif" alt="Expert Scene 1" width="300"/></td>
    <td><img src="docs/assets/trajectories/agent/scene1.gif" alt="Agent Scene 1" width="300"/></td>
  </tr>
  <tr>
    <td><img src="docs/assets/trajectories/expert/scene2.gif" alt="Expert Scene 2" width="300"/></td>
    <td><img src="docs/assets/trajectories/agent/scene2.gif" alt="Agent Scene 2" width="300"/></td>
  </tr>
</table>
</div>

## Key Features

- **Reinforcement Learning (SAC, PPO)** and **Imitation Learning (BC)** algorithms
- **Rule-based policies** (IDM, PDM)
- **Advanced network architectures** (MTR, Wayformer, ...)
- **Comprehensive metrics and evaluations**
- **ScenarioMax**: Unified datasets format with nuPlan, nuScenes and WOMD, with **SDC paths** support

## Framework Structure

The V-Max codebase is organized for modularity and extensibility:

```
vmax/
├── agents/
│   ├── learning/          # Reinforcement & imitation learning algorithms
│   ├── networks/          # Neural network architectures (MTR, Wayformer, etc.)
│   └── rule_based/        # Rule-based policies (IDM, PDM)
├── simulator/
│   ├── features/          # Feature extraction modules
│   ├── metrics/           # Evaluation metrics
│   ├── overrides/         # Waymax extensions and customizations
│   ├── visualization/     # Visualization tools and utilities
│   └── wrappers/          # Observation and environment wrappers
└── scripts/
```

- **agents/**: All agent logic, including learning-based and rule-based policies.
- **simulator/**: Simulation engine, feature extraction, metrics, and visualization.
- **scripts/**: Entry points for training and evaluation.

## ScenarioMax

[**ScenarioMax**](https://github.com/valeoai/ScenarioMax) is a core feature of V-Max that enhances our data with **SDC paths**. These paths are crucial for calculating targets, rewards, and various metrics during simulation.

Key objectives:

- **Enrich Data:** By incorporating SDC paths, ScenarioMax helps improve the precision of target computations, reward evaluations, and metric calculations.
- **Unified Dataset:** It consolidates data from different autonomous driving (AD) datasets into a single, standardized format, similar to the approaches found in [ScenarioNet](https://github.com/metadriverse/scenarionet).

For those who prefer to run V-Max without the complete ScenarioMax integration, a lightweight wrapper is available. This wrapper generates one single SDC path at every scenario reset. Keep in mind that while this approach simplifies testing, it increases computational overhead and may not always produce an SDC path that perfectly matches the ground truth.

#### Download

Datasets processed via ScenarioMax with SDC paths are available on HuggingFace:

  - [Mini datasets](https://huggingface.co/datasets/vcharraut/V-Max_Mini_Datasets) (~1,000 scenarios for nuPlan and WOMD)
  - [Full datasets](https://huggingface.co/datasets/vcharraut/V-Max_Datasets)


## Get Started

### Installation

1. **Clone the Repository**

   ```bash
   git clone https://github.com/valeoai/v-max
   cd v-max
   ```

2. **Create a Virtual Environment & Install Dependencies**

    ```bash
    python3 -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt
    pip install -e .
    ```

### Quickstart

Train any RL/IL algorithm and network encoder implemented in V-Max:

```bash
python vmax/scripts/training/train.py total_timesteps=$num_env_steps path_dataset="" algorithm=$alg_type network/encoder=$encoder_type
```

- See [`docs/training.md`](docs/training.md) for detailed training, feature selection, reward metrics, and configuration options.


## Documentation

- [Training & Configurations](docs/training.md)
- [Metrics](docs/metrics.md)
- [Observation Wrappers](docs/observations.md)
- [Simulator Overview](docs/v-max.md)


## Authors

- **[Valentin Charraut](https://github.com/vcharraut)**
- **[Thomas Tournaire](https://github.com/Titou78)**
- **[Waël Doulazmi](https://github.com/WaelDLZ)**

## Acknowledgements

V-Max is built upon the innovative ideas and contributions of several outstanding open-source projects:

- **[Brax](https://github.com/google/brax)** – RL pipeline philosophy
- **[Waymax](https://github.com/waymo-research/waymax)** – Simulation foundation
- **[ScenarioNet](https://github.com/metadriverse/scenarionet)** – Unified data strategies

We are grateful to these communities for advancing autonomous driving research.
