# Data Dictionary

The night sky is a collection of particles influenced by many compounding variables, some of which can be predicted, some of which cannot.

To ensure cross-compatibility and prevent unit-conversion errors, all variables within the OBSCURA pipeline must adhere to the following standards.

| Variable Name | Description | Units | Data Type | Source / Calculation |
| :--- | :--- | :--- | :--- | :--- |
| `category` | Classification of the measurement (e.g., Transect Route, Baseline) | Text | Character | Field Data |
| `location` | Specific name or geographic descriptor of the stop | Text | Character | Field Data |
| `greenhouse` | Presence of nearby commercial greenhouse lighting | Binary (1=Yes, 0=No) | Integer | Field Observation |
| `stadium_light` | Presence of nearby high-intensity stadium lighting | Binary (1=Yes, 0=No) | Integer | Field Observation |
| `latitude` | GPS Latitude of the sensor location | Decimal Degrees | Numeric (Float) | GPS Device |
| `longitude` | GPS Longitude of the sensor location | Decimal Degrees | Numeric (Float) | GPS Device |
| `sqm_1` | First Sky Quality Meter reading | mag/arcsec$^2$ | Numeric (Float) | Unihedron SQM-L |
| `sqm_2` | Second Sky Quality Meter reading | mag/arcsec$^2$ | Numeric (Float) | Unihedron SQM-L |
| `sqm_avg` | Averaged field reading used for computation | mag/arcsec$^2$ | Numeric (Float) | Calculated: Mean(`sqm_1`, `sqm_2`) |
| `datetime_local` | Combined date and time of reading | YYYY-MM-DD HH:MM:SS | Datetime | Field Data |
| `moon_cycle` | Lunar illumination percentage (Ideally 0%) | Percentage | Numeric (Float) | Astronomical Data |
| `elevation` | Altitude of the sensor location | Meters | Numeric (Float) | GPS Device / DEM |
| `cloud_cover` | Estimated percentage of cloud cover (Ideally 0%) | Percentage | Numeric (Integer) | Field Observation |
| `weather_conditions`| General atmospheric description (e.g., clear, hazy, windy) | Text | Character | Field Observation |
| `field_notes` | Open text field for anomalies (e.g., passing cars, animal activity) | Text | Character | Field Notes |
| `Irradiance` | Linear sky brightness | Relative | Numeric (Float) | Calculated: $10^{-0.4 \times sqm\_avg}$ |
| `I_0` | Baseline urban emission | $nW \cdot cm^{-2} \cdot sr^{-1}$ | Numeric (Float) | VIIRS EOG `vcmcfg` extraction |
| `distance_km` | Haversine radial distance from urban centroid | Kilometers | Numeric (Float) | R `geosphere` (`distHaversine`) |
| `alpha` | Atmospheric attenuation coefficient | $km^{-1}$ | Numeric (Float) | Derived via `nlsLM` regression |
| `Viewshed` | Topographic visibility multiplier | Binary (1 or 0) | Integer | R `terra` / `elevatr` analysis |
| `I_base` | Natural dark sky floor (asymptote) | Relative | Numeric (Float) | Derived via `nlsLM` regression |
