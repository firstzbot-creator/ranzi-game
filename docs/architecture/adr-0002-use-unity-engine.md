# ADR-0002: Use Unity Engine for Game Development

## Status
Accepted

## Date
2026-03-31

## Context

### Problem Statement
We need to select a primary game engine for developing "ranzi-game". Initially, Unreal Engine was considered (see [ADR-0001](adr-0001-use-unreal-engine.md)), but concerns were raised regarding the developer experience on the current hardware setup.

### Constraints
- **Hardware Profile**: 
  - iMac 20,1 (Intel Core i5 6-Core @ 3.1 GHz)
  - 40 GB RAM
  - AMD Radeon Pro 5300 (4 GB VRAM)
  - 5K Retina Display
- **Developer Experience**: Unreal Engine (especially UE5 with Lumen/Nanite) is extremely demanding on VRAM. Running it on a 4GB graphics card while driving a 5K display would result in a poor, sluggish developer experience with loud fan usage and slow iterations.

### Requirements
- Must provide a smooth, responsive developer experience on the current iMac hardware.
- Must support robust 3D game development with good visual fidelity.

## Decision

We will adopt the **Unity Engine** as the primary game engine for this project.

Unity provides a substantially better developer experience on mid-range Mac hardware. The 4GB VRAM is ample for most 3D/2D workflows in Unity, and the massive 40GB system RAM will make compiling and multitasking extremely fast. We prioritize a fast iteration cycle and responsive editor over the out-of-the-box AAA graphics capabilities of Unreal Engine.

### Architecture Diagram
N/A - Foundational tooling decision.

### Key Interfaces
- C# will be the primary programming language for all game logic and scripting, replacing Blueprint visual scripting or C++.

## Alternatives Considered

### Alternative 1: Unreal Engine
- **Description**: The original proposition; an industry-standard engine capable of incredible photorealism.
- **Pros**: Advanced rendering (Lumen, Nanite), visual scripting (Blueprints).
- **Cons**: Extremely heavy on system resources, particularly VRAM. The 4GB VRAM limitation on the current hardware would cause severe stuttering, long compile times, and potential crashes.
- **Rejection Reason**: The developer experience would be heavily compromised on the current hardware setup.

### Alternative 2: Godot
- **Description**: An open-source, ultra-lightweight game engine.
- **Pros**: Lightning-fast to open, completely free, GDScript is fast to write, perfectly suited for the current hardware.
- **Cons**: Still maturing for high-end 3D graphics compared to Unity.
- **Rejection Reason**: Unity provides a better middle ground specifically for 3D development, with a more extensive asset store and proven 3D workflows.

## Consequences

### Positive
- Excellent editor performance and fast iteration times on the target iMac.
- Access to the industry's largest Asset Store for quick prototyping.
- C# provides a strongly-typed, widely supported language with a vast ecosystem of libraries.

### Negative
- Lacks the high-end, out-of-the-box dynamic lighting (Lumen) and micro-polygon geometry (Nanite) of UE5. Achieving high visual fidelity requires more manual setup (e.g., baking lights, post-processing stacks).
- The team must use C# rather than visual scripting (though Unity tools like Bolt exist, they are not as unified as Blueprints).

### Risks
- **Risk**: Potential frustration with Unity's render pipeline fragmentation (Built-in vs URP vs HDRP).
- **Mitigation**: Standardize on the Universal Render Pipeline (URP) immediately, as it offers the best balance of performance and graphics quality for the target hardware.

## Performance Implications
- **CPU**: Excellent performance during script compilation. Memory/CPU overhead of the editor is relatively low.
- **Memory**: The 40GB of RAM allows running Unity flawlessly alongside IDEs (Rider/Visual Studio) and web browsers without paging.
- **Network**: Standard package management downloads.

## Migration Plan
N/A - This decision supersedes the unreal engine proposal prior to any code being written.

## Validation Criteria
- Install Unity Hub and the latest LTS version of the editor.
- Create a URP project.
- Verify that the editor runs at a smooth 60+ FPS in the viewport without excessive fan noise or stuttering.
