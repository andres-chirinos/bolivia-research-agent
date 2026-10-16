---
name: bolivia-data-research
description: Guía metodológica y técnica para investigación de datos económicos, financieros y gubernamentales de Bolivia usando DataMesh SDK, estándar OKF v0.2 y catálogos soberanos federados. Usar al formular consultas analíticas sobre cotizaciones P2P, indicadores MEFP/BCB/INE y linaje epistémico boliviano.
---

# Habilidad: bolivia-data-research

Esta habilidad instruye al agente en los procedimientos normativos y técnicos para realizar investigaciones de datos económicos, financieros y soberanos de Bolivia mediante **DataMesh SDK** y el estándar **Open Knowledge Format (OKF / ODKF v0.2)**.

---

## 1. Ecosistema de Datos Boliviano

1. **Mercado Cambiario P2P (Binance USDT/BOB):**
   - Dataset principal: `p2p-bob-exchange:advice` (almacenado en `data/advice.parquet`).
   - Contiene millones de posturas de compra (`BUY`) y venta (`SELL`).
   - Variables clave: `timestamp`, `tradetype`, `price`, `tradablequantity`, `minsingletransamount`, `maxsingletransamount`.
   - Filtros de sanidad: Descartar anomalías o precios fuera del rango razonable (`price BETWEEN 6.0 AND 30.0`).
   - Métrica estándar: Promedios ponderados y medianas por día o mes.

3. **Catálogos Soberanos Federados (`llms.txt`):**
   - Formato semántico descentralizado que lista conjuntos de datos y recursos disponibles en nodos soberanos.
   - Exploración: `dm.discover(url_o_path)` y `dm.search(palabras_clave)`.

---

## 2. Sintaxis y Operación con DataMesh SDK

El agente utiliza la fachada unificada en Python de DataMesh:

```python
import datamesh as dm

# 1. Descubrimiento de fuentes soberanas
catalogos = dm.discover("catalogs/llms.txt")

# 2. Consulta analítica SQL directa con DuckDB (sin pasos manuales de ETL)
res = dm.sql("""
    SELECT 
        tradetype,
        COUNT(*) AS total_ofertas,
        ROUND(AVG(price), 4) AS precio_promedio,
        ROUND(MEDIAN(price), 4) AS precio_mediana
    FROM 'p2p-bob-exchange:advice'
    WHERE price BETWEEN 6.0 AND 25.0
    GROUP BY tradetype
""")
df = dm.to_df(res)

# 3. Gobernanza y Tríadas Canónicas
# Toda tabla o recurso debe citarse bajo el formato [catalogo:dataset:recurso]
```

---

## 3. Protocolo de Investigación Rigurosa

1. **Verificación de Esquema Previa:** Ejecutar `LIMIT 1` o consultar esquemas antes de proponer consultas complejas.
2. **Cero Alucinación:** Nunca inventar cifras ni extrapolaciones no fundamentadas en registros observados.
3. **Cita Explícita de Procedencia:** Citar la tríada correspondiente a cada dato presentado.
4. **Reproducibilidad:** Plasmar transformaciones en notebooks de Jupyter gestionados con `data-shield-mcp`.
