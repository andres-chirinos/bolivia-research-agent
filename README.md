# Plugin Antigravity: `bolivia-research-agent` (`data-shield`)

`bolivia-research-agent` (construido sobre la infraestructura de `data-shield`) es un plugin avanzado para **Antigravity CLI** diseñado para la **investigación agnóstica de información**, exploración profunda de datos y modelado estadístico riguroso en **Jupyter Notebooks (`.ipynb`)**.

Proporciona al agente de IA capacidades abiertas para descubrir, consultar y correlacionar datos en cualquier formato (archivos tabulares, bases de datos SQL, APIs o catálogos), integrando un **escudo de tokens (`data-shield-mcp`)** que sanitiza salidas de datos masivas (truncando DataFrames) y filtra binarios pesados (como gráficos en Base64), protegiendo la ventana de contexto del modelo y preservando de manera íntegra el archivo `.ipynb` físico con figuras interactivas para revisión humana.

---

## 1. Configuración del Espacio de Trabajo del Usuario

El plugin opera sobre cualquier directorio de análisis de datos de forma limpia y no invasiva:

### 1.1 Aislamiento de Archivos (`.gitignore` y `.antigravityignore`)
Crea un archivo `.antigravityignore` en la raíz de tu proyecto de análisis para evitar que la IA indexe gigabytes de datos o lea directamente el JSON crudo de los notebooks:

```text
data/
.venv/
notebooks/
```

> **Regla de Oro:** Todo notebook debe residir obligatoriamente dentro de la carpeta `notebooks/`. Al ocultar este directorio a las herramientas genéricas del CLI, fuerzas a la IA a interactuar con los notebooks **exclusivamente mediante las herramientas del servidor `data-shield-mcp`**, garantizando la sanitización de salidas.

### 1.2 Entorno Virtual del Proyecto de Datos
En la raíz de tu proyecto de análisis, inicializa el entorno virtual con `uv` e instala `ipykernel` junto con las librerías analíticas esenciales:

```bash
uv add ipykernel pandas pyarrow openpyxl ipympl
```

### 1.3 Contexto Semántico de Datos (Opcional pero Recomendado)
Si dispones de metadatos o esquemas de las tablas en `data/`, crea un archivo `contexto_datos.md` en la raíz del proyecto cliente detallando nombres de variables, tipos, relaciones (1:1, 1:N) y particularidades estadísticas.

---

## 2. Modos de Uso en Antigravity CLI

Una vez registrado el plugin, cuentas con dos formas sencillas de interactuar con él:

### Opción A: Cambiar al Agente Especializado (`bolivia-research-agent`)
Puedes cambiar el agente principal por defecto ejecutando el comando interactivo en Antigravity CLI:
```text
/agents
```
En el menú de selección, escoge **`bolivia-research-agent`** (o el alias compatible `data-shield-agent`). A partir de ese momento, el agente asumirá directamente el rol de **Investigador Senior de Datos y Científico Analítico**:
- Explora fuentes de información de forma abierta, sin cerrarse a un dominio o formato específico.
- Cruza datos multiformato (CSV, Parquet, JSON, SQL, APIs).
- Estructura el notebook con narrativa metodológica en Markdown.
- Valida hipótesis en borrador (`run_scratchpad_code`, `inspect_memory`).
- Acata estrictamente los guardrails antialucinación (cero números inventados, transparencia ante nulos).

### Opción B: Usar las Habilidades Incluidas
Las habilidades se activan automáticamente según la tarea, o puedes invocarlas explícitamente:
- `/data-shield-skill`: Procedimientos para manipular y ejecutar celdas en `.ipynb` vía MCP.
- `/data-research`: Metodología universal de exploración de información y análisis de datos.
- `/agent-guardrails`: Guardrails de fundamentación estricta y citas de procedencia.
- `/okf-knowledge-base`: Estructuración de paquetes de datos y linaje epistémico.
- `/research-methodology`: Clasificación y diseño metodológico experimental y cuantitativo.

---

## 3. Instalación y Registro en Antigravity CLI

### Instalación mediante CLI:
```bash
agy plugin install /home/andreschirinos/Proyectos/data-shield/plugin
```

### Registro del Servidor MCP:
El plugin registra automáticamente `data-shield-mcp`. También puedes añadirlo o verificarlo globalmente mediante:
```bash
agy mcp add data-shield-mcp uv -- run --project /home/andreschirinos/Proyectos/data-shield -m data_shield_mcp
agy mcp list
```

---

## 4. Arquitectura del Repositorio

```text
data-shield/
├── README.md                          # Documentación del plugin y guía de uso
├── pyproject.toml                     # Configuración de empaquetado del servidor MCP (hatchling)
├── data_shield_mcp/                   # Servidor MCP (Python + MCP SDK v2)
│   ├── __init__.py
│   ├── __main__.py                    # Entrypoint ejecutable
│   ├── kernel.py                      # Gestor asíncrono del kernel IPython y kernelspec
│   ├── sanitizer.py                   # Filtro de sanitización y escudado de tokens
│   ├── server.py                      # Definición de las 16 herramientas MCP
│   └── context/                       # Especificaciones técnicas de referencia
└── plugin/                            # Paquete del Plugin para Antigravity CLI
    ├── plugin.json                    # Manifiesto oficial del plugin
    ├── mcp_config.json                # Configuración de arranque del servidor MCP
    ├── agents/
    │   ├── bolivia-research-agent.md  # Agente de Investigación y Ciencia de Datos
    │   └── data-shield-agent.md       # Alias compatible: Científico de Datos Senior
    ├── rules/
    │   └── AGENTS.md                  # Reglas de blindaje de tokens y antialucinación
    └── skills/
        ├── data-shield-skill/         # Habilidad de ejecución y manipulación de notebooks
        ├── data-research/             # Habilidad de investigación y exploración abierta de datos
        ├── agent-guardrails/          # Guardrails antialucinación y citas de procedencia
        ├── okf-knowledge-base/        # Empaquetado y linaje de datos
        └── research-methodology/      # Metodología de investigación y controles de validez
```

---

## 5. Mecanismo de Blindaje de Contexto (El "Escudo")

Cuando el modelo ejecuta código en el notebook a través del MCP, `data-shield-mcp` procesa las salidas en memoria:

1. **Gráficos Interactivos y Widgets (`ipympl`):**
   - El código en el notebook renderiza figuras interactivas con `%matplotlib ipympl` (`fig, ax = plt.subplots()`, `plt.show()`).
   - El servidor MCP intercepta los datos pesados en Base64 y JSON de widgets, guardándolos en el `.ipynb` para su visualización humana en el editor, pero devolviendo al modelo únicamente: `[Gráfico renderizado localmente]`.
2. **DataFrames y Tablas Masivas:**
   - Si se evalúa un DataFrame de Pandas (dejando la variable en la última línea), el sanitizador intercepta la tabla y trunca su salida a las 5 primeras y 5 últimas filas con un indicador intermedio (`... [X filas omitidas] ...`).
3. **Limpieza de Trazas de Error:**
   - Los mensajes de error y tracebacks son saneados eliminando códigos ANSI de color y anonimizando rutas del sistema operativo para ahorrar tokens y proteger la privacidad.