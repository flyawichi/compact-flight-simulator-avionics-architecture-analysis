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

### Architecture Type

Independent Touch Navigator

### Installation Context

GTN-series units are typically installed as standalone GPS/NAV/COM navigators rather than as integrated PFD/MFD display pairs.

A GTN750 or GTN650 may be installed as a single primary navigator, or it may be paired with another GTN, GNS, or NAV/COM unit depending on the aircraft configuration.

Unlike a G1000 installation, the GTN does not normally provide a PFD/MFD split where FMS1 and FMS2 represent two displays within a shared avionics suite.

Standby flight instrumentation is typically provided through conventional six-pack instruments, electronic standby instruments, or other backup flight instruments separate from the GTN navigator.

### Characteristics

- Self-contained flight management and navigation computer
- Independent map state
- Independent procedure management
- Touchscreen-based interaction model
- May be installed as a single unit or paired with another independent navigator
- Does not operate as a PFD/MFD display pair like a G1000 system

### Controller Design Implication

The GTN should be treated as an independent navigator, not as part of an integrated PFD/MFD avionics suite.

If a second navigator is installed, FMS2 should represent that second independent navigator and should provide complete operational parity with FMS1 where supported by the aircraft and avionics package.

If only one GTN is installed, FMS2 may have no corresponding second navigator function unless the aircraft provides another supported navigation unit.

### Observed Result

GTN-specific control events may operate correctly when the GTN package exposes those events, but this does not imply that the same event model applies to GNS430/530 or G1000 systems.

This reinforces the need for architecture-specific controller profiles rather than a single generic FMS1/FMS2 abstraction.
