# Architecture Comparison

## Garmin G1000

Architecture Type:
Integrated Avionics System

Characteristics:
- Shared flight management system
- Shared navigation database
- Shared cursor state
- Shared map state
- FMS1 and FMS2 operate as interface extensions

Implication:
A controller may safely abstract FMS2 as an extension of FMS1.


## Garmin GNS430/530

Architecture Type:
Independent Navigator System

Characteristics:
- Independent flight management systems
- Independent cursor states
- Independent navigation databases
- Independent map states

Implication:
FMS2 must provide full navigator functionality independent of FMS1.


## Garmin GTN650/750

Architecture Type:
Independent Touch Navigator

Characteristics:
- Self-contained flight management computer
- Independent cursor and map state
- Independent procedure management

Implication:
FMS2 must provide complete operational parity with FMS1.
