# Compact Flight Simulator Avionics Architecture Analysis

## Overview

This repository documents a systems engineering and human factors analysis conducted during evaluation of the Octavi IFR-1 avionics controller within Microsoft Flight Simulator.

The study investigates architectural differences between integrated avionics systems such as the Garmin G1000 and independent navigator installations such as dual Garmin GNS430/530 and GTN650/750 configurations.

The objective is to identify requirements gaps, evaluate operational impacts, and propose design improvements that better align controller behavior with real-world avionics architectures and pilot workflows.

---

## Problem Statement

During operational evaluation of the Octavi IFR-1, a functional asymmetry was observed between integrated and independent flight management system architectures.

The current controller abstraction successfully supports Garmin G1000 installations where FMS1 and FMS2 operate as logical extensions of a common avionics system.

However, the same abstraction introduces limitations when applied to dual Garmin GNS430/530 and GTN650/750 installations, where each navigator represents an independent flight management system requiring full functional parity.

This difference affects:

- Cursor mode management
- Map panning operations
- Zoom control
- CDI source selection
- User feedback and annunciation
- Controller state awareness

---

## Systems Engineering Focus Areas

- Requirements Analysis
- Functional Architecture
- Human Factors Engineering
- Human-Machine Interface (HMI)
- Operational Usability
- Control Allocation
- Flight Deck Workflow Analysis
- Safety-Oriented Interface Design

---

## Case Study

### Integrated Architecture

Garmin G1000

- FMS1 = Primary Flight Display (PFD)
- FMS2 = Multi Function Display (MFD)
- Shared avionics architecture
- Shared state management

### Independent Architecture

Dual Garmin GNS430/530

- GNS430 #1 = Independent Navigator
- GNS430 #2 = Independent Navigator
- Independent state management
- Independent CDI functions
- Independent cursor modes
- Independent flight plan management

---

## Current Findings

1. FMS2 cursor mode behavior does not fully represent independent navigator operation.

2. CDI functionality is available for FMS1 but not consistently exposed for FMS2.

3. GTN750-specific map functions operate correctly while equivalent GNS430/530 functions are not always available.

4. Current controller abstraction appears optimized for integrated avionics architectures.

5. Independent navigator architectures require expanded requirements allocation and control parity.

---

## Future Work

- Functional decomposition
- Requirements traceability matrix
- Human factors assessment
- Operational hazard analysis
- Architecture recommendations
- Product enhancement proposals
