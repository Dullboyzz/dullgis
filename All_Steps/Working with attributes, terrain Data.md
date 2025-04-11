# Practical - 4: Working with Terrain Data

---

## Part A: Working with Attributes

### Step 1: Load the Vector Layer
1. Open **QGIS**.
2. Go to **Layer** → **Add Layer** → **Add Vector Layer**.
3. Select: `Practical_04 → A → ne10m_populated_places_Simple.zip`
4. Click **Add**, then **Close**.

### Step 2: Filter by Population Attribute
1. Right-click on the layer `ne_10m_populated_places_Simple` → **Open Attribute Table**.
2. Locate the column **pop_max**.
3. Click the first value under `pop_max`, then:
   - Click **Select Features Using an Expression**.
   - In the Expression Dialog, type:
     ```sql
     pop_max > 100 AND pop_max < 1000
     ```
   - Click **Select Features** → **Close** the expression window and attribute table.

---

## Part B: Terrain Data & Hillshade Analysis (Geographical Surface)

### **Overview:**
- **Terrain data** (TIN-based or raster) represents geographical surfaces (e.g., elevation).
- **Hillshade** visually enhances topography by simulating light and shadow.

---

## Part B Steps:

### Step 1: Load Elevation Raster Layer
1. Go to **Layer** → **Add Layer** → **Add Raster Layer**.
2. Select: `Practical_04_Data → GMTED 2010N10E060_300 → 10n060e20101117_gmted-mea300.tif`
3. Click **Add**, then **Close**.

> 🔎 Dark regions = lower elevation, Light regions = higher elevation.

---

### Step 2: Set Coordinates to Mt. Everest
1. Set the center of the view to:
   - **Longitude**: `86.92`
   - **Latitude**: `27.98`
2. Set **Scale** to: `1:900000`
3. Set **Magnifier** to: `100%`

---

### Step 3: Clip Raster to Mt. Everest Region
1. Go to **Raster** → **Extraction** → **Clip Raster by Extent**.
2. Set:
   - **Input Layer**: `10n060e20101117_gmted-mea300.tif`
   - **CRS**: `EPSG:4326`
   - **Clipping Extent**: Use **Canvas Extent**
   - **Output File**: `clippedhimalaya.tif`
3. Click **Run**, then **Close**.

---

### Step 4: Generate Contours from Clipped Raster
1. Uncheck the original raster layer (`10n060e...mea300.tif`).
2. Go to **Raster** → **Extraction** → **Contour**.
3. Set:
   - **Input Layer**: `clippedhimalaya.tif`
   - **Interval**: `100.000000`
   - **Output File**: `contourhimalaya.gpkg`
4. Click **Run**, then **Close**.

---

### Step 5: Label Elevation Contours
1. Right-click on `contourhimalaya` → **Properties**.
2. Go to **Labels** → Enable **Single Labels**.
3. Set:
   - **Value**: `ELEV`
   - **Color**: `Red`
4. Click **Apply**, then **OK**.

---

### Step 6: Generate Hillshade
1. Go to **Raster** → **Analysis** → **Hillshade**.
2. Set:
   - **Input Layer**: `clippedhimalaya.tif`
   - **Output File**: `hillshade.tif`
3. Click **Run**, then **Close**.

---

## Notes:
- Always ensure your raster and vector layers share a **common CRS** (e.g., `EPSG:4326`).
- Save your QGIS project regularly.
- Hillshades help in visual interpretation of elevation data and terrain forms.
