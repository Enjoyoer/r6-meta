# Rainbow Six Siege — Verification Checklist

To ensure your system is properly configured according to the `r6_optimization_handoff.md` specification, verify each of the following settings.

### 1. OS & System Level
- [x] **SMT (Simultaneous Multithreading):** Verify in your BIOS or Ryzen Master that this is **ON**.
- [x] **PPT (Eco Mode):** Verify in your BIOS or Ryzen Master that your CPU package power limit is at **95W**.
- [x] **Process Lasso:** Open Process Lasso while Siege is running, right-click `RainbowSix.exe` -> CPU Priority -> Always -> **High**.
- [x] **Windowed Optimizations:** Go to Windows Settings -> System -> Display -> Graphics -> Change default graphics settings -> turn ON **"Optimizations for windowed games"** (Allows DX12 Independent Flip).

### 2. GPU & Driver (NVIDIA Control Panel)
Open the NVIDIA Control Panel and navigate to **Manage 3D Settings** (Global or specific to Siege):
- [x] **Max Frame Rate:** Set to **277 FPS**.
- [x] **Monitor Technology:** Set to **Fixed Refresh Rate** (G-SYNC OFF per user preference).
- [x] **Vertical sync:** Set to **Off** (CRITICAL: Must be off since G-SYNC is disabled to prevent input latency).
- [x] **Shader Cache Size:** Set to **Unlimited**.

### 3. In-Game Settings (GameSettings.ini / UI)
Under the **Options -> Display & Graphics** tabs in-game:
- [x] **API:** Ensure you launched the standard game (DX12 by default).
- [x] **Display Mode:** Fullscreen (Strictly Fullscreen, no Borderless).
- [x] **Resolution:** 2560x1440.
- [x] **V-Sync:** **Off** (in-game V-Sync conflicts with NVCP V-Sync).
- [x] **NVIDIA Reflex Low Latency:** **On + Boost**.
- [x] **Texture Quality:** Medium or High.
- [x] **LOD Quality:** High or Very High (Critical for long-range engagements).
- [x] **Shadow Quality:** Medium (Critical for dynamic shadows).
- [x] **Shading Quality:** Low.
- [x] **Reflection Quality:** Low.
- [x] **Ambient Occlusion:** Off.
- [x] **Lens Effects:** Off.
- [x] **Zoom-In Depth of Field:** Off.
- [x] **Anti-Aliasing:** Off (or FXAA/TAA on Low if preferred to reduce OLED shimmering).