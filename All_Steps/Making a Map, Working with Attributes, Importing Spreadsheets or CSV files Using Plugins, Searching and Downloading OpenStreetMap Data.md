# Practical - 3: Making a Map, Working with Attributes, Importing Spreadsheets or CSV Files, Using Plugins, and Downloading OpenStreetMap Data

---

## Part A: Making a Thematic Map Using Print Layout

### Step 1: Add Vector Layers
1. Open **QGIS**.
2. Go to **Layer** → **Add Layer** → **Add Vector Layer**.
3. Add the following shapefiles:
   - `IND_admi.shp` (India_State_Admin)
   - `maharashtra_administrative.shp`
   - `maharashtra_coastline.shp`
   - `maharashtra_highway.shp`
   - `maharashtra_location.shp`
   - `maharashtra_natural.shp`
   - `maharashtra_poi.shp`
   - `maharashtra_water.shp`

### Step 2: Set Layer Properties
- Right-click on `IND_admi.shp` → **Properties** → **Symbology** → Set **Outline Color** to **Green**.
- Right-click on `maharashtra_poi.shp` → **Properties** → **Symbology** → Set **Point Color** to **Red**.

### Step 3: Create a New Print Layout
1. Go to **Project** → **New Print Layout** → Name: `Practical 3a` → Click **OK**.
2. In the layout window:
   - Click **Add Item** → **Add Map**
   - Drag over the canvas to insert the map
   - On the right panel, check **Lock Styles for Layers**

### Step 4: Zoom and Focus on Mumbai
- In the main QGIS window, zoom in to the **Mumbai region**
- Go back to the print layout and adjust the map display accordingly

### Step 5: Add Inset Map
- **Add another map** for inset view (overview)
- In the **Items panel**, select `Map 1` → **Properties** → **Overviews**
- Click `+`, create **Overview 1** → Set linked frame to `Map 2`

### Step 6: Format Inset Map
- Select `Map 2` → **Properties** → Under **Frame**:
  - **Color**: Black
  - **Thickness**: 0.70

### Step 7: Add Labels
- **Add Label**: `Mumbai Map`
  - Customize font, size, color, alignment
- **Add Copyright**
  - Use HTML:
    ```html
    <h2>&copy; Copyright Reserved</h2>
    <h1>Saraf College</h1>
    ```
  - Enable **Render as HTML**

### Step 8: Add Legend
1. Add **Legend**
2. In **Item Properties**:
   - Uncheck **Auto Update**
   - Rename layers (e.g., `maharashtra_water` → `Water`)
   - Use **Custom Symbol** → Change water layer to **Blue**

### Step 9: Add Scale Bar and North Arrow
- **Add Scale Bar**
  - In Item Properties → Segments → Right = 10
- **Add North Arrow**
  - Choose SVG image from properties

### Step 10: Export the Map
- Go to **Layout** → **Export as Image**
- File name: `prac_3a.jpeg`
- Resolution: **600 dpi** → Save

---

## Part B: Importing Spreadsheets or CSV Files

### Step 1: Add Delimited Text Layer
1. Go to **Layer** → **Add Layer** → **Add Delimited Text Layer**
2. File: `sample.csv` (from Practical_03 → data)
3. File Format: **Tab-separated**
4. Set:
   - **X Field**: `Longitude`
   - **Y Field**: `Latitude`
   - **Geometry CRS**: `EPSG:4326 - WGS 84`
5. Click **Add** → **Close**

---

## Part C: Using Plugins

### Step 1: Install Plugins
1. Go to **Plugins** → **Manage and Install Plugins**
2. Search and install:
   - `OSM Place Search`
   - `OpenLayers Plugin` (enable experimental plugins)

---

## Part D: Searching and Downloading OpenStreetMap Data

### Step 1: Open OSM Layer
- Go to **Web** → **OpenLayers Plugin** → **OpenStreetMap** → Add **OpenStreetMap** base map

### Step 2: Search for a Location
1. In the **OSM Place Search** panel (left side)
2. Type: `University of Mumbai`
3. From the list, select: `Bharati Vidyapeeth Deemed University Department`
4. Click **Zoom**

---

## Notes
- Save your QGIS project frequently
- Ensure all layers use a common CRS (e.g., `EPSG:4326`)
- Customize your print layout to improve map readability and aesthetics
