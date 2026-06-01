# Architecture Comparison

## Garmin G1000
### Architecture Type

Integrated Avionics System

### System Description

The Garmin G1000 consists of a Primary Flight Display (PFD) and Multi-Function Display (MFD) operating as components of a common avionics suite. Both displays share a common navigation architecture and exchange information through an integrated flight management system.

### Characteristics
Shared flight management functionality
Shared navigation database
Shared map state
Shared cursor state
Shared flight plan management
Shared CDI source management
PFD and MFD operate as logical display interfaces to a common avionics system
Operational Model
          
          Shared Avionics Core
                   |
      +------------+------------+
      |                         |
      PFD (FMS1)               MFD (FMS2)

### Controller Design Implication

A hardware controller may reasonably abstract FMS2 as an extension of FMS1 because both interfaces ultimately manipulate a common system state.

### Observed Result

The Octavi IFR-1 architecture aligns well with this model and exhibits expected behavior.

## Garmin GNS430/530
Architecture Type

Independent Navigator System

## System Description

Dual GNS430/530 installations consist of two independent navigation computers. Each unit maintains its own navigation state, cursor state, flight plan management, and operational workflow.

### Characteristics
Independent flight management systems
Independent cursor states
Independent navigation databases
Independent map states
Independent flight plans
Independent procedure selection
Independent pilot interaction workflows

###Operational Model
               
               |                              |
          GNS430/530 #1                  GNS430/530 #2
             (FMS1)                         (FMS2)
          Independent System            Independent System

### Controller Design Implication

FMS2 cannot be treated as a reduced-function extension of FMS1.

The controller must provide:

Independent cursor control
Independent map manipulation
Independent CDI management
Independent workflow support
Independent annunciation
Observed Result

Certain FMS2 functions available on FMS1 are not currently exposed, creating a functional asymmetry between Navigator 1 and Navigator 2.

## Garmin GTN650/750
Architecture Type

Independent Touch Navigator

### System Description

GTN-series navigators function as independent flight management computers. Each unit provides complete navigation and procedure management capability independent of other installed navigators.

### Characteristics
Self-contained flight management computer
Independent cursor state
Independent map state
Independent flight planning capability
Independent procedure management
Independent navigation source selection
