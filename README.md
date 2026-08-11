# Compact Flight Simulator Avionics Architecture Analysis

## About

This repository documents a systems-engineering and human-factors analysis developed from evaluation of the Octavi IFR-1 avionics controller in Microsoft Flight Simulator. The case study examines how controller behavior maps differently to integrated avionics architectures and to installations containing independent navigators.

The project demonstrates requirements analysis, functional architecture reasoning, human-machine-interface assessment, and operational workflow analysis in an aviation context.

## Problem / Operational Context

During operational evaluation, a functional asymmetry was observed between integrated avionics architectures and independent navigator architectures.

The controller abstraction supports Garmin G1000 installations, where FMS1 and FMS2 can operate as logical extensions of a common integrated avionics environment. Dual Garmin GNS430/530 and GTN650/750 installations, however, represent independent navigators that require greater functional independence and explicit state awareness.

The architectural distinction affects pilot interaction with functions including:

- cursor-mode management;
- map panning and zoom;
- CDI source selection;
- controller annunciation; and
- pilot situational awareness.

## Engineering Objectives

The analysis is intended to:

- identify requirements gaps created by differing avionics architectures;
- distinguish integrated-system behavior from independent-navigator behavior;
- evaluate operational and human-factors consequences of control allocation;
- identify where controller state or function availability may be ambiguous; and
- develop architecture and product-improvement recommendations grounded in pilot workflow.

## System Context

The system of interest is the interaction among the pilot, the physical avionics controller, the simulator integration layer, and the simulated avionics equipment.

The analysis treats the avionics architecture itself as an important design input. A control model appropriate for an integrated flight deck may not provide equivalent behavior when mapped to two independent navigation units.

## Requirements & Constraints

The assessment considers several systems-level constraints:

- independent navigators require independent access to operationally necessary controls;
- controller state should be understandable to the pilot without unnecessary mode ambiguity;
- physical control allocation should remain consistent with the functional architecture being represented;
- simulator limitations must be distinguished from controller-design limitations; and
- recommendations should preserve usability without assuming that unlike avionics architectures behave identically.

## Architecture Analysis

Two architecture patterns are central to the case study:

**Integrated avionics architecture** — multiple flight-management functions operate within a coordinated avionics environment, allowing some shared abstractions and control behavior.

**Independent navigator architecture** — each navigator maintains its own functional state and therefore requires appropriate independent control access and annunciation.

This architectural distinction provides the basis for evaluating the observed FMS1/FMS2 behavior.

## Engineering Decisions & Tradeoffs

The analysis intentionally avoids treating every observed difference as a software defect. Instead, observations are evaluated against system architecture, control allocation, pilot workflow, and the possibility of simulator/integration constraints.

That distinction is important because a credible recommendation must identify the layer at which a requirement or behavior actually belongs.

## Current Findings

1. FMS2 behavior appears better aligned with integrated avionics architectures than with fully independent navigator installations.
2. Dual GNS430/530 installations require independent navigator support to preserve functional parity.
3. GTN750 map functions are available while equivalent GNS430/530 support appears more limited.
4. Cursor-mode state awareness is not consistently represented on the controller.
5. CDI functionality appears available on FMS1 but is not consistently exposed on FMS2.

These are case-study observations and should be interpreted within the evaluated simulator/controller configuration rather than as certification findings about the referenced avionics products.

## Implementation / Technical Evidence

The current repository focuses on systems analysis rather than production software implementation. Technical evidence will be expanded through functional decomposition, interface mapping, requirements artifacts, and architecture diagrams.

## Verification & Validation

Planned verification will trace observed behaviors and proposed requirements to representative operational scenarios. The objective is to determine whether recommended controller behavior preserves functional independence, state awareness, and pilot workflow across the architecture patterns evaluated.

## Engineering Outcomes

The project establishes a systems-level explanation for why a controller abstraction that is effective for an integrated avionics suite may not transfer cleanly to independent navigator installations. It converts an operational usability observation into an architecture and requirements problem suitable for structured engineering analysis.

## Future Evolution / Known Limitations

Planned work includes:

- functional decomposition;
- requirements traceability matrix;
- system and interface diagrams;
- human-factors assessment;
- architecture recommendations; and
- product-enhancement proposals.

## Author

**Chineye J. Okowi**  
Systems Engineering | Aviation Safety | Data Engineering
