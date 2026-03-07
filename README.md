# Quick Return (Shaper) Mechanism — Kinematic Simulation & Analysis

> **Course Project · Mechanical Engineering — Theory of Machines**  
> Simulation Environment: MATLAB R2025b · Simscape Multibody  
> Author: Kanishk

---

## Table of Contents
- [Overview](#overview)
- [Mechanism Description](#mechanism-description)
- [Simulation Setup](#simulation-setup)
- [How to Run](#how-to-run)
- [Results & Analysis](#results--analysis)
- [Planned Work](#planned-work)
- [Requirements](#requirements)

---

## Overview

This project presents a full kinematic simulation and analysis of a **Quick Return Mechanism**, specifically the type used in **shaper machines** for metal cutting operations.

The defining characteristic of this mechanism is that the **forward (cutting) stroke is slower than the return stroke** — allowing more time for the tool to cut while minimizing idle return time. This makes it highly efficient for reciprocating machining processes.

This repository contains:
- A complete **Simscape Multibody model** of the mechanism
- **Kinematic analysis** outputs: position, velocity, and acceleration of key links
- *(Upcoming)* Force analysis in simulation and hardware validation

---

## Mechanism Description

The shaper mechanism is a **six-link kinematic chain** that converts continuous rotary motion (crank) into asymmetric reciprocating linear motion (ram/slider).

### How It Works

1. The **crank** rotates at a constant angular velocity driven by a motor.
2. A **slider block on the crank** slides along a **slotted rocker arm**, causing it to oscillate.
3. The rocker arm drives the **ram** back and forth through a connecting link.
4. Because the crank center is offset, the rocker sweeps a larger angle during the return stroke in less time — producing the **quick return effect**.

### Components Modeled

| Block Name | Type | Description |
|---|---|---|
| World Frame | Fixed Frame | Absolute ground reference |
| Mechanism Configuration | Configuration | Gravity and environment settings |
| Crank | Brick Solid | Input rotating link |
| Connecting Rod | Brick Solid | 15 cm steel rod (ρ = 7800 kg/m³) linking crank to rocker |
| EE1 | Brick Solid | End effector / output link |
| J1 | Revolute Joint | Crank pivot — input actuation joint |
| J3, J4 | Revolute Joint | Intermediate pin joints |
| Joint 3 | Revolute Joint | Rocker-to-frame pivot |
| Prismatic Joint, Prismatic Joint 1 | Prismatic Joint | Slider constraints for linear motion |
| Rigid Transform (×5) | Transform | Frame offsets and coordinate alignments |
| PS-Simulink Converters (×12) | Signal Converter | Converts physical signals to Simulink for scopes |
| Scope (×4) | Scope | Output displays for position, velocity, acceleration |

---

## Simulation Setup

| Parameter | Value |
|---|---|
| Software | MATLAB R2025b + Simscape Multibody |
| Solver | Variable-Step Auto |
| Simulation Stop Time | 10 seconds |
| Crank Input | Constant velocity actuation via J1 |
| Damping (J1) | 0.01 N·m/(deg/s) |
| Connecting Rod Dimensions | 15 × 1 × 1 cm |
| Connecting Rod Density | 7800 kg/m³ (steel) |

The model uses **PS-Simulink Converter** blocks to extract physical signals (position, velocity, acceleration) from the Simscape domain into standard Simulink scopes for visualization.

---

## How to Run

### Prerequisites
Make sure you have the following installed:
- MATLAB R2025b (or later)
- **Simscape** toolbox
- **Simscape Multibody** toolbox

### Steps

```
1. Clone or download this repository
2. Open MATLAB and navigate to the project folder
3. Open the model:
      >> open('Mechanisms_PROJECT.slx')
4. Run the simulation:
      >> sim('Mechanisms_PROJECT')
   Or press Ctrl+T / click the green Run button in Simulink
5. Double-click any Scope block to view the output graphs
```

### Scope Outputs

| Scope | Signal | Joint / Link |
|---|---|---|
| Scope | Position | Output slider displacement |
| Scope1 | Velocity | Slider / rocker velocity |
| Scope2 | Acceleration | Link acceleration |
| Scope3 | Additional signal | *(see model)* |

---

## Results & Analysis

All kinematic outputs were recorded over a 10-second simulation run covering multiple complete crank cycles.

### Position
> 📷 *Graph coming soon*  
> `results/position.png`

The position plot shows the **reciprocating displacement** of the output link. The forward stroke covers a larger time window than the return stroke, clearly demonstrating the quick-return behavior.

---

### Velocity
> 📷 *Graph coming soon*  
> `results/velocity.png`

The velocity graph reveals the **asymmetry between strokes** — the return stroke reaches a noticeably higher peak velocity than the cutting stroke, confirming the quick-return ratio is functioning as expected.

---

### Acceleration
> 📷 *Graph coming soon*  
> `results/acceleration.png`

Acceleration peaks occur at the **stroke reversals** (dead positions of the mechanism). These correspond to the highest inertial loads on the links — important for future force and stress analysis.

---

### Key Mechanism Metrics

| Metric | Value |
|---|---|
| Quick Return Ratio (α/β) | *(to be filled after measurement)* |
| Stroke Length | *(to be filled)* |
| Max Velocity — Cutting Stroke | *(to be filled)* |
| Max Velocity — Return Stroke | *(to be filled)* |

---

## Planned Work

- [ ] Add screenshots of all simulation graphs to `results/`
- [ ] Measure and record quick-return ratio from simulation data
- [ ] Force analysis in Simscape — joint reaction forces and crank torque
- [ ] Hardware prototype build
- [ ] Physical testing — compare measured kinematics against simulation
- [ ] Final comparison report: simulation vs hardware

---

## Repository Structure

```
├── Mechanisms_PROJECT.slx      # Main Simscape Multibody model
├── README.md                   # This file
├── .gitignore                  # Excludes MATLAB cache/build files
└── results/                    # Simulation output graphs (add here)
    ├── position.png
    ├── velocity.png
    └── acceleration.png
```

---

## Requirements

| Tool | Version |
|---|---|
| MATLAB | R2025b or later |
| Simscape | Included with R2025b |
| Simscape Multibody | Included with R2025b |

---

*Mechanical Engineering — Theory of Machines / Kinematics of Machinery*  
*Feel free to fork, reference, or reach out with questions.*
