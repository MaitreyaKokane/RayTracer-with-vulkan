# LumaRT — Real-Time Path Tracer

> A CPU path tracer built in C++ on the [Walnut](https://github.com/StudioCherno/Walnut) application framework, using Vulkan for presentation and ImGui for interactive controls.

![Metallic + Emissive Materials](https://github.com/user-attachments/assets/27fbc6ad-658e-45a7-b3b2-dad6e574fef7)
![Scene with Reflections](https://github.com/user-attachments/assets/c07699f2-2c09-4e78-9371-f3beff5819f6)

---

## Overview

LumaRT is an interactive **path tracer** that simulates physically-based light transport by shooting rays backwards from the camera into the scene. Each ray bounces off surfaces multiple times, accumulating color and energy loss at every hit — mimicking how real light behaves. The result is presented through a Vulkan-backed viewport and progressively refines over time for noise-free images.

The project uses Walnut as an external submodule, which provides the Vulkan renderer, windowing, and ImGui integration so the codebase stays focused on path tracing logic.

---

## How It Works

1. **Ray generation** — for each pixel, a ray is shot from the camera into the scene (backwards ray tracing)
2. **Intersection** — the ray tests against all spheres and finds the closest hit
3. **Bounce** — the ray reflects or scatters based on the material (diffuse or metallic)
4. **Throughput** — each bounce attenuates the ray's energy by the surface albedo, simulating light absorption
5. **Accumulation** — the process repeats across many frames, averaging samples to converge on a noise-free image

---

## Features

- **Progressive accumulation** — samples stack up over time for noise-free converged images
- **Interactive camera** — WASD + Q/E movement, right-click mouse look
- **Multi-bounce path tracing** — rays bounce up to 5 times, collecting indirect lighting
- **Material system**
  - Diffuse / Lambertian — random hemisphere scattering
  - Metallic with adjustable roughness — sharp to blurry reflections via `glm::reflect`
  - Emissive with per-material on/off toggle and strength control
- **Sky color control** — pick any sky color from the UI via ColorEdit3
- **Multithreaded rendering** — parallel row dispatch via `std::execution::par`
- **Russian Roulette** — probabilistic early termination for low-energy rays
- **Real-time UI** — all scene and material parameters editable live via ImGui

---

## Repository Layout

```
LumaRT/
├── RayTracer/          # Main application source
│   └── src/
│       ├── WalnutApp.cpp   # Entry point, UI, scene setup
│       ├── Renderer.h/cpp  # Path tracing core
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

|         Input      |           Action           |
|--------------------|----------------------------|
| Right Mouse + WASD | Move camera                |
| Right Mouse + drag | Look around                |
| Q / E              | Move down / up             |
| UI — Reset         | Clear accumulated samples  |
| UI — Accumulate    | Toggle progressive sampling|

---

## Credits

- Path tracing implementation follows [The Cherno's Ray Tracing series](https://www.youtube.com/playlist?list=PLlrATfBNZ98edc5GshdBtREv5asFW3yXl) on YouTube
- Application framework: [Walnut](https://github.com/StudioCherno/Walnut) by [StudioCherno (The Cherno)](https://github.com/StudioCherno)
