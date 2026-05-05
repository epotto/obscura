# Methodology: The OBSCURA Pipeline

This document outlines the standard operating procedure for executing an OBSCURA spatial light model. The pipeline relies on a three-tier approach: top-down satellite extraction, ground field data, and R-based spatial computation.

## 1. Source Data Acquisition (VIIRS)
To establish the baseline urban radiance ($I_0$), we utilize the Earth Observation Group (EOG) repository.
* **Product:** VIIRS Day/Night Band (DNB), Monthly Cloud-Free Composites (`vcmcfg`).
* **Protocol:** A 500-meter buffer is applied to a defined urban centroid coordinate. The R `terra` package is used to extract the mean radiance from the `.avg_rade9.tif` GeoTIFF, ensuring the model accounts for the total luminous output of the core before atmospheric scattering occurs.

## 2. Ground Field Protocol
To empirically determine regional atmospheric attenuation, field data is gathered via Radial Transect Networks.
* **Environmental Prerequisites:** Data collection is strictly limited to New Moon phases with 0% cloud cover to eliminate lunar interference and cloud-albedo reflection.
* **Routing:** Transects are driven outward from the urban centroid along paths of least topographic resistance to capture the natural geometric spread of the light dome.
* **Measurement:** Stops are conducted at variable intervals (1-mile spacing near the urban core, expanding to 5-mile spacing in dark-sky zones). Sky Quality Meter (SQM) readings are averaged in triplicate. Vehicle odometers are explicitly ignored in favor of exact GPS coordinate logging.

## 3. Computational Pipeline (R)
The spatial and thermodynamic mathematics are executed autonomously via R scripts.
* **Spatial Calculations:** GPS coordinates are converted to Haversine radial distance ($r$) from the centroid using the `geosphere` package.
* **Topographic Shielding:** The `elevatr` and `terra` packages generate a viewshed raster from a Digital Elevation Model (DEM), applying a binary multiplier to account for light blocked by geographic barriers (e.g., canyon walls or mesas).
* **The Thermodynamic Model:** Logarithmic SQM data is converted to linear irradiance. The `minpack.lm` package utilizes the Levenberg-Marquardt algorithm (`nlsLM`) to solve the exponential decay function, isolating the region's specific atmospheric attenuation coefficient ($\alpha$).
