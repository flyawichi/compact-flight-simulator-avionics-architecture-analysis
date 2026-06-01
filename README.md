# Compact Flight Simulator Avionics Architecture Analysis

## Overview

This repository documents a systems engineering and human factors analysis conducted during evaluation of the Octavi IFR-1 avionics controller within Microsoft Flight Simulator.

The study investigates architectural differences between integrated avionics systems such as the Garmin G1000 and independent navigator installations such as dual Garmin GNS430/530 and GTN650/750 configurations.

The objective is to identify requirements gaps, evaluate operational impacts, and propose design improvements that better align controller behavior with real-world avionics architectures and pilot workflows.

## Problem Statement

During operational evaluation of the Octavi IFR-1 controller, a functional asymmetry was observed between integrated avionics architectures and independent navigator architectures.

The current controller abstraction successfully supports Garmin G1000 installations where FMS1 and FMS2 operate as logical extensions of a common avionics system.

However, dual Garmin GNS430/530 and GTN650/750 installations represent independent navigators, each requiring complete functional parity and operational independence.

This difference affects:

- Cursor mode management
- Map panning operations
- Zoom control
- CDI source selection
- Controller annunciation
- Pilot situational awareness

## Systems Engineering Focus Areas

- Requirements Analysis
- Functional Architecture
- Human Factors Engineering
- Human-Machine Interface Design
- Control Allocation
- Flight Deck Workflow Analysis
- Operational Usability Assessment

## Current Findings

1. FMS2 functionality appears optimized for integrated avionics architectures.

2. Dual GNS430/530 installations require independent navigator support.

3. GTN750 map functions are available while equivalent GNS430/530 support appears limited.

4. Cursor mode state awareness is not consistently represented on the controller.

5. CDI functionality appears available on FMS1 but not consistently exposed on FMS2.

## Future Work

- Functional decomposition
- Requirements traceability matrix
- Human factors assessment
- Architecture recommendations
- Product enhancement proposals

## Author

Chineye J. Okowi

Systems Engineering | Aviation Safety | Data Engineering

GitHub: https://github.com/flyawichi
LinkedIn: https://www.linkedin.com/in/chineye-o-19860391/
