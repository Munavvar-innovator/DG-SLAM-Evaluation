# DG-SLAM-Evaluation
"Empirical evaluation of DG-SLAM paper (NeurIPS 2024)..."
# DG-SLAM Hyper Pose Estimation Stage 1: DROID-SLAM Coarse Tracking

Implementation of Stage 1 (Coarse Tracking) from the paper:
**"DG-SLAM: Robust Dynamic Gaussian Splatting SLAM with Hybrid Pose Optimization"** (NeurIPS 2024)

**EECE 5550 Mobile Robotics - Fall 2025**  
**Team:** Raphael Dias, Ahmad Hassan, Mir Munavvar Ali  
**Northeastern University**

##  Overview

This repository implements the **coarse tracking stage** of DG-SLAM, which uses DROID-SLAM visual odometry with pretrained weights for robust pose estimation in dynamic scenes.

### What's Included:
- ✅ DROID-SLAM visual odometry with pretrained weights
- ✅ Motion mask generation using depth warping
- ✅ TUM RGB-D dataset loader
- ✅ Evaluation metrics (ATE)
- ✅ Trajectory visualization

### What's NOT Included:
-  Stage 2 (Gaussian Splatting fine refinement)

##  Quick Start

### Installation
```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/DG-SLAM-Stage1.git
cd DG-SLAM-Stage1

# Install dependencies
pip install -r requirements.txt
```

### Download Pretrained Weights

The DROID-SLAM pretrained weights will be automatically downloaded when you run the code, or download manually:
```bash
# Manual download (optional)
mkdir checkpoints
# Download droid.pth from: https://drive.google.com/file/d/1PpqVt1H4maBa_GbPJp4NwxRsd9jk-elh
```

### Run on TUM Dataset
```bash
# The code will automatically download the TUM sequence
python stage1_complete.py
```

The script will:
1. Download pretrained DROID weights (~100MB)
2. Download TUM RGB-D sequence (~500MB)
3. Run Stage 1 tracking
4. Display results and plots

##  Usage

### Basic Usage
```python
from stage1_complete import main

# Run on TUM walking sequence (100 frames)
results = main(
    sequence_name='rgbd_dataset_freiburg3_walking_xyz',
    num_frames=100,
    start_frame=0,
    download=True
)
```

### Custom Parameters
```python
# Run on different sequence with custom parameters
results = main(
    sequence_name='rgbd_dataset_freiburg3_sitting_xyz',
    num_frames=200,
    start_frame=50,
    download=True
)

## 🛠️ Technical Details

### Architecture
```
Stage 1: DROID-SLAM Coarse Tracking
├── Feature Extraction
│   ├── RGB Encoder (Conv + GroupNorm)
│   └── Depth Encoder (Conv + GroupNorm)
├── Iterative Refinement (GRU-based)
└── Motion Mask Generation
    ├── Depth Warping (Eq. 5)
    ├── Depth Difference Check (Eq. 6)
    └── Temporal Consistency (Eq. 7)
```

### Key Components

1. **DROID-SLAM Network**: Visual odometry with pretrained weights
2. **Motion Mask Generator**: Identifies static/dynamic regions
3. **TUM Dataset Loader**: Loads and processes TUM RGB-D data
4. **Evaluation**: Computes ATE and visualizes trajectories

##  Project Structure
```
DG-SLAM-Stage1/
├── stage1_complete.py      # Main implementation
├── requirements.txt        # Python dependencies
├── README.md              # This file
├── results/               # Output directory (gitignored)
├── checkpoints/          # Pretrained weights (gitignored)
└── data/                 # TUM dataset (gitignored)
```

## 🔬 Experiments

### Reproduction Study
- Evaluate on TUM RGB-D dynamic sequences
- Compare ATE with paper results
- Verify motion mask effectiveness

### Robustness Testing
- Frame skip (2x, 3x speed)
- Varying depth thresholds (0.3, 0.6, 0.9)
- Different dynamic object densities

## 📚 References
```bibtex
@inproceedings{xu2024dgslam,
  title={DG-SLAM: Robust Dynamic Gaussian Splatting SLAM with Hybrid Pose Optimization},
  author={Xu, Yueming and Jiang, Haochen and Xiao, Zhongyang and Feng, Jianfeng and Zhang, Li},
  booktitle={NeurIPS},
  year={2024}
}

@article{teed2021droid,
  title={DROID-SLAM: Deep Visual SLAM for Monocular, Stereo, and RGB-D Cameras},
  author={Teed, Zachary and Deng, Jia},
  journal={NeurIPS},
  year={2021}
}
```

## 🙏 Acknowledgments

- **DG-SLAM**: https://github.com/fudan-zvg/DG-SLAM
- **DROID-SLAM**: https://github.com/princeton-vl/DROID-SLAM
- **TUM RGB-D**: https://vision.in.tum.de/data/datasets/rgbd-dataset

## 📝 License

MIT License - see LICENSE file for details

## 👥 Team

- **Raphael Dias** - dias.ra@northeastern.edu
- **Ahmad Hassan** - hassan.ahmad@northeastern.edu
- **Mir Munavvar Ali** - mirmunavvarali.f@northeastern.edu

**Course**: EECE 5550 Mobile Robotics  
**Institution**: Northeastern University  
**Semester**: Fall 2025

## 📧 Contact

For questions or issues, please open an issue on GitHub or contact the team members.
