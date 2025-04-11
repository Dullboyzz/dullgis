# Practical - 2: Exploring and Managing Raster Data: Adding Raster Layers, Raster Styling and Analysis, Raster Mosaicking, and Clipping

---

## Part (A): Adding Raster Layer

### Step 1: Add the First Raster Layer
1. Go to **Layer** → **Add Layers** → **Add Raster Layer**.
2. Click **Browse** and select:
   - **File**: `gl_gpwv3_pdens_90_ascii_one` → `glds90ag60.asc`.
3. Click **Add** and then **Close**.

### Step 2: Add the Second Raster Layer
1. Go to **Layer** → **Add Layers** → **Add Raster Layer**.
2. Click **Browse** and select:
   - **File**: `gl_gpwv3_pdens_00_ascii_one` → `glds00ag60.asc`.
3. Click **Add** and then **Close**.

---

## Part (B): Raster Styling

### Example: Finding the Largest Population Change (1990 to 2000)
#### Step 1: Convert to Color Format
1. Right-click on `glds90ag60` → **Properties**.
2. Under **Render type**, select **Singleband pseudocolor**.
   - **Min**: `0`, **Max**: `240`, **Mode**: `Continuous`.
3. Click **Classify**, then **Apply** and **OK**.

#### Step 2: Apply Styling to the Second Layer
1. Right-click on `glds00ag60` → **Properties**.
2. Under **Render type**, select **Singleband pseudocolor**.
   - **Min**: `0`, **Max**: `240`, **Mode**: `Continuous`.
3. Click **Classify**, then **Apply** and **OK**.

---

## Part (C): Raster Calculation for Population Difference

### Step 1: Use the Raster Calculator
1. Go to **Raster** → **Raster Calculator**.
2. In the **Output layer** field, name the new layer `Population Difference`.
3. Set the **Output format** to **GeoTIFF**.
4. Click on **[…]** to save the layer as `C:\GIS\pract2\Population_Difference`.

### Step 2: Perform the Calculation
1. Select the first layer `glds00gs60@1` and subtract the second layer `glds90gs60@1`.
2. In the **Raster Calculator Expression**, type: `glds00ag60@1 - glds90ag60@1`
3. Set the **Output CRS** to **Project CRS: EPSG: 4326 - WGS84** and click **OK**.

### Step 3: Apply Styling to the Population Difference Layer
1. Right-click on `Population Difference` → **Properties**.
2. Under **Render type**, select **Singleband pseudocolor**.
- **Min**: `-20,000`, **Max**: `6,000`.
- Set **Interpolation** to **Discrete**.
- Choose a **Color Ramp** and adjust **Color Labels** using **Shift**.
3. Click **Apply** and then **OK**.

### Step 4: Verify Classification
1. Click on the **i** icon in the menu to verify the classification.

---

## Part (D): Raster Mosaicking and Clipping

### Step 1: Add the Raster Layers for Mosaicking
1. Go to **Layer** → **Add Layers** → **Add Raster Layers**.
2. Click **Browse** and select the following files:
- `FAS_India1.2018349.terra.367.2km`
- `FAS_India2.2018349.terra.367.2km`
- `FAS_India3.2018349.terra.367.2km`
- `FAS_India4.2018349.terra.367.2km`
3. Click **Open**, **Add**, and then **Close**.

### Step 2: Merge the Raster Layers
1. Go to **Raster** → **Miscellaneous** → **Merge**.
2. In the dialog box, select **Select All** for the input layers.
3. Click **Run**, then **Close**.

### Step 3: Deselect All Layers
1. In the Layers panel, uncheck all layers.
2. Select only the **Merged** layer.

### Step 4: Add the Vector Layer for Clipping
1. Go to **Layer** → **Add Layers** → **Add Vector Layer**.
2. Browse and select the shapefile: `INDadm0.shp` from the `pract02` folder.
3. Click **Add** and then **Close**.

### Step 5: Set Symbology for the Admin Boundary Layer
1. Double-click on the `IND_adm0` layer.
2. In the **Symbology** tab, set **Outline** to **Blue**.
3. Click **Apply** and then **OK**.

### Step 6: Clip the Raster Layer Using the Admin Boundary
1. Go to **Raster** → **Extraction** → **Clip Raster by Mask Layer**.
2. In the dialog box, set:
- **Input layer**: `MERGED (EPSG:4326)`
- **Mask layer**: `IND_adm0 (EPSG:4326)`
3. Click **Run**, then **Close**.

---

## Notes:
- Ensure to save your work periodically.
