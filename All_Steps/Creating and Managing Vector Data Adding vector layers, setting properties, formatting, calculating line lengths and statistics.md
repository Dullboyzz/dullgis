# Practical - 1: Creating and Managing Vector Data: Adding Vector Layers, Setting Properties, Formatting, Calculating Line Lengths and Statistics

<!-- ## Practical Files:

- **[Practical File Part 1](Creating%20and%20Managing%20Vector%20Data%20%20Adding%20vector%20layers,%20setting%20properties,%20formatting(Practical_1).qgz)**: Contains vector layers and data for Part 1.
- **[Practical File Part 2](Calculating%20line%20lengths%20and%20statistics_part_2_final.qgz)**: Contains the data for calculating line lengths and statistics in Part 2. -->

---
## Part 1: Creating and Managing Vector Data

### Step 1: Create a New Shapefile Layer for Polygon Data
1. Open **QGIS**.
2. From the **Layers** menu, go to **Toolbox** → **Create Layers** → **New Shapefile Layer**.
3. Set the following parameters:
   - **File Name**: `NAME_OF_AREA` (e.g., Malad).
   - **Encoding System**: SYSTEM or UTS.
   - **Geometry Type**: POLYGON.
4. Add a new field:
   - **Name**: `MALAD`.
   - **Type**: `TEXT`.
5. Click **OK** to create the shapefile.

### Step 2: Toggle Editing and Draw Polygons
1. Click on the **Toggle Editing** button.
2. Select the **Polygon** tool and draw the polygon in the display window.
3. Right-click on the polygon to assign a name (e.g., `Malad`).
4. Click **OK**.

### Step 3: Add More Polygons
1. Draw two more polygons using the same steps as above and assign appropriate names.

### Step 4: Create a New Shapefile Layer for Road Data
1. From **Create Layers** → **New Shapefile Layer**, set:
   - **File Name**: `ROADS`.
   - **Geometry Type**: LINE.
   - **Field Name**: `ROADNAME` (type: `TEXT`).
2. Click **OK** to create the shapefile.

### Step 5: Draw Roads
1. Click on the **Toggle Editing** button.
2. Select the **Line** tool and draw roads on the display window.
3. Right-click on each road to assign a name (e.g., `ROAD 1`).

### Step 6: Add More Roads
1. Draw two to three more roads and assign appropriate names.

### Step 7: Create a New Shapefile Layer for Building Data
1. From **Create Layers** → **New Shapefile Layer**, set:
   - **File Name**: `GSC`.
   - **Geometry Type**: POINT.
   - **Field Name**: `GSC_NAME` (type: `TEXT`).
2. Click **OK** to create the shapefile.

### Step 8: Add Buildings
1. Right-click on the newly created point layer and assign a name.
2. Add two to three buildings by clicking in the display window.

---

## Part 2: Calculating Line Lengths and Statistics

### Step 1: Add Vector Layer for India’s Outline
1. Open **QGIS**.
2. Go to **Layers** → **Add Layers** → **Add Vector Layer**.
3. Click on the **Browse** button and select the shapefile:
   - **File Name**: `IND_adm0.shp` (India outline).
4. Click **Add** and then **Close**.

### Step 2: Add Rail Layer
1. Go to **Layers** → **Add Layers** → **Add Vector Layer**.
2. Select the shapefile: `IND_rails.shp` (Railways).
3. Click **Add** and then **Close**.

### Step 3: Open Attribute Table for Rail Layer
1. Right-click on `IND_rails` and select **Open Attribute Table**.
2. You will need to add a new attribute to this table.

### Step 4: Toggle Editing for Rail Layer
1. Click on the **Toggle Editing** button.

### Step 5: Add a Field for Track Length
1. Click on the **Field Calculator** button.
2. Set the following:
   - **Field Name**: `Track.len`.
   - **Field Type**: **Decimal number (real)**.
   - In the expression box, type the formula to calculate the length (convert meters to kilometers):
     ``` 
     $length / 1000
     ```
3. Click **OK** to create the field.

### Step 6: Calculate Statistics for Track Lengths
1. Go to **Vector** → **Analysis Tools** → **Basic Statistics for Fields**.
2. In the dialog box, set:
   - **Field to calculate statistics on**: `Track_len2`.
3. Click **Run** to generate the statistics.

### Step 7: Close the Statistics Tool
1. Once the statistics are generated, close the dialog box.

### Step 8: Select the HTML Report
1. Select the link to the **.html** file from the **Right bottom corner** of the dialog box.

---


## Notes:
- Ensure that you save all your work periodically.

