# Design Recommendations

## Purpose

This document provides design recommendations based on the architecture comparison, operational observations, requirements analysis, human factors review, systems engineering assessment, and preliminary hazard analysis.

The goal is to improve controller usability, mode awareness, and functional alignment across both integrated avionics systems and independent navigator installations.

---

## Recommendation 1: Implement Architecture Profiles

The controller should support selectable architecture profiles based on the avionics configuration being operated.

Different avionics architectures impose different control requirements. A single generic FMS1/FMS2 abstraction may work for integrated avionics systems but may not adequately support independent navigator installations.

---

### Profile A: Integrated Avionics Mode

#### Intended Systems

- Garmin G1000
- Garmin G3000
- Garmin G5000

#### Architecture Model

Integrated avionics systems use a shared avionics architecture where the Primary Flight Display (PFD) and Multi-Function Display (MFD) operate as interfaces to a common flight management and navigation system.

```text
FMS1 = Primary Flight Display
FMS2 = Multi-Function Display
```

#### Design Logic

In this mode, FMS2 may reasonably operate as an extension of FMS1 because both displays interact with a shared avionics system.

#### Recommended Behavior

| Control Area | Recommended Behavior |
|--------------|----------------------|
| FMS1 | Primary flight management and navigation interface |
| FMS2 | MFD/map/system page interface |
| CDI | Primarily associated with the PFD/navigation source workflow |
| Cursor Mode | Managed according to integrated avionics behavior |
| Map Control | Shared or display-specific based on aircraft implementation |
| Annunciation | Indicate active FMS/display context |

---

### Profile B: Independent Navigator Mode

#### Intended Systems

- Garmin GNS430
- Garmin GNS530
- Garmin GTN650
- Garmin GTN750

#### Architecture Model

Independent navigator systems use separate GPS/NAV units. Each unit functions as its own flight management and navigation system.

```text
FMS1 = Navigator 1
FMS2 = Navigator 2
```

#### Design Logic

In this mode, FMS2 should not be treated as an extension of FMS1. FMS2 represents an independent navigator and should provide complete operational parity with FMS1.

#### Recommended Behavior

| Control Area | Recommended Behavior |
|--------------|----------------------|
| FMS1 | Full Navigator 1 functionality |
| FMS2 | Full Navigator 2 functionality |
| CDI | Available for both navigator workflows where supported |
| Cursor Mode | Independently available for FMS1 and FMS2 |
| Map Control | Independent zoom/pan behavior for each navigator |
| Annunciation | Independent LED/state feedback for each navigator |

---

## Recommendation 2: Provide FMS1/FMS2 Functional Parity in Independent Navigator Mode

When operating in Independent Navigator Mode, FMS1 and FMS2 should expose equivalent functions unless restricted by the simulated aircraft or avionics package.

Recommended parity functions include:

- CDI source selection
- OBS mode
- Direct-To
- Flight Plan
- Procedures
- Cursor mode
- Map range/zoom
- Map pan
- Menu functions
- Clear/Enter behavior
- Active navigator state indication

The current physical device already provides dedicated controls for common avionics functions such as Direct-To, Menu, Flight Plan, Clear, and Enter. Therefore, the primary concern is not the absence of those physical controls, but rather whether equivalent FMS1 and FMS2 functionality is exposed across supported avionics architectures.

---

## Recommendation 3: Implement Shift + FMS Pan/Zoom Mode

The strongest recommended functional improvement is to implement a dedicated Pan/Zoom mode using the existing shifted FMS controls.

### Recommended Behavior

| Input | Recommended Function |
|------|----------------------|
| Shift + FMS1 | Activate Pan/Zoom mode for Navigator 1 / FMS1 |
| Shift + FMS2 | Activate Pan/Zoom mode for Navigator 2 / FMS2 |

This approach preserves the current hardware layout while adding a high-value map control workflow.

---

### Default Pan/Zoom Mode Behavior

When Pan/Zoom mode is activated:

| Control | Recommended Function |
|--------|----------------------|
| Large knob left | Zoom out |
| Large knob right | Zoom in |
| Small knob left/right | Optional horizontal pan |
| Large knob in Pan mode | Optional vertical pan |
| Toggle/swap button | Optional Zoom/Pan mode switch |

The base implementation should prioritize map zoom first, because map range changes are more frequently used during IFR operations than manual map panning.

---

### FMS1 and FMS2 Independence

In Independent Navigator Mode:

| Mode | Requirement |
|------|-------------|
| Shift + FMS1 | Controls map range/pan for Navigator 1 |
| Shift + FMS2 | Controls map range/pan for Navigator 2 |

FMS2 should not inherit reduced behavior from the integrated avionics model. In dual GNS/GTN installations, FMS2 represents a complete second navigator and should support independent map control.

---

## Recommendation 4: Improve Shift Mode Annunciation

The controller should provide clear visual feedback when operating in shifted control states.

When any shift mode is active, the selected mode LED should blink continuously.

Recommended behavior:

| Mode State | Recommended LED Behavior |
|------------|--------------------------|
| Base Mode | LED off or steady normal state |
| Shift Mode Active | Selected mode LED blinks continuously |
| Shift Mode Inactive | LED returns to normal state |

Preferred blink rate:

```text
Approximately 2 blinks per second
```

This would reduce ambiguity and help the pilot immediately recognize when shifted functions are armed.

This recommendation is especially important because shifted functions may be used during high-workload IFR tasks such as approach setup, CDI source management, procedure selection, and map range changes.

---

## Recommendation 5: Provide FMS Cursor and Map Mode Annunciation

Cursor mode and map mode should provide clear state feedback, especially for independent navigator workflows.

Recommended behavior:

| State | Recommended Feedback |
|-------|----------------------|
| FMS1 Cursor Active | FMS1 LED blinks or provides distinct indication |
| FMS2 Cursor Active | FMS2 LED blinks or provides distinct indication |
| FMS1 Map/Pan-Zoom Mode Active | FMS1 LED indicates active shifted map mode |
| FMS2 Map/Pan-Zoom Mode Active | FMS2 LED indicates active shifted map mode |

This would improve mode awareness and reduce the need for the pilot to verify controller state visually on the simulated avionics display.

---

## Recommendation 6: Move High-Frequency IFR Functions to the Base Layer Where Possible

Shifted functions are useful for lower-frequency or secondary tasks, but high-frequency Instrument Flight Rules (IFR) functions should remain directly accessible where possible.

Functions that should be prioritized for base-layer access include:

- CDI source selection
- Direct-To
- Flight Plan
- Procedures
- Cursor activation
- Map range/zoom
- Primary navigator selection
- Common autopilot interactions

Since the current device already includes dedicated controls for several core avionics functions, the primary improvement should focus on preserving direct access and reducing unnecessary dependence on shifted commands for time-sensitive IFR workflows.

---

## Recommendation 7: Optional Future Hardware Enhancement — Multifunction Soft Keys

A future hardware revision could optionally benefit from additional multifunction programmable buttons.

This is not a required fix for the current controller architecture. The more immediate recommendation is to improve profile behavior, shift-mode annunciation, and FMS1/FMS2 functional parity.

However, additional programmable buttons could improve support for integrated avionics soft-key workflows, especially Garmin G1000-style operations.

### Optional Hardware Concept

- Add up to eight multifunction programmable buttons
- Support soft-key style operations
- Allow aircraft-specific or avionics-specific labeling through profiles
- Improve compatibility with G1000-style soft-key workflows

### Potential Benefits

- Better support for G1000 soft-key operations
- Reduced reliance on shifted functions
- Improved direct access to profile-specific functions
- More flexible mapping across G1000, GNS, and GTN systems
- Reduced pilot workload during procedure-heavy IFR operations

This should be treated as a future product enhancement, not a required correction for the existing device.

---

## Recommendation 8: Optional Future Hardware Enhancement — Five-Way Directional Control

A five-way directional control could optionally improve map, cursor, and menu interaction.

### Potential Functions

- Map panning
- Cursor movement
- Menu navigation
- Page selection
- Enter/confirm command

### Benefit

A five-way control would reduce the need to overload concentric knobs for both data entry and map manipulation. This would improve usability during map review, flight plan editing, and procedure setup.

This recommendation should be treated as an optional future enhancement rather than a required design change.

---

## Recommendation 9: Expose LED States and Control States to External Profiles

The controller should expose relevant mode and LED states to external configuration tools and profiles.

Recommended exposed states include:

- FMS1 active
- FMS2 active
- FMS1 shift active
- FMS2 shift active
- FMS1 cursor active
- FMS2 cursor active
- FMS1 map mode active
- FMS2 map mode active
- CDI state
- OBS state
- Active architecture profile

This would allow advanced users, developers, and profile designers to create more accurate behavior for different avionics configurations.

---

## Recommendation 10: Document Supported Behavior by Avionics Type

The controller documentation should clearly distinguish supported behavior by avionics architecture.

Recommended documentation structure:

| Avionics Type | Recommended Documentation |
|---------------|---------------------------|
| G1000/G3000/G5000 | Integrated Avionics Mode behavior |
| GNS430/530 | Independent Navigator Mode behavior |
| GTN650/750 | Independent Navigator Mode behavior |
| Custom Profiles | User-configurable mapping guidance |

This would reduce user confusion and make it clear when FMS2 is functioning as an MFD extension versus an independent navigator.

---

## Summary of Recommendations

| Recommendation ID | Recommendation | Priority | Primary Benefit |
|-------------------|----------------|----------|-----------------|
| REC-001 | Implement architecture profiles | High | Aligns controller behavior with avionics architecture |
| REC-002 | Provide FMS1/FMS2 parity in Independent Navigator Mode | High | Supports dual navigator workflows |
| REC-003 | Implement Shift + FMS Pan/Zoom mode | High | Adds useful map control without redesigning hardware |
| REC-004 | Improve shift mode annunciation | High | Reduces mode confusion |
| REC-005 | Add FMS cursor/map mode annunciation | High | Improves mode awareness |
| REC-006 | Move high-frequency IFR functions to the base layer where possible | Medium | Reduces workload |
| REC-007 | Add multifunction programmable buttons | Optional Future Enhancement | Improves G1000 soft-key support |
| REC-008 | Consider a five-way directional control | Optional Future Enhancement | Improves cursor and map control |
| REC-009 | Expose LED and control states externally | Medium | Supports advanced profiles |
| REC-010 | Document supported behavior by avionics type | Medium | Improves user understanding |

---

## Conclusion

The primary design recommendation is to move from a generic FMS1/FMS2 abstraction toward an architecture-aware control model.

Integrated avionics systems and independent navigator installations impose different operational requirements. Supporting both through selectable architecture profiles would improve usability, reduce workload, and better align controller behavior with real-world avionics workflows.

For independent navigator installations, FMS2 should be treated as a complete second navigator rather than a reduced-function extension of FMS1.

The strongest near-term recommendations do not require physical hardware redesign. They are:

1. Implement Shift + FMS1 and Shift + FMS2 Pan/Zoom modes.
2. Provide blinking LED annunciation when shift modes are active.
3. Provide FMS1/FMS2 functional parity in Independent Navigator Mode.
4. Expose relevant LED and control states to external profiles.

Optional hardware enhancements, such as additional multifunction buttons or a five-way directional control, may improve future product capability but should not be treated as required to address the current architecture and mode-awareness findings.
