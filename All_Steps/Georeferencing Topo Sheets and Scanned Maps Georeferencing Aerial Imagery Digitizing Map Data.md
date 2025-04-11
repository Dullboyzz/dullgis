# Practical - 6: Georeferencing and Digitizing Map Data

---

## Part A: Georeferencing Topo Sheets and Scanned Maps

### Step 1: Add Vector Layer for Reference
1. Open **QGIS**.
2. Go to **Layer** → **Add Layer** → **Add Vector Layer**.
3. Select: `Practical_6A_Georeferencing_Toposheet → IND_adm0.shp`
4. Click **Add**, then **Close**.
5. **Zoom into the Mumbai region** for reference.

---

### Step 2: Open Georeferencer
1. Go to **Raster** → **Georeferencer**.
2. **File** → **Open Raster** → `Bombay_1909.jpg`
3. Add three ground control points (GCPs):
   - Click on the original map to add each point.
   - Choose "From Map Canvas" to assign coordinates.
4. Go to **Settings** → **Transformation Settings**:
   - **Transformation Type**: Thin Plate Spline
   - **Resampling Method**: Nearest Neighbor
   - **Target SRS**: `EPSG:4044 - Everest 1830`
   - Check: **Load in QGIS when done**
5. Click **OK**, then go to **File** → **Start Georeferencing**

---

### Step 3: Finalize the Georeferencing
1. After processing, **close the Georeferencer** window.
2. When prompted, **save changes** and choose **Replace → Yes**.

---

### Step 4: Adjust Image Transparency
1. In the **Layers panel**, right-click `Bombay_1909_modified` → **Properties**.
2. Go to **Transparency** → Set **Global Opacity** to `32.0%`.
3. Click **Apply**, then **OK**.

> ✅ **Output**: Image is now properly aligned on the vector map (georeferenced).

---

## Part B: Georeferencing Aerial Imagery

### Step 1: Add OpenStreetMap Base Layer
1. Go to **Web** → **OpenLayers Plugin** → **OpenStreetMap** → Add **OpenStreetMap**

---

### Step 2: Set Project CRS
1. Go to **Project** → **Properties** → **CRS**
2. Select: `EPSG:3857 - WGS 84 / Pseudo Mercator`
3. Click **Apply**, then **OK**

---

### Step 3: Locate Area via OSM Place Search
1. Go to **View** → **Panels** → Enable **OSM Place Search**
2. Search: `Washington Square Park`
3. From the list, select the appropriate result → Click **Zoom**

---

### Step 4: Georeference the Aerial Image
1. Go to **Raster** → **Georeferencer**
2. **File** → **Open Raster** → `NewYork_Washington.jpg`
3. Add four GCPs (preferably one at each corner):
   - **Edit** → **Add Point** (click on the image)
   - Get coordinates **From Map Canvas**

4. Go to **Settings** → **Transformation Settings**:
   - **Transformation Type**: Thin Plate Spline
   - **Resampling**: Nearest Neighbor
   - **Target SRS**: `EPSG:3857 - WGS 84 / Pseudo Mercator`
   - Output File: `gateway_Aerial_Imagery_modified.tif`
   - Enable: **Load in QGIS when done**

5. Click **File** → **Start Georeferencing**
6. Once complete, **close the Georeferencer** and **save changes**

> ✅ **Output**: Aerial image correctly georeferenced on OpenStreetMap base

---

## Part C: Digitizing Map Data

### Step 1: Load Topographic Map
1. Go to **Layer** → **Add Layer** → **Add Raster Layer**
2. Select: `Practical_6C → Christchurch_topo50_map.tif`
3. Click **Add**, then **OK**

---

### Step 2: Build Raster Pyramids
1. Right-click on the raster layer → **Properties** → **Pyramids**
2. Select **all resolutions** → Click **Build Pyramids** → **OK**

---

### Step 3: Adjust Snapping Settings
1. Go to **Settings** → **Options** → **Digitizing**
2. Uncheck: **Enable snapping by default**
3. Click **OK**

---

### Step 4: Create New Spatialite Layer for Roads
1. Go to **Layer** → **Create Layer** → **New Spatialite Layer**
2. Set:
   - **Database**: `digitization.sqlite`
   - **Layer Name**: `digitized_road`
   - **Geometry Type**: `LineString`
   - **CRS**: `EPSG:4167 - NZGD2000`
3. Add Fields:
   - `name` (Text)
   - `class` (Text)
4. Click **OK**

---

### Step 5: Start Digitizing Roads
1. Click **Toggle Editing**
2. Draw the road lines over the map
3. For each road:
   - Name: `sv road`
   - Class: `street`

---

### Step 6: Style Road Layer
1. Right-click `digitized_road` → **Properties** → **Symbology**
2. Set line **color to red**
3. Click **Apply**, then **OK**

---

### Step 7: Create New Spatialite Layer for Gardens
1. Go to **Layer** → **Create Layer** → **New Spatialite Layer**
2. Set:
   - **Database**: `digitization.sqlite`
   - **Layer Name**: `digitized_garden`
   - **Geometry Type**: `Polygon`
   - **CRS**: `EPSG:4326 - WGS 84`
3. Add Field:
   - `name` (Text)

---

### Step 8: Digitize Garden Areas
1. Click **Toggle Editing**
2. Draw polygon inside the red road
3. Name entries:
   - First: `garden`
   - Second: `garden2`
4. Save edits and toggle editing off

---

## Notes:
- Make sure to use the correct **CRS** during all steps.
- Save your **Spatialite** file regularly.
- **Digitizing** allows converting raster-based maps into editable vector features.
- **Georeferencing** aligns old or unreferenced maps to real-world coordinates.
