## DESCRIPTION

*r.horizon.neg* is a copy of
*[r.horizon](https://grass.osgeo.org/grass-stable/manuals/r.horizon.html)*
(GRASS 8.5.0) that also returns horizon angles **below the horizontal**.
*r.horizon* reports a horizon height of 0 for any direction in which all
the terrain within reach lies below the cell; *r.horizon.neg* reports the
actual (negative) angle to the highest of that terrain instead.

Options, flags and outputs are the same as for *r.horizon*; see its
manual page for their description.

The module was written for
*[r.skyview](r.skyview.md)*, whose openness (flag **-o**) needs horizons
below the horizontal to give values above 1 for cells that stand above
their surroundings (ridges, summits, tops of structures).

## NOTES

Where the horizon is above the horizontal, the results are the same as
those of *r.horizon*, except for differences of up to 0.5 degrees:
*r.horizon* stops searching at the distance beyond which the highest
terrain in the map could rise no more than 0.5 degrees above the
horizontal. That shortcut is only valid when horizons cannot be
negative, so *r.horizon.neg* always searches up to **maxdistance** (or
to the edge of the map). Setting **maxdistance** is recommended.

Other differences from *r.horizon*:

- Cells with no data are ignored when searching for the horizon (in
  *r.horizon* they can never raise a horizon above 0, so no test is
  needed there).
- If there is no valid cell at all in a direction (at the edge of the
  map), the horizon height is 0.
- The coarse (100 x 100 cell) search grid that is used to skip terrain
  that cannot affect the horizon is tested more cautiously when the
  line of sight points below the horizontal.

The module requires GRASS 8.5 or newer.

## EXAMPLE

Horizon height maps in degrees for 16 directions, looking up to 500 m:

```sh
g.region raster=elevation
r.horizon.neg -d elevation=elevation step=22.5 maxdistance=500 output=horizon
```

## SEE ALSO

*[r.horizon](https://grass.osgeo.org/grass-stable/manuals/r.horizon.html),
[r.skyview](r.skyview.md)*

## AUTHORS

*r.horizon*: Thomas Huld, Tomas Cebecauer, Jaroslav Hofierka, Marcel
Suri (see the *r.horizon* manual page for the full list of
contributors).

Modification to return horizons below the horizontal: Kevin Tolan,
Vermont Center for Ecostudies.
