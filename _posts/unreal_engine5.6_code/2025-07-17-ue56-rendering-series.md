---
layout: post
title: "UE 5.6 Rendering Pipeline — Source Deep Dive"
date: 2025-07-17 00:00:00 +0800
category: Unreal Engine
tags: [UE5, Rendering, C++, Graphics]
permalink: /ue/
---

A hands-on reading series through the C++ source of Unreal Engine 5.6's rendering subsystem. Each article dissects a specific area of the pipeline — from the top-level `Render()` loop all the way down to Nanite cluster rasterization, Lumen surface caching, and virtual shadow map page allocation.

---

## Part 01 — Pipeline Paradigms

| Article | Topic |
|---|---|
| [Deferred Rendering Pipeline](/ue/01-pipeline-paradigms/deferred-shading.html) | `FDeferredShadingSceneRenderer` — the full deferred pipeline, GBuffer layout, all 12 render stages |
| [Forward Shading Pipeline](/ue/01-pipeline-paradigms/forward-shading.html) | `FMobileSceneRenderer` / Desktop Forward — dual-track analysis, TBDR hardware, single-pass design |

---

## Part 02 — Infrastructure & Graph

*Coming soon.*

## Part 03 — Shader Architecture

*Coming soon.*

## Part 04 — Next-Gen Hardware Features

*Coming soon.*

## Part 05 — Engine Modding

*Coming soon.*

## Part 06 — Profiling Deep Dives

*Coming soon.*

---

Source: `Engine/Source/Runtime/Renderer/Private/`, UE 5.6
