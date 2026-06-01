# Hazard Analysis
## Preliminary Hazard Analysis

Hazard ID	  |Hazard Description	                                  |Effect
|---------|----------|----------|
HZ-001	    |FMS2 cursor mode not annunciated	                    |Pilot uncertainty
HZ-002	    |FMS1/FMS2 functional asymmetry	                      |Increased workload
HZ-003	    |Incorrect architecture abstraction	                  |Mode confusion
HZ-004	    |Missing navigator parity	                            |Reduced situational awareness


Hazard:
Pilot assumes FMS2 has entered cursor mode.

Condition:
Cursor mode entered but controller provides no indication.

Potential Effects:

- Increased workload
- Additional heads-down time
- Incorrect map manipulation
- User confusion

| Function | Failure Condition | Effect | Recommendation |
|------------|------------|------------|------------|
| FMS2 Cursor Mode | No annunciation | User uncertainty | Add dedicated LED state |
| FMS2 CDI | Function unavailable | Reduced operational parity | Implement CDI mapping |
| FMS2 Map Control | Limited feedback | Increased workload | Add mode indication |


| Hazard ID | Description | Potential Effect | Severity |
|------------|------------|------------|------------|
| HZ-001 | Missing FMS2 cursor annunciation | Increased pilot workload | Minor |
| HZ-002 | FMS1/FMS2 functional asymmetry | Operational confusion | Major |
| HZ-003 | Incorrect architecture abstraction | Mode awareness degradation | Major |
| HZ-004 | Missing navigator parity | Reduced usability | Minor |


| Requirement | Source | Observation | Status |
|------------|------------|------------|------------|
| REQ-001 | Architecture Analysis | Support Integrated and Independent modes | Open |
| REQ-002 | Operational Evaluation | FMS2 parity with FMS1 | Open |
| REQ-003 | Human Factors Review | Independent mode indication | Open |
| REQ-004 | User Testing | Cursor mode annunciation | Open |


| Function | Failure Condition | Effect | Recommendation |
|------------|------------|------------|------------|
| FMS2 Cursor Mode | No annunciation | User uncertainty | Add dedicated LED state |
| FMS2 CDI | Function unavailable | Reduced operational parity | Implement CDI mapping |
| FMS2 Map Control | Limited feedback | Increased workload | Add mode indication |


| System | Architecture Type | FMS Relationship | Design Implication |
|----------|----------|----------|----------|
| Garmin G1000 | Integrated Avionics | FMS1/FMS2 share common state | FMS2 may be abstracted as an extension of FMS1 |
| Garmin GNS430/530 | Independent Navigator | FMS1/FMS2 are separate systems | FMS2 requires full operational parity |
| Garmin GTN650/750 | Independent Touch Navigator | FMS1/FMS2 are separate systems | FMS2 requires complete feature parity |
