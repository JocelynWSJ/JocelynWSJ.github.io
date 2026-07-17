---
layout: post
title: "UE 5.6 Rendering Pipeline — Source Deep Dive"
date: 2025-07-17 00:00:00 +0800
category: Unreal Engine
tags: [UE5, Rendering, C++, Graphics]
permalink: /ue/
thumbnail: "/i/ue5-cover.jpg"
---

A hands-on reading series through the C++ source of Unreal Engine 5.6's rendering subsystem. Each article dissects a specific area of the pipeline with actual source code references and bilingual (English/Chinese) explanations.

---

## Introduction

| Article | Topic |
|---|---|
| [Introduction](/ue/00-introduction/introduction.html) | What is UE 5.6, the three renderers, next-gen technologies overview, series map and prerequisites |

---

## Part 01 — Pipeline Paradigms

| Article | Topic |
|---|---|
| [Deferred Rendering Pipeline](/ue/01-pipeline-paradigms/deferred-shading.html) | `FDeferredShadingSceneRenderer` — full deferred pipeline, GBuffer layout, all 12 render stages |
| [Forward Shading Pipeline](/ue/01-pipeline-paradigms/forward-shading.html) | `FMobileSceneRenderer` / Desktop Forward — TBDR analysis, single-pass design, light data architecture |
| *(planned)* Visibility & Culling | `SceneVisibility.cpp` — frustum cull, HZB occlusion, `ComputeRelevance`, draw call dispatch |
| *(planned)* Translucency In Depth | All translucency lighting modes, Lumen interaction, Separate Translucency, Front Layer |
| *(planned)* Decal Rendering | DBuffer vs Deferred Decals, Mesh Decals, interaction with GBuffer and Nanite |

---

## Part 02 — Infrastructure & Graph

| Article | Topic |
|---|---|
| [RDG — Render Dependency Graph](/ue/02-infrastructure-graph/rdg-compiler.html) | `FRDGBuilder` — resource lifetime, pass culling, render pass merging, async compute, custom pass example |
| [Thread Concurrency](/ue/02-infrastructure-graph/thread-concurrency.html) | Game / Render / RHI thread architecture, `ENQUEUE_RENDER_COMMAND`, `FRenderCommandFence`, RenderCommandPipe |
| *(planned)* Screen Space Effects | SSAO, SSR, SSGI — sampling, temporal accumulation, when Lumen disables them |
| *(planned)* Scene Capture & Render Targets | `SceneCaptureComponent2D`, runtime render targets in materials, timing pitfalls |

---

## Part 03 — Shader Architecture

| Article | Topic |
|---|---|
| [Shader Compilation & Material Translation](/ue/03-shader-architecture/material-translation.html) | `FShader` hierarchy, permutation domains, `FHLSLMaterialTranslator`, ShaderMap caching |
| [Post-Processing Pipeline](/ue/03-shader-architecture/post-processing.html) | Execution order (EPass enum), all 16 effects, TSR pivot, Tonemap+LUT, three ways to write custom PP shaders |
| *(planned)* Material Permutation Explosion | What features multiply permutation count, cost analysis, pruning strategies |
| *(planned)* Subsurface Scattering In Depth | Pre-Integrated Skin Profile, GBufferD layout, screen-space SSS filter, Subsurface Profile asset |

---

## Part 04 — Next-Gen Hardware Features

| Article | Topic |
|---|---|
| [Nanite — Virtual Geometry](/ue/04-next-gen-hardware/nanite-rasterizer.html) | Cluster hierarchy (BVH/DAG), `FPackedCluster`, two-pass occlusion, software vs hardware rasterizer, shading bins |
| [Lumen — Dynamic GI](/ue/04-next-gen-hardware/lumen-raytracing.html) | Surface Cache (Mesh Cards), hybrid tracing decision tree, Screen Probes, Radiance Cache, async compute |
| [Virtual Shadow Maps](/ue/04-next-gen-hardware/virtual-resources.html) | 16K² virtual address space, physical page pool, page table indirection, static/dynamic cache split |
| *(planned)* Distance Field System | Mesh SDF generation & precision, Global Distance Field, DFAO, Lumen SDF tracing internals |
| *(planned)* Hair Strands Rendering | Visibility Buffer approach, Marschner dual-scattering lighting, performance bottlenecks |
| *(planned)* GPU Skin Cache | Compute-based skeletal deformation, Ray Tracing integration, Nanite skinning |

---

## Part 05 — Engine Modding

| Article | Topic |
|---|---|
| [Custom Shading Model & Substrate](/ue/05-engine-modding/shading-model-hack.html) | `SHADINGMODELID_*` system, step-by-step custom model implementation, Substrate BSDF layers |
| [Niagara — GPU Compute & Simulation Stages](/ue/05-engine-modding/niagara-gpu-compute.html) | Simulation Stages, Grid2D/3D Data Interfaces, custom DI authoring, fluid/crowd/physics use cases |
| *(planned)* Custom Depth & Stencil | `RenderCustomDepthPass`, use cases (outlines, X-ray, masking), mobile limitations |
| *(planned)* ViewExtension — Plugin-Safe Injection | Inject RDG passes without engine modification, PP chain hooks, third-party upscaler pattern |
| *(planned)* Substrate Advanced | Multi-layer BSDF storage format, multi-layer car paint / skin / cloth material authoring |

---

## Part 06 — Profiling Deep Dives

| Article | Topic |
|---|---|
| [Profiling — Insights, RDG & Hardware Profilers](/ue/06-profiling-deep-dives/hardware-profiling.html) | Unreal Insights, GPU Visualizer, RDG Insights, RenderDoc, PIX, NSight, Snapdragon Profiler, bandwidth analysis |
| *(planned)* Memory & VRAM Optimization | Texture streaming budgets, transient resource aliasing, VRAM overflow diagnosis |

---

## Part 07 — Scene Rendering Features *(planned)*

| Article | Topic |
|---|---|
| *(planned)* Landscape Rendering | Virtual Texture LOD, Material Layers blending, Nanite for Landscape |
| *(planned)* Water Rendering | Single Layer Water shading, refraction/scattering/reflection composition, Lumen interaction |
| *(planned)* LOD & HLOD System | Screen-space LOD threshold math, HLOD proxy generation, Nanite as LOD replacement |

---

## Part 08 — Character Rendering *(planned)*

| Article | Topic |
|---|---|
| *(planned)* Hair Strands Deep Dive | Full pipeline: interpolation → visibility → lighting → composition |
| *(planned)* Skin Rendering | Subsurface profile authoring, Pre-Integrated GF, dual normal maps, pore-level detail |
| *(planned)* Cloth & Simulation | Chaos cloth rendering integration, Niagara cloth, translucency on fabric |

---

Source: `Engine/Source/Runtime/Renderer/Private/`, UE 5.6
