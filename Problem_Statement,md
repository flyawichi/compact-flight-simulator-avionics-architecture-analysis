# Problem Statement

During evaluation of the Octavi IFR-1 avionics controller, an architectural mismatch was observed between integrated avionics systems and independent navigator systems.

The IFR-1 controller maps FMS1 and FMS2 as though both represent components of a common avionics system. This aligns well with Garmin G1000 installations where FMS1 and FMS2 correspond to the PFD and MFD.

However, dual Garmin GNS430/530 installations represent two independent navigators. Each unit requires complete operational functionality, including CDI selection, cursor mode management, map control, and navigation state awareness.

Testing indicated that some functions available to FMS1 are not consistently available to FMS2, suggesting the architecture may have been optimized around integrated avionics assumptions.
