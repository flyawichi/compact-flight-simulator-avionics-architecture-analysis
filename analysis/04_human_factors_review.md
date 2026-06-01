# Human Factors Review

## Purpose

This document evaluates the human factors implications of controller behavior when operating integrated avionics systems versus independent navigator systems.

The objective is to identify how controller abstraction, mode awareness, and functional asymmetry may affect pilot workload, usability, and operational confidence during simulated instrument flight operations.

---

## Human Factors Context

Flight deck controls must support the pilot’s mental model of the avionics system being operated.

When the controller model aligns with the avionics architecture, the pilot can operate the system predictably.

When the controller model does not align with the avionics architecture, the pilot may experience:

- Mode confusion
- Increased heads-down time
- Increased workload
- Reduced trust in the controller
- Reduced training transferability

---

## User Mental Model vs System Model

| Area | Pilot Mental Model | Observed Controller Model | Human Factors Concern |
|------|-------------------|---------------------------|-----------------------|
| Garmin G1000 | FMS1 controls PFD; FMS2 controls MFD | FMS1/FMS2 behave as display interfaces to a shared system | Low concern |
| Dual GNS430/530 | FMS1 and FMS2 are independent navigators | FMS2 appears partially dependent or reduced-function | User expectation mismatch |
| Dual GTN650/750 | Each GTN is an independent navigator | GTN-specific commands may work, but parity assumptions remain important | Requires architecture-specific support |
| Cursor Mode | Active cursor state should be clearly indicated | FMS2 cursor state may not be annunciated | Mode awareness degradation |
| CDI Control | Each navigator may require independent source/function control | CDI behavior appears more complete on G1000 than GNS/FMS2 workflows | Functional inconsistency |

---

## Mode Awareness

Mode awareness is the pilot’s understanding of the current operating state of the system.

In this case, the key concern is whether the pilot can determine:

- Which navigator is currently active
- Whether cursor mode is active
- Whether map mode is active
- Whether knob input will control zoom, pan, page selection, or data entry
- Whether FMS2 is operating as an independent navigator or as an extension of FMS1

Poor mode awareness can lead to incorrect control inputs and increased time spent verifying system behavior.

---

## Workload Impact

Functional asymmetry between FMS1 and FMS2 may increase pilot workload because the pilot must remember which functions are supported on each side.

| Condition | Workload Impact |
|----------|-----------------|
| FMS1 and FMS2 behave differently | Requires additional memory and verification |
| FMS2 cursor mode lacks annunciation | Requires visual confirmation on the simulated avionics display |
| FMS2 CDI functionality is unavailable or inconsistent | Reduces predictable workflow |
| Map zoom/pan behavior differs across avionics types | Increases configuration burden |
| Controller behavior changes by avionics architecture | Requires profile-specific learning |

---

## Training Transferability

A flight simulator controller used for instrument proficiency should support workflows that resemble real cockpit operations.

For integrated avionics systems such as the Garmin G1000, the current control model appears generally aligned with the avionics architecture.

For independent navigator systems such as dual GNS430/530 or GTN650/750 installations, training transferability may be reduced if the controller does not preserve independent navigator behavior.

Key transferability concerns include:

- Independent navigator selection
- Independent CDI/source control
- Independent cursor mode
- Independent map manipulation
- Clear annunciation of active control state

---

## Human-Machine Interface Observations

| Observation | Human Factors Implication |
|------------|---------------------------|
| FMS2 does not appear to provide full parity with FMS1 in independent navigator workflows | Creates expectation mismatch |
| FMS2 cursor/map mode may not be clearly annunciated | Reduces mode awareness |
| CDI behavior differs between G1000 and GNS workflows | Increases cognitive burden |
| GTN-specific controls may work while GNS equivalents are unavailable | Creates inconsistent user experience |
| Controller profiles appear optimized for integrated avionics | Limits usability for independent navigator aircraft |

---

## Recommended Human Factors Improvements

| Recommendation | Human Factors Benefit |
|---------------|----------------------|
| Add Integrated Avionics Mode and Independent Navigator Mode | Aligns controller model with aircraft avionics architecture |
| Provide FMS1/FMS2 functional parity in Independent Navigator Mode | Reduces user expectation mismatch |
| Add FMS2 cursor/map mode annunciation | Improves mode awareness |
| Provide visual LED state feedback for active navigator modes | Reduces verification burden |
| Support architecture-specific control profiles | Improves training transferability |
| Document supported behavior by avionics type | Reduces user confusion |

---

## Human Factors Conclusion

The primary human factors issue is not the absence of a single button mapping.

The primary issue is a mismatch between the pilot’s mental model and the controller’s architecture model.

For integrated avionics systems, the controller model appears generally appropriate.

For independent navigator systems, the controller should treat FMS1 and FMS2 as separate operational systems with equivalent functionality and independent state feedback.

Improving this alignment would reduce pilot workload, improve mode awareness, and increase training transferability for users operating legacy and dual-navigator IFR aircraft.
