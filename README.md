# EUDR Deforestation Risk Map — Northern Argentina

Interactive geospatial risk assessment tool for EU Deforestation Regulation (EUDR) compliance in Argentina's Gran Chaco region.



---

## Overview

The **EU Deforestation Regulation (Reg. 2023/1115)** requires that commodities placed on the EU market — including soy, corn, and cattle — have not contributed to deforestation after **December 31, 2020**. For Argentine agribusiness operators leasing land in northern provinces, this creates direct operational risk: any lot with post-2020 deforestation activity may trigger compliance failures at the export stage.

This project builds a **department-level EUDR deforestation risk index** for the four highest-risk provinces in Argentina's Gran Chaco:

- **Chaco**
- **Santiago del Estero**
- **Salta**
- **Formosa**

The output is an interactive HTML map that allows operators to identify which departments carry elevated EUDR exposure **before signing new land-lease contracts**.

---

## Use Case

> *"Which departments in northern Argentina should we flag before expanding our lease portfolio?"*

This tool answers that question directly — not as an ESG reporting exercise, but as an **operational due diligence instrument** for agribusiness companies with supply chain exposure to European buyers.

---

## Data Sources

| Source | Description |
|---|---|
| **UMSEF-MAyDS** | Unidad de Manejo del Sistema de Evaluación Forestal — deforestation figures (has.) by department, post-2020 |
| **IGN Argentina** (georef API) | Official department boundaries — `apis.datos.gob.ar/georef` |
| **EUDR Reg. 2023/1115** | EU regulatory framework defining the December 2020 deforestation cutoff |

---

## Risk Scoring Methodology

Each department is assigned a risk score based on the percentage of its total surface area deforested after December 2020:

| Score | Label | Threshold |
|---|---|---|
| 3 | 🔴 Alto (High) | > 3% of surface area |
| 2 | 🟠 Medio (Medium) | 1–3% |
| 1 | 🟢 Bajo (Low) | < 1% |
| 0 | ⬜ Sin datos | No data available |

---

## Tech Stack

- **Python 3** (Google Colab)
- `geopandas` — spatial join between deforestation data and official department polygons
- `folium` — interactive HTML map with tooltips and legend
- `pandas` — data processing and risk scoring
- IGN georef API — live download of official Argentine department boundaries

---

## Repository Structure

```
eudr-deforestation-risk-map/
├── Georreferenciacion.ipynb     # Full pipeline — run in Google Colab
├── riesgo_eudr_norte_argentina.html  # Output: interactive map
└── README.md
```

---

## How to Run

1. Open `Georreferenciacion.ipynb` in [Google Colab](https://colab.research.google.com/)
2. Run Cell 1 to install dependencies (`geopandas`, `folium`, `mapclassify`)
3. Run Cells 2–5 sequentially
4. Cell 6 downloads the final HTML map to your machine

No API keys required. No local installation needed.

---

## Output

The final deliverable is a self-contained HTML file (`riesgo_eudr_norte_argentina.html`) that:

- Renders department polygons colored by EUDR risk level
- Shows interactive tooltips with deforested hectares and % surface affected on hover
- Includes a legend and title overlay
- Works offline in any browser — no server required

---

## Context & Limitations

- Deforestation figures are based on UMSEF public reports (2021–2023). For production use, this pipeline should be validated against **MapBiomas Argentina** vegetation loss layers and **OTBN** (Ordenamiento Territorial de Bosques Nativos) categories under Ley 26.331.
- The risk index is at the **department level** — lot-level compliance requires polygon intersection with parcel coordinates, which is the next step in the pipeline.
- This project is a proof-of-concept entry point for a full per-lot EUDR compliance report service.

---

## Author

**Mariano Romero**  
Political Scientist| Buenos Aires, Argentina  
Master's in Energy Economics & Regulation — CEARE, UBA Facultad de Derecho  
[LinkedIn](https://www.linkedin.com/in/marianoromero23)
