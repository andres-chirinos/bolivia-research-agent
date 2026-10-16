# Reglas para Agentes de Investigación Bolivia (bolivia-research-agent)

Este archivo de reglas rige el comportamiento analítico y metodológico del agente en proyectos de investigación económica, financiera y social de Bolivia.

---

## 1. Mandato de Blindaje de Tokens y Aislamiento de Notebooks

- **Ubicación Exclusiva:** Todo análisis en Jupyter debe residir en `notebooks/`.
- **Uso Estricto de `data-shield-mcp`:** Jamás leer, crear ni editar archivos `.ipynb` con comandos directos de texto (`cat`, `view_file`, `write_to_file`).
- **Exploración Segura:** Usar `run_scratchpad_code` para validar esquemas y columnas en RAM antes de consolidar celdas en el cuaderno final.
- **Truncamiento de Tablas:** Dejar variables de DataFrames al final de la celda de código sin envolver en `print()`.

---

## 2. Guardrails Antialucinación

- **Fundamentación Estricta:** Responder única y exclusivamente con los números y registros devueltos por el motor SQL (`DuckDB`) o las herramientas de datos.
- **Cita Obligatoria de Tríada:** Siempre indicar el origen del dato citando la tríada canónica `[catalogo:dataset:recurso]` (ej. `[p2p-bob-exchange:advice:parquet]`, `[mefp:indicadores_macro_fmi:req_13_a]`).
- **Transparencia ante Nulos:** Si una consulta devuelve 0 filas o valores `NULL`, reportarlo explícitamente sin extrapolar.
- **Verificación de Esquema Previa:** No adivinar nombres de columnas; consultar el esquema con `LIMIT 1` antes de armar consultas SQL complejas.

---

## 3. Normativa de Datos Soberanos (OKF v0.2)

- Utilizar el estándar **Open Knowledge Format (OKF / ODKF v0.2)** para linaje epistémico y manifiestos `datapackage.yaml`.
- Declarar dependencias *upstream* (fuentes primarias) y transformaciones verificables por hash SHA-256.
