# Ionizing radiation simulation comparison database (scdb-ri)

**Metrological traceability for simulations of ionizing radiation transport**

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgreen.svg)](https://creativecommons.org/licenses/by/4.0/)

## Overview

The ionizing radiation simulation comparison database (scdb-ri) provides a systematic framework for benchmarking Monte Carlo radiation transport software through rigorous intercomparisons, modelled after the BIPM Key Comparison Database (KCDB).

Just as the KCDB establishes equivalence between measurement standards maintained by National Metrology Institutes, scdb-ri establishes equivalence between simulation results produced by different Monte Carlo software, creating a traceable foundation for computational radiation dosimetry.

## Problem

Monte Carlo simulations are essential for radiation dosimetry, treatment planning, radiation protection, and industrial applications. However, the field historically lacks:

- **Systematic intercomparisons** with quantified degrees of equivalence between software.
- **Reference benchmarks** with well-characterized uncertainties.
- **Standardized test cases** covering the full range of radiation transport scenarios.
- **Traceable validation** linking simulation results to fundamental physics.
- **Public repository** of comparative performance metrics.

Without these elements, each research group validates independently using different test cases, making it difficult to establish confidence in simulation results across different implementations.

## Solution

This repository implements a metrological approach to simulation comparison by:

- **Defining reference problems** spanning key application domains.
- **Establishing comparison protocols** including geometry, materials, scoring, reporting formats.
- **Quantifying degrees of equivalence** between Monte Carlo software.
- **Documenting software capabilities** as Certified Simulation Capabilitis (CSCs).
- **Providing traceable benchmarks** to be cited in publications and regulatory submissions.

## Structure

Each simulation comparison is coordinated in a separate directory under `comparisons/`, named according to the date the comparison was created, for example `20251015-energy-conservation`. Each comparison directory contains its own README file detailing the specific structure, participating software, scenario, specifications, and required inputs and outputs for that comparison.

## License

Documents in this repository are licensed under a Creative Commons Attribution 4.0 International License (CC BY 4.0). Any computer source code in this repository is licensed under the MIT Licence.

## AI Disclosure

This README was developed collaboratively using Claude (Anthropic, Opus 4.1). The original concept, structure, and domain-specific content were provided by the human author, while Claude assisted in organizing and refining the text for clarity and completeness.
