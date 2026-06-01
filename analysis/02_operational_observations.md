Operational Model
   GTN #1                     GTN #2
   (FMS1)                     (FMS2)

 Independent System      Independent System
Controller Design Implication

FMS2 requires complete operational parity with FMS1.

Any function available on Navigator 1 should be available on Navigator 2 unless restricted by the actual avionics manufacturer.

Observed Result

GTN support currently exceeds equivalent GNS support, suggesting architecture-specific implementation rather than a generalized navigator abstraction.

Systems Engineering Observation

The root issue is not a missing button mapping.

The root issue is a requirements allocation mismatch between:

Integrated Avionics Architecture

and

Independent Navigator Architecture

The current control abstraction appears optimized for integrated avionics systems such as the G1000.

Independent navigator installations require a different control philosophy because FMS1 and FMS2 represent separate operational systems rather than separate interfaces to a common system.

