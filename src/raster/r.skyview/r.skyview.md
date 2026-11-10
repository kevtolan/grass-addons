## DESCRIPTION

Module *r.skyview* computes skyview factor, a relief visualization
technique (Zaksek et al. 2011). The value of each cell is given by the
portion of visible sky (from that cell) limited by the surrounding
relief. The values range from 0 to 1. The lighter the value is, the more
open the terrain is.

When flag **-o** is set, r.skyview computes openness instead of skyview
factor. Openness (based on positive openness by Yokoyama et al. 2002)
takes into account zenith angles greater than 90 degrees, while skyview
limits zenith angles to 90 degrees (celestial hemisphere). This makes
difference for example for visualization of horizontal planes and
slopes. Openness values range from 0 to 2.

## NOTES

Module
*[r.horizon](https://grass.osgeo.org/grass-stable/manuals/r.horizon.html)*
is used to compute elevation angles.

*r.horizon* does not compute horizon angles below the horizontal (it
returns 0 instead), so with *r.horizon* alone openness cannot exceed 1.
When flag **-o** is set and the addon *[r.horizon.neg](r.horizon.neg.md)*
is installed, *r.skyview* uses it instead of *r.horizon*; openness is
then greater than 1 for cells that stand above their surroundings. If
*r.horizon.neg* is not installed, *r.skyview* prints a warning and
openness is limited to 1.

The openness value is 1 minus the mean sine of the horizon angle, so it
is not an angle. To get openness as the mean zenith angle in degrees
(as in Yokoyama et al. 2002), keep the horizon maps with **basename**
and average 90 minus the horizon angle over the directions.

## EXAMPLES

We compute the skyview factor map of the North Carolina sample dataset
`elevation` map:

```sh
g.region raster=elevation
r.skyview input=elevation output=elevation_skyview ndir=8
```

![image-alt](elevation.jpg)

## SEE ALSO

*[r.horizon](https://grass.osgeo.org/grass-stable/manuals/r.horizon.html),
[r.horizon.neg](r.horizon.neg.md),
[r.relief](https://grass.osgeo.org/grass-stable/manuals/r.relief.html),
[r.shaded.pca](r.shaded.pca.md), [r.local.relief](r.local.relief.md)*

## REFERENCES

- Zaksek K, Ostir K, Kokalj Z. *Sky-View Factor as a Relief
    Visualization Technique.* Remote Sensing. 2011; 3(2):398-415.
- Yokoyama R, Shirasawa M, Pike J R. *Visualizing topography by
    Openness: A new application of image processing to digital elevation
    models.* Photogrammetric engineering and remote sensing 68.3 (2002):
    257-266.

## AUTHOR

Anna Petrasova, [NCSU GeoForAll](https://geospatial.ncsu.edu/geoforall/)
