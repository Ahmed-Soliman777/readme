# Railway Network Data Documentation

This repository contains geospatial data for Egypt's railway infrastructure in GeoJSON format, sourced from OpenStreetMap. The data is organized into two main datasets: railway lines and railway stations.

## 📁 Data Structure

```
train/
├── railway/
│   └── export.geojson    # Railway line segments and tracks
├── stations/
│   └── export.geojson    # Railway stations and stops
└── README.md             # This file
```

## 📊 Dataset Overview

### 1. Railway Lines (`railway/export.geojson`)

**File Statistics:**
- **Total Lines:** 63,067
- **File Size:** ~1.19 MB
- **Total Features:** Multiple railway segments (exact count varies)
- **Last Updated:** 2026-01-16T19:06:45Z

**Data Source:**
- Generator: overpass-turbo
- Copyright: © OpenStreetMap contributors
- License: Open Database License (ODbL)
- Source: www.openstreetmap.org

**Feature Type:** `FeatureCollection` containing `LineString` geometries

#### Properties Description

Each railway feature contains the following properties:

| Property | Type | Description | Example Values |
|----------|------|-------------|----------------|
| `@id` | String | OpenStreetMap way identifier | `"way/7849688"` |
| `railway` | String | Type of railway infrastructure | `"rail"`, `"light_rail"`, `"subway"` |
| `electrified` | String | Whether the track is electrified | `"no"`, `"yes"`, `"contact_line"` |
| `gauge` | String | Track gauge in millimeters | `"1435"` (standard gauge) |
| `passenger_lines` | String | Number of passenger lines | `"2"`, `"1"` |
| `usage` | String | Primary usage of the track | `"main"`, `"branch"`, `"industrial"` |
| `bridge` | String | Indicates if segment is on a bridge | `"yes"` |
| `layer` | String | Vertical layering (for bridges/tunnels) | `"1"`, `"-1"` |
| `source` | String | Data source | `"GPS"`, `"Bing"`, `"survey"` |

#### Coordinate System

- **Format:** GeoJSON coordinates `[longitude, latitude]`
- **Coordinate Reference System:** WGS84 (EPSG:4326)
- **Geographic Coverage:** Egypt
- **Coordinate Range:** 
  - Longitude: ~27.3° to 32.9° E
  - Latitude: ~24.0° to 31.5° N

#### Example Feature

```json
{
  "type": "Feature",
  "properties": {
    "@id": "way/7849688",
    "electrified": "no",
    "gauge": "1435",
    "passenger_lines": "2",
    "railway": "rail",
    "usage": "main"
  },
  "geometry": {
    "type": "LineString",
    "coordinates": [
      [32.6971577, 25.1996007],
      [32.6961802, 25.1997263],
      [32.6953713, 25.1998302]
    ]
  }
}
```

### 2. Railway Stations (`stations/export.geojson`)

**File Statistics:**
- **Total Lines:** 7,814
- **File Size:** ~188 KB
- **Total Features:** Multiple station points (exact count varies)
- **Last Updated:** 2026-01-16T19:14:50Z

**Data Source:**
- Generator: overpass-turbo
- Copyright: © OpenStreetMap contributors
- License: Open Database License (ODbL)
- Source: www.openstreetmap.org

**Feature Type:** `FeatureCollection` containing `Point` geometries

#### Properties Description

Each station feature contains the following properties:

| Property | Type | Description | Example Values |
|----------|------|-------------|----------------|
| `@id` | String | OpenStreetMap node identifier | `"node/269662884"` |
| `name` | String | Station name (usually in Arabic) | `"الحضرة"`, `"محطة رمسيس"` |
| `name:ar` | String | Arabic name | `"محطة رمسيس"` |
| `name:en` | String | English name | `"Ramses Station"`, `"Al-Hadra"` |
| `name:de` | String | German name (if available) | `"Ramses-Bahnhof"` |
| `name:fr` | String | French name (if available) | `"Station Ramsès"` |
| `railway` | String | Type of railway facility | `"station"`, `"halt"`, `"stop"` |
| `public_transport` | String | Public transport type | `"station"`, `"stop_position"` |
| `train` | String | Indicates train service availability | `"yes"` |
| `operator` | String | Operating company | `"سكك حديد مصر"` (Egyptian Railways) |
| `station` | String | Station classification | `"train"` |
| `wikidata` | String | Wikidata identifier | `"Q633754"` |
| `wikipedia` | String | Wikipedia article reference | `"ar:محطة مصر (القاهرة)"` |
| `int_name` | String | International/transliterated name | `"Aswān, Aswan"` |
| `alt_name` | String | Alternative name | `"محطة مصر"` |
| `monorail` | String | Indicates monorail station | `"yes"` |
| `level` | String | Station level/floor | `"2"` |

#### Coordinate System

- **Format:** GeoJSON coordinates `[longitude, latitude]`
- **Coordinate Reference System:** WGS84 (EPSG:4326)
- **Geographic Coverage:** Egypt
- **Coordinate Range:**
  - Longitude: ~27.3° to 32.9° E
  - Latitude: ~24.0° to 31.5° N

#### Example Feature

```json
{
  "type": "Feature",
  "properties": {
    "@id": "node/271864421",
    "alt_name": "محطة مصر",
    "alt_name:en": "Misr Station",
    "name": "محطة رمسيس",
    "name:ar": "محطة رمسيس",
    "name:en": "Ramses Station",
    "operator": "سكك حديد مصر",
    "public_transport": "station",
    "railway": "station",
    "train": "yes",
    "wikidata": "Q633754"
  },
  "geometry": {
    "type": "Point",
    "coordinates": [31.2460533, 30.0629785]
  },
  "id": "node/271864421"
}
```

## 🗺️ Major Stations Included

The dataset includes major Egyptian railway stations such as:

- **Ramses Station** (محطة رمسيس) - Cairo's main railway station
- **Alexandria stations:** Al-Hadra, Sidi Beshr, Abu Qir
- **Upper Egypt:** Aswan, Luxor, Qena, Asyut
- **Delta region:** Kafr El-Dauwar, Tanta, Zagazig
- **And many more regional stations**

## 📏 Technical Specifications

### Railway Gauge
- **Standard Gauge:** 1435mm (4 ft 8½ in) - predominant across the network
- Matches international standard gauge used in Europe and North America

### Electrification Status
- Most lines in the dataset show `"electrified": "no"`
- Some modernized segments may have electrification

### Track Configuration
- Single and double track configurations
- Passenger lines typically have 1-2 dedicated tracks

## 🔧 Usage Examples

### Loading Data in Python (GeoPandas)

```python
import geopandas as gpd

# Load railway lines
railway_lines = gpd.read_file('railway/export.geojson')
print(f"Total railway segments: {len(railway_lines)}")

# Load stations
stations = gpd.read_file('stations/export.geojson')
print(f"Total stations: {len(stations)}")

# Filter stations with English names
stations_en = stations[stations['name:en'].notna()]
print(f"Stations with English names: {len(stations_en)}")
```

### Loading Data in JavaScript

```javascript
// Using fetch API
fetch('railway/export.geojson')
  .then(response => response.json())
  .then(data => {
    console.log('Railway features:', data.features.length);
    // Process railway data
  });

fetch('stations/export.geojson')
  .then(response => response.json())
  .then(data => {
    console.log('Station features:', data.features.length);
    // Process station data
  });
```

### Filtering Examples

**Find all electrified railway segments:**
```python
electrified = railway_lines[railway_lines['electrified'] == 'yes']
```

**Find all stations with public transport integration:**
```python
pt_stations = stations[stations['public_transport'] == 'station']
```

**Get stations in Cairo area (approximate bounding box):**
```python
cairo_bbox = stations.cx[31.0:31.5, 29.8:30.3]
```

## 📊 Data Quality Notes

### Completeness
- Data sourced from OpenStreetMap, community-maintained
- Coverage is comprehensive for major lines and stations
- Some rural or less-used lines may have limited detail

### Multilingual Support
- Station names available in multiple languages (Arabic, English, French, German)
- Arabic is the primary language
- Not all stations have translations in all languages

### Accuracy
- Coordinates are based on GPS surveys and satellite imagery
- Railway line geometry represents approximate centerline
- Station points represent approximate station locations

### Missing Data
- Some properties may be `null` or missing for certain features
- Not all stations have operator information
- Some historical or proposed lines may be included

## 🔄 Data Updates

- **Current Timestamp (Railway):** 2026-01-16T19:06:45Z
- **Current Timestamp (Stations):** 2026-01-16T19:14:50Z
- Data can be updated from OpenStreetMap using Overpass Turbo API

### Updating from OpenStreetMap

To update the data, use Overpass Turbo queries similar to:

**For Railway Lines:**
```
[out:json][timeout:25];
area["name:en"="Egypt"]->.searchArea;
(
  way["railway"="rail"](area.searchArea);
);
out geom;
```

**For Stations:**
```
[out:json][timeout:25];
area["name:en"="Egypt"]->.searchArea;
(
  node["railway"="station"](area.searchArea);
);
out body;
```

## 📖 Additional Resources

- **OpenStreetMap Egypt:** https://www.openstreetmap.org/relation/1473947
- **Overpass Turbo:** https://overpass-turbo.eu/
- **OSM Wiki - Railway:** https://wiki.openstreetmap.org/wiki/Railways
- **GeoJSON Specification:** https://geojson.org/

## ⚖️ License

This data is made available under the **Open Database License (ODbL)** by OpenStreetMap contributors.

**Attribution Required:** © OpenStreetMap contributors

When using this data, you must:
1. Attribute OpenStreetMap and its contributors
2. If you alter or build upon the data, distribute the result under the same license
3. Keep the data open

Full license: https://opendatacommons.org/licenses/odbl/

## 📞 Contact & Contributions

For data corrections or improvements, please contribute directly to OpenStreetMap:
- Visit www.openstreetmap.org
- Create an account and start editing
- Follow the railway tagging guidelines

---

**Last Updated:** January 16, 2026
**Data Version:** Based on OSM snapshot from 2026-01-16
