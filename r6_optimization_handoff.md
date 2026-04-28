# Rainbow Six Siege Performance Tuning — Agent Handoff

This document provides the blueprint for optimizing **Rainbow Six Siege** for consistent 277 FPS competitive performance on the established hardware profile. 

It builds upon the OS and system-level findings from the Star Citizen project, adapted for the latest R6 engine updates (DirectX 12).

## Hardware Profile Context
- **CPU:** Ryzen 7 5800X3D (SMT ON, 95 W PPT eco)
- **GPU:** Zotac RTX 5070 Ti (PCIe Gen 3)
- **Display:** Dell AW2725D — 1440p 280 Hz OLED, HDR10, G-SYNC Compatible

## Key Engine Context (Current Patch)
> [!WARNING]
> Ubisoft has permanently removed the Vulkan and DirectX 11 APIs. **DirectX 12 is now the only supported graphics API.** You no longer need to choose launch options; the default executable is DX12.

Unlike Star Citizen's heavy CPU-bound simulation, Rainbow Six Siege is highly optimized and will easily hit our 277 FPS cap on this hardware. The goal here shifts from "relieving the CPU" to **"minimizing input latency and maximizing visual clarity"** without dropping below the 277 FPS floor.

---

## Phase 1: OS & System Level
The foundation laid in the Star Citizen tuning remains optimal for Rainbow Six Siege.

- **SMT:** **Keep ON.** (As verified in `smt_experiment_results.md`, the 5800X3D's thread scheduling is highly efficient with SMT on. R6's DX12 implementation thrives on multithreading).
- **PPT:** **Keep at 95 W.** Siege is far less demanding on the CPU than SC; the CPU will rarely, if ever, hit the 95W cap in this game.
- **Process Priority (Process Lasso):** Set `RainbowSix.exe` to **High** priority. *Do not use Realtime.*
- **Windowed Optimizations:** Go to Windows Settings -> System -> Display -> Graphics -> Change default graphics settings -> turn ON **"Optimizations for windowed games"**. Do NOT disable Fullscreen Optimizations on the executable, as DX12 relies on this for the low-latency Independent Flip presentation model.

---

## Phase 2: GPU & Driver Strategy
The RTX 5070 Ti is vastly overqualified for Siege at 1440p, even at PCIe Gen 3. The focus is purely on tearing prevention and latency reduction.

- **NVCP Frame Rate Limiter:** Maintain the global/SC limit of **277 FPS** (3 FPS below the 280 Hz OLED refresh rate).
- **Tearing vs Latency (User Preference):**
  - G-SYNC: **OFF** (Opting for absolute minimum latency over tear-prevention. At 280Hz, screen tearing is barely perceptible).
  - NVCP V-Sync: **OFF** (CRITICAL: Since G-SYNC is off, V-Sync must also be off to prevent massive input delay).
  - In-Game V-Sync: **OFF**.
- **NVIDIA Reflex:** Set to **On + Boost** in-game. Because the 5070 Ti might sit at lower utilization (CPU/engine limits), "Boost" ensures the GPU clock stays high to minimize rendering latency, preventing aggressive downclocking.
- **Shader Cache:** Maintain "Unlimited" or 10GB+ in NVCP to prevent mid-round DX12 compilation stutters.

---

## Phase 3: In-Game Competitive Settings (Finalized)
The visual tuning strategy for Siege balances **competitive visibility** (spotting enemy silhouettes) with **minimum visual noise**. Since the RTX 5070 Ti is vastly overqualified at 1440p (holding a locked 270+ FPS easily), we pushed the rendering distances and texture details to the absolute maximum.

> [!IMPORTANT]  
> All Depth of Field, Bloom, and Lens Flares must be OFF. They simulate camera flaws and actively obscure enemy models.

**Finalized Settings (`GameSettings.ini` or In-Game UI):**
*   **Display Mode:** Fullscreen (Strictly Fullscreen. In DX12, this acts as a low-latency Independent Flip borderless, but explicitly selecting Fullscreen prevents DWM composition fallback).
*   **Resolution:** 2560x1440 (Native).
*   **Anti-Aliasing:** DLSS (Quality) OR TAA (with Sharpness tuned low). This is essential to prevent sub-pixel shimmering on the 1440p OLED grid, which can be mistaken for enemy movement.
*   **Texture Quality:** High (Sharpened surfaces to prevent operators from blending in).
*   **LOD Quality (Geometry):** Ultra+ (Forces the engine to render exact hitbox/helmet shapes at extreme distances without simplifying them to blocks).
*   **Shading Quality:** Low (Flattens lighting, removing dark corners where enemies can hide).
*   **Shadow Quality:** High (Crucial: Enables dynamic player shadows with sharp edges, allowing you to see enemy shadows cast around corners before they swing).
*   **Reflection Quality:** Low.
*   **Ambient Occlusion:** Off (Reduces muddy darkening in corners).
*   **Lens Effects:** Off.
*   **Zoom-In Depth of Field:** Off.
*   **Input Sensitivity (GameSettings.ini):** MouseYawSensitivity=50, MouseSensitivityMultiplierUnit=0.000872.

---

## Verification Checklist (Completed)

### 1. OS & System Level
- [x] **SMT (Simultaneous Multithreading):** Verified in BIOS/Ryzen Master that this is **ON**.
- [x] **PPT (Eco Mode):** Verified CPU package power limit is at **95W**.
- [x] **Process Lasso:** Set `RainbowSix.exe` -> CPU Priority -> Always -> **High**.
- [x] **Windowed Optimizations:** Windows Settings -> System -> Display -> Graphics -> **"Optimizations for windowed games"** is **ON** (Allows DX12 Independent Flip).

### 2. GPU & Driver (NVIDIA Control Panel)
- [x] **Max Frame Rate:** Set to **277 FPS**.
- [x] **Monitor Technology:** Set to **Fixed Refresh Rate** (G-SYNC OFF per user preference).
- [x] **Vertical sync:** Set to **Off** (CRITICAL: Must be off since G-SYNC is disabled to prevent massive input latency).
- [x] **Shader Cache Size:** Set to **Unlimited**.
- [x] **Digital Vibrance:** Increased to **75%** (Makes operator uniforms pop against drab backgrounds).

### 3. In-Game Settings
- [x] **API:** Launched the standard game (DX12 by default).
- [x] **Display Mode:** Fullscreen.
- [x] **Resolution:** 2560x1440.
- [x] **V-Sync:** **Off**.
- [x] **NVIDIA Reflex Low Latency:** **On + Boost**.
- [x] **Texture Quality:** High.
- [x] **LOD Quality (Geometry):** Ultra+.
- [x] **Shadow Quality:** High.
- [x] **Shading / Reflection Quality:** Low.
- [x] **Ambient Occlusion / Lens Effects / Depth of Field:** Off.
- [x] **Anti-Aliasing:** DLSS Quality / TAA (Sharpness tuned to prevent shimmering).
