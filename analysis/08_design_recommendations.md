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

---

## Recommendation 3: Improve Mode Annunciation

The controller should provide clear visual feedback when operating in alternate or shifted control states.

### Shift Mode Annunciation

When shift mode is active, the selected mode LED should blink continuously.

Recommended behavior:

| Mode State | Recommended LED Behavior |
|------------|--------------------------|
| Base Mode | LED off or steady normal state |
| Shift Mode Active | LED blinks continuously |
| Shift Mode Inactive | LED returns to normal state |

Preferred blink rate:

```text
Approximately 2 blinks per second
```

This would reduce ambiguity and help the pilot immediately recognize when shifted functions are armed.

---

## Recommendation 4: Provide FMS Cursor and Map Mode Annunciation

Cursor mode and map mode should provide clear state feedback, especially for independent navigator workflows.

Recommended behavior:

| State | Recommended Feedback |
|-------|----------------------|
| FMS1 Cursor Active | FMS1 LED blinks |
| FMS2 Cursor Active | FMS2 LED blinks |
| FMS1 Map Mode Active | FMS1 LED or secondary indication active |
| FMS2 Map Mode Active | FMS2 LED or secondary indication active |

This would improve mode awareness and reduce the need for the pilot to verify controller state visually on the simulated avionics display.

---

## Recommendation 5: Move High-Frequency IFR Functions to the Base Layer

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

This would reduce pilot workload during high-task-load phases such as approach setup, missed approach preparation, procedure modification, and navigation source management.

---

## Recommendation 6: Add Eight Multifunction Programmable Buttons

A future hardware revision could benefit from the addition of eight multifunction programmable buttons.

These buttons could mimic the soft-key concept used in integrated avionics systems such as the Garmin G1000 while also supporting independent navigator workflows.

### Potential Uses

| Button Group | Possible Function |
|--------------|-------------------|
| Soft Key 1 | CDI |
| Soft Key 2 | OBS |
| Soft Key 3 | Direct-To |
| Soft Key 4 | Flight Plan |
| Soft Key 5 | Procedures |
| Soft Key 6 | Nearest |
| Soft Key 7 | Clear |
| Soft Key 8 | Enter/Menu |

### Benefits

- Reduces reliance on shifted functions
- Improves direct access to common IFR functions
- Supports aircraft-specific profiles
- Improves training transferability
- Reduces pilot workload
- Better aligns the controller with real avionics workflows

---

## Recommendation 7: Consider a Five-Way Directional Control

A five-way directional control could improve map, cursor, and menu interaction.

### Potential Functions

- Map panning
- Cursor movement
- Menu navigation
- Page selection
- Enter/confirm command

### Benefit

A five-way control would reduce the need to overload concentric knobs for both data entry and map manipulation. This would improve usability during map review, flight plan editing, and procedure setup.

---

## Recommendation 8: Expose LED States and Control States to External Profiles

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

## Recommendation 9: Document Supported Behavior by Avionics Type

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

| Recommendation ID | Recommendation | Primary Benefit |
|-------------------|----------------|-----------------|
| REC-001 | Implement architecture profiles | Aligns controller behavior with avionics architecture |
| REC-002 | Provide FMS1/FMS2 parity in Independent Navigator Mode | Supports dual navigator workflows |
| REC-003 | Improve shift mode annunciation | Reduces mode confusion |
| REC-004 | Add FMS cursor/map mode annunciation | Improves mode awareness |
| REC-005 | Move high-frequency IFR functions to the base layer | Reduces workload |
| REC-006 | Add eight multifunction programmable buttons | Improves direct access to common functions |
| REC-007 | Consider a five-way directional control | Improves cursor and map control |
| REC-008 | Expose LED and control states externally | Supports advanced profiles |
| REC-009 | Document supported behavior by avionics type | Improves user understanding |

---

## Conclusion

The primary design recommendation is to move from a generic FMS1/FMS2 abstraction toward an architecture-aware control model.

Integrated avionics systems and independent navigator installations impose different operational requirements. Supporting both through selectable architecture profiles would improve usability, reduce workload, and better align controller behavior with real-world avionics workflows.

For independent navigator installations, FMS2 should be treated as a complete second navigator rather than a reduced-function extension of FMS1.

Additional improvements such as shift mode annunciation, FMS cursor state feedback, programmable buttons, and optional directional controls would further improve mode awareness and training transferability.
