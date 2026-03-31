# ADR-0001: Use Unreal Engine for Game Development

## Status
Rejected - Superseded by [ADR-0002](adr-0002-use-unity-engine.md)

## Date
2026-03-31

## Context

### Problem Statement
We need to select a primary game engine for developing "ranzi-game". The user has expressed a strong preference for Unreal Engine, but needed to verify if their current development hardware is capable of running it effectively.

### Constraints
- **Hardware Constraints**: The primary development machine is an iMac 20,1 with the following specifications:
  - CPU: 6-Core Intel Core i5 @ 3.1 GHz
  - RAM: 40 GB
  - GPU: AMD Radeon Pro 5300 with 4 GB VRAM
  - Resolution: 5K Retina (5120 x 2880)
- **Engine Requirements**: Unreal Engine (especially UE5) requires robust hardware. While the CPU and 40GB of RAM are highly capable, the 4GB of VRAM on the Radeon Pro 5300 may become a bottleneck for highly complex scenes utilizing advanced UE5 features like Lumen (Global Illumination) or Nanite at native 5K resolution.

### Requirements
- Must facilitate robust 3D game development.
- Must run acceptably on the current Mac hardware, scaling down viewport resolution or advanced features if necessary during development.

## Decision

We will adopt **Unreal Engine** as the primary game engine for this project.

The user's iMac is technically capable of running Unreal Engine. The 40GB of RAM is excellent for editor performance, and the 6-core Intel i5 meets the baseline CPU requirements. Using Metal 3 on the AMD Radeon Pro 5300 allows UE to function, though we must be mindful of graphics settings in the editor to maintain a smooth framerate.

### Architecture Diagram
N/A - This is foundational tooling, not system architecture.

### Key Interfaces
- C++ and Blueprints (Unreal Engine visual scripting) will be the primary interfaces for game logic.

## Alternatives Considered

### Alternative 1: Unity
- **Description**: Use Unity, a highly popular C#-based engine that often runs better on mid-range hardware and natively supports Mac development quite well.
- **Pros**: Lower system requirements, strong community, C# is often more approachable for rapid prototyping.
- **Cons**: User explicitly requested Unreal Engine; migrating to Unity would ignore this preference. Visual fidelity out-of-the-box often requires more setup than UE.
- **Rejection Reason**: The primary stakeholder expressed a preference for Unreal, and their hardware is adequately capable of running it.

### Alternative 2: Godot
- **Description**: Use Godot, an open-source, lightweight game engine.
- **Pros**: Extremely lightweight, runs on almost any hardware effortlessly, fast iterations.
- **Cons**: 3D workflow is improving but not as robust or industry-standard as Unreal Engine's out-of-the-box rendering capabilities.
- **Rejection Reason**: User preference is aligned with Unreal Engine for its specific capabilities.

## Consequences

### Positive
- Access to high-end rendering features and a robust, industry-standard toolset (Blueprints, Nanite, Lumen).
- Strong ecosystem for 3D assets (Quixel Megascans).

### Negative
- Steeper learning curve compared to lightweight engines.
- The Unreal Editor may run heavily on the Mac; optimization of editor settings (e.g., lowering engine scalability settings) will be required to maintain performance.

### Risks
- **Risk**: Device overheating or editor lagging due to 4GB VRAM limits on the GPU.
- **Mitigation**: Lower editor graphics scalability settings down from 'Epic' or 'Cinematic' to 'High' or 'Medium'. Avoid running the editor viewport at native 5K resolution.

## Performance Implications
- **CPU**: Moderate to High impact during code compilation and shader compilation.
- **Memory**: 40GB RAM provides extensive headroom, minimizing out-of-memory risks.
- **VRAM/GPU**: High impact. The 4GB VRAM will be heavily utilized.

## Migration Plan
N/A - This is a greenfield project setup.

## Validation Criteria
- Successful installation and launch of Unreal Engine.
- Creating a blank project and successfully piecing together a small scene at a stable 30+ FPS in the editor viewport.
