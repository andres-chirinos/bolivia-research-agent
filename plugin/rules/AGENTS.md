# Reglas de Operación e Investigación

Este archivo rige el comportamiento analítico y metodológico del agente en tareas de investigación, exploración de información y análisis de datos.

---

## 1. Mandato de Blindaje de Tokens y Aislamiento de Notebooks

- **Ubicación Exclusiva:** Todo análisis en Jupyter debe residir en `notebooks/`.
- **Uso Estricto de `data-shield-mcp`:** Jamás leer, crear ni editar archivos `.ipynb` con comandos directos de texto (`cat`, `view_file`, `write_to_file`).
- **Exploración Segura:** Usar `run_scratchpad_code` e `inspect_memory` para validar esquemas, formas y columnas en RAM antes de consolidar celdas en el cuaderno final.
- **Truncamiento de Tablas:** Dejar variables de DataFrames al final de la celda de código sin envolver en `print()`.

---

## 2. Guardrails Antialucinación y Fundamentación en Datos

- **Fundamentación Estricta:** Responder única y exclusivamente con los números, registros y evidencias devueltos por las herramientas de consulta y ejecución.
- **Cita Obligatoria de Procedencia:** Indicar siempre la fuente o dataset de origen de los datos citados.
- **Transparencia ante Nulos:** Si una consulta devuelve 0 filas o valores `NULL`, reportarlo con total transparencia sin extrapolar ni inventar datos.
- **Verificación de Esquema Previa:** No adivinar nombres de columnas ni relaciones; consultar el esquema con `LIMIT 1`, `df.columns` o herramientas de metadatos antes de armar consultas complejas.

---

## 3. Trazabilidad y Reproducibilidad

- Mantener registro de fuentes de datos utilizadas y transformaciones aplicadas.
- Documentar el propósito y justificación metodológica de cada fase del análisis mediante celdas Markdown.
