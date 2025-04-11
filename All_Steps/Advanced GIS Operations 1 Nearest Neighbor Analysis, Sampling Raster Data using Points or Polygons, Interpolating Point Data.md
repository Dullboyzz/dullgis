# Practical No. 8  
**Aim:** Advanced GIS Operations 1:  
Nearest Neighbor Analysis, Sampling Raster Data using Points or Polygons, Interpolating Point Data  

---

## A) Nearest Neighbor Analysis

### Step I: Add Populated Places Layer  
- **Layer** → **Add Layer** → **Add Vector Layer**  
- File: `ne_10m_populated_places_simple.shp` → **Add** → **Close**

### Step II: Add Earthquake Data (TSV)  
- **Layer** → **Add Layer** → **Add Delimited Text Layer**  
- File: `earthquakes_2021_11_25_14_31_59_+0530.tsv`  
- Encoding: `UTF-8`  
- Format: **Custom Delimiters** (Tab)  
- **X Field**: Longitude | **Y Field**: Latitude  
- CRS: `EPSG:4326 - WGS 84` → **Add** → **Close**

### Step III: Style Layers  
- Change color via **Symbology**

### Step IV: Clean the Data  
- Right-click on earthquake layer → **Open Attribute Table**  
- Remove null geometries:  
  - **Processing** → **Toolbox** → **Vector Geometry** → **Remove Null Geometries**  
  - Input: `earthquakes_2021_11_25...`  
  - Check: Remove empty geometries → **Run** → **Close**

### Step V: Style Cleaned Layer  
- Deselect original earthquake layer  
- Right-click on cleaned layer → **Symbology** → Color: Green  
- Check attribute table → ensure valid latitude and longitude

### Step VI: Nearest Hub Analysis  
- **Processing** → **Toolbox** → **Vector Analysis** → **Distance to Nearest Hub (Line to Hub)**  
- Source Points: `Cleaned Earthquake Layer`  
- Destination: `ne_10m_populated_places_simple`  
- Hub Layer Attribute: `name`  
- Measurement Unit: `Kilometer`  
- Output: `earthquake_city.gpkg` → Save → **Run** → **Close**

### Step VII: View Output  
- Right-click on `earthquake_city` → **Open Attribute Table**  
- Check: `Hub_Name`, `HubDist` columns  
- Visual: Green dots (earthquakes), Red dots (cities), connecting lines

> ✅ **Output**: Distance to nearest populated place visualized with connecting lines

---

## B) Sampling Raster Data using Points & Polygons

### Step I: Load Raster Layer  
- **Layer** → **Add Raster Layer**  
- File: `us.tmax_nohads-II-20140525-float.tif`

### Step II: Coordinate Check  
- Click on **[i] Identify Tool** → Move cursor to check coordinates

### Step III: Add Point Layer (Gazetteer)  
- **Layer** → **Add Delimited Text Layer**  
- File: `2018-Gaz_ua_national`  
- Encoding: `UTF-8`  
- Delimiter: Tab  
- X: Longitude | Y: Latitude  
- CRS: `EPSG:4326 - WGS 84` → **Add** → **Close**

### Step IV: Sample Raster Values  
- **Processing** → **Toolbox** → **Raster Analysis** → **Sample Raster Values**  
- Input Layer: `2018-Gaz_ua_national`  
- Raster: `us.tmax_nohads...`  
- Output Column Prefix: `tmax_`  
- Enable: **Open output file after running** → **Run** → **Close**

### Step V: View Results  
- Use **[i] Identify Tool** → Check tmax values  
- Open attribute table → Confirm `tmax_` column added

> ✅ **Output**: Temperature values sampled at point locations

---

### Part 2: Zonal Statistics using Polygons

### Step I: Load County Layer  
- **Layer** → **Add Vector Layer** → `tl_2018_us_country.shp`  
- **Processing** → **Toolbox** → **Raster Analysis** → **Zonal Statistics**  
  - Input Layer: `tl_2018_us_country`  
  - Raster: `us_tmax_nohads-II-20140525-float.tif`  
  - Band: 1 (Gray)  
  - Output Prefix: `tmax_`  
  - Statistics: **Mean**  
  - Enable: **Open output after run** → **Run** → **Close**

### Step II: View Attribute Table  
- Use **[i] Identify Tool** → Check for `tmax_mean` field  
- Right-click → **Open Attribute Table**

### Step III: Style Layer  
- Right-click → **Properties** → **Symbology** → **Graduated**  
  - Column: `tmax_mean`  
  - Color: Purple  
  - Click **Classify** → **Apply** → **OK**

> ✅ **Output**: Mean raster values calculated and visualized per polygon

---

## C) Interpolating Point Data

### Step I: Add Soundings Layer  
- **Layer** → **Add Vector Layer** → `Arlington_Soundings_2007_stp183.shp` → **Add** → **Close**

### Step II: Add Boundary Layer  
- File: `Boundary2004_550_stp183.shp` → **Add** → **Close**

### Step III: Hide Boundary Layer  
- Deselect in layer panel  
- Zoom in to see soundings (dotted lines)

### Step IV: Identify Features  
- Use **Identify Tool** to click on individual points  
- Zoom out using **Pan Tool** to restore full view

### Step V: Add Islands Layer  
- Add vector layer: `Islands_2004_550_stp183.shp`

### Step VI: Interpolate (TIN)  
- **Processing** → **Toolbox** → **TIN Interpolation**  
  - Vector Layers:
    - `Arlington_Soundings` → **Points**  
    - `Islands_2004` → **Break Lines**
  - Method: **Linear**
  - Extent: **Calculate from Boundary Layer**
  - Pixel Size: X = 5, Y = 5
  - Output File: `elevation_tin.tif`  
  - Enable: **Open output file** → **Run** → **Close**

### Step VII: Clip Raster by Boundary  
- **Processing** → **Toolbox** → **GDAL → Raster Extraction → Clip Raster by Mask Layer**  
  - Input: `elevation_tin.tif`  
  - Mask: `Boundary2004_550_stp183`  
  - Output: `elevation_tin_clipped.tif` → **Run** → **Close**

### Step VIII: Style Raster  
- Keep only `elevation_tin_clipped` visible  
- Right-click → **Properties** → **Symbology**  
  - Render Type: `Singleband Pseudocolor`  
  - Min: `501.84`, Max: `550`  
  - Color Ramp: **Inverted**  
  - Interpolation: `Linear`  
  - Click **Classify** → **OK**

### Step IX: Generate Contours  
- **Processing** → **GDAL → Raster Extraction → Contour**  
  - Input: `elevation_tin_clipped`  
  - Interval: `5.000000`  
  - Attribute: `ELEV`  
  - Output: `Contour.gpkg` → **Run** → **Close**

### Step X: Style Contours  
- Right-click → **Properties** → **Labels**  
  - Enable: **Single Labels**  
  - Label with: `ELEV`  
  - Placement: **Curved**, Distance: `0.0000`  
  - Repeat: **No Repeat** → **Apply** → **OK**

> ✅ **Output**: Elevation map and contours interpolated from lake sounding points

---

## 🔚 End of Practical 8
