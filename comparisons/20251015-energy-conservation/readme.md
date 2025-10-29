# 20251015: Energy conservation in unbounded media <!-- omit in toc -->

## Table of contents <!-- omit in toc -->

- [1. Overview](#1-overview)
  - [1.1. Purpose](#11-purpose)
  - [1.2. Scope](#12-scope)
  - [1.3. Rationale](#13-rationale)
  - [1.4. Expectation](#14-expectation)
- [2. Specification](#2-specification)
  - [2.4. Geometry](#24-geometry)
  - [2.2. Materials](#22-materials)
  - [2.5. Source](#25-source)
  - [2.6. Physics](#26-physics)
- [3. Measurand](#3-measurand)
- [4. Method](#4-method)
- [5. Analysis](#5-analysis)
- [6. Report](#6-report)
  - [6.1. Input](#61-input)
  - [6.2. Results](#62-results)
- [7. Results](#7-results)

## 1. Overview

### 1.1. Purpose

Verify that Monte Carlo simulations correctly conserve energy during particle transport, up to floating-point precision.

### 1.2. Scope

Verify energy conservation for monoenergetic electrons and photons (1 keV to 20 MeV) in infinite homogeneous media. Test matrix includes 9 materials: 7 representative elements, plus air and liquid water. Each software simulates 72 cases (2 particles × 9 materials × 4 energies) with the expectation that total deposited energy equals the imparted energy, within machine precision. This benchmark tests internal algorithm consistency and floating-point precision, rather than agreement between simulations or with experimental data.

### 1.3. Rationale

- Energy conservation is a fundamental principle and requirement for a software modelling the transport of ionizing radiation.

- In numerical work on a finite-precision computer, floating-point arithmetic errors ($2^{-52}$ in 64-bit IEEE 754 representation) accumulate during calculation.

- This scenario seeks to verify that floating-point errors are under control in the software.

- A set of representative energies and materials is considered, because the accumulated floating-point error in this scenario is expected to grow like the number of energy deposition events during the simulation, which is proportional to $N$, with a constant that depends on the incident energy and the atomic number.

### 1.4. Expectation

The total energy deposited per incident particle is equal to the initial particle energy, up to a precision that can be understood in terms of floating-point errors.

## 2. Specification

### 2.4. Geometry

![diagram.png](assets/diagram.png)

- Infinite homogeneous medium (no boundaries).

- Each particle starts at origin with kinetic energy $E_0$, in a random direction.

- If the software cannot model an infinite medium space, the implementation should:

  - Use a sphere of radius 40 × the mean free path of photons with the incident energy.
  - Center the sphere at the origin.
  - Document the actual sphere radius used for each case.
  - Verify that the fraction of particles reaching the sphere radius is less than $10^{-16}$.

### 2.2. Materials

- Atomic number (symbol): 1 (H), 6 (C), 13 (Al), 27 (Co), 47 (Ag), 74 (W), 82 (Pb)
- Compounds: Air, Water
- State: Natural state at room temperature (gas, liquid, or solid)

### 2.5. Source

- Particle: Electron or Photon.
- Shape: Point source.
- Position: (0, 0, 0).
- Direction: Isotropic (uniformly random in 4π).
- Spectrum: Monoenergetic
- Kinetic energy (MeV): 1.234567890123456e-2, 1.234567890123456e-1, 1.234567890123456e0, 1.234567890123456e1

### 2.6. Physics

- Default physical data, options and cross sections.
- Default particle production thresholds and transport cutoffs.
- No variance reduction techniques.
- For parameters without a default value, use the value or option that is typically recommended.

## 3. Measurand

- Total energy deposited in medium, per incident particle.

## 4. Method

1. Run the simulation for $N=10^9$ independent incident particles.

2. Record the total energy $E$ deposited in the medium.

3. Determine the energy deposited per incident particle: $E/N$.

## 5. Analysis

1. Compute the difference between the deposited energy per history and the source particle energy $E_0$.

2. Report the result $R$ as the normalized difference between the deposited and incident energy:

  $$
  R = \frac{E-E_0}{E_0}.
  $$

## 6. Report

### 6.1. Input

- Simulation input files for all cases (or a script to generate them from a template).
- Instructions to reproduce the simulations from a default installation of the software.

### 6.2. Results

- For each case, report the result $R$.
- No statistical uncertainty is required since results should be exact on a per-history basis.
- Provide the result dataset as a .csv file according to the following template:

  ```csv
  software,version,particle,material,MeV,R
  EGSnrc,2025,electron,H2O,0.01,1.34e-15
  ```

## 7. Results
