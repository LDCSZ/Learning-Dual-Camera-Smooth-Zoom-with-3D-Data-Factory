# Learning-Dual-Camera-Smooth-Zoom-with-3D-Data-Factory
Code of Learning Dual-Camera Smooth Zoom via Decoupled Geometric-Photometric Data Synthesis

## 1.Abstract
<p align="center"><img src="./assets/intro.png" width="95%"></p>
When zooming between dual cameras on smartphones, prominent discontinuities in both geometric perspective and color rendition inevitably degrade the visual experience of users. To address this, we introduce the dual-camera smooth zoom (DCSZ) task, aiming to synthesize continuous intermediate frames for fluid zooming. However, directly applying existing video frame interpolation (VFI) models to this task is severely hindered by substantial domain gaps and the physical intractability of capturing real-world continuous ground truth. To this end, we propose a novel data synthesis framework to generate high-fidelity DCSZ training sequences, named ZoomGS v2. It explicitly decouples geometric trajectories and photometric transformations from 3D representation modeling, thereby enabling extensive data generation from easily accessible single-camera 3D scenes. Furthermore, we design ZoomFI, a specialized VFI network tailored to the DCSZ task, which leverages complementary bidirectional optical flows for comprehensive dual-camera information fusion. Extensive experiments on real-world datasets of two mobile phones demonstrate that training with our constructed DCSZ data significantly improves the performance of various VFI models. Moreover, the proposed ZoomFI achieves state-of-the-art results in both quantitative metrics and visual quality. The datasets, codes, and pre-trained models will be publicly available.

## 2.Method
### 2.1 ZoomGS v2
<p align="center"><img src="./assets/pipline_synzoomgs.png" width="95%"></p>
(a) The pipeline of ZoomGS v2. ZoomGS v2 first construct corresponding W camera from UW via math operations and relative vector sampled from Distribution, and calculate camera parameters of UW and W and interpolate camera parameter of virtual cameras. Then it render image sequence from reconstructed 3DGS representation. Finally it predict photometric transformation parameters from color predicting CNN and interpolates them, and applies them to the photometric transformation. (b) Statistics of relative vector Distribution. ZoomGS v2 collect multiple camera parameters from UW&W pairs and statistically obtain gaussian distribution. (c) Training of Color Prediction CNN. ZoomGS v2 train a CNN with UW&W pairs to predict the parameters of photometric transformation pipline from UW to W. The UW images are aligned to W images.

### 2.2 Zoom FI
<p align="center"><img src="./assets/FI_model.png" width="95%"></p>
Structure of ZoomFI. Left is the pipeline of ZoomFI, right is the structure of RBlock in ZoomFI.

## 3.Prerequisites and Datasets
### 3.1 Prerequisites
- Python 3.8.16, PyTorch 2.1.1, **cuda-11.8**
- We provide detailed dependencies in [`environment.yml`] for Real-ZoomGS and ZoomFI, and [`./SynZoomGS/environment.yml`] for Syn-ZoomGS.

### 3.2 Datasets

### 3.3 Pretrained models

## 4.Start for Syn-ZoomGS
- Run [`cd ./SynZoomGS`](./SynZoomGS)
- For xiaomi data, zoom factor of W set to 0.6, 
  Run [`bash ./zoomgs_render_xiaomi06.sh`](./zoomgs_trains.sh)
- For xiaomi data, zoom factor of W set to 0.85, 
  Run [`bash ./zoomgs_render_xiaomi85.sh`](./zoomgs_trains.sh)
- For huawei data, zoom factor of W set to 0.6, 
  Run [`bash ./zoomgs_render_huawei06.sh`](./zoomgs_trains.sh)
- For huawei data, zoom factor of W set to 0.85, 
  Run [`bash ./zoomgs_render_huawei85.sh`](./zoomgs_trains.sh)

## 5.Start for Real-ZoomGS
- Run [`cd ./RealZoomGS`](./ZoomGS)
- Run [`bash ./zoomgs_train.sh`](./zoomgs_trains.sh)

## 6.Start for ZoomFI
- Run [`cd ./ZoomFI`](./FrameInterpolation)
- Training: run [`bash ./train.sh`](./train.sh)
- Testing on synthetic data: run [`bash ./test_syn.sh`](./test_syn.sh)
- Testing on real-world data: run [`bash ./test_real.sh`](./test_real.sh)

## Acknowledgement

Special thanks to the following awesome projects!

- [DCSZ](https://github.com/ZcsrenlongZ/ZoomGS)
- [SEA-RAFT](https://github.com/princeton-vl/SEA-RAFT)
- [DL3DV-10K](https://github.com/DL3DV-10K/Dataset)
- [Gaussian-Splatting](https://github.com/graphdeco-inria/gaussian-splatting)
- [FSGS](https://github.com/VITA-Group/FSGS)
- [BAD-Gaussian](https://github.com/WU-CVGL/BAD-Gaussians)
- [RIFE](https://github.com/hzwer/ECCV2022-RIFE)

## Citation
If you make use of our work, please cite our paper.
