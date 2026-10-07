# Models Directory

This directory contains trained model weights, export targets, and training metadata for perception and trajectory prediction modules.

---

## 📂 Subdirectories

- **`checkpoints/`**: Checkpoints organized by model category:
  - `checkpoints/detector/` (e.g. YOLO/LiDAR detector checkpoints)
  - `checkpoints/person_type/` (role classification weights)
  - `checkpoints/intent/` (trajectory and intention prediction weights)
- **`exported/`**: Serialized deployment-ready models (e.g. `.onnx`, TorchScript `.pt`, TensorRT engine files) optimized for inference in ROS 2 nodes.
- **`metadata/`**: Model configuration files, training hyperparameters, dataset version tags, benchmark metrics, and model cards.
