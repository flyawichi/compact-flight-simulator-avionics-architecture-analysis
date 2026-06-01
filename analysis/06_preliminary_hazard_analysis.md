# Hazard Analysis

## Purpose

This Preliminary Hazard Analysis (PHA) evaluates potential operational risks associated with controller abstraction and functional asymmetry between Navigator 1 (FMS1) and Navigator 2 (FMS2) when operating independent avionics architectures.

The objective is not to perform a formal aircraft safety assessment, but rather to identify potential operator impacts resulting from controller design assumptions and architecture-specific behavior.

---

## Hazard Identification

| Hazard ID | Hazard Description | Potential Effect |
|-----------|-------------------|------------------|
| HZ-001 | FMS2 cursor mode not annunciated | Pilot uncertainty |
| HZ-002 | FMS1/FMS2 functional asymmetry | Increased workload |
| HZ-003 | Incorrect architecture abstraction | Mode confusion |
| HZ-004 | Missing navigator parity | Reduced situational awareness |

---

## Detailed Hazard Assessment

### HZ-001 – Missing FMS2 Cursor Annunciation

#### Hazard

Pilot assumes FMS2 has entered cursor mode.

#### Condition

Cursor mode has been entered on Navigator 2, but the controller provides no dedicated visual indication.

#### Potential Effects

- Increased pilot workload
- Additional heads-down time
- Incorrect map manipulation
- User confusion
- Reduced mode awareness

#### Recommendation

Provide dedicated FMS2 cursor annunciation through controller LED state indication.

---

### HZ-002 – Functional Asymmetry Between FMS1 and FMS2

#### Hazard

Equivalent navigator functions are not available across both installed navigators.

#### Condition

Controller behavior assumes a shared-system architecture while operating independent navigator systems.

#### Potential Effects

- Increased task complexity
- Reduced workflow consistency
- Additional training burden
- User expectation mismatch

#### Recommendation

Provide architecture-aware operational profiles that support independent navigator implementations.

---

## Functional Failure Assessment

| Function | Failure Condition | Effect | Recommendation |
|----------|------------------|---------|----------------|
| FMS2 Cursor Mode | No annunciation | User uncertainty | Add dedicated LED state |
| FMS2 CDI | Function unavailable | Reduced operational parity | Implement CDI mapping |
| FMS2 Map Control | Limited feedback | Increased workload | Add mode indication |

---

## Preliminary Operational Impact Assessment

| Hazard ID | Description | Potential Impact |
|-----------|-------------|------------------|
| HZ-001 | Missing FMS2 cursor annunciation | Increased pilot workload |
| HZ-002 | FMS1/FMS2 functional asymmetry | Operational inconsistency |
| HZ-003 | Incorrect architecture abstraction | Reduced mode awareness |
| HZ-004 | Missing navigator parity | Reduced usability |

---

## Safety Observation

The observed issue is not a hardware malfunction or missing button assignment.

The observed issue is a requirements allocation mismatch between:

- Integrated avionics architectures
- Independent navigator architectures

Current controller behavior aligns well with integrated avionics systems such as the Garmin G1000.

Independent navigator architectures such as dual Garmin GNS430/530 and GTN650/750 installations require independent operational state management and full navigator parity between FMS1 and FMS2.

This observation suggests that architecture-specific operational profiles may improve controller usability, reduce pilot workload, and improve mode awareness.

---

## Conclusions

The identified hazards do not represent unsafe aircraft operation.

The observed issues are associated with controller abstraction and operator interaction rather than aircraft navigation performance.

The primary finding is that integrated avionics architectures and independent navigator architectures impose different operational requirements on controller design.

Future controller implementations should consider architecture-aware operational profiles to ensure consistent functionality and mode awareness across supported avionics platforms.

---

## Key Finding

The observed behavior is not a hardware defect.

The observed behavior is a systems engineering issue resulting from differing assumptions regarding:

1. Integrated Avionics Architectures
2. Independent Navigator Architectures

This study demonstrates that controller requirements should be derived from the operational architecture of the target avionics system rather than assumed common functionality across all navigator implementations.
