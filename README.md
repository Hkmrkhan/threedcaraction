# AURA GT — Interactive 3D Showroom

> *“Engineered to be felt.”*

[![Next.js](https://img.shields.io/badge/Next.js-16.4.2-black?logo=next.js)](https://nextjs.org/)
[![React](https://img.shields.io/badge/React-19.2.9-61dafb?logo=react)](https://react.dev/)
[![Three.js](https://img.shields.io/badge/Three.js-0.186.1-black?logo=three.js)](https://threejs.org/)
[![React Three Fiber](https://img.shields.io/badge/R3F-9.8.1-black)](https://r3f.docs.pmnd.rs/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-4.3.3-38bdf8?logo=tailwindcss)](https://tailwindcss.com/)
[![TypeScript](https://img.shields.io/badge/TypeScript-6.0.3-blue?logo=typescript)](https://www.typescriptlang.org/)

**AURA GT** is a high-performance, real-time 3D automotive showroom built on the modern web stack with Next.js 16, React Three Fiber, and Three.js. It features photorealistic PBR materials, dynamic studio lighting, interior cockpit exploration, responsive layout framing, adaptive performance scaling, and an automated asset optimization pipeline.

---

## 🌟 Highlights & Features

### 🏎️ Photorealistic 3D Rendering & Materials
- **Multi-layer Car Paint**: Dual-coat metallic car paint simulation with metallic flake normal maps (`flakeNormalScale`), clearcoat gloss layer, and distance-based mip/flake fade to eliminate moiré.
- **Realistic Glass & Interior Optics**: Physical glass transmission and refraction with adaptive IOR, realistic rim finishes (Gloss Black, Satin Graphite, Brushed Silver), chrome accents, and tyre tread textures.
- **Detailed Cabin Interior**: Full driver cockpit view with leather sheen, soft-touch dashboard/door cards, brushed aluminium paddles, rubber floor mats, and illuminated emissive dials/gauges.
- **Procedural Interior Extras**: Code-generated rear-view mirror accurately calculated and mounted to windscreen geometry with soft-touch casing and calibrated glass reflectivity.

### 💡 Dynamic Studio Stage & Lighting
- **Pre-filtered HDRI Reflections**: Gaussian pre-filtered 32-bit Radiance RGBE environment map eliminating acoustic foam/octabox grid aliasing on curved panels.
- **Studio Flags & Custom Lightformers**: Portal-masked HDRI ceiling and dark ground disc matching the dark studio floor, complemented by an overhead rectangular softbox lightformer.
- **Planar Ground Reflections & Contact Shadows**: High-fidelity `MeshReflectorMaterial` blended with soft blur contact shadows (`ContactShadows`) for grounding the vehicle seamlessly.

### 🎥 Cinematic Camera System & Interior Navigation
- **Exterior Presets**: Smooth spherical orbital navigation between Three-quarter (`¾`), Front, Side, and Rear presets.
- **Interior Cabin Transition**: Seamless entry into the central driver’s seat with restricted look-around yaw/pitch to prevent clipping through roof or A-pillars.
- **Interior Sub-Presets**: Jump straight to Dashboard, Pedals, Door Card, or Steering Wheel/Controls using collision-aware linear interpolation.
- **Interactive Controls**: Full mouse drag, pinch-to-zoom, touch gestures, and keyboard-accessible glass dock navigation. Auto-rotation gracefully resumes after 5 seconds of inactivity.

### ✨ Post-Processing HDR Pipeline
- **Tone Mapping**: ACES Filmic (or AgX) tone mapping in full HDR linear floating-point color space.
- **Context-Aware Bloom**: Mipmapped bloom with dynamic luminance thresholding (exterior threshold targets high-intensity specular highlights; cabin view lowers threshold to bring out subtle dashboard gauge glow).
- **Subpixel Anti-Aliasing (SMAA)** & subtle studio vignette.

### ⚡ Adaptive Performance & Mobile Optimization
- **Dynamic Quality Scaling**: Integrated `PerformanceMonitor` dynamically tracks FPS and transitions between Quality Tiers (`0: Low`, `1: Medium`, `2: High`).
- **Scalable Features per Tier**: Automatically scales Device Pixel Ratio (DPR), reflector map resolution (256/512/1024), shadow resolution, MSAA samples, and glass transmission fallback.
- **Responsive Stage Framing**: CSS container queries adapt canvas framing between desktop landscape (canvas on right 60%, copy on left) and mobile portrait (canvas top 56%, copy below) without shifting camera center.

### 🎬 Developer & Recording Tooling
- **Live Material Tuner (`?tune`)**: Interactive Leva GUI for tweaking paint swatches, metalness, roughness, clearcoat, flake scales, and studio lighting in real time.
- **Scripted Recording Mode (`?record`)**: Clean presentation mode with UI hidden, quality tier locked, and scripted automated camera sweep across hero angles for promo captures.
- **Social Video Framing (`?record&ratio=4x5`)**: Constrains stage to a 1080×1350 (4:5) aspect ratio frame optimized for social media captures (e.g., Instagram, LinkedIn).

---

## 🛠️ Tech Stack

| Category | Technology |
|---|---|
| **Framework** | [Next.js 16](https://nextjs.org/) (App Router, Server Components) |
| **UI Library** | [React 19](https://react.dev/) |
| **3D Engine** | [Three.js 0.186](https://threejs.org/) |
| **3D React Bridge** | [@react-three/fiber](https://r3f.docs.pmnd.rs/) (v9) & [@react-three/drei](https://github.com/pmndrs/drei) (v10) |
| **Post-Processing** | [@react-three/postprocessing](https://github.com/pmndrs/react-postprocessing) & [postprocessing](https://github.com/pmndrs/postprocessing) |
| **State Management** | [Zustand](https://github.com/pmndrs/zustand) |
| **Styling** | [Tailwind CSS v4](https://tailwindcss.com/) |
| **Asset Optimization** | [@gltf-transform/core](https://gltf-transform.dev/), [meshoptimizer](https://github.com/zeux/meshoptimizer), [sharp](https://sharp.pixelplumbing.com/) |
| **Dev Tools** | [Leva](https://github.com/pmndrs/leva), [Playwright](https://playwright.dev/) |

---

## 🚀 Getting Started

### Prerequisites
- **Node.js**: v18.18+ (v20+ recommended)
- **npm** or preferred package manager
- *(Optional)* [KTX-Software](https://github.com/KhronosGroup/KTX-Software/releases) (`toktx`) if re-running model texture compression.

### Installation

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd threedcar
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```
   > *Note:* The `postinstall` hook automatically copies the self-hosted Basis Universal transcoder binaries (`basis_transcoder.js` and `basis_transcoder.wasm`) from `three` into `public/basis/`.

3. **Start the development server**:
   ```bash
   npm run dev
   ```

4. **Open in browser**:
   Navigate to [http://localhost:3000](http://localhost:3000).

---

## 📦 Asset Pipeline & Build Scripts

The repository includes dedicated automated scripts to process raw 3D models and HDR environment maps into optimized, web-ready, content-hashed assets:

| Command | Description |
|---|---|
| `npm run dev` | Runs the Next.js development server with hot reload |
| `npm run build` | Builds the Next.js application for production |
| `npm run start` | Starts the production server |
| `npm run typecheck` | Validates TypeScript types across the project (`tsc --noEmit`) |
| `npm run build:model` | Optimizes `public/models/car.glb`: strips third-party trademarks, optimizes geometry with Meshoptimizer, converts textures to KTX2/Basis, and writes a content-hashed GLB file |
| `npm run build:hdri` | Pre-filters `public/hdri/studio.hdr` using linear-float Gaussian blur to eliminate moiré, outputting a content-hashed soft HDR map |
| `npm run postinstall` | Copies Basis Universal transcoder files to `public/basis/` for offline/self-hosted texture decoding |

Asset references are stored and resolved through `src/config/assets.generated.json`.

---

## 🎛️ URL Parameters & Modes

You can pass query parameters to explore specialized modes:

- **`http://localhost:3000/?tune`**  
  Activates the **Leva Tuning Panel**. Allows real-time tweaking of:
  - Paint swatch color, metalness, roughness, clearcoat roughness
  - Flake normal strength (near/far) and camera fade ranges
  - Accent graphite paint parameters
  - Studio HDRI intensity and rotation angle
  - Values can be copied directly into `src/config/car.ts`.

- **`http://localhost:3000/?record`**  
  Enables **Clean Capture Mode**:
  - Hides UI hints and controls
  - Locks quality tier to prevent mid-recording quality shifts
  - Executes an automated, cinematic camera tour (¾ → Front → Side → Rear → ¾) followed by idle auto-rotation.

- **`http://localhost:3000/?record&ratio=4x5`**  
  Frames the viewport within a 1080×1350 container (4:5 aspect ratio) ideal for social media video recordings.

---

## 📁 Project Structure

```text
threedcar/
├── assets-src/            # Raw upstream asset sources and licenses
├── public/
│   ├── basis/             # Self-hosted Basis Universal KTX2 transcoders
│   ├── hdri/              # Original & generated soft HDR maps
│   └── models/            # Original car.glb & optimized content-hashed car.opt.*.glb
├── review/                # Reference screenshots & visual verification renders
├── scripts/
│   ├── build-hdri.mjs     # Gaussian blur pre-filtering for HDR environments
│   ├── build-model.mjs    # GLTF-transform, trademark stripping & KTX2/Meshopt pipeline
│   ├── copy-basis.mjs     # Postinstall helper copying Basis transcoder WASM
│   └── hashed-asset.mjs   # Helper for writing content-hashed assets & manifest
├── src/
│   ├── app/
│   │   ├── globals.css    # Responsive container query stage layout & styling
│   │   ├── layout.tsx     # Root layout with font imports and asset preloading
│   │   └── page.tsx       # Showroom entry point
│   ├── components/
│   │   ├── RecordDirector.tsx # Camera sequence orchestrator for ?record mode
│   │   ├── SceneRoot.tsx      # Dynamic SSR-free 3D canvas loader
│   │   ├── Showroom.tsx       # Main stage view orchestrator
│   │   ├── three/
│   │   │   ├── CabinLights.tsx    # Distance-fading interior cabin light fixtures
│   │   │   ├── CameraRig.tsx      # OrbitControls, presets, tweens & cabin limits
│   │   │   ├── Car.tsx            # GLTF loader, PBR material setup, flakes & KTX2
│   │   │   ├── Effects.tsx        # Postprocessing: Bloom, ACES/AgX tone mapping, SMAA
│   │   │   ├── Experience.tsx     # Canvas root, quality tier scaling, R3F Scene
│   │   │   ├── InteriorExtras.tsx # Procedural rear-view mirror with soft-touch shell
│   │   │   ├── Stage.tsx          # Studio environment, softbox lightformer, reflector floor
│   │   │   └── Tuner.tsx          # Leva debug GUI for material & lighting tuning
│   │   └── ui/
│   │       ├── CountUp.tsx        # Animated count-up stat numbers
│   │       ├── HeroCopy.tsx       # Glass hero description overlay with staggered reveal
│   │       ├── Loader.tsx         # Asset loading progress indicator
│   │       └── ViewControls.tsx   # Glass navigation pill for camera presets & zoom
│   ├── config/
│   │   ├── assets.generated.json # Manifest mapping assets to content-hashed files
│   │   └── car.ts                # Single source of truth: brand, specs, presets, materials
│   ├── hooks/
│   │   ├── useRecordParams.ts    # Parses ?record, ?ratio, and ?tune query params
│   │   └── useReducedMotion.ts   # Accessibility: prefers-reduced-motion check
│   └── store/
│       └── experience.ts         # Zustand global state (color, rim, tier, camera preset)
├── CREDITS.md             # Third-party model and HDRI licenses & attribution
├── next.config.ts         # Cache-Control headers for 3D assets
└── tsconfig.json          # TypeScript compiler configuration
```

---

## 🎨 Configuration

The central configuration lives in [`src/config/car.ts`](file:///c:/Users/hkmrk/Desktop/threedcar/src/config/car.ts). Here you can customize:

- **Brand & Copy**: Vehicle name, specs, count-up stats, hero descriptions, CTAs.
- **Paint Swatches**: Colors, metalness, roughness, clearcoat roughness for configurator swatches.
- **Material Tuning**: Flake repetition count, normal intensity, fading distances, glass transmission and IOR.
- **Lighting & Stage**: Studio floor reflection blur, contact shadow opacity, HDR ceiling cutoffs, softbox light dimensions and intensity.
- **Camera Presets & Interior Constraints**: Spherical angles, target offsets, field-of-view, look-around bounding yaw/pitch inside the cabin.

---

## 📄 Credits & Licenses

- **Car Model**: ["Car Concept"](https://github.com/KhronosGroup/glTF-Sample-Assets/tree/main/Models/CarConcept) by Eric Chadwick, © 2024 Darmstadt Graphics Group GmbH, licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Derived from ["Free Concept Car 004"](https://sketchfab.com/3d-models/free-concept-car-004-public-domain-cc0-4cba124633eb494eadc3bb0c4660ad7e) by Unity Fan (CC0).  
  *Modifications:* Khronos / 3D Commerce logos removed from textures, licence plate replaced with custom "AURA" badge, textures compressed to KTX2/Meshopt, and materials tuned at runtime.
- **Studio HDRI**: ["Studio Small 09"](https://polyhaven.com/a/studio_small_09) by Sergej Majboroda, licensed under [CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/) (Public Domain). Pre-filtered for anti-aliased reflections.

For full license details and attribution guidelines, see [CREDITS.md](file:///c:/Users/hkmrk/Desktop/threedcar/CREDITS.md).
