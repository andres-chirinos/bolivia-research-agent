---
name: data-research
description: Guía metodológica para la exploración profunda, análisis y modelado de datos en cualquier dominio. Usar al formular estrategias de búsqueda de información, exploración de fuentes multiformato (CSV, Parquet, JSON, SQL, APIs) y estructuración de investigaciones analíticas reproducibles.
---

# Habilidad: data-research

Esta habilidad instruye al agente en procedimientos universales para explorar información, analizar datasets de cualquier naturaleza y estructurar investigaciones reproducibles con rigor analítico.

---

## 1. Principio de Apertura y Exploración Holística

1. **Investigación sin Restricciones:**
   - Como agente de investigación, no debes limitarte a un único catálogo, formato o temática. Tu objetivo es buscar y correlacionar toda información pertinente disponible: archivos locales, fuentes remotas, bases de datos, APIs y catálogos de metadatos.
   - Analiza el contexto completo del problema antes de seleccionar herramientas o fuentes.

2. **Ingesta y Consulta Multiformato:**
   - Trabaja con soltura sobre cualquier formato estructurado o semiestructurado (Parquet, CSV, TSV, JSON, GeoJSON, SQLite, DuckDB).
   - Prioriza motores de consulta analítica directa (como DuckDB o Pandas) para procesar datos in situ sin requerir pipelines de ETL pesados o invasivos.

---

## 2. Metodología de Exploración y Análisis

1. **Inspección de Esquema Preliminar:**
   - Antes de formular consultas complejas o proponer hipótesis definitivas, examina la estructura real de los datos:
     - Nombres exactos de columnas y tipos de datos.
     - Dimensiones (`shape`), cardinalidad y rango temporal o numérico.
     - Muestra representativa de filas (`LIMIT 5` o `df.head()`).

2. **Diagnóstico Estadístico y Calidad de Datos:**
   - Evalúa la completitud: porcentaje y patrón de valores faltantes (`NULL` / `NaN`).
   - Revisa medidas de tendencia central y dispersión (media, mediana, percentiles, desviación estándar).
   - Identifica valores atípicos (outliers) y anomalías estructurales antes de aplicar modelos paramétricos.

3. **Formulación y Contraste de Hipótesis:**
   - Cada análisis debe responder a preguntas concretas o hipótesis de trabajo explícitas.
   - Aplica métodos adecuados según la naturaleza del problema (análisis descriptivo, series temporales, correlaciones, modelos de regresión o agrupamiento).

---

## 3. Síntesis y Trazabilidad

1. **Documentación Clara:**
   - Explica el racional teórico de cada decisión metodológica antes de ejecutar transformaciones.
   - Presenta interpretaciones sustantivas de los resultados (no te limites a confirmar que el código corrió).
2. **Trazabilidad y Linaje:**
   - Documenta el origen de los datos analizados y las transformaciones aplicadas para asegurar reproducibilidad total.
3. **Manejo de Incertidumbre:**
   - Si los datos son insuficientes, contradictorios o inconclusos, decláralo abiertamente sin forzar conclusiones.
