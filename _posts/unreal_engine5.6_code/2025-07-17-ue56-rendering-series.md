---
layout: post
title: "UE 5.6 Rendering Pipeline — Source Deep Dive"
date: 2025-07-17 00:00:00 +0800
category: Unreal Engine
tags: [UE5, Rendering, C++, Graphics]
permalink: /ue/
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

---

## Part 02 — Infrastructure & Graph

| Article | Topic |
|---|---|
| [RDG — Render Dependency Graph](/ue/02-infrastructure-graph/rdg-compiler.html) | `FRDGBuilder` — resource lifetime, pass culling, render pass merging, async compute, custom pass example |
| [Thread Concurrency](/ue/02-infrastructure-graph/thread-concurrency.html) | Game / Render / RHI thread architecture, `ENQUEUE_RENDER_COMMAND`, `FRenderCommandFence`, RenderCommandPipe |

---

## Part 03 — Shader Architecture

| Article | Topic |
|---|---|
| [Shader Compilation & Material Translation](/ue/03-shader-architecture/material-translation.html) | `FShader` hierarchy, permutation domains, `FHLSLMaterialTranslator`, ShaderMap caching |
| [Post-Processing Pipeline](/ue/03-shader-architecture/post-processing.html) | Execution order (EPass enum), all 16 effects, TSR pivot, Tonemap+LUT, three ways to write custom PP shaders |

---

## Part 04 — Next-Gen Hardware Features

| Article | Topic |
|---|---|
| [Nanite — Virtual Geometry](/ue/04-next-gen-hardware/nanite-rasterizer.html) | Cluster hierarchy (BVH/DAG), `FPackedCluster`, two-pass occlusion, software vs hardware rasterizer, shading bins |
| [Lumen — Dynamic GI](/ue/04-next-gen-hardware/lumen-raytracing.html) | Surface Cache (Mesh Cards), hybrid tracing decision tree, Screen Probes, Radiance Cache, async compute |
| [Virtual Shadow Maps](/ue/04-next-gen-hardware/virtual-resources.html) | 16K² virtual address space, physical page pool, page table indirection, static/dynamic cache split |

---

## Part 05 — Engine Modding

| Article | Topic |
|---|---|
| [Custom Shading Model & Substrate](/ue/05-engine-modding/shading-model-hack.html) | `SHADINGMODELID_*` system, step-by-step custom model implementation, Substrate BSDF layers |
| [Niagara — GPU Compute & Simulation Stages](/ue/05-engine-modding/niagara-gpu-compute.html) | Simulation Stages, Grid2D/3D Data Interfaces, custom DI authoring, fluid/crowd/physics use cases |

---

## Part 06 — Profiling Deep Dives

| Article | Topic |
|---|---|
| [Profiling — Insights, RDG & Hardware Profilers](/ue/06-profiling-deep-dives/hardware-profiling.html) | Unreal Insights, GPU Visualizer, RDG Insights, RenderDoc, PIX, NSight, Snapdragon Profiler, bandwidth analysis |

---

Source: `Engine/Source/Runtime/Renderer/Private/`, UE 5.6
