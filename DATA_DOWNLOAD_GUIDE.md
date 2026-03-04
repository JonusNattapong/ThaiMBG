# Thailand Raster Data - Manual Download Guide

# ================================================

## WORKING DOWNLOAD LINKS (Verified)

### 1. WORLDPOP POPULATION 2020 (Thailand)

**Source:** WorldPop (University of Southampton) **URL:**
<https://hub.worldpop.org/geodata/listdata?id=64> **Direct Link:**
<https://data.worldpop.org/GIS/Population/Global_2000_2020_Constrained/2020/maxar_v1/THA/tha_ppp_2020_constrained.tif>
**File Size:** ~20-30 MB **Resolution:** 1km (30 arc-seconds)
**Steps:** 1. Visit <https://hub.worldpop.org/geodata/listdata?id=64> 2.
Select “Thailand” from country list 3. Download “Unconstrained
individual countries 2020 UN adjusted (1km resolution)”

### 2. WORLDCLIM TEMPERATURE (Annual Mean)

**Source:** WorldClim 2.1 (UC Davis) **URL:**
<https://www.worldclim.org/data/worldclim21.html> **Direct Link:**
<https://biogeo.ucdavis.edu/data/worldclim/v2.1/base/wc2.1_30s_bio.zip>
**File Size:** ~3.8 GB (full package), extract only BIO1 **Resolution:**
30 arc-seconds (~1km) **Steps:** 1. Download wc2.1_30s_bio.zip 2.
Extract wc2.1_30s_bio_1.tif (BIO1 = Annual Mean Temperature) 3. Rename
to thailand_temperature.tif

### 3. MAP TRAVEL TIME TO CITIES

**Source:** Malaria Atlas Project (Oxford University) **URL:**
<https://map.ox.ac.uk/explore-accessibility> **Dataset:** Weiss et
al. 2018 - Accessibility to cities **Resolution:** 1km **Options:** -
**Option A (R users):** Use malariaAtlas package

``` r
install.packages("malariaAtlas")
library(malariaAtlas)
access <- getRaster(surface = "Accessibility", year = 2015)
```

- **Option B (Web):** Visit <https://malariaatlas.org/geoserver/ows>
- **Option C (GEE):** Google Earth Engine

### 4. MODIS EVI (Enhanced Vegetation Index)

**Source:** NASA MODIS **Options:** - **Option A (Easiest):** Google
Earth Engine

``` javascript
var evi = ee.ImageCollection('MODIS/061/MOD13Q1')
  .select('EVI')
  .filterDate('2020-01-01', '2020-12-31')
  .mean()
  .clip(thailand_boundary);
```

- **Option B:** NASA AppEEARS
  <https://appeears.earthdatacloud.nasa.gov/>
- **Option C:** USGS Earth Explorer <https://earthexplorer.usgs.gov/>
  **Product:** MOD13Q1 (250m, 16-day composites) or MOD13A3 (1km,
  monthly)

## ALTERNATIVE: R AUTOMATED DOWNLOAD

Run this in R:

``` r
# Install packages
install.packages(c("terra", "geodata", "malariaAtlas"))

library(terra)
library(geodata)

# Download WorldPop for Thailand
pop <- population_count(year=2020, res=0.5, path="downloads/")
pop_rast <- rast(pop)
th_pop <- crop(pop_rast, ext(97, 106, 6, 21))
writeRaster(th_pop, "inst/extdata/thailand_population_2020.tif")

# Download WorldClim temperature
bio <- worldclim_global(var="bio", res=0.5, path="downloads/")
temp <- rast(bio[1])  # BIO1 = Annual mean temperature
th_temp <- crop(temp, ext(97, 106, 6, 21))
writeRaster(th_temp, "inst/extdata/thailand_temperature.tif")

# Download MAP accessibility
library(malariaAtlas)
# Use getRaster() function with Thailand boundary
```

## FILE PLACEMENT

After downloading, place files in:

    inst/extdata/
    ├── thailand_population_2020.tif
    ├── thailand_temperature.tif
    ├── thailand_access.tif
    ├── thailand_evi.tif
    └── ...

## THAILAND BOUNDING BOX (for cropping)

- Xmin (West): 97.0°
- Xmax (East): 105.5°
- Ymin (South): 6.0°
- Ymax (North): 20.5°

## CROPPING COMMAND (GDAL)

``` bash
gdal_translate -projwin 97 20.5 105.5 6 input.tif output_thailand.tif
```

## QUICK START

1.  Open browser
2.  Go to <https://hub.worldpop.org/geodata/listdata?id=64>
3.  Download Thailand 2020 population
4.  Go to <https://www.worldclim.org/data/worldclim21.html>
5.  Download bio-climate variables (wc2.1_30s_bio.zip)
6.  Extract and crop to Thailand
7.  Place in inst/extdata/
