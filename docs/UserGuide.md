# 3DSlicer: A Student's Guide to GPU-Accelerated Mesh Slicing

Welcome to the **3DSlicer User Guide**. This document is designed for undergraduate students in computer science, mechanical engineering, or computer graphics who wish to understand and utilize GPU-accelerated techniques for 3D mesh processing.

---

## 1. Introduction to Mesh Slicing

### 1.1 What is Mesh Slicing?
Mesh slicing is the process of intersecting a 3D geometric model (typically represented as a collection of triangles) with a 2D plane. The result is a cross-section that reveals the internal structure of the model at a specific location.

### 1.2 Applications
- **3D Printing**: Generating "layers" (G-code) for additive manufacturing.
- **Medical Imaging**: Visualizing internal structures from volumetric scans.
- **CAD/CAM**: Verifying the thickness and internal clearances of mechanical parts.

### 1.3 The GPU Approach
Traditional CPU-based slicing involves complex geometric intersections and can be slow for high-resolution meshes. **3DSlicer** uses the Graphics Processing Unit (GPU) and a technique called **Constructive Solid Geometry (CSG)** via the OpenCSG library. By using the OpenGL stencil buffer, we can perform boolean operations (specifically, the intersection between the mesh and a thin box) at the hardware level, achieving real-time performance.

---

## 2. Getting Started

### 2.1 Prerequisites
Before building the project, ensure your environment has the following tools installed:
- **C++ Compiler**: Supporting C++20 (GCC 10+, Clang 10+, or MSVC 2019+).
- **CMake**: Version 3.11 or higher.
- **OpenGL**: Modern graphics drivers.
- **GLEW**: The OpenGL Extension Wrangler Library.
- **GLUT**: A toolkit for window management (FreeGLUT is recommended for Linux).

### 2.2 Installation (macOS)
If you are using Homebrew, run:
```bash
brew install glew cmake
```

### 2.3 Building the Project
Navigate to the project root and run the following commands:
```bash
mkdir build
cd build
cmake ..
make
```
This will generate the `meshslicer` executable in the `app/` directory.

---

## 3. Using 3DSlicer

### 3.1 Basic Usage
The application is launched from the command line. At a minimum, you must provide a path to a mesh file in `.off` (Object File Format).

```bash
./build/app/meshslicer dataset/radial.off
```

### 3.2 Advanced Command-Line Arguments
You can customize the slicing process using additional parameters:
```bash
./build/app/meshslicer <filename> [numSlices] [windowSize] [frameRatio]
```
- **numSlices**: The number of intervals to divide the mesh into along the Z-axis.
- **windowSize**: The resolution of the viewer window (e.g., 800 for 800x800).
- **frameRatio**: Scales the viewing volume.

---

## 4. Navigation and Controls

The interactive viewer allows you to inspect the mesh and its slices in real-time.

### 4.1 Keyboard Shortcuts
| Key | Action |
| :--- | :--- |
| `+` / `-` | Move the slicing plane forward/backward. |
| `n` | Step to the next slice in the current animation direction. |
| `a` | Toggle **Animation** (automatically cycle through slices). |
| `o` | Toggle **Auto-Rotation** (spins the mesh for better viewing). |
| `m` | Toggle Mesh visibility. |
| `w` | Toggle Wireframe mode. |
| `p` | Toggle Slicing Plane visibility. |
| `i` | Toggle Intersection (highlight the actual cross-section). |
| `s` | **Save Screenshots**: Generates `.pgm` images of every slice. |
| `r` | Reset camera view. |
| `x`/`y`/`z` | Rotate the mesh 90 degrees around the respective axis. |
| `t` | Toggle Coordinate Axis display. |
| `ESC` | Exit the application. |

### 4.2 Mouse Controls
- **Right-Click**: Opens a context menu to switch between CSG algorithms (Goldfeather vs. SCS) and rendering settings.
- **Arrow Keys**:
    - `Up` / `Down`: Zoom in and out.
    - `Left` / `Right`: Rotate the camera manually.

---

## 5. Technical Insights for Students

### 5.1 The OFF File Format
The project uses the `.off` format, which is simple and human-readable. It lists the number of vertices and faces, followed by their coordinates and indices. Understanding this format is a great first step into 3D data structures.

### 5.2 CSG Algorithms
In the right-click menu, you will see options for **Goldfeather** and **SCS**.
- **Goldfeather**: A robust algorithm for rendering CSG by counting parity in the stencil buffer.
- **SCS (Sequenced Convex Subtraction)**: An alternative algorithm that can be faster for certain types of geometry.
Experimenting with these will show you how different algorithms handle edge cases in geometry.

### 5.3 Offscreen Rendering
When you press `s`, the application uses **Frame Buffer Objects (FBOs)**. This allows the GPU to render the slices to a memory buffer instead of the screen, enabling high-resolution image generation without window size constraints.

---

## 6. Exercises for Undergraduates
1. **Geometric Transformation**: Modify `main.cpp` to slice along the X or Y axis instead of Z.
2. **Color Customization**: Find the `display()` function in `main.cpp` and change the color of the intersection highlight.
3. **Format Support**: Extend the `readMesh()` function to support `.obj` or `.stl` files.

---
*Happy Slicing!*
