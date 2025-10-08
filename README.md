# Higgs Engine

Higgs is a lightweight 3D engine written in C++ using Vulkan.  
It is designed around minimal dependencies, using only **Vulkan**, **GLFW**, and the **C++ standard library**.

---

## Download

To try out Higgs, download and run the latest build from the **Releases** section of this repository:

1. Click on **Releases** in the GitHub sidebar.  
2. Download the latest `.rar` archive.  
3. Unzip the archive to any folder.  
4. Open the extracted folder and run **higgs.exe**.  
5. Windows may block the executable because it is from an unknown source.  
   - Click **More info**  
   - Then click **Run anyway**

**Note:** The current implementation only supports **Windows**, primarily because the windowing system is built on GLFW with Windows-specific handling.

---

## Input Mapping

The engine supports basic FPS-style controls:

| Input | Action |
|--------|---------|
| **W, ↑ / A, ← / S, ↓ / D, →** | Move forward, left, backward, right |
| **Mouse (Left Click + Move)** | Rotate camera |
| **Wheel** | World z forawrd and backward |

---

## Overview

Higgs provides a foundational framework for real-time 3D graphics with a focus on clarity and low-level control.  
It implements a complete Vulkan rendering backend, a custom math, image and model loading libraries.

---

## Design Philosophy

Higgs follows an object-oriented structure built around explicit, minimal dependencies and clear data flow.  
Each system is self-contained and communicates through well-defined abstractions.  

A central inheritance chain illustrates this approach:

`Transform → Renderable → Light → DirectionalLight`

This allows extensions and modifications to rendering entities without rewriting core systems, keeping the codebase transparent and adaptable.

---

## Math and Transform System

Higgs includes a custom math library for linear algebra and spatial transformations, built from the ground up.

Features:
- Generic **vectors (`Vec`)**, **matrices (`Mat`)** and **Quaternions (`Quat`)**
- Comprehensive **transform utilities** (position, rotation, scale)
- Quaternion-based rotation logic for both entities and the camera

All camera orientation and renderables positioning are handled through this math layer.

---

## Rendering System

The rendering backend is fully implemented with Vulkan, abstracting the essentials while maintaining explicit control over rendering operations.

Implemented features:
- Depth testing (depth buffers)
- MSAA (multisample anti-aliasing)
- Vertex buffers (for model properties encapsulation)
- Descriptor manager (for uniform and texture bindings)
- UBOs for vertex, lighting, and texture data
- A lighting system (currently only directional light)

---

## Resource and Asset Loading

Higgs uses custom, lightweight loaders for assets and images:

- **Model Loader** – Supports `.obj` models
- **Image Loader** – Supports `.png`, `.tga`, and `.bga`

---

## Camera and Input System

The camera system integrates directly with the input manager to provide a first-person navigation setup.

- **Camera**
  - Perspective projection
  - Maintains `view` and `projection` matrices
  - Tracks directional vectors (`forward`, `right`, `up`)
  - Updates dynamically with quaternion rotation

- **Input Manager**
  - Handles keyboard and mouse input
  - FPS-style movement
  - Mouse drag rotates the camera in real time

---

## Current State

Higgs currently includes:
- Custom math and transform library  
- Vulkan-based rendering pipeline  
- Depth testing and MSAA  
- Directional lighting system  
- Input and camera system  
- Custom OBJ model loader  
- PNG, TGA, and BGA image loading  
- Descriptor and uniform buffer management  

While fully functional at a base level, the engine is still under development and serves primarily as a platform for low-level graphics experimentation.

---

## Planned Work

- More comprehensive resource management system
- glTF model format support
- Material system with PBR 
- Scene graph or ECS  
- Shadow mapping  
- Comprehensive Scene editor  
- Physics System  

---

## Note

This project is **private** and intended for personal use and learning.  
It was not created with professional presentation or production deployment in mind.