# BlackHole-Simulation
# GPU-Accelerated Black Hole Ray Tracing

## Overview
Visualizing a black hole requires calculating the complex paths that light takes as it bends through extreme gravitational fields. This repository contains a Jupyter Notebook (`Black Hole Simulation.ipynb`) that generates images of a rotating (Kerr) black hole's shadow and accretion disk by simulating photon geodesics.

To handle the immense computational load of rendering millions of pixels, the simulation is fully vectorized and hardware-accelerated using `cupy`. 

## Key Features
1. **Kerr Metric Physics:** Accurately computes the constants of motion (Energy, Angular Momentum, and Carter Constant) for photons based on their impact parameters.
2. **GPU Parallelization:** Leverages `cupy` arrays (`cp.linspace`, `cp.meshgrid`, `cp.where`) to execute the ray-tracing equations concurrently on the GPU, vastly outperforming standard CPU loops.
3. **Shadow Processing:** Includes a safety net that zeros out the intensity of any ray falling too close to the outer event horizon to ensure the central artifact is cleaned up and the shadow is perfectly black.
4. **High Dynamic Range Rendering:** Outputs the final image using `matplotlib` with an `afmhot` colormap and Logarithmic Normalization to capture the extreme brightness gradients of the accretion disk.

(If running locally, ensure you install the correct cupy wheel for your installed CUDA toolkit version).

## Notebook Structure
The Black Hole Simulation.ipynb notebook handles the following pipeline:
**Grid Initialization:** Generates a 2D camera field-of-view (FOV) grid using impact parameters $\alpha$ and $\beta$.
**Ray Tracing Loop:** Iteratively steps the photons backward in time through the Kerr spacetime geometry, timing the execution speed using the time module.
**Disk Intersection & Intensity:** Accumulates intensity based on how the rays intersect with the accretion disk.
**Visualization:** Forces the plot face-color to black to hide background noise and saves a high-resolution 300 DPI image of the black hole.

## Disclaimer
This project relies on cupy for GPU memory allocation. Depending on your Image Resolution (IMG_N), you may need to monitor your GPU VRAM to prevent Out-Of-Memory (OOM) errors.

## Getting Started

### Prerequisites
A CUDA-capable GPU is highly recommended. The notebook is pre-configured to run seamlessly on Google Colab with a T4 GPU. 

Ensure you have Python 3 and the required dependencies:
```bash
git clone [https://github.com/yourusername/kerr-ray-tracing.git](https://github.com/yourusername/kerr-ray-tracing.git)
cd kerr-ray-tracing
pip install -r requirements.txt
