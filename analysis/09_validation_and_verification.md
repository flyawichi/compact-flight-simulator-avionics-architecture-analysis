# Validation and Verification

## Objective

This document defines a preliminary validation and verification approach for evaluating whether the controller behavior satisfies derived operational and human factors requirements.

The intent is to assess whether the observed controller behavior aligns with the expected avionics architecture model for both:

1. Integrated avionics systems
2. Independent navigator systems

This is not a certification-level verification activity. It is a systems engineering validation exercise performed within a flight simulation environment.

---

## Verification Scope

The verification activity focuses on the following areas:

- Avionics architecture alignment
- FMS1/FMS2 functional behavior
- Independent navigator support
- Shift mode awareness
- Pan/zoom mode behavior
- LED/state annunciation
- Human-machine interface consistency
- Training transferability

---

## Verification Matrix

| Requirement ID | Requirement | Verification Method | Observed Result | Status |
|----------------|-------------|---------------------|-----------------|--------|
| REQ-001 | Controller shall support Integrated Avionics Mode | Architecture review and G1000 workflow evaluation | G1000-style FMS1/FMS2 behavior appears generally aligned with PFD/MFD architecture | Pass |
| REQ-002 | Controller shall support Independent Navigator Mode | Architecture review and GNS/GTN workflow comparison | FMS2 behavior does not consistently provide full independent navigator functionality | Gap Identified |
| REQ-003 | FMS2 shall provide functional parity with FMS1 in Independent Navigator Mode | Operational testing and function comparison | FMS2 does not appear to expose equivalent CDI/cursor/map behavior across all tested workflows | Gap Identified |
| REQ-004 | Shift + FMS1 shall activate Pan/Zoom mode for Navigator 1 | Proposed behavior review | Not confirmed as native behavior in current implementation | Open |
| REQ-005 | Shift + FMS2 shall activate Pan/Zoom mode for Navigator 2 | Proposed behavior review and MobiFlight testing | Native behavior not confirmed; attempted custom implementation highlighted state-management limitations | Open |
| REQ-006 | Active shift modes shall provide continuous LED annunciation | Human factors review and controller output evaluation | Shift state annunciation does not appear sufficiently explicit for all modes | Gap Identified |
| REQ-007 | FMS1/FMS2 cursor or map mode shall provide clear state indication | Human factors review and controller output evaluation | FMS2 cursor/map mode annunciation appears limited or unavailable | Gap Identified |
| REQ-008 | High-frequency IFR functions should remain available on base control layer where possible | Control allocation review | Several common functions are already dedicated; remaining concern is minimizing shifted access for high-frequency map/navigation tasks | Partial |
| REQ-009 | Controller behavior shall be documented by avionics architecture type | Documentation review | Architecture-specific behavior is not clearly separated between integrated avionics and independent navigators | Gap Identified |
| REQ-010 | External profiles shall be able to access relevant LED/control states | Configuration review | Some output states appear limited or unavailable for FMS-specific LED behavior | Gap Identified |

---

## Validation Findings

### Integrated Avionics Validation

The current implementation appears generally valid for integrated avionics systems such as the Garmin G1000.

In this architecture:

```text
FMS1 = Primary Flight Display
FMS2 = Multi-Function Display
```

This model supports the idea that FMS2 may act as an extension of FMS1 because both displays interact with a shared avionics system.

### Finding

The evaluated controller abstraction is generally compatible with integrated avionics workflows.

### Validation Status

```text
Integrated Avionics Model: Validated at a preliminary level
```

---

## Independent Navigator Validation

Independent navigator installations such as dual Garmin GNS430/530 or GTN650/750 systems require a different control model.

In this architecture:

```text
FMS1 = Navigator 1
FMS2 = Navigator 2
```

Each navigator should support independent state management, independent map behavior, independent cursor behavior, and independent control access.

### Finding

The evaluated controller abstraction does not fully validate against the independent navigator model because FMS2 does not consistently appear to provide full operational parity with FMS1.

### Validation Status

```text
Independent Navigator Model: Gap identified
```

---

## Pan/Zoom Mode Validation

A key recommended behavior is implementation of dedicated Pan/Zoom mode through shifted FMS controls.

Recommended behavior:

| Input | Expected Behavior |
|------|-------------------|
| Shift + FMS1 | Activate Pan/Zoom mode for Navigator 1 |
| Shift + FMS2 | Activate Pan/Zoom mode for Navigator 2 |

### Expected Pan/Zoom Behavior

| Control | Expected Function |
|--------|-------------------|
| Large knob left | Zoom out |
| Large knob right | Zoom in |
| Optional toggle/swap input | Switch between zoom and pan behavior |
| Small knob | Optional horizontal pan |
| Large knob in pan mode | Optional vertical pan |

### Finding

Native Shift + FMS Pan/Zoom behavior was not confirmed during the evaluation. Custom implementation attempts through MobiFlight suggested that state handling and avionics-specific events vary by supported avionics package.

### Validation Status

```text
Pan/Zoom Mode: Open requirement
```

---

## Shift Mode Annunciation Validation

Shifted functions can increase capability, but they require clear state awareness.

Recommended behavior:

```text
When shift mode is active, the selected mode LED should blink continuously at approximately two blinks per second.
```

### Finding

Shift mode annunciation does not appear sufficiently explicit to support high-workload IFR tasks without additional verification by the user.

### Validation Status

```text
Shift Mode Annunciation: Gap identified
```

---

## Verification Evidence Summary

| Evidence Area | Observation |
|--------------|-------------|
| G1000 behavior | Current controller model appears generally compatible with integrated PFD/MFD workflows |
| GNS/GTN behavior | FMS2 requires independent navigator functionality rather than reduced MFD-style behavior |
| CDI behavior | CDI behavior appears more consistent in G1000 workflows than GNS/FMS2 workflows |
| Map control behavior | GTN-specific functions may be available while equivalent GNS behavior is less consistently exposed |
| FMS2 state awareness | FMS2 cursor/map/shift state annunciation requires improvement |
| MobiFlight configuration testing | Custom state and output experiments showed limitations in exposed LED/control states |

---

## Verification Conclusions

The current controller behavior appears to satisfy many expectations for integrated avionics systems.

However, independent navigator architectures require additional requirements allocation and verification because FMS2 represents a complete second navigator rather than an extension of FMS1.

The strongest verification gaps are:

1. Independent FMS2 navigator functionality
2. Shift + FMS1/FMS2 Pan/Zoom mode
3. Shift mode LED annunciation
4. FMS2 cursor/map state indication
5. Architecture-specific documentation

---

## Recommended Follow-Up Verification Activities

| Activity ID | Verification Activity | Purpose |
|------------|----------------------|---------|
| V-001 | Test Shift + FMS1 Pan/Zoom behavior | Confirm Navigator 1 map control behavior |
| V-002 | Test Shift + FMS2 Pan/Zoom behavior | Confirm Navigator 2 map control behavior |
| V-003 | Test LED blink behavior for shift mode | Confirm mode annunciation |
| V-004 | Test FMS2 CDI behavior in GNS/GTN aircraft | Confirm independent navigator parity |
| V-005 | Test behavior across G1000, GNS430/530, GTN650/750 | Confirm architecture-specific profile requirements |
| V-006 | Review profile documentation | Confirm supported behavior is clearly documented |
| V-007 | Verify exposed LED/control states through external profile tools | Confirm support for advanced user profiles |

---

## Summary

The evaluated controller implementation appears preliminarily valid for integrated avionics systems.

Independent navigator systems require additional functionality, annunciation, and documentation to fully satisfy the operational expectations of dual GNS/GTN workflows.

The primary verification finding is that controller behavior should be validated against the architecture of the avionics system being simulated rather than assuming a common FMS1/FMS2 behavior model across all avionics types.
