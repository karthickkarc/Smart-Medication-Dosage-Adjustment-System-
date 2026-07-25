Safety notes for anyone extending this
The original sketch had a live API key hardcoded in it — that's been moved
into secrets.h so it can be kept out of version control. Rotate any key
that was previously committed anywhere.
If you build on this for something closer to a real device, treat dosage
limits, confirmation logic, and failure states (lost WiFi, sensor faults,
brownout) as safety-critical and get a qualified biomedical engineer
involved — software like this should never control an actual infusion
pump without formal medical-device certification (e.g. IEC 62304).
