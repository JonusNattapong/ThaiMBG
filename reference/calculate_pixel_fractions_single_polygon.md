# Calculate fractional pixels in a polygon

Calculate the fraction of each pixel's area that falls within a single
polygon

## Usage

``` r
calculate_pixel_fractions_single_polygon(polygon, id_raster, polygon_id = NULL)
```

## Arguments

- polygon:

  [terra::SpatVector](https://rspatial.github.io/terra/reference/SpatVector-class.html)
  object of length 1. The polygon to calculate fractional areas across.

- id_raster:

  [terra::SpatRaster](https://rspatial.github.io/terra/reference/SpatRaster-class.html)
  object. ID raster created for the set of all polygons to be
  considered, created by
  [`build_id_raster()`](https://henryspatialanalysis.github.io/mbg/reference/build_id_raster.md).

- polygon_id:

  (optional). ID for this polygon. Must have length 1.

## Value

data.table containing two or three columns:

- pixel_id: unique pixel ID from the ID raster

- area_fraction: fraction of the pixel area falling within this polygon

- polygon_id (optional): If `polygon_id` was defined, it is added to the
  table

## Details

This is a helper function called by
[`build_aggregation_table()`](https://henryspatialanalysis.github.io/mbg/reference/build_aggregation_table.md).

## See also

build_aggregation_table

## Examples

``` r
if (FALSE) { # \dontrun{
  polygons <- sf::st_read(system.file('extdata/Benin_communes.gpkg', package = 'mbg'))
  id_raster <- build_id_raster(polygons)
  pixel_fractions <- calculate_pixel_fractions_single_polygon(
    polygon = polygons[1, ], id_raster
  )
  head(pixel_fractions)
} # }
```
