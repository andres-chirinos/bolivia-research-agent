# Reglas de Ingeniería, Arquitectura e Investigación

Este archivo de reglas rige el comportamiento técnico, metodológico y arquitectónico de la suite de agentes especializados de Antigravity.

---

## 1. Gobernanza de Arquitectura y Dominio (Domain-Driven Design)

- **Aislamiento del Núcleo:** La lógica de negocio pura y los modelos del dominio deben residir en `domain/` y ser completamente agnósticos de frameworks, bases de datos o protocolos de transporte.
- **Entidades y Value Objects:** Modelar conceptos inmutables como Value Objects (`frozen=True` con validación interna). Asignar identidad explícita únicamente a Entidades con ciclo de vida.
- **Registro de Decisiones (ADRs):** Cualquier cambio estructural, adición de dependencias o alteración de contratos públicos debe registrarse formalmente en un ADR documentando contexto, alternativas y compensaciones.
- **Simplicidad (KISS / YAGNI):** Cero abstracciones especulativas. Diseñar la solución completa más simple que resuelva el problema planteado.

---

## 2. Arquitectura Hexagonal y Principios SOLID

- **Inversión de Dependencias:** El dominio nunca importa adaptadores ni infraestructura. Las dependencias apuntan siempre hacia el centro (`Adapters -> UseCases -> Ports -> Domain`).
- **Contratos de Puerto Explícitos:** Todo acceso a persistencia, almacenamiento o llamadas de red se realiza a través de puertos de salida (`ports/outbound`). Toda invocación externa llega a través de puertos de entrada (`ports/inbound`).
- **Atomicidad y Responsabilidad Única:** Un archivo por clase o responsabilidad. Evitar archivos monolíticos.
- **Pruebas Automatizadas:** 100% de éxito en la suite de pruebas. El código nuevo debe incluir tests herméticos con mocks adecuados para I/O.

---

## 3. Exploración de Datos, Veracidad y Blindaje de Tokens

- **Ubicación Exclusiva de Cuadernos:** Todo análisis interactivo en Jupyter debe residir en `notebooks/`.
- **Uso Estricto de `data-shield-mcp`:** Jamás leer, crear ni editar archivos `.ipynb` con comandos directos de texto (`cat`, `view_file`, `write_to_file`).
- **Fundamentación Estricta:** Responder única y exclusivamente con los números, registros y evidencias devueltos por las herramientas de consulta y ejecución. Cero invención o extrapolación ante nulos.
- **Verificación de Esquema Previa:** No adivinar nombres de campos ni esquemas; consultar la estructura con `LIMIT 1` o metadatos antes de armar consultas complejas.
