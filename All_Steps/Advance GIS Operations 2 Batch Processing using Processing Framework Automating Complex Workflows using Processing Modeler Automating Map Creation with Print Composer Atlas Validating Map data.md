# Practical No: 9  
**Aim:** Advanced GIS Operations 2  
**Topics:**  
- Batch Processing using Processing Framework  
- Automating Complex Workflows using Processing Modeler  
- Automating Map Creation with Print Composer Atlas  

---

## A) Batch Processing using Processing Framework

**Definition:**  
Batch processing allows you to execute a single GIS tool on multiple layers with different inputs, automating repetitive tasks.

### **Objective:**  
Clip multiple global vector layers (e.g., airports, ports, railroads) to the extent of Africa.

---

### **Steps:**

**Step I:**  
- **Layer** → **Add Layer** → **Add Vector Layer**  
- File: `ne_10m_admin_0_countries.shp` → **Add** → **Close**

**Step II:**  
- **Vector** → **Geoprocessing Tools** → **Dissolve**  
- Input Layer: `ne_10m_admin_0_countries`  
- Dissolve Field: `Continent` (✓ Checked)  
- Output: `continent.shp` → **Run** → **Close**

**Step III:**  
- Use the **Selection Tool** to select **Africa** from the `continent` layer

**Step IV:**  
- Right-click → **Export** → **Save Selected Features As**  
- Format: `ESRI Shapefile`  
- File Name: `Africa.shp`  
- CRS: `EPSG:4326 - WGS 84`  
- (✓) Save only selected features → **OK**

**Step V:**  
- Deselect previous layers, keep only `Africa.shp`

**Step VI:**  
- **Processing Toolbox** → **Vector Overlay** → **Clip**  
- Right-click → **Execute as Batch Process**  
- Input Layers:
  - `ne_10m_airports.shp`
  - `ne_10m_ports.shp`
  - `ne_10m_railroads.shp`  
- Overlay Layer (for all): `Africa.shp`  
- Clipped Layers: save as → `clipped_shp`  
- (✓) Load layers on completion → **OK**

**Step VII:**  
- Deselect Africa layer  
- Zoom in to verify clipped layers

✅ **Output:**  
Three layers (airports, ports, railroads) clipped to the African continent.

---

## B) Automating Complex Workflows using Processing Modeler

**Goal:**  
- Filter raster  
- Convert to vector  
- Extract class = 12

---

### **Steps:**

**Step I:**  
- **Processing** → **Graphical Modeler**  
- Add Input: `Raster Layer`  
- Description: `Input` (✓ Mandatory)

**Step II:**  
- Algorithms → **Majority/Minority Filter**  
- Type: `Majority`  
- Grid: Model Input  
- Kernel Type: `Square`, Radius: `1` → **OK**

**Step III:**  
- Algorithms → **Polygonize (Raster to Vector)**  
- Input Layer: Previous Output  
- Band: 1, Field Name: `IN`, 8-connectedness: `No` → **OK**

**Step IV:**  
- Algorithms → **Extract by Attribute**  
- Input Layer: Polygonized Output  
- Attribute: `DN`, Operator: `=`, Value: `12`  
- Output Layer: `Vectorized_class` → **OK**

**Step V:**  
- Model Properties:  
  - Name: `vectorized`, Group: `raster`

**Step VI:**  
- **Model** → **Save Model** → Save as: `vectorize.model3`

**Step VII:**  
- Load Raster: `LC_hd_global_2001.tif` → **Add** → **Close**

**Step VIII:**  
- **Processing** → **Toolbox** → **Models → raster → vectorized**  
- Input: `LC_hd_global_2001.tif` → **Run**

**Step IX:**  
- Right-click on model → **Edit Model**

**Step X:**  
- Add **Input → String**  
- Parameter Name: `class`, Value: `12`, (✓) Mandatory → **OK**

**Step XI:**  
- In `Extract by Attribute`:  
  - Value → Link to `Model Input (class)` → **OK**

**Step XII:**  
- Save and **Run** Model

**Step XIII:**  
- Try with `Class = 16`, Input: `LC_hd_global_2001.tif` → **Run**

**Step XIV:**  
- Add: `LC_hd_global_2012.tif` → Run model with `Class = 12`

**Step XV:**  
- Deselect unnecessary layers

✅ **Output:**  
Vectorized polygons of selected landcover class created using an automated model.

---

## C) Automating Map Creation with Print Composer Atlas

(*This section isn't explicitly included in the prompt, but typically part of such practicals. Let me know if you want this part filled in too.*)

---

## ✅ Final Outputs

1. Africa-specific vector layers clipped using **batch processing**  
2. Reusable **automated model** for vectorizing raster based on class values  
3. Time-efficient GIS workflows, reducing repetitive tasks  
