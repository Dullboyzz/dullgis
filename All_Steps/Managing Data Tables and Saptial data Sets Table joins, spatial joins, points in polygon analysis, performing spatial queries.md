# Practical - 7: Managing Data Tables and Spatial Data Sets

**Aim**: Table Joins, Spatial Joins, Points-in-Polygon Analysis, Performing Spatial Queries

---

## Part A: Table Joins

### Step 1: Load Vector Layers
1. Go to **Layer** → **Add Layer** → **Add Vector Layer**
2. Add the following files:
   - `nybb.shp`
   - `OEM_NursingHomes_001.shp`
3. Click **Add**, then **Close**

---

### Step 2: Inspect Attribute Tables
1. Right-click on each layer → **Open Attribute Table**
2. Observe the attribute data for joining

---

### Step 3: Perform Attribute Join by Location
1. Go to **Vector** → **Data Management Tools** → **Join Attributes by Location**
2. Set:
   - **Base Layer**: `nybb [EPSG:2263]`
   - **Join Layer**: `OEM_NursingHomes_001 [EPSG:2263]`
   - **Geometric Predicate**: `Intersects`
   - **Fields to Add**: Click `[…]` → **Select All**
   - **Join Type**: `One-to-one (first matching feature)`
   - Enable: **Open output file after running algorithm**
3. Click **Run**, then **Close**

---

### Step 4: View Joined Attributes
1. Deselect the original `nybb` and `OEM` layers in the panel
2. Use the **Identify Tool (`i`)**
3. Click on the map to see new attributes from the joined table

> ✅ **Output**: Attributes from nursing homes joined to polygons for spatial analysis (e.g., earthquake-prone areas)

---

## Part B: Points-in-Polygon Analysis

### Step 1: Load Earthquake Data (CSV/TXT)
1. Go to **Layer** → **Add Layer** → **Add Delimited Text Layer**
2. File: `EarthQuakeDatabase.txt`
3. Set:
   - **Layer Name**: `Earthquake Database`
   - **Encoding**: UTF-8
   - **Custom Delimiters** → Enable
   - Check: `First record has field names` and `Detect field types`
   - **X Field**: `Longitude`, **Y Field**: `Latitude`
   - **Geometry CRS**: `EPSG:4326 - WGS 84`
4. Click **Add**, then **Close**

---

### Step 2: Load Polygon Layer
1. Go to **Layer** → **Add Layer** → **Add Vector Layer**
2. File: `ne_10m_admin_0_countries.zip`
3. Click **Add**, then **Close**

---

### Step 3: Count Points in Polygons
1. Go to **Vector** → **Analysis Tools** → **Count Points in Polygon**
2. Set:
   - **Polygon Layer**: `ne_10m_admin_0_countries`
   - **Points Layer**: `Earthquake Database [EPSG:4326]`
   - **Count Field Name**: `earthquake_count`
   - Save to: `practical_07 → earthquake_count.gpkg`
   - Enable: **Open output file after running**
3. Click **Run**, then **Close**

---

### Step 4: View Counted Data
1. Use **Identify Tool (`i`)** and click on map polygons
2. Check the **numpoint** attribute in the result panel

> ✅ **Output**: Number of earthquakes counted per country displayed on map

---

## Part C: Performing Spatial Queries

### Step 1: Load Populated Places Layer
1. Go to **Layer** → **Add Vector Layer**
2. File: `ne_10m_populated_places_simple.shp`
3. Click **Add**, then **Close**

---

### Step 2: Load Rivers and Lakes Layer
1. Go to **Layer** → **Add Vector Layer**
2. File: `ne_10m_rivers_lake_centerlines.shp`
3. Click **Add**, then **Close**

---

### Step 3: Label the Rivers Layer
1. Right-click `ne_10m_rivers_lake_centerlines.shp` → **Properties**
2. Go to **Labels** → Set:
   - **Label With**: `name`
   - Click **Apply**, then **OK**

---

### Step 4: Set CRS to 3D Globe
1. Go to **Project** → **Properties** → **CRS**
2. Set CRS: `ESRI:54032 - World Azimuthal Equidistant`
3. Click **OK**

> 🌍 Now the map appears as a 3D globe projection

---

### Step 5: Create a Buffer Around Rivers
1. Go to **Vector** → **Geoprocessing Tools** → **Buffer**
2. Set:
   - **Input Layer**: `ne_10m_rivers_lake_centerlines`
   - **Distance**: `0.020000` (approx. 2 km)
   - **Segments**: `5`
   - **End Cap Style**: Round
   - **Join Style**: Round
   - **Miter Limit**: `2.000000`
   - Output: **Temporary Layer** (don’t save to file)
   - Enable: **Open output file after running**
3. Click **Run**, then **Close**

---

### Step 6: Style Populated Places
1. Right-click `ne_10m_populated_places_simple` → **Properties**
2. Go to **Labels** → Enable **Single Labels**
3. Label with: `name`
4. Click **Apply**, then **OK**

> ✅ **Output**: Populated places are labeled and visualized alongside buffered rivers on a 3D globe

---

## Notes:
- Always check and match **CRS (Coordinate Reference System)** between layers.
- Temporary files will be lost if not saved manually.
- **Spatial joins** and **point-in-polygon** analysis are core for thematic mapping and spatial pattern identification.
- Save QGIS project frequently.
