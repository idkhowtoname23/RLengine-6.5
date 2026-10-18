# RLengine 6.5 — The 1,000,000 Entity & Display Sync Update

### Dev Update: Breaking the 50K Ceiling & Smart Frame Pacing

Following the launch of RLengine 6.0, the primary focus for **6.5** was scaling the engine's scene capacity by **20x** and introducing native display refresh rate synchronization for smooth, tear-free frame pacing.

* **Massive 20x Scale-Up:** While RLengine 6.0 had a hard limit of **50,000 objects**, RLengine 6.5 unlocks full support for **1,000,000 active objects** in the viewport simultaneously.
* **Display Refresh Rate Sync (VSync):** 
  * In **6.0**, the swap chain ran completely uncapped—hitting **1,000 FPS** on light scenes (wasting GPU power) and dropping to **200 FPS** at the 50,000-entity cap.
  * In **6.5**, the engine automatically locks its ceiling to your **monitor's native refresh rate** (e.g., **100 FPS on a 100Hz display**, 144 FPS on 144Hz, etc.) for zero screen tearing and rock-solid frame times.
* **Extreme Stress-Test Stability:** Even when pushing the viewport to the absolute limit of **1,000,000 active entities**, RLengine 6.5 maintains a smooth **60–70 FPS**.

---

## RLengine 6.0 vs. RLengine 6.5 — Benchmark Comparison

| Metric / Feature | RLengine 6.0 | RLengine 6.5 |
| :--- | :--- | :--- |
| **Max Entity Capacity** | **50,000** Entities (Hard Cap) | **1,000,000** Entities (**20x Increase**) |
| **1,000,000 Entity Support** | ❌ Not Supported | ✅ Native Support (Stress-Test Ready) |
| **Frame Rate Limiting** | Uncapped (**1,000 FPS** peak) | **Synced to Monitor Refresh Rate (Hz)** (e.g., 100 FPS @ 100Hz) |
| **FPS at 50,000 Entities** | **200 FPS** (80% drop from peak) | **100 FPS** (Locked to 100Hz Refresh Rate) |
| **FPS at 1,000,000 Entities** | N/A (Exceeds engine limit) | **60–70 FPS** (~14.2–16.6 ms frame time) |
| **DX12 Swap Chain & Memory** | Uncapped Present + Standard ECS | VSync-Aware Present + High-Density Instancing |

---

## Key Architectural Highlights in 6.5

1. **Native Refresh Rate Matching:** The DX12 Swap Chain now dynamically adapts to the active display's refresh rate (Hz), eliminating coil whine, wasted GPU cycles, and screen tearing.
2. **20x Scene Capacity Expansion:** Expanded buffer allocations, descriptor tables, and ECS entity pools to seamlessly address up to 1,000,000 transforms in real time.
3. **High-Density GPU Throughput:** Re-engineered how entity transforms are batched and fed to the GPU, maintaining 100% of a 100Hz refresh rate at 50K objects and holding 60–70 FPS at 1,000,000 objects.
