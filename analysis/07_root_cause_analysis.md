Problem

FMS2 functionality differs between avionics architectures.

Observed Symptoms

- Missing CDI support
- Missing cursor annunciation
- Missing map mode indication

Root Cause

Controller abstraction assumes shared-system architecture.

Contributing Factors

- G1000-centric implementation
- Navigator independence not modeled
- Limited state feedback
