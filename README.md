# RLengine 6.5 — The 1,000,000 Entity Update

### Dev Update: Breaking the 50K Ceiling

Following the launch of RLengine 6.0, the main architectural goal for **6.5** was scaling the engine's scene capacity by **20x** and re-engineering the DirectX 12 memory and draw-call pipeline to handle massive entity counts without crashing or stalling.

* **Massive Scale-Up:** While RLengine 6.0 was capped at **50,000 objects**, RLengine 6.5 unlocks full support for **1,000,000 active objects** in the viewport simultaneously.
* **Pacing & Frame Stability:** 
  * In **6.0**, uncapped rendering peaked at **1,000 FPS** on light scenes and dropped to **200 FPS** at its 50,000-entity limit.
  * In **6.5**, the pipeline is tuned for heavy-load pacing—running at a **100 FPS** cap on light workloads and holding a rock-solid **60–70 FPS** even with **1,000,000 entities** active on screen.

---

## RLengine 6.0 vs. RLengine 6.5 — Benchmark Comparison

| Metric / Feature | RLengine 6.0 | RLengine 6.5 |
| :--- | :--- | :--- |
| **Max Entity Capacity** | **50,000** Entities (Hard Cap) | **1,000,000** Entities (**20x Increase**) |
| **1,000,000 Entity Support** | ❌ Not Supported | ✅ Native Support (Stress-Test Ready) |
| **Peak FPS (Light Scene)** | **1,000 FPS** (Uncapped) | **100 FPS** (Paced / Capped) |
| **FPS at 50,000 Entities** | **200 FPS** (80% drop from peak) | **~95–100 FPS** (Near-zero drop) |
| **FPS at 1,000,000 Entities** | N/A (Exceeds engine limit) | **60–70 FPS** (~14.2–16.6 ms frame time) |
| **DX12 Memory & Batching** | Standard ECS Buffer Allocation | High-Density Instanced Pipeline |

---

## Key Architectural Highlights in 6.5

1. **20x Scene Capacity Expansion:** Expanded buffer allocations, descriptor tables, and ECS entity pools to seamlessly address up to 1,000,000 transforms in real time.
2. **High-Density GPUThroughput:** Re-engineered how entity transforms are fed to the GPU, preventing command queue saturation when rendering a million instances.
3. **Consistent Frame Pacing:** Instead of chasing raw uncapped 1,000 FPS numbers on empty scenes, 6.5 prioritizes rock-solid frame times under extreme stress—losing only ~30–40% from its 100 FPS ceiling when scaling all the way to 1,000,000 objects.
