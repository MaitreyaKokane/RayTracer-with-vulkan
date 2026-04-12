RAYTRACER (VULKAN + WALNUT)

LumaRT is a real-time, interactive ray tracer built in C++ on top of the Walnut application template.
Walnut provides the Vulkan renderer + windowing + ImGui-based tooling so the project can focus
on ray tracing logic (per-pixel rendering, camera, materials, etc.).  

--------------------------------------------------------------------------------
PROJECT OVERVIEW

This project is created using the Walnut app template (Walnut kept as an external submodule),
and implements a ray tracer as a desktop application. 
# LumaRT — Real-Time Ray Tracer

> A CPU path tracer built in C++ on the [Walnut](https://github.com/StudioCherno/Walnut) application framework, using Vulkan for presentation and ImGui for interactive controls.

![Metallic + Emissive Materials](https://github.com/user-attachments/assets/27fbc6ad-658e-45a7-b3b2-dad6e574fef7)
![Scene with Reflections](https://github.com/user-attachments/assets/c07699f2-2c09-4e78-9371-f3beff5819f6)

---

## Overview

LumaRT is an interactive ray tracer that renders scenes per-pixel on the CPU and presents the result through a Vulkan-backed viewport. Each frame accumulates samples for progressive refinement — move the camera or change any parameter and the image resets cleanly.

The project uses Walnut as an external submodule, which provides the Vulkan renderer, windowing, and ImGui integration so the codebase stays focused on ray tracing logic.

---

## Features

- **Progressive accumulation** — samples stack up over time for noise-free converged images
- **Interactive camera** — WASD + Q/E movement, right-click mouse look
- **Path tracing with multiple bounces** — configurable ray bounce depth
- **Material system**
  - Diffuse (Lambertian)
  - Metallic with adjustable roughness (sharp to blurry reflections)
  - Emissive with per-material on/off toggle and strength control
- **Sky color control** — pick any sky color from the UI via ColorEdit3
- **Multithreaded rendering** — parallel row dispatch via `std::execution::par`
- **Russian Roulette** early termination for low-contribution rays
- **Real-time UI** — all scene and material parameters editable live via ImGui

---

## Repository Layout

```
LumaRT/
├── RayTracer/          # Main application source
│   └── src/
│       ├── WalnutApp.cpp   # Entry point, UI, scene setup
│       ├── Renderer.h/cpp  # Ray tracing core
│       ├── Camera.h/cpp    # Camera, ray direction cache
│       ├── Scene.h         # Sphere + Material structs
│       └── Ray.h           # Ray struct
├── Walnut/             # Walnut framework (git submodule)
├── scripts/            # Setup scripts (Premake)
└── premake5.lua        # Workspace configuration
```

---

## Prerequisites

- Windows 10 / 11
- Visual Studio 2022
- Git (with submodule support)
- Vulkan-capable GPU and up-to-date drivers

---

## Build & Run

### 1. Clone with submodules
```bash
git clone --recursive https://github.com/MaitreyaKokane/LumaRT.git
```

If you already cloned without `--recursive`:
```bash
git submodule update --init --recursive
```

### 2. Generate project files
```bash
scripts\Setup.bat
```

### 3. Build and run
Open the generated `RayTracer.sln` in Visual Studio 2022, set the build configuration, and run.

---

## Controls

| Input | Action |
|-------|--------|
| Right Mouse + WASD | Move camera |
| Right Mouse + drag | Look around |
| Q / E | Move down / up |
| UI — Reset | Clear accumulated samples |
| UI — Accumulate | Toggle progressive sampling |

---

## Credits

- Ray tracing implementation follows [The Cherno's Ray Tracing series](https://www.youtube.com/playlist?list=PLlrATfBNZ98edc5GshdBtREv5asFW3yXl) on YouTube
- Application framework: [Walnut](https://github.com/StudioCherno/Walnut) by [StudioCherno (The Cherno)](https://github.com/StudioCherno)

---

## Roadmap

- [ ] BVH acceleration structure
- [ ] Triangle mesh support
- [ ] Texture mapping
- [ ] GPU path tracing (compute shaders)
- [ ] Environment / HDR sky maps
Typical workflow:
- Update camera / UI
- Ray trace into an image buffer
- Present the image in a Walnut viewport (Vulkan-backed)

--------------------------------------------------------------------------------
KEY FEATURES (CURRENT / INTENDED)

- Interactive viewport (Walnut)
- CPU ray tracing loop (per-pixel shading) rendered into a framebuffer
- UI controls for parameters (via Walnut/ImGui)
- Easy iteration using Premake + Visual Studio solution generation

  <img width="694" height="533" alt="image" src="https://github.com/user-attachments/assets/27fbc6ad-658e-45a7-b3b2-dad6e574fef7" />

  Metallic Material along with emissive material simulation 
  
  ---------------------------------------------------------------------------------------------------------------------------------------------------------
  
  <img width="838" height="519" alt="Screenshot 2026-04-12 033317" src="https://github.com/user-attachments/assets/c07699f2-2c09-4e78-9371-f3beff5819f6" /> 


Note:
Exact rendering features (materials, bounces, BVH, etc.) depend on the current implementation.
This README is structured so you can expand the "FEATURES" section as you add more.

--------------------------------------------------------------------------------
REPOSITORY LAYOUT

/ RayTracer/        -> Main application (your ray tracer code)
/ Walnut/           -> Walnut framework as a git submodule 
/ scripts/          -> Setup scripts (Premake generation, dependencies, etc.) 
  premake5.lua      -> Premake workspace configuration 
--------------------------------------------------------------------------------
PREREQUISITES (RECOMMENDED)

- Windows 10/11
- Visual Studio 2022
- Git (with submodules)
- Vulkan-capable GPU + drivers (Walnut uses Vulkan)

--------------------------------------------------------------------------------
BUILD & RUN (WINDOWS)

1) Clone with submodules:
   git clone --recursive https://github.com/MaitreyaKokane/LumaRT.git

   If you already cloned without --recursive:
   git submodule update --init --recursive

2) Generate Visual Studio project files:
   scripts\Setup.bat 

3) Open the generated Visual Studio 2022 solution and build.
4) First Build RayTracer.sln then run the RayTracer.sln or RayTracer/src/WalnutApp.cpp from Visual Studio.



--------------------------------------------------------------------------------
CREDITS
- Credits:
- This ray tracer was implemented by following The Cherno’s Ray Tracing tutorial series (YouTube).
- Application framework: Walnut / Walnut App Template by StudioCherno (The Cherno).
- Walnut framework provides the Vulkan + ImGui application layer.



--------------------------------------------------------------------------------
LINKS
- Template source: StudioCherno/WalnutAppTemplate .
