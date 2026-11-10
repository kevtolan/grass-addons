cmake_minimum_required(VERSION 3.22)

project(r.horizon.neg)

include(build_addon)

find_M()

build_addon(
  ${PROJECT_NAME}
  GRASSLIBS
    gis
    gproj
    parson
    raster
  DEPENDS
    LIBM
  SOURCES main.c
  DOCFILES
    ${PROJECT_NAME}.html
    ${PROJECT_NAME}.md)
