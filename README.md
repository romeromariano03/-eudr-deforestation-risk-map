# Mapa de Riesgo de Deforestación EUDR — Norte de Argentina
Trabajo en curso.

Herramienta geoespacial interactiva de evaluación de riesgo para el cumplimiento del Reglamento de Deforestación de la UE (EUDR) en la región del Gran Chaco argentino.

---

## Descripción General

El **Reglamento de Deforestación de la UE (Reg. 2023/1115)** exige que los productos comercializados en el mercado europeo —incluyendo soja, maíz y carne vacuna— no hayan contribuido a la deforestación posterior al **31 de diciembre de 2020**. Para los operadores agroindustriales argentinos que arriendan tierras en las provincias del norte, esto genera un riesgo operativo directo: cualquier lote con actividad de deforestación posterior a 2020 puede provocar fallas de cumplimiento al momento de la exportación.

Este proyecto construye un **índice de riesgo de deforestación EUDR a nivel departamental** para las cuatro provincias de mayor riesgo del Gran Chaco argentino:

- **Chaco**
- **Santiago del Estero**
- **Salta**
- **Formosa**

El resultado es un mapa HTML interactivo que permite a los operadores identificar qué departamentos presentan una exposición EUDR elevada **antes de firmar nuevos contratos de arrendamiento**.

---

## Caso de Uso

> *"¿Qué departamentos del norte argentino deberíamos señalar antes de expandir nuestra cartera de arrendamientos?"*

Esta herramienta responde esa pregunta directamente — no como un ejercicio de reporte ESG, sino como un **instrumento operativo de due diligence** para empresas agroindustriales con exposición en su cadena de suministro hacia compradores europeos.

---

## Fuentes de Datos

| Fuente | Descripción |
|---|---|
| **UMSEF-MAyDS** | Unidad de Manejo del Sistema de Evaluación Forestal — cifras de deforestación (has.) por departamento, posteriores a 2020 |
| **IGN Argentina** (API georef) | Límites departamentales oficiales — `apis.datos.gob.ar/georef` |
| **EUDR Reg. 2023/1115** | Marco regulatorio de la UE que define el corte de diciembre de 2020 para deforestación |

---

## Metodología de Puntuación de Riesgo

A cada departamento se le asigna un puntaje de riesgo según el porcentaje de su superficie total deforestada después de diciembre de 2020:

| Puntaje | Etiqueta | Umbral |
|---|---|---|
| 3 | 🔴 Alto | > 3% de la superficie |
| 2 | 🟠 Medio | 1–3% |
| 1 | 🟢 Bajo | < 1% |
| 0 | ⬜ Sin datos | Sin información disponible |

---

## Stack Tecnológico

- **Python 3** (Google Colab)
- `geopandas` — unión espacial entre los datos de deforestación y los polígonos departamentales oficiales
- `folium` — mapa HTML interactivo con tooltips y leyenda
- `pandas` — procesamiento de datos y puntuación de riesgo
- API georef del IGN — descarga en vivo de los límites departamentales oficiales de Argentina

---

## Estructura del Repositorio

```
eudr-deforestation-risk-map/
├── Georreferenciacion.ipynb     # Pipeline completo — ejecutar en Google Colab
├── riesgo_eudr_norte_argentina.html  # Resultado: mapa interactivo
└── README.md
```

---

## Cómo Ejecutarlo

1. Abrir `Georreferenciacion.ipynb` en [Google Colab](https://colab.research.google.com/)
2. Ejecutar la Celda 1 para instalar las dependencias (`geopandas`, `folium`, `mapclassify`)
3. Ejecutar las Celdas 2 a 5 secuencialmente
4. La Celda 6 descarga el mapa HTML final a tu equipo

No requiere claves de API. No requiere instalación local.

---

## Resultado

El entregable final es un archivo HTML autocontenido (`riesgo_eudr_norte_argentina.html`) que:

- Renderiza los polígonos departamentales coloreados según el nivel de riesgo EUDR
- Muestra tooltips interactivos con hectáreas deforestadas y % de superficie afectada al pasar el cursor
- Incluye leyenda y título superpuesto
- Funciona offline en cualquier navegador — no requiere servidor

---

## Contexto y Limitaciones

- Las cifras de deforestación se basan en informes públicos de UMSEF (2021–2023). Para uso productivo, este pipeline debería validarse contra las capas de pérdida de vegetación de **MapBiomas Argentina** y las categorías del **OTBN** (Ordenamiento Territorial de Bosques Nativos) bajo la Ley 26.331.
- El índice de riesgo está construido a **nivel departamental** — el cumplimiento a nivel de lote requiere la intersección de polígonos con coordenadas de parcela, que es el siguiente paso del pipeline.
- Este proyecto es una prueba de concepto como punto de entrada para un futuro servicio de reporte de cumplimiento EUDR por lote.

---

## Autor

**Mariano Romero**
Politólogo | Buenos Aires, Argentina
Maestría en Economía y Regulación Energética — CEARE, UBA Facultad de Derecho
[LinkedIn](https://www.linkedin.com/in/marianoromero23)
