# Learning-Dual-Camera-Smooth-Zoom-with-3D-Data-Factory
Code of Learning Dual-Camera Smooth Zoom with 3D Data Factory

1.Abstract
=======================
<img width="3084" height="515" alt="intro1" src="https://github.com/user-attachments/assets/ed361cf5-ea27-42d5-a0bc-ac09957990a9" />
When zooming between dual cameras on a mobile, noticeable jumps in geometric content and image color occur in the preview, inevitably affecting the user’s zoom experience. To address this, we introduce the dual-camera smooth zoom (DCSZ) task, aiming to synthesize intermediate frames for fluid zooming. However, naively applying existing frame interpolation (FI) models for the task is challenging due to the motion domain gap and the scarcity of real-world ground truth. In this paper, we propose a novel data factory based on 3D Gaussian Splatting (3DGS) to construct large-scale training data. Specifically, we introduce Syn-ZoomGS, which generates extensive data from camera-independent 3D models by sampling camera parameters from fitted distributions, and Real-ZoomGS, which achieves high-fidelity synthesis by decoupling scene geometry from camera-specific characteristics. Furthermore, we design ZoomFI, an effective FI network tailored for DCSZ that incorporates bidirectional optical flows for photo-realistic zooming. Extensive experiments on both synthetic and real-world datasets of two mobile phones demonstrate that fine-tuning with our constructed DCSZ data significantly improves the performance of FI methods. Moreover, the proposed ZoomFI achieves state-of-the-art results in both quantitative metrics and visual quality. The datasets, codes, and pre-trained models will be publicly available.

2.Method
=======================
2.1 Syn-ZoomGS
-----------------------
<img width="3284" height="511" alt="pipline_2" src="https://github.com/user-attachments/assets/2996e5bd-b140-426e-b8b0-c82c15e59820" />
First we use the Syn-ZoomGS method to generate training data. (a)The pipline of Syn-ZoomGS. Syn-ZoomGS first sample $\Delta \mathbf{T}$ from $\mathcal{T}$, calculate camera parameters of UW and W and interpolate camera parameter of ${v}_{i}$. Then it render image sequence $\{\mathbf{X}_{{v}_{i}}\}_{i=1}^{N}$ from reconstructed 3DGS representation. Finally it samples color transformation parameters from $\mathcal{C}$ and interpolates them, and applies them to $\{\mathbf{X}^{(m)}_{uw}\}_{m=1}^{M}$ as ~\cref{eq:brightnesst_transform,eq:contrast_transform,eq:hue_transform,eq:saturation_transform}.
		%
		(b) Statistics of Geometric transformation parameters. Syn-ZoomGS collect multiple $\Delta \mathbf{T}$(~\cref{equ32303}) from UW\&W pairs and statistically obtain gaussian distribution $\mathcal{T}$.
		%
		(c) Statistics of Color transformation parameters. Syn-ZoomGS collect multiple color parameters $\{b_f, c_f, h_f, s_f\}$ from UW\&W pairs through Color Fit framework and statistically obtain gaussian distribution $\mathcal{C}$.
		%
