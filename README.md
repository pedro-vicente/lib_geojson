# geojson
a C++ geoJSON parser. GeoJSON is a format for encoding a variety of geographic data structures.


[![Build status](https://ci.appveyor.com/api/projects/status/wuivv12v10r2i4sw?svg=true)](https://ci.appveyor.com/project/pedro-vicente/lib-geojson)



## geoJSON specification

http://geojson.org/

JSON parsing is done with gason

https://github.com/vivkin/gason

## Usage

One argument, geoJSON file

```
./parser <geojon file>
```


## C++ usage

Storage is done into a list of features

```c++
std::vector<feature_t> m_feature;
```

A feature is a list geometries, and a geometry is a list of polygons.

```c++
geojson_t geojson;
if (geojson.convert(argv[1]) < 0)
{
  return 1;
}
size_t size_features = geojson.m_feature.size();
for (size_t idx_fet = 0; idx_fet < size_features; idx_fet++)
{
  feature_t feature = geojson.m_feature.at(idx_fet);
  size_t size_geometry = feature.m_geometry.size();
  for (size_t idx_geo = 0; idx_geo < size_geometry; idx_geo++)
  {
    geometry_t geometry = feature.m_geometry.at(idx_geo);
    size_t size_pol = geometry.m_polygons.size();
    for (size_t idx_pol = 0; idx_pol < size_pol; idx_pol++)
    {
      polygon_t polygon = geometry.m_polygons[idx_pol];
      size_t size_crd = polygon.m_coord.size();
      if (size_crd == 0)
      {
        continue;
      }
      std::vector<double> lat;
      std::vector<double> lon;
      for (size_t idx_crd = 0; idx_crd < size_crd; idx_crd++)
      {
        lat.push_back(polygon.m_coord[idx_crd].m_lat);
        lon.push_back(polygon.m_coord[idx_crd].m_lon);
      }
      if (geometry.m_type.compare("Point") == 0)
      {
      }
      else if (geometry.m_type.compare("Polygon") == 0 ||
        geometry.m_type.compare("MultiPolygon") == 0)
      {
      }
    }
  }
}
```

## Sample geoJSON file



```
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {
        "name": "name 1",
        "marker-color": "#0000ff"
      },
      "geometry": {
        "type": "Point",
        "coordinates": [
          -77.12911152370515,
          38.79930767201779
        ]
      }
    },
    {
      "type": "Feature",
      "properties": {
        "name": "name 2",
        "marker-color": "#0000ff"
      },
      "geometry": {
        "type": "Point",
        "coordinates": [
          -77.16797018042666,
          38.766521892689916
        ]
      }
    }
  ]
}
```

## Rendering

Render by WxWidgets GUI library

https://github.com/pedro-vicente/render_geojson

![image](https://user-images.githubusercontent.com/6119070/41935976-a4eb5530-7959-11e8-9f51-5a7e0be79197.png)

Render by Wt web framewwork, Leaflet branch

https://github.com/pedro-vicente/wt

![image](https://user-images.githubusercontent.com/6119070/41950762-ae7f33aa-7995-11e8-85a7-661c3630d5c8.png)