# Hazard Analysis

## Purpose

This Preliminary Hazard Analysis (PHA) evaluates operational risks associated with controller abstraction and functional asymmetry between Navigator 1 (FMS1) and Navigator 2 (FMS2) when operating independent avionics architectures.

---

## Hazard Identification

| Hazard ID | Hazard Description | Potential Effect |
|------------|------------|------------|
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

Cursor mode entered but controller provides no visual indication.

#### Potential Effects

- Increased pilot workload
- Additional heads-down time
- Incorrect map manipulation
- User confusion
- Reduced mode awareness

#### Severity

Minor

#### Recommendation

Provide dedicated FMS2 cursor annunciation through LED state indication.

---

## Functional Failure Assessment

| Function | Failure Condition | Effect | Recommendation |
|------------|------------|------------|------------|
| FMS2 Cursor Mode | No annunciation | User uncertainty | Add dedicated LED state |
| FMS2 CDI | Function unavailable | Reduced operational parity | Implement CDI mapping |
| FMS2 Map Control | Limited feedback | Increased workload | Add mode indication |

---

## Hazard Severity Assessment

| Hazard ID | Description | Potential Effect | Severity |
|------------|------------|------------|------------|
| HZ-001 | Missing FMS2 cursor annunciation | Increased pilot workload | Minor |
| HZ-002 | FMS1/FMS2 functional asymmetry | Operational confusion | Major |
| HZ-003 | Incorrect architecture abstraction | Mode awareness degradation | Major |
| HZ-004 | Missing navigator parity | Reduced usability | Minor |

---

## Derived Requirements

| Requirement | Source | Observation | Status |
|------------|------------|------------|------------|
| REQ-001 | Architecture Analysis | Support Integrated and Independent modes | Open |
| REQ-002 | Operational Evaluation | FMS2 parity with FMS1 | Open |
| REQ-003 | Human Factors Review | Independent mode indication | Open |
| REQ-004 | User Testing | Cursor mode annunciation | Open |

---

## Architecture Context

| System | Architecture Type | FMS Relationship | Design Implication |
|------------|------------|------------|------------|
| Garmin G1000 | Integrated Avionics | FMS1/FMS2 share common state | FMS2 may be abstracted as an extension of FMS1 |
| Garmin GNS430/530 | Independent Navigator | FMS1/FMS2 are separate systems | FMS2 requires full operational parity |
| Garmin GTN650/750 | Independent Touch Navigator | FMS1/FMS2 are separate systems | FMS2 requires complete feature parity |

---

## Safety Observation

The observed issue is not a hardware malfunction or missing button assignment.

The observed issue is a requirements allocation mismatch between:

- Integrated avionics architectures
- Independent navigator architectures

Current controller behavior aligns with integrated avionics systems such as the Garmin G1000.

Independent navigator architectures such as dual Garmin GNS430/530 and GTN650/750 installations require independent operational state management and full navigator parity between FMS1 and FMS2.

This observation suggests that architecture-specific operational profiles may improve controller usability and reduce pilot workload.
