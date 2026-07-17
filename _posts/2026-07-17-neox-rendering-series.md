---
layout: post
title: "NeoX Engine Rendering — Shader Deep Dive"
date: 2026-07-17 12:00:00 +0800
category: NeoX Engine
tags: [NeoX, Rendering, Shader, Graphics, HLSL]
permalink: /neox-series/
thumbnail: "/i/neox-cover.jpg"
---

A hands-on deep dive into NetEase's NeoX engine rendering system, as used in the G86 (Infinite Lagrange) project. Each article dissects a specific shader subsystem with actual source code from `res/shader/` and bilingual (English/Chinese) explanations.

---

## Introduction

| Article | Topic |
|---|---|
| [Introduction](/neox/00-introduction/introduction.html) | What is NeoX, core architecture (SURF/NFX/HLSL), rendering technologies overview, comparison with UE5.6 |

---

## Part 01 — Shader System

| Article | Topic |
|---|---|
| [NFX & SURF Format](/neox/01-shader-system/nfx-surf.html) | Material descriptor XML format, technique/pass declarations, resource bindings, material pipeline walkthrough |
| [NeoX HLSL Dialect](/neox/01-shader-system/hlsl-dialect.html) | Four-struct interface (Material/View/Light/Fragment), cross-platform macros, include hierarchy, utility library |

---

## Part 02 — Rendering Pipeline

| Article | Topic |
|---|---|
| [Forward Shading Pipeline](/neox/02-rendering-pipeline/forward-shading.html) | `forward_shading.hlsl` — vs_main/ps_main flow, vertex transform chain, lighting loop, special modes |
| [Deferred Shading Pipeline](/neox/02-rendering-pipeline/deferred-shading.html) | `deferred_shading_gbuffer.hlsl` — 3-RT GBuffer layout, Single-Pass Deferred for TBDR, flag encoding, UE5 comparison |

---

## Part 03 — Material System

| Article | Topic |
|---|---|
| [PBR Material System](/neox/03-material-system/pbr-material.html) | Standard PBR workflow, texture slot conventions (Albedo/Normal/MixMap), `GetAlbedo`/`GetRoughness`/`GetMetalness` |
| [Multi-Layered PBR](/neox/03-material-system/multi-layered-pbr.html) | N-layer clearcoat stack, BSDF layer blending, comparison with UE5 Substrate |

---

## Part 04 — Lighting Models

| Article | Topic |
|---|---|
| [GGX BRDF Implementation](/neox/04-lighting-models/ggx-brdf.html) | `brdf.hlsl` — D_GGX, F_Schlick, SmithJointGGX, anisotropic GGX, EnvBRDFApprox, full specular assembly |
| [13 Shading Models](/neox/04-lighting-models/shading-models.html) | All models: Isotropy, Skin, Hair (Marschner R/TT/TRT), ClearCoat, Toon, Glass, Eye, Subsurface, Transparent, Unlit, Mobile PBR |

---

## Part 05 — Post Processing

| Article | Topic |
|---|---|
| [Post Effects Overview](/neox/05-post-processing/post-effects.html) | 60+ effects: Bloom, DOF, ACES/Filmic tonemapping, Eye Adaptation, FXAA/TAA, Fog, Sun Shafts, Color Grading |

---

## Part 06 — Custom Features *(planned)*

| Article | Topic |
|---|---|
| *(planned)* Planet Rendering | Complete planet shader system — cube map + fractal noise + detail texture arrays |
| *(planned)* PSE Particle System | Particle effect shader architecture, billboard rendering, GPU instancing |
| *(planned)* Procedural Generation | Bullet trails, black holes, laser beams — procedural geometry shaders |

---

Source: `G:\SVN\G86\project_res_pc\res\shader\` · NeoX Engine
