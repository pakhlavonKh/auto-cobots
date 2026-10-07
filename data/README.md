# Data Directory

This directory stores all project datasets, recordings, intermediate artifacts, and experiment results.

> **Note:** Large data files (raw datasets, rosbags, large processed datasets) should **not** be committed directly to Git. Ensure large artifacts are managed via external storage (e.g., DVC, cloud buckets) or listed in `.gitignore`.

---

## 📂 Subdirectories

- **`raw/`**: Unmodified public datasets, original downloads (pedestrian datasets, warehouse scans).
- **`interim/`**: Intermediate transformed data during cleaning, synchronization, or formatting.
- **`processed/`**: Training-ready datasets (clean trajectories, calibrated bounding boxes, normalized feature vectors).
- **`synthetic/`**: Simulation-generated sensor logs, human trajectories, and synthetic camera/LiDAR recordings.
- **`rosbags/`**: ROS 2 bag files recorded from physical or simulated test runs for offline testing and replay.
- **`results/`**: Outputs from experiment runs, benchmark logs, evaluation summaries, and metric tables.
