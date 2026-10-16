# Suite Multidisciplinaria de Agentes Antigravity: `bolivia-research-agent` (`data-shield`)

Esta suite proporciona un ecosistema modular de **agentes especializados** para **Antigravity CLI**, diseñados para cubrir el ciclo completo de vida del software y la analítica: desde la investigación abierta de datos y el modelado en Jupyter Notebooks con protección de contexto (`data-shield-mcp`), hasta el refinamiento metodológico de requerimientos, diseño arquitectónico con **Domain-Driven Design (DDD)** e implementación técnica desacoplada bajo **Arquitectura Hexagonal (Ports & Adapters)** y principios **SOLID**.

---

## 1. Catálogo de Agentes Especializados

Puedes seleccionar cualquiera de estos agentes en cualquier momento ejecutando en la terminal de Antigravity CLI:
```text
/agents
```

### 1. `bolivia-research-agent` (Investigador Senior y Ciencia de Datos)
- **Propósito:** Exploración abierta de información, formulación y contraste de hipótesis, análisis multiformato (CSV, Parquet, JSON, SQL, APIs) y manipulación reproducible de Jupyter Notebooks.
- **Blindaje de Tokens:** Opera con el soporte del servidor **`data-shield-mcp`**, ejecutando transformaciones y gráficos interactivos (`ipympl`) en el kernel local mientras trunca tablas pesadas y protege la ventana de contexto.
- **Guardrails:** Fundamentación estricta en datos reales, cita obligatoria de procedencia y transparencia absoluta ante datos nulos o vacíos.

### 2. `software-architect-agent` (Arquitectura de Software, Requerimientos y Calidad)
- **Propósito:** Levantamiento y refinamiento formal de requerimientos, diseño arquitectónico estratégico y táctico, y aseguramiento de calidad de software.
- **Domain-Driven Design (DDD):** Delimitación de Bounded Contexts, mapeo de relaciones (Context Maps), definición de lenguaje ubicuo compartido, diseño de Aggregates, Entities, Value Objects y Domain Events.
- **Registro de Decisiones (ADRs):** Documentación del *por qué*, evaluando alternativas, compensaciones (trade-offs) y consecuencias de diseño.
- **Gobierno de Calidad:** Simplicidad pragmática (KISS/YAGNI), estándares de tipado estricto, inmutabilidad y diseño de la pirámide de pruebas.

### 3. `hexagonal-implementer-agent` (Ingeniero de Software e Implementador Técnico)
- **Propósito:** Implementación de código de producción desacoplado, mantenible y de alto rendimiento.
- **Arquitectura Hexagonal (Ports & Adapters):**
  - Núcleo de dominio puro (`domain/`) sin dependencias de infraestructura ni frameworks.
  - Puertos de entrada y salida explícitos (`ports/inbound`, `ports/outbound`).
  - Casos de uso orquestadores (`usecases/`).
  - Adaptadores desacoplados (`adapters/`).
- **Principios SOLID:** Responsabilidad única (un archivo por responsabilidad), abierto/cerrado, sustitución de Liskov, segregación de interfaces e inversión de dependencias estricta.
- **Pruebas y Robustez:** Desarrollo guiado por pruebas (TDD), fixtures herméticas en `pytest`, 100% de éxito en pruebas, auditoría de seguridad defensiva (anti-SSRF, path traversal) y optimización de rendimiento en streaming.

---

## 2. Habilidades Disponibles (`skills/`)

El plugin empaqueta un conjunto completo de habilidades para asistir a los agentes:

| Habilidad | Comando | Descripción |
| :--- | :--- | :--- |
| **`data-shield-skill`** | `/data-shield-skill` | 16 herramientas MCP para manipular notebooks, scratchpad invisible e inspección de memoria en RAM. |
| **`data-research`** | `/data-research` | Metodología de exploración profunda de datos, diagnóstico estadístico y calidad de fuentes multiformato. |
| **`domain-driven-design`** | `/domain-driven-design` | Modelado de dominio, Bounded Contexts, Aggregates, Context Maps y lenguaje ubicuo. |
| **`documentation-and-adrs`** | `/documentation-and-adrs` | Registro de decisiones arquitectónicas (ADRs), trade-offs y especificaciones de casos de uso. |
| **`hexagonal-architecture`** | `/hexagonal-architecture` | Diseño e implementación de sistemas desacoplados con Ports & Adapters y Dependency Inversion. |
| **`python-code-style`** | `/python-code-style` | Estándares de código, tipado estricto Python 3.10+, inmutabilidad (`frozen=True`) y control de errores. |
| **`python-testing-patterns`**| `/python-testing-patterns`| Patrones avanzados de pruebas con `pytest`, dobles de prueba (mocks), fixtures y verificación de invariantes. |
| **`security-review`** | `/security-review` | Auditoría de seguridad de código, validación defensiva de inputs, prevención de SSRF y path traversal. |
| **`keep-it-simple`** | `/keep-it-simple` | Filosofía KISS/YAGNI para evitar sobreingeniería y abstracciones prematuras innecesarias. |
| **`agent-guardrails`** | `/agent-guardrails` | Guardrails antialucinación, fundamentación factual y citas obligatorias de procedencia. |
| **`research-methodology`** | `/research-methodology` | Diseño de investigación científica, validez metodológica y clasificación de hipótesis. |
| **`okf-knowledge-base`** | `/okf-knowledge-base` | Estándar Open Knowledge Format (OKF / ODKF v0.2) para linaje epistémico y paquetes Frictionless. |

---

## 3. Instalación y Registro en Antigravity CLI

### Instalación del Plugin Completo:
```bash
agy plugin install /home/andreschirinos/Proyectos/data-shield/plugin
```

### Registro del Servidor MCP:
El plugin expone automáticamente `data-shield-mcp`. Para añadirlo globalmente a Antigravity:
```bash
agy mcp add data-shield-mcp uv -- run --project /home/andreschirinos/Proyectos/data-shield -m data_shield_mcp
agy mcp list
```

---

## 4. Estructura del Repositorio

```text
data-shield/
├── README.md                            # Guía completa de la suite y catálogo de agentes
├── pyproject.toml                       # Configuración de empaquetado del servidor MCP
├── data_shield_mcp/                     # Servidor MCP (Python + MCP SDK v2)
│   ├── __init__.py
│   ├── __main__.py                      # Entrypoint ejecutable
│   ├── kernel.py                        # Gestor asíncrono del kernel IPython y kernelspec
│   ├── sanitizer.py                     # Filtro de sanitización y escudado de tokens
│   ├── server.py                        # Definición de las 16 herramientas MCP
│   └── context/                         # Especificaciones técnicas de referencia
└── plugin/                              # Paquete del Plugin para Antigravity CLI
    ├── plugin.json                      # Manifiesto oficial del plugin (v1.1.0)
    ├── mcp_config.json                  # Configuración de arranque del servidor MCP
    ├── agents/                          # Suite de agentes especializados
    │   ├── bolivia-research-agent.md    # Investigación y Ciencia de Datos
    │   ├── software-architect-agent.md  # Arquitectura, Requerimientos y DDD
    │   ├── hexagonal-implementer-agent.md # Implementación Hexagonal y SOLID
    │   ├── software-engineer-agent.md   # Alias de implementador técnico
    │   └── data-shield-agent.md         # Alias de científico de datos
    ├── rules/
    │   └── AGENTS.md                    # Reglas unificadas de arquitectura, código y veracidad
    └── skills/                          # Las 12 habilidades técnicas y metodológicas
```