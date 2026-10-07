# AutoCobots

An autonomous collaborative robot (cobot) system designed for dynamic human-aware navigation, dynamic SLAM, risk-aware safety control, and human intention prediction in warehouse and industrial environments.

---

## 📁 Project Architecture & Directory Structure

```text
├── README.md
├── docker/                        # Dockerfiles, docker-compose (sim + ROS 2 + web)
├── config/                        # YAML configs: robot, sensors, behavior profiles, scenarios
├── scripts/                       # setup, build, run-experiment, export-results helpers
├── tests/                         # automated tests (mirrors src/ structure)
│
├── src/                           # all source code, one package per architecture module
│   ├── interfaces/                # custom ROS 2 msgs / srvs / actions (shared contracts)
│   ├── common/                    # shared utils: geometry, logging, config loading, time sync
│   ├── simulation/
│   │   ├── worlds/                # warehouse layout, shelves, aisles, restricted zones
│   │   ├── robot/                 # robot model, sensor models (LiDAR, RGB-D, IMU, noise)
│   │   ├── human_avatars/         # worker / visitor / child avatars and motion scripts
│   │   └── scripted_events/       # fallen box, shifted rack, blocked aisle, crossing person
│   ├── slam/
│   │   ├── baseline/              # SLAM Toolbox / RTAB-Map wrapper
│   │   ├── dynamic_filter/        # moving-object detection and filtering
│   │   ├── change_detection/      # temporary vs persistent change
│   │   └── map_confidence/        # confidence / age of map elements
│   ├── perception/
│   │   ├── detection/             # camera + LiDAR person detection
│   │   ├── tracking/              # SORT / ByteTrack, anonymous track IDs
│   │   └── person_type/           # role classification (worker, visitor, child, unknown)
│   ├── prediction/
│   │   ├── baseline/              # constant-velocity model
│   │   ├── learned/               # LSTM / Transformer intent + trajectory models
│   │   └── uncertainty/           # uncertainty estimation and calibration
│   ├── safety_control/
│   │   ├── risk/                  # risk score
│   │   ├── behavior_profiles/     # type-dependent parameter sets
│   │   ├── navigation/            # Nav2 integration, adaptive speed / path
│   │   ├── explanations/          # human-readable decision explanations
│   │   └── safety_layer/          # deterministic limits + e-stop (no learned models)
│   ├── control_center/
│   │   ├── backend/               # FastAPI + database
│   │   ├── frontend/              # React + roslibjs (live map, control, replay, performance)
│   │   └── bridge/                # rosbridge configuration
│   └── experiments/
│       ├── runner/                # scenario execution, repeatable runs
│       ├── baselines/             # static-map and reactive stop-and-wait comparisons
│       ├── metrics/               # ATE, RPE, ADE/FDE, safety and efficiency metrics
│       └── logging/               # run recording for replay
│
├── doc/                           # reports and all project documents
│   ├── semester-1/
│   ├── semester-2/
│   ├── architecture/              # module diagrams, ROS 2 topic/node graph
│   ├── api/                       # ROS 2 interfaces and REST endpoints
│   ├── user-guide/                # installation and usage
│   ├── safety-and-ethics/         # privacy, bias risks, limits of role classification / fatigue proxy
│   ├── experiment-reports/        # results write-ups per experiment
│   └── presentations/
│
├── ref/                           # literature and reference material
│   ├── papers/                    # SLAM, pedestrian prediction, human-aware navigation
│   ├── reports/
│   ├── standards/                 # e.g. ISO 10218, ISO/TS 15066, ISO 3691-4
│   └── datasets/                  # dataset descriptions, licenses, download notes
│
├── log/                           # team records
│   ├── meetings/
│   ├── weekly-progress/
│   ├── risks/
│   └── decisions/
│
├── data/                          # all project data (large files not committed to Git)
│   ├── README.md
│   ├── raw/                       # public pedestrian datasets, original downloads
│   ├── interim/
│   ├── processed/                 # training-ready trajectory / image sets
│   ├── synthetic/                 # simulation-generated pedestrians and images
│   ├── rosbags/                   # recorded simulation runs (for replay)
│   └── results/                   # experiment outputs, metric tables
│
├── models/                        # trained or pretrained AI models
│   ├── README.md
│   ├── checkpoints/               # one subfolder per model (detector, person_type, intent)
│   ├── exported/                  # ONNX / TorchScript for deployment
│   └── metadata/                  # training configs, datasets used, metrics, versions
│
└── ai/                            # AI-assistant working files
    ├── prompts/
    ├── plans/
    ├── task-templates/
    └── generated-change-records/
```

---

## 🚀 Key Modules Overview

- **`src/simulation`**: Gazebo/Ignition simulation environments, warehouse world definitions, robot URDF/SDF models, sensor setups, human avatar animations, and scripted stress scenarios.
- **`src/slam`**: Dynamic SLAM incorporating dynamic object filtering, long-term vs. short-term map change detection, and spatial map confidence calculation.
- **`src/perception`**: Multi-modal (camera + LiDAR) person detection, multi-object tracking (e.g., ByteTrack/SORT), and role/type classification.
- **`src/prediction`**: Trajectory and intention prediction with baselines (CV) and neural architectures (LSTM/Transformer) alongside uncertainty calibration.
- **`src/safety_control`**: Multi-tiered safety stack featuring deterministic safety envelopes, dynamic risk assessment, behavior profiles, Nav2 controllers, and explainable safety decisions.
- **`src/control_center`**: Central operator dashboard featuring FastAPI backend, React + roslibjs frontend, and rosbridge integration.
- **`src/experiments`**: Experiment runner, benchmarking suite, baselines, and standardized safety/efficiency evaluation metrics.
