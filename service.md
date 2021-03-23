# QGIS free online class

## 001- Add Web Map Service using QGIS

การใช้งาน Web Map Service เพื่อนำเข้าข้อมูลภาพถ่ายทางอากาศและภาพถ่ายจากดาวเทียมด้วยโปรแกรม QGIS  

#### 1. Web Map Service (WMS)
```
http://change2.gistda.or.th/geoserver/wms?version=1.3.0

https://sos-s03.gistda.or.th/geoserver/SDS/wms?version=1.3.0
```

#### 2. Web Map Tile Service (WMTS)
```
https://gistdaportal.gistda.or.th/data/rest/services/L02_base/mo_Thailand_GISTDA_2m/ImageServer/WMTS?
```
#### 2. Web Map Tile Service (WMTS) -> longdo maps
```
http://ms.longdo.com/mapproxy/wmts/1.0.0/WMTSCapabilities.xml
```
#### 3. ArcGIS Map Server
```
http://eis.ldd.go.th/ArcGIS/rest/services/LDD_RASTER_WM_CACHE/MapServer
```

#### 4. XYZ Tile Server
```
OpenStreetMap:
http://tile.openstreetmap.org/{z}/{x}/{y}.png

Google Maps:
https://mt1.google.com/vt/lyrs=r&x={x}&y={y}&z={z}

Google Satellite:
https://mt1.google.com/vt/lyrs=s&x={x}&y={y}&z={z}

Google Hybrid:
https://mt1.google.com/vt/lyrs=y&x={x}&y={y}&z={z}

Google Terrain:
https://mt1.google.com/vt/lyrs=p&x={x}&y={y}&z={z}
```
#### 5. Add XYZ Tile Server with Python Console
```python
"""
This script should be run from the Python consol inside QGIS.
It adds online sources to the QGIS Browser.

Sources from
http://eis.ldd.go.th
https://gistdaportal.gistda.or.th
https://www.openstreetmap.org
https://www.google.co.th/maps
https://www.bing.com/maps

Script by MAPEDIA
https://github.com/mapedia-th/qgis-free-online/blob/master/qgis3_basemaps.py
Note: [sourcetype, title, authconfig, password, referer, url, username, zmax, zmin]
"""


# Sources
sources = []
sources.append(["connections-xyz","LDD Orthophoto 2545", "", "", "", "http://eis.ldd.go.th/ArcGIS/rest/services/LDD_RASTER_WM_CACHE/MapServer/tile/%7Bz%7D/%7By%7D/%7Bx%7D", "", "17", "0"])
sources.append(["connections-xyz","L02_base_mo_Thailand_GISTDA_2m", "", "", "", "https://gistdaportal.gistda.or.th/data/rest/services/L02_base/mo_Thailand_GISTDA_2m/ImageServer/tile/%7Bz%7D/%7By%7D/%7Bx%7D", "", "23", "0"])
sources.append(["connections-xyz","LDD Landuse", "", "", "", "http://eis.ldd.go.th/ArcGIS/rest/services/LDD_LU_WM_CACHE/MapServer/tile/%7Bz%7D/%7By%7D/%7Bx%7D", "", "19", "0"])
sources.append(["connections-xyz","Bing VirtualEarth", "", "", "", "http://ecn.t3.tiles.virtualearth.net/tiles/a{q}.jpeg?g=1", "", "19", "1"])
sources.append(["connections-xyz","Google Maps","","","","https://mt1.google.com/vt/lyrs=m&x=%7Bx%7D&y=%7By%7D&z=%7Bz%7D","","19","0"])
sources.append(["connections-xyz","Google Satellite", "", "", "", "https://mt1.google.com/vt/lyrs=s&x=%7Bx%7D&y=%7By%7D&z=%7Bz%7D", "", "19", "0"])
sources.append(["connections-xyz","Google Terrain Hybrid", "", "", "", "https://mt1.google.com/vt/lyrs=p&x=%7Bx%7D&y=%7By%7D&z=%7Bz%7D", "", "19", "0"])
sources.append(["connections-xyz","Google Satellite Hybrid", "", "", "", "https://mt1.google.com/vt/lyrs=y&x=%7Bx%7D&y=%7By%7D&z=%7Bz%7D", "", "19", "0"])
sources.append(["connections-xyz","OpenStreetMap Standard", "", "", "OpenStreetMap contributors, CC-BY-SA", "http://tile.openstreetmap.org/%7Bz%7D/%7Bx%7D/%7By%7D.png", "", "19", "0"])

# Add sources to browser
for source in sources:
   connectionType = source[0]
   connectionName = source[1]
   QSettings().setValue("qgis/%s/%s/authcfg" % (connectionType, connectionName), source[2])
   QSettings().setValue("qgis/%s/%s/password" % (connectionType, connectionName), source[3])
   QSettings().setValue("qgis/%s/%s/referer" % (connectionType, connectionName), source[4])
   QSettings().setValue("qgis/%s/%s/url" % (connectionType, connectionName), source[5])
   QSettings().setValue("qgis/%s/%s/username" % (connectionType, connectionName), source[6])
   QSettings().setValue("qgis/%s/%s/zmax" % (connectionType, connectionName), source[7])
   QSettings().setValue("qgis/%s/%s/zmin" % (connectionType, connectionName), source[8])

# Update GUI
iface.reloadConnections()
```
