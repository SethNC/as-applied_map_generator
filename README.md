# as-applied_map_generator
The As-Applied Map Generator is a HTML/JS web application designed for precision agriculture drone (UAV) operators. Its purpose is to visualize spray application data from drone flight logs as a colored “as-applied” map.


# UAV As-Applied Map Generator

UAV As-Applied Map tool for visualizing drone agricultural applications. [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) [![Leaflet](https://img.shields.io/badge/Powered%20by-Leaflet-blue)](https://leafletjs.com/) [![PapaParse](https://img.shields.io/badge/CSV-PapaParse-orange)](https://www.papaparse.com/)

**web-based interactive tool** for rendering as-applied maps from UAV flight logs. Polygons are color-coded by application rate on satellite imagery or custom tiles. Ideal for precision ag analysis and reporting.

This tool processes CSV flight data to calculate rates (gal/ac or lbs/ac), overlays mission boundaries, and generates stats like total applied, area, average rate, and %CV. Exports include GeoJSON for GIS integration and PDF reports. Pair with tools like QGIS for deeper analysis or drone software for mission planning.

## Summary of work flow
- Upload flight log CSVs (auto-detect spray/broadcast).
- Optional: Load mission KML/GeoJSON as red overlay.
- Set rate scale and colors.
- Render map and view stats.
- Export GeoJSON/PDF.

## 🌟 Features
- **CSV Processing**: Auto-detects work type from `work type` column; calculates rates from `discharge rate(ml/min)`.
- **Interactive Map**: Leaflet with Esri World Imagery (toggle custom XYZ tiles); color-coded swath polygons.
- **Mission Overlay**: KML/GeoJSON as medium-thick red lines.
- **Statistics**: Total applied, area (acres), average rate, %CV (coefficient of variation).
- **Exports**: GeoJSON (swaths), PDF (report with map & summary).
- **Dynamic Legend**: Color ramp with min/max rates.

## 🚀 Quick Start
Download `dgt.html` and open in a modern browser (Chrome/Firefox recommended).

**Demo Data**  
- Use sample CSVs below to test.  
- Zoom to North Carolina (default view: 35.2, -79.9).  

**Sample CSV** (spray example):
```
latitude,longitude,speed(m/s),flight UTC time,work type,discharge rate(ml/min)
35.123,-79.456,2.5,2023-01-01T12:00:00Z,spray,100.0
35.124,-79.457,2.6,2023-01-01T12:00:01Z,spray,105.0
```

## 📸 Screenshots
![Map View](screenshots/map.png)  
![Controls](screenshots/controls.png)  

> *Example: Spray mission with rate-colored swaths (red=low, blue=high), stats panel, and red mission overlay*

## 🛠️ How to Use
1. **Upload CSVs**: One file auto-added; click "+ Add File" for multiples. Set swath width (ft).
2. **Optional Mission**: Upload KML/GeoJSON for red line overlay.
3. **Configure**: Set min/max rates, color ramp; toggle custom tiles if needed.
4. Click **Render Map**.
5. View summary stats; download GeoJSON/PDF.

> 💡 **Pro Tip**: Ensure CSV headers match exactly (case-sensitive). For broadcast, use "broadcast" in `work type` and grams/min in discharge column. Use Google Maps for lat/lon verification.

## 📂 Output Files
| File | Description |
|------|-------------|
| `as_applied_YYYY-MM-DD.geojson` | Swath polygons with rates, flows, areas (for QGIS/ArcGIS) |
| `as_applied_report_YYYY-MM-DD.pdf` | Full report: stats, map screenshot, mission/as-applied details |

## 🗺️ Custom Base Maps
Enter XYZ tile URL (e.g., drone orthomosaics). Supports `{z}/{x}/{y}` or `{z}/{y}/{x}`. Toggle checkbox to switch from Esri default. Generate tiles in QGIS: Processing Toolbox > Raster > Generate XYZ Tiles.

## 🧠 Design Philosophy: *Do One Thing Well*
This tool follows the **Unix philosophy** — *programs that do one thing and do it well*. Focused on rapid as-applied visualization from flight logs, with GIS-ready outputs for precision ag workflows.

> **Learn more**: [“The Art of Unix Programming” by Eric S. Raymond](http://www.catb.org/esr/writings/taoup/html/ch01s06.html) – Chapter on modularity and transparency
