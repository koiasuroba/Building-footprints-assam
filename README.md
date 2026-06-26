# Building-footprints-assam
Per-district building footprints for the state of Assam, India — extracted from Overture Maps (Google Open Buildings, Microsoft, OpenStreetMap), separated by source, and clipped to official district boundaries. Includes the full Python / JupyterLab extraction workflow.
# Building Footprints — Assam, India

Per-district building footprint layers for all administrative districts of the state of Assam, north-eastern India, extracted from open building datasets and made freely available for research, disaster risk management, and urban planning purposes.

---

## About This Project

Building footprints — the two-dimensional outlines of individual buildings — are a foundational geospatial dataset for urban planning, population estimation, infrastructure assessment, and disaster risk management.

This project extracts, separates, and clips building footprints for every district of Assam from **Overture Maps**, a conflated open dataset that combines three major sources:

- 🟦 **Google Open Buildings** — AI-derived footprints from Google satellite imagery
- 🟩 **Microsoft Global ML Building Footprints** — machine-learning-derived footprints
- 🟧 **OpenStreetMap (OSM)** — crowd-sourced, volunteer-mapped buildings

Each footprint is tagged by its originating source, and all layers are clipped to official district boundaries.

The workflow was first developed and validated on **Morigaon** and **Sivasagar** districts, then scaled to the remaining districts of Assam.

---

## Repository Contents
Building-footprints-assam/

├── notebooks/

│   └── extraction_workflow.ipynb   # Full Python extraction and processing workflow

├── data/

│   ├── morigaon/                   # Footprints clipped to Morigaon district

│   ├── sivasagar/                  # Footprints clipped to Sivasagar district

│   └── .../                        # Remaining districts

├── README.md

└── LICENSE

---

## Data Sources

| Source | Type | Coverage in Assam |
|---|---|---|
| Google Open Buildings | AI / ML | High |
| Microsoft ML Buildings | AI / ML | Moderate |
| OpenStreetMap | Crowd-sourced | Sparse in rural areas |

Footprints are downloaded via the **Overture Maps CLI**, which conflates all three sources into a single deduplicated dataset with a `sources` field for every feature.

Boundary data: official **ASDMA district shapefiles** (Morigaon, Sivasagar) and **geoBoundaries gbOpen ADM2** boundaries for remaining districts.

---

## Tools & Software

All extraction and processing was carried out in **Python 3** within **JupyterLab** (Anaconda distribution on Windows). Accuracy assessment was performed in **ArcGIS**.

**Key Python libraries:**

| Library | Purpose |
|---|---|
| `geopandas` / `shapely` | Reading, reprojecting, clipping, and writing vector data |
| `overturemaps` (CLI) | Downloading Overture Maps footprints by bounding box |
| `requests` | Retrieving district boundaries from the geoBoundaries API |
| `pandas` / `numpy` | Tabulation and bounding-box tiling |

---

## Methodology (Summary)

The workflow consisted of six stages:

1. **Assemble district boundaries** — from ASDMA shapefiles and geoBoundaries API
2. **Select Overture Maps** as the conflated footprint source
3. **Download footprints by bounding box** and split by originating source (Google / Microsoft / OSM)
4. **Clip each source layer** to the exact district polygon
5. **Tile large districts** to manage memory during processing
6. **Assess coverage** — compare Microsoft vs. Google footprint counts per district

For full step-by-step details, refer to the notebook in `notebooks/`.

---

## How to Use

```bash
# Install dependencies
pip install geopandas osmnx mercantile overturemaps requests shapely pandas

# Run the notebook
jupyter lab notebooks/Untitled6.ipynb
```

To use the pre-extracted footprint files directly, open any `.gpkg` file in **QGIS**, **ArcGIS**, or load it with geopandas:

```python
import geopandas as gpd
gdf = gpd.read_file("data/morigaon/morigaon_google.gpkg")
print(gdf.head())
```

---

## Potential Uses

- 🌊 Flood exposure and risk assessment
- 🏘️ Settlement mapping and population estimation
- 🗺️ Urban morphology and land use analysis
- 🚨 Disaster preparedness and emergency response
- 📊 Coverage comparison of open building datasets in northeast India

---

## Attribution & License

This project is released under the **MIT License** for the code and workflow.

The underlying building footprint data is derived from:
- **Overture Maps Foundation** — https://overturemaps.org
- **Google Open Buildings** — licensed under CC BY 4.0
- **Microsoft Global ML Building Footprints** — licensed under ODbL
- **OpenStreetMap contributors** — licensed under ODbL

> Please credit these sources if you use or build upon this data.

---

## Author

koiasuroba
Internship Project — Flood Impact Assessment & Geospatial Analysis, Assam
June 2026

---

## Feedback & Contributions

If you find errors, missing districts, or want to contribute improvements, feel free to open an **Issue** or submit a **Pull Request**. This data is shared freely — the more people who use and improve it, the better.
