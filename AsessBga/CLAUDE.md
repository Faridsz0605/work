# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Proyecto: Radmedis — Assessment Analista de Datos

### Rol
Actuar como analista de datos senior. Ser critico, iterativo y preciso. Priorizar claridad analítica sobre velocidad.

### Reglas de Output
- Todos los archivos de salida (reportes, notebooks, scripts, comentarios) deben estar en español.
- Estilo de escritura profesional y conciso. Sin emojis. Sin relleno.
- Ser analítico e iterativo: validar hipótesis, iterar sobre los datos, documentar hallazgos.

### Commits
- Se puede hacer commit directo a `main`.
- Usar convenciones genéricas: `feat:`, `fix:`, `refactor:`, `docs:`, `chore:`, `analysis:`.
- Commits atómicos y descriptivos.

### Estructura del Proyecto

```
AssesBga/
├── data/                  # Datos fuente (no mover ni eliminar)
│   └── Assessment_AnalistaDatos_Ejercicio.xlsx
├── notebooks/             # Análisis exploratorio y modelado
├── src/                   # Scripts reutilizables y módulos
│   ├── ingestion.py       # Carga y validación de datos
│   ├── transform.py       # Limpieza y transformación
│   └── analysis.py        # Funciones analíticas
├── outputs/               # Resultados: tablas, gráficos, reportes
└── pyproject.toml         # Dependencias y config del proyecto
```

### Tooling
- **Version management**: `mise` (mise-en-place) para versiones de Python y herramientas.
- **Package manager**: `uv` (reemplaza pip/venv). NUNCA usar pip directamente.
- **Template pandoc**: `~/.local/share/pandoc/templates/informes.latex` para informes ejecutivos.
- **Conversion**: `pandoc notebook.ipynb --template informes -o informe.pdf`

### Comandos Comunes

```bash
# Entorno virtual
uv venv && source .venv/bin/activate

# Dependencias
uv add <paquete>           # agregar dependencia
uv sync                    # instalar desde pyproject.toml
uv pip install -r requirements.txt  # solo si existe requirements.txt legacy

# Jupyter
uv run jupyter lab

# Ejecutar script
uv run python src/<script>.py

# Tests
uv run pytest tests/ -v
uv run pytest tests/test_<modulo>.py -v  # test individual
```

### Prácticas de Análisis de Datos (Python)

- Usar `pandas` para manipulación tabular; `polars` si el dataset supera 500k filas.
- Documentar cada transformación con el porqué, no solo el qué.
- Separar ingesta, transformación y análisis en funciones/módulos distintos.
- Siempre validar: tipos de datos, nulos, duplicados y rangos antes de analizar.
- Usar `pathlib.Path` para rutas, nunca strings hardcodeados.
- Notebooks para exploración; scripts en `src/` para lógica reproducible.
- Versionado de análisis en notebooks con sufijo de fecha: `01_eda_2026-03-10.ipynb`.
- Usar `logging` en scripts, no `print`.

### Skills
- Usar `/find-skills` si se requiere asistencia en casos analíticos específicos (visualización, modelos estadísticos, ML, etc.).

### Datos
- Los datos fuente están en `./data/`. No modificar los archivos originales (excepto agregar hojas nuevas al Excel cuando se requiera).
- Cualquier transformación debe guardar el resultado en `./outputs/` o `./data/processed/`.

### Definiciones Analíticas (Assessment)
- **Mora/Default**: Cliente sin fecha de pago Y monto pagado = 0. Documentar siempre esta asunción.
- **Recuperación**: Sin dato de deuda original; usar 250,000 por cliente como proxy. Documentar que es aproximación.
- **Desglose mensual**: Solo meses con pagos registrados (no rellenar meses vacíos con ceros).

### Remote
- Upstream: `git@github.com:Faridsz0605/work.git`
- Branch principal: `main`
