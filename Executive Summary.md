# Executive Summary

This repository documents an independent systems engineering and human factors assessment of compact avionics controller behavior across integrated avionics and independent navigator architectures.

The analysis began with an operational observation: controller behavior that appeared appropriate for Garmin G1000-style integrated avionics did not fully translate to dual independent navigator workflows such as Garmin GNS430/530 or GTN installations.

The assessment evaluates architecture alignment, requirements gaps, human factors concerns, preliminary hazards, root cause, validation findings, and recommended design improvements.

## Key Finding

The issue is not primarily a missing button assignment.

The issue is a requirements allocation mismatch between integrated avionics assumptions and independent navigator workflows.

## Primary Recommendation

The controller should support selectable architecture profiles:

- Integrated Avionics Mode
- Independent Navigator Mode

In Independent Navigator Mode, FMS1 and FMS2 should operate as separate navigators with functional parity.

## Highest-Priority Improvements

1. Implement Shift + FMS1 and Shift + FMS2 Pan/Zoom modes.
2. Provide blinking LED annunciation when shift mode is active.
3. Provide FMS1/FMS2 functional parity in Independent Navigator Mode.
4. Expose LED and control states to external profiles.
5. Document supported behavior by avionics architecture.

## Relevance to Systems Safety

This project demonstrates:

- Requirements analysis
- Architecture comparison
- Human factors review
- Mode awareness analysis
- Preliminary hazard analysis
- Functional Hazard Assessment-style reasoning
- Validation and verification planning
- Design recommendation development
