# Human Factors Review

## Purpose

This document evaluates the human factors implications of controller behavior when operating integrated avionics systems versus independent navigator systems.

The objective is to identify how controller abstraction, mode awareness, and functional asymmetry may affect pilot workload, usability, and operational confidence during simulated Instrument Flight Rules (IFR) operations.

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

## Shift Mode Awareness and Workload

A key human factors concern identified during the controller evaluation is the use of shifted functions during IFR operations.

Shifted functions can increase controller capability without increasing hardware size, but they also introduce a mode-awareness requirement. The pilot must know whether the controller is operating in its base state or shifted state before making an input.

During high-workload IFR tasks, such as approach setup, procedure loading, CDI source management, map range changes, or cursor manipulation, uncertainty about shift-state activation may increase cognitive workload and reduce operational confidence.

---

## Shift Mode Annunciation

When shift mode is active, the controller should provide an unmistakable visual indication.

Recommended behavior:

| Mode State | Recommended LED Behavior |
|-----------|--------------------------|
| Base Mode | LED off or steady normal state |
| Shift Mode Active | LED blinks continuously |
| Shift Mode Inactive | LED returns to normal state |

The preferred blink rate is approximately **two times per second** while shift mode is active.

This would allow the pilot to immediately recognize that shifted functions are armed without needing to verify the state through software, memory, or trial-and-error input.

---

## Shifted Function Workload Concern

If the pilot cannot clearly determine whether shift mode is active, the following issues may occur:

- Increased heads-down time
- Increased cognitive workload
- Incorrect function selection
- Reduced confidence in controller state
- Increased likelihood of mode confusion
- Reduced training transferability during IFR procedures

This issue becomes more significant when shifted functions are used for high-frequency IFR tasks.

---

## Control Allocation Consideration

Shifted functions are useful for secondary or low-frequency tasks.

However, functions that are frequently used during IFR operations should remain on the base control layer where possible.

Examples of functions that should generally be available without shift activation include:

- CDI source selection
- Direct-To
- Flight Plan
- Procedures
- Cursor activation
- Map range/zoom
- Primary navigator selection
- Common autopilot interactions

Moving high-frequency IFR functions to the base layer would reduce pilot workload and improve operational usability.

---

## Recommended Hardware Enhancement

One potential hardware enhancement would be the addition of **eight multifunction programmable buttons**.

These buttons could mimic the soft-key concept used in integrated avionics systems such as the Garmin G1000 while also supporting independent navigator workflows.

Potential benefits include:

- Reduced reliance on shifted functions
- Improved direct access to high-frequency IFR functions
- Better alignment with real avionics workflows
- More flexible profile mapping across G1000, GNS, and GTN systems
- Improved training transferability
- Reduced pilot workload during procedure-heavy IFR operations

---

## Optional Navigation Control Enhancement

An optional **five-way directional control** could further improve usability.

A five-way control could support:

- Map panning
- Cursor movement
- Menu navigation
- Page selection
- Confirmation or enter commands

This would reduce the need to overload concentric knobs for both navigation and map manipulation tasks.

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
| Shift mode state is not clearly annunciated | Increases mode verification burden |
| Frequently used IFR functions require shifted inputs | Increases task complexity during high-workload phases of flight |

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
- Clear annunciation of shifted controller state
- Base-layer access to high-frequency IFR functions

---

## Human-Machine Interface Observations

| Observation | Human Factors Implication |
|------------|---------------------------|
| FMS2 does not appear to provide full parity with FMS1 in independent navigator workflows | Creates expectation mismatch |
| FMS2 cursor/map mode may not be clearly annunciated | Reduces mode awareness |
| CDI behavior differs between G1000 and GNS workflows | Increases cognitive burden |
| GTN-specific controls may work while GNS equivalents are unavailable | Creates inconsistent user experience |
| Controller profiles appear optimized for integrated avionics | Limits usability for independent navigator aircraft |
| Shift mode may not provide sufficient visual annunciation | Increases risk of mode confusion |
| High-frequency IFR functions may require shifted inputs | Increases pilot workload during time-sensitive tasks |

---

## Recommended Human Factors Improvements

| Recommendation | Human Factors Benefit |
|---------------|----------------------|
| Add Integrated Avionics Mode and Independent Navigator Mode | Aligns controller model with aircraft avionics architecture |
| Provide FMS1/FMS2 functional parity in Independent Navigator Mode | Reduces user expectation mismatch |
| Add FMS2 cursor/map mode annunciation | Improves mode awareness |
| Provide visual LED state feedback for active navigator modes | Reduces verification burden |
| Add continuous blinking LED indication when shift mode is active | Improves shift-state awareness |
| Move high-frequency IFR functions to the base control layer | Reduces workload during instrument procedures |
| Add eight multifunction programmable buttons | Improves direct access to common avionics functions |
| Consider an optional five-way directional control | Improves map panning and cursor navigation |
| Support architecture-specific control profiles | Improves training transferability |
| Document supported behavior by avionics type | Reduces user confusion |

---

## Human Factors Conclusion

The primary human factors issue is not the absence of a single button mapping.

The primary issue is a mismatch between the pilot’s mental model and the controller’s architecture model.

For integrated avionics systems, the controller model appears generally appropriate.

For independent navigator systems, the controller should treat FMS1 and FMS2 as separate operational systems with equivalent functionality and independent state feedback.

In addition, shifted controller functions should be clearly annunciated when active. If shift mode is active, the device should provide a continuous visual indication, preferably through a blinking LED at approximately two times per second. This would reduce ambiguity and support improved mode awareness during IFR operations.

High-frequency IFR functions should be prioritized for the base control layer where possible. Additional programmable buttons and an optional five-way directional control would reduce reliance on shifted inputs, improve operational usability, and better support realistic avionics workflows.

Improving this alignment would reduce pilot workload, improve mode awareness, and increase training transferability for users operating legacy and dual-navigator IFR aircraft.
