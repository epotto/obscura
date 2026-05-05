# Known Limitations & Areas for Future Research

Scientific rigor requires acknowledging the boundaries of the current model. The Phase I OBSCURA architecture is subject to the following limitations:

## Environmental Variables
* **Snow Albedo:** The current model does not dynamically adjust for winter snowpack, which acts as a massive reflector, bouncing outward-traveling urban light back up into the atmosphere and artificially expanding the radius of the light dome.
* **Atmospheric Inversions:** In mountainous valley topographies, cold air frequently pools on the valley floor, trapping high concentrations of aerosols, particulate matter, and smog. These inversion layers drastically alter the attenuation coefficient ($\alpha$) compared to standard atmospheric mixing conditions. 

## Hardware Bias
* **The Zenith Limitation:** The Unihedron SQM-L features a roughly 20-degree field of view oriented straight up (the zenith). It is possible for the sensor to report a pristine dark sky reading overhead while a massive, ecologically disruptive light dome dominates the horizon. This physical hardware limitation necessitates the transition to Phase II All-Sky Photometry.

## Spatial Superposition
* **Single-Source Assumption:** The current distance-decay model treats an urban core as a single, isolated point source. While highly accurate for isolated cities surrounded by dark sinks, this mathematics breaks down in megalopolises (e.g., the Eastern Seaboard) where light from multiple cities overlaps. Future iterations will utilize spatial convolution integrals across the entire VIIRS raster to calculate the superposition of multiple light domes.
