# 3DSlicer

A GPU-accelerated tool for generating cross-sectional slices of 3D triangular meshes using OpenGL and OpenCSG. By leveraging the GPU, this approach provides efficient and reliable Boolean operations for mesh slicing.

## Features

- **GPU-Accelerated Slicing**: Uses OpenGL stencil buffer techniques for high-performance Boolean operations.
- **Robust Boolean Operations**: Integrated with [OpenCSG](http://www.opencsg.org/) for constructive solid geometry.
- **Interactive Viewer**: GLUT-based interface for visualizing meshes and their slices.
- **C++20**: Updated to modern C++ standards.

## Prerequisites

- **CMake** (3.11 or higher)
- **C++20 Compiler** (e.g., AppleClang, GCC, or Clang)
- **OpenGL**
- **GLEW**
- **GLUT** (FreeGLUT recommended on Linux; native GLUT on macOS)

### Installation on macOS (Homebrew)
```bash
brew install glew cmake
```

## External Libraries

This project uses the following external libraries:

| Library | Version | Source | Notes |
|---------|---------|--------|-------|
| **OpenCSG** | 1.8.2 | Bundled | CSG rendering (latest) |
| **GLAD** | Bundled | Inside OpenCSG | OpenGL loader |
| **RenderTexture** | Custom | src/RenderTexture/ | Internal render-to-texture utility |
| **GLEW** | System | find_package | OpenGL extension handling |
| **GLUT** | System | find_package | Window management |
| **OpenGL** | System | find_package | Graphics API |

### Bundled Libraries
OpenCSG and GLAD are bundled in `src/OpenCSG/` and are kept up to date with the latest releases.

### System Libraries
GLEW, GLUT, and OpenGL are detected via CMake and depend on your system installation.

## Building the Project

The project uses a standard CMake build workflow:

```bash
mkdir build
cmake -B build -S .
cmake --build build
```

## Usage

Run the `meshslicer` executable with a mesh file. Other parameters are optional and have default values.

```bash
./build/app/meshslicer <meshfile> [numslices] [winSize] [frameRatio]
```

### Parameters:
- `meshfile`   : Path to the input 3D model (e.g., `.off` files). **(Required)**
- `numslices`  : Number of slices to generate. (Default: `100`)
- `winSize`    : Window width/height in pixels. (Default: `1000`)
- `frameRatio` : Scaling factor for the view frame. (Default: `1.0`)

### Examples:
```bash
# Using all defaults
./build/app/meshslicer dataset/radial.off

# Custom slices and window size
./build/app/meshslicer dataset/radial.off 200 800
```

## Keyboard Shortcuts
- `g`: Toggle Goldfeather / SCS algorithm.
- `a`: Toggle Automatic / Manual offscreen rendering.
- `ESC`: Exit the application.
- (Right-click for the context menu to change CSG algorithms and settings).

## Project Structure
- `app/`: Main application logic and viewer.
- `src/OpenCSG/`: Bundled OpenCSG library for Boolean rendering.
- `dataset/`: Sample meshes for testing.

## License
This project includes OpenCSG, which is typically licensed under GPL. Please refer to `src/OpenCSG/copying.txt` for details.
