# Known Limitations & Areas for Future Research

Scientific rigor requires acknowledging the boundaries of the current model. The Phase I OBSCURA architecture is subject to the following limitations:

## 1. Environmental Variables
* **Snow Albedo:** The current model does not dynamically adjust for winter snowpack, which acts as a massive reflector, bouncing outward-traveling urban light back up into the atmosphere and artificially expanding the radius of the light dome.
* **Atmospheric Inversions:** In mountainous valley topographies, cold air frequently pools on the valley floor, trapping high concentrations of particulate matter and smog. These inversion layers drastically alter the attenuation coefficient ($\alpha$) compared to standard atmospheric mixing conditions. 
* **Aerosol Optical Depth (AOD) & Wildfire Smoke:** The model calculates a single $\alpha$ for the night of observation. However, in regions like the American West, localized dust and transient wildfire smoke can drastically alter atmospheric scattering geometries from one week to the next, requiring multiple temporal datasets to establish a true regional baseline. This is especially relevent for the region since it is common practice for farmers in the region to burn their fields to sow nutrients into the soil.

## 2. Hardware Bias & Spectral Mismatch
* **The Zenith Limitation:** The Unihedron SQM-L features a roughly 20-degree field of view oriented straight up (the zenith). It is possible for the sensor to report a pristine dark sky reading overhead while a massive, ecologically disruptive light dome dominates the horizon. 
* **Near-Infrared (NIR) Mismatch:** The VIIRS Day/Night Band (DNB) has a broad spectral sensitivity range (500–900 nm), meaning it detects Near-Infrared emissions from urban landscapes. The SQM, however, utilizes an infrared-blocking filter. Consequently, VIIRS may report a high baseline radiance ($I_0$) that the SQM mathematically cannot detect, artificially skewing the distance-decay relationship in cities with high NIR outputs.

## 3. Spectral Physics (The LED Transition)
* **Wavelength-Dependent Scattering:** The current distance-decay model assumes a uniform scattering of light. However, Rayleigh scattering is highly dependent on wavelength ($1/\lambda^4$). As cities transition from warm High-Pressure Sodium (HPS) streetlights to blue-rich, high-kelvin White LEDs, the light scatters much more aggressively in the atmosphere. The model currently tracks total luminance rather than isolating wavelength-specific attenuation.

## 4. Operational & Spatial Assumptions
* **Intra-Night Temporal Decay:** The model uses a single extracted $I_0$ baseline from satellite data. However, during a 2-hour field transect drive, urban luminous output actively decreases as businesses close, traffic diminishes, and municipal lighting curfews engage. A measurement taken at 2:00 AM is tracking a dimmer light dome than a measurement taken at 10:00 PM on the same route.
* **Single-Source Superposition Limits:** The current iteration treats an urban core as a single, isolated point source. While highly accurate for isolated cities surrounded by dark sinks, this mathematics breaks down in megalopolises where light from multiple cities overlaps.
