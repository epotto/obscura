# Data Dictionary

To ensure cross-compatibility and prevent unit-conversion errors, all variables within the OBSCURA pipeline must adhere to the following standards.

| Variable Name | Description | Units | Data Type | Source / Calculation |
| :--- | :--- | :--- | :--- | :--- |
| `SQM` | Sky Quality Meter reading | mag/arcsec$^{2}$ | Numeric (Float) | Field Data (Unihedron SQM-L) |
| `Irradiance` | Linear sky brightness | Relative | Numeric (Float) | Calculated: $10^{-0.4 \times SQM}$ |
| `I_0` | Baseline urban emission | $nW \cdot cm^{-2} \cdot sr^{-1}$ | Numeric (Float) | VIIRS EOG `vcmcfg` extraction |
| `distance_km` | Haversine radial distance | Kilometers | Numeric (Float) | R `geosphere` (`distHaversine`) |
| `alpha` ($\alpha$) | Atmospheric attenuation | $km^{-1}$ | Numeric (Float) | Derived via `nlsLM` regression |
| `Viewshed` | Topographic visibility | Binary (1 or 0) | Integer | R `terra` / `elevatr` analysis |
| `I_base` | Natural dark sky floor | Relative | Numeric (Float) | Derived via `nlsLM` regression |
