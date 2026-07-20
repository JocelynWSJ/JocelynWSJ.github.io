---
layout: post
title: "UE 5.6 Rendering Pipeline — Source Deep Dive"
date: 2026-07-17 00:00:00 +0800
category: Unreal Engine
tags: [UE5, Rendering, C++, Graphics]
permalink: /ue/
thumbnail: "/i/ue5-cover.jpg"
---

A hands-on reading series through the C++ source of Unreal Engine 5.6's rendering subsystem. Each article dissects a specific area of the pipeline with actual source code references and bilingual (English / Chinese) explanations.

---

## 00 — Overview

| Article | Topic |
|---|---|
| [Introduction](/ue/00-overview/introduction.html) | What is UE 5.6, the three renderers, next-gen technologies overview, series map and prerequisites |

---

## 01 — Rendering Pipeline

| Article | Topic |
|---|---|
| [Deferred Rendering](/ue/01-rendering-pipeline/deferred-shading.html) | `FDeferredShadingSceneRenderer` — full deferred pipeline, GBuffer layout, all 12 render stages |
| [Forward Rendering](/ue/01-rendering-pipeline/forward-shading.html) | `FMobileSceneRenderer` / Desktop Forward — TBDR analysis, single-pass design, light data architecture |
| *(planned)* Visibility & Culling | `SceneVisibility.cpp` — frustum cull, HZB occlusion, `ComputeRelevance`, draw call dispatch |
| *(planned)* Translucency In Depth | All translucency lighting modes, Lumen interaction, Separate Translucency, Front Layer |
| *(planned)* Decal Rendering | DBuffer vs Deferred Decals, Mesh Decals, interaction with GBuffer and Nanite |

---

## 02 — Engine Infrastructure

| Article | Topic |
|---|---|
| [RDG — Render Dependency Graph](/ue/02-engine-infrastructure/rdg-compiler.html) | `FRDGBuilder` — resource lifetime, pass culling, render pass merging, async compute, custom pass example |
| [Thread Concurrency](/ue/02-engine-infrastructure/thread-concurrency.html) | Game / Render / RHI thread architecture, `ENQUEUE_RENDER_COMMAND`, `FRenderCommandFence`, frame pipelining |
| [Virtual Texture Streaming](/ue/02-engine-infrastructure/virtual-texture.html) | Page table, physical pool, GPU feedback buffer, Runtime VT for landscapes, Adaptive VT |
| *(planned)* GPU Scene & Instance Culling | `FGPUScene` primitive buffer, instance culling dispatcher, multi-view load balancing |
| *(planned)* Scene Capture & Render Targets | `SceneCaptureComponent2D`, runtime render targets in materials, timing pitfalls |

---

## 03 — Lighting & Shadows

| Article | Topic |
|---|---|
| [Lighting Architecture](/ue/03-lighting-shadows/lighting-architecture.html) | Clustered deferred, froxel light grid, three-tier evaluation, MegaLights stochastic sampling, IES atlas |
| [Virtual Shadow Maps](/ue/03-lighting-shadows/virtual-shadow-maps.html) | 16K² virtual address space, physical page pool, page table indirection, static/dynamic cache split |
| *(planned)* Distance Field System | Mesh SDF generation & precision, Global Distance Field, DFAO, Lumen SDF tracing internals |
| *(planned)* Ray Tracing Infrastructure | TLAS/BLAS management, SBT, hit shaders, RT shadows / AO / reflections beyond Lumen |

---

## 04 — Material & Shader System

| Article | Topic |
|---|---|
| [Shader Compilation & Architecture](/ue/04-material-shader/material-translation.html) | `FShader` hierarchy, permutation domains, `FHLSLMaterialTranslator`, ShaderMap caching |
| [Shading Models Reference](/ue/04-material-shader/shading-models-reference.html) | All 13 built-in BRDFs — Default Lit (GGX), Subsurface Profile (Burley), Clear Coat, Hair (Marschner), Cloth (Ashikhmin), Eye, Water, Substrate |
| [USF / HLSL Writing Guide](/ue/04-material-shader/usf-hlsl-guide.html) | Virtual path system, key include files, shader types, permutation domains, full compute + VS/PS examples, hot-reload & debugging |
| *(planned)* Material Permutation Explosion | What features multiply permutation count, cost analysis, pruning strategies |
| *(planned)* Substrate Advanced | Multi-layer BSDF storage format, multi-layer car paint / skin / cloth material authoring |

---

## 05 — UE5 Core Technologies

| Article | Topic |
|---|---|
| [Nanite — Virtual Geometry](/ue/05-ue5-core/nanite-rasterizer.html) | Cluster hierarchy (BVH/DAG), `FPackedCluster`, two-pass occlusion, software vs hardware rasterizer, shading bins |
| [Lumen — Dynamic GI](/ue/05-ue5-core/lumen-raytracing.html) | Surface Cache (Mesh Cards), hybrid tracing decision tree, Screen Probes, Radiance Cache, async compute |
| *(planned)* Lumen — Software Tracing Deep Dive | Global SDF construction, per-object SDF culling, mesh card capture, radiosity multi-bounce |
| *(planned)* MegaLights | Stochastic many-light evaluation, ReSTIR reservoir resampling, VSM integration |

---

## 06 — Post-Processing & Effects

| Article | Topic |
|---|---|
| [Post-Processing Pipeline](/ue/06-post-processing/post-processing.html) | Execution order (EPass enum), all 16 effects, TSR pivot, Tonemap + LUT, three ways to write custom PP shaders |
| [Screen Space Effects](/ue/06-post-processing/screen-space-effects.html) | SSR (Hi-Z ray march), GTAO horizon-based AO, contact shadows, spatiotemporal denoiser |
| *(planned)* Depth of Field In Depth | Diaphragm DOF: gather / scatter / recombine passes, Bokeh, Circle of Confusion |
| *(planned)* Motion Blur & Velocity Buffer | `VelocityRendering.cpp`, per-object / camera blur, TSR interaction |

---

## 07 — Specialized Rendering

| Article | Topic |
|---|---|
| [Volumetric Fog & Atmosphere](/ue/07-specialized-rendering/volumetric-atmosphere.html) | Four-layer stack — Sky Atmosphere (Bruneton LUTs), Volumetric Clouds (ray-march), Volumetric Fog (froxel grid + light scatter), Exponential Height Fog |
| [Water Rendering](/ue/07-specialized-rendering/water-rendering.html) | Single Layer Water BRDF — Fresnel, Beer-Lambert absorption, refraction UV offset, water info texture, SSR/Lumen integration |
| [Hair & Groom](/ue/07-specialized-rendering/hair-groom-rendering.html) | Strand data layout, visibility buffer rasterization, Marschner R/TT/TRT BRDF, deep shadow maps, voxel self-shadowing, Groom asset pipeline |
| *(planned)* Landscape Rendering | Virtual Texture LOD, Material Layer blending, Runtime VT baking, Nanite for Landscape |
| *(planned)* Skin Rendering Deep Dive | Subsurface Profile authoring, Pre-Integrated GF, dual normal maps, pore-level detail |
| *(planned)* LOD & HLOD System | Screen-space LOD threshold math, HLOD proxy generation, Nanite as LOD replacement |

---

## 08 — Engine Customization

| Article | Topic |
|---|---|
| [Custom Shading Model](/ue/08-engine-customization/custom-shading-model.html) | `SHADINGMODELID_*` system, step-by-step custom model implementation (C++ + HLSL), Substrate BSDF layers |
| [Niagara GPU Compute](/ue/08-engine-customization/niagara-gpu-compute.html) | Simulation Stages, Grid2D/3D Data Interfaces, custom DI authoring, fluid / crowd / physics use cases |
| *(planned)* ViewExtension — Plugin-Safe Injection | Inject RDG passes without engine modification, PP chain hooks, third-party upscaler pattern |
| *(planned)* Custom Depth & Stencil | `RenderCustomDepthPass`, use cases (outlines, X-ray, masking), mobile limitations |

---

## 09 — Performance & Profiling

| Article | Topic |
|---|---|
| [Hardware Profiling](/ue/09-profiling/hardware-profiling.html) | Unreal Insights, GPU Visualizer, RDG Insights, RenderDoc, PIX, NSight, Snapdragon Profiler, bandwidth analysis |
| *(planned)* Memory & VRAM Optimization | Texture streaming budgets, transient resource aliasing, VRAM overflow diagnosis |
| *(planned)* GPU Timing & Frame Pacing | `stat GPU`, frame pipelining latency, async compute overlap measurement |

---

Source: `Engine/Source/Runtime/Renderer/Private/` · UE 5.6
