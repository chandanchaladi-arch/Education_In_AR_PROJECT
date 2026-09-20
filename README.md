# Edu-AR: AI-Assisted Augmented Reality Virtual Science Laboratory

Android + Unity + AR Foundation (ARCore) app that lets Class 10 students
place a virtual science lab on any flat surface and perform Physics/Chemistry
experiments interactively, with an AI mentor, Telugu/English support, and
free-exploration and textbook-scanning modes.

Full requirements: see the project brief shared with this repo (Android app,
markerless AR lab, curriculum experiments, AI mentor, multilingual support,
3D asset interactions, free-experiment mode, textbook/photo scanning,
educational videos, progress tracking, expandable classes/subjects).

## What's in this repo right now

- `web-prototype/edu-ar-demo.html` — a standalone browser prototype (three.js)
  of the **interaction model**: select subject/experiment → simulated
  markerless placement (tap-to-place on a detected grid, standing in for
  ARCore plane detection) → step-by-step interactive experiment (clean →
  pick up → ignite → observe → collect) → observation/result/conclusion →
  AI mentor chat (canned demo) → free-experiment mode → mock textbook
  scanning → local progress tracking. English/Telugu toggle included.
  Open it directly in a browser (double-click the file, or serve it
  statically) — no build step required.

  This prototype validates the UX flow and content structure; it is **not**
  the Unity/ARCore deliverable. It has no camera-based plane detection or
  image recognition, and its 3D models are simple placeholder primitives.

## Why Unity + AR Foundation (ARCore) for the real app

The requirements need reliable markerless plane detection, ARCore Augmented
Images for textbook/photo recognition, offline classroom use, and
high-fidelity object interaction (pour, mix, heat, measure) — a native
Android app built with Unity's AR Foundation is the right fit, not a WebXR
page. Delivery should be an APK distributed to schools directly or via a
Play Store internal/closed testing track, not a public listing at first.

## Planned Unity project architecture (next step)

- `Assets/Scripts/AR/` — plane detection, tap-to-place, anchor management
  (AR Foundation `ARPlaneManager`, `ARRaycastManager`).
- `Assets/Scripts/Experiments/` — `ExperimentDefinition` ScriptableObjects
  (objective, apparatus, procedure, steps, observation, result, conclusion)
  so new experiments can be added as data, without rebuilding the app.
  Mirrors the step/apparatus model already prototyped in
  `web-prototype/edu-ar-demo.html`.
- `Assets/Scripts/Interaction/` — grab/place/pour/mix/heat/measure
  interaction components attachable to any apparatus prefab.
- `Assets/Scripts/Mentor/` — AI mentor client (calls an LLM API such as the
  Claude API) with a small local fallback for offline/no-connectivity use.
- `Assets/Scripts/Localization/` — string tables keyed the same way as the
  prototype's `I18N` object (English/Telugu now, more languages later).
- `Assets/Scripts/Recognition/` — ARCore Augmented Images (or a cloud
  vision fallback) mapping recognized textbook pages to an experiment,
  info card, or video.
- `Assets/Scripts/Progress/` — local save now, syncing to a backend/student
  account later for teacher analytics.
- `Assets/StreamingAssets/Experiments/` — per-experiment content bundles
  (data, videos, localized text) so content ships independently of app
  binaries.

## Setup (once the Unity project is scaffolded)

Requires Unity Hub + Unity LTS with Android Build Support, AR Foundation
and ARCore XR Plugin packages, and an Android device with ARCore support
for testing. Instructions will be added here as the Unity project lands.
