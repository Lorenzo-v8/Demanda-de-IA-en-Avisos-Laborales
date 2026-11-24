# Demanda de IA en Avisos Laborales

Análisis exploratorio de datos sobre los requisitos de IA en el mercado de empleo tech, con foco en **detectar y corregir quiebres metodológicos** de la serie antes de sacar conclusiones.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TU_USUARIO/TU_REPO/blob/main/demanda_ia_avisos_laborales.ipynb)

## Contexto

El [AI Requirements Index](https://www.datamatastudios.com/datasets/ai-requirements-index) de Datamata Studios publica, día a día, el porcentaje de avisos laborales tech que mencionan habilidades de IA, separado por **6 categorías de empleo**, **niveles de seniority** y **tipo de habilidad** (IA generativa, ML clásico o cualquiera de las dos).

## El problema central

Al leer la serie "tal cual", el porcentaje de avisos que piden IA puede mostrar saltos enormes. Pero cuando el **universo de avisos relevados cambia abruptamente de un día para otro**, el movimiento refleja un cambio de alcance del relevamiento y no del mercado laboral.

El notebook:

1. Grafica la serie "ingenua" del % de avisos con IA.
2. **Detecta automáticamente los quiebres**: saltos del universo total superiores a un umbral configurable (por defecto ×1,8).
3. Aísla el **tramo más largo con cobertura estable** y recalcula la variación con criterio de medición constante.
4. Compara ambas lecturas.

## Preguntas que responde

1. ¿La demanda de IA realmente cambió, o es un artefacto de medición?
2. ¿Cuánto cambió con un criterio de medición consistente?
3. ¿Cómo varía la exigencia de IA según el nivel de seniority?
4. ¿IA generativa y ML clásico se piden para los mismos puestos?

## Qué calcula

- Serie del % de avisos con IA y del universo total relevado
- Tabla de quiebres detectados (universo antes/después, factor de salto)
- Variación real en el tramo estable vs. variación ingenua
- Promedio de exigencia de IA por seniority (entry / mid / senior)
- Brecha GenAI − ML por categoría
- Conclusiones que se **recalculan solas** con los datos descargados

## Datos

Fuente: [Datamata Studios — AI Requirements Index](https://www.datamatastudios.com/datasets/ai-requirements-index), también en [Kaggle](https://www.kaggle.com/datasets/datamatastudios/ai-requirements-index) y [Hugging Face](https://huggingface.co/datasets/datamatastudios/ai-requirements-index). Se actualiza a diario.

| columna | descripción |
|---|---|
| `snapshot_date` | fecha del relevamiento (UTC) |
| `category` | `data`, `engineering`, `product`, `devops`, `security`, `ai` |
| `seniority` | `all`, `entry`, `mid`, `senior`, `lead`, `unknown` |
| `tier` | `genai`, `ml`, `any_ai` |
| `listings_with_ai` | avisos que mencionan al menos una habilidad del tier |
| `total_listings` | avisos activos relevados en el grupo |
| `pct` | `listings_with_ai / total_listings × 100` |
| `required_count` | avisos donde la habilidad es requisito duro |

El notebook descarga el CSV directamente desde la API del proveedor y guarda una copia local (`ai-requirements-index.csv`). Si la descarga falla, usa esa copia; también podés subir el CSV bajado de Kaggle con ese mismo nombre.

> Como la serie se actualiza a diario, los números al ejecutar el notebook van a diferir de otras fechas. Para reproducir un período específico, usá `FECHA_DESDE` y `FECHA_HASTA` en la celda de configuración.

## Configuración

En la celda de configuración del notebook:

```python
CATEGORIA_FOCO = "ai"      # categoría analizada en detalle
FECHA_DESDE = None         # ej: "2026-03-01"
FECHA_HASTA = None         # ej: "2026-07-22"
UMBRAL_SALTO = 1.8         # sensibilidad de la detección de quiebres
```

## Cómo ejecutarlo

**En Google Colab:** botón "Open in Colab" de arriba → *Entorno de ejecución → Ejecutar todo*.

**En local:**

```bash
git clone https://github.com/TU_USUARIO/TU_REPO.git
cd TU_REPO
pip install pandas numpy matplotlib jupyter
jupyter notebook demanda_ia_avisos_laborales.ipynb
```

## Estructura

```
.
├── demanda_ia_avisos_laborales.ipynb   # análisis completo
├── ai-requirements-index.csv           # copia local de los datos (se genera al ejecutar)
└── README.md
```

## Stack

Python · pandas · NumPy · matplotlib

## Licencia y atribución

Los datos pertenecen a **Datamata Studios** y se publican bajo [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

> Datamata Studios. "Datamata AI Requirements Index." https://www.datamatastudios.com/datasets/ai-requirements-index. Licensed under CC BY 4.0.

## Autor

**Lorenzo Ciprés** · proyecto de portfolio de ciencia de datos.
