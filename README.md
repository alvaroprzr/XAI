# Explicabilidad de modelos de caja negra en *credit scoring*

Trabajo de Fin de Grado del Grado en Ciencia e Ingeniería de Datos (Universidade da Coruña).

Se estudia hasta qué punto las explicaciones SHAP de un modelo de caja negra (XGBoost)
son estables y coherentes cuando se aplican a la concesión de crédito, tomando como
referencia una regresión logística entrenada sobre los mismos datos. Se analizan cuatro
dimensiones: concordancia con la logística, estabilidad ante el reentrenamiento,
estabilidad ante el conjunto de referencia (*background*) y consistencia/coherencia de
las explicaciones locales.

## Estructura del repositorio

```
.
├── code/
│   ├── TFG_analisis_datasets.ipynb     # análisis de los cinco datasets candidatos
│   ├── TFG_SHAP_credit_scoring.ipynb   # experimento completo sobre el dataset de Taiwán
│   └── resultados/                     # figuras, tablas, resumen JSON y .npz (no versionado)
├── data/                               # datasets (no versionados, ver más abajo)
├── documentos/
│   └── Documento_TFG_agosto_revisado.docx   # informe: datasets, bibliografía y propuesta
├── README.md
├── pyproject.toml / uv.lock            # dependencias fijadas
└── .python-version                     # Python 3.9
```

`TFG_analisis_datasets.ipynb` explora los cinco datasets candidatos y produce las cifras que
después se recogen en el informe: tamaño, número y tipo de variables, definición y tasa de la
variable objetivo, desequilibrio, valores perdidos, inventario de ficheros y anomalías de
codificación. Termina con una ficha por dataset, con los números ya formateados, lista para
trasladar al documento. No escribe nada en disco: todo queda en el propio notebook. Necesita
los cinco datasets descargados.

## Datos

Los datasets no se incluyen en el repositorio. Deben descargarse y dejarse en `data/`:

| Dataset | Fuente | Carpeta esperada |
|---|---|---|
| Default of Credit Card Clients (principal) | [UCI #350](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients) | `data/default+of+credit+card+clients/` |
| South German Credit (secundario) | [UCI #573](https://archive.ics.uci.edu/dataset/573/south+german+credit) | `data/south+german+credit+update/` |
| Give Me Some Credit | [Kaggle](https://www.kaggle.com/c/GiveMeSomeCredit) | `data/GiveMeSomeCredit/` |
| Home Credit Default Risk | [Kaggle](https://www.kaggle.com/c/home-credit-default-risk) | `data/home-credit-default-risk/` |
| Lending Club | [Kaggle](https://www.kaggle.com/datasets/wordsforthewise/lending-club) | `data/lending-club/` |

`TFG_analisis_datasets.ipynb` necesita los cinco. El experimento usa por ahora solo el de
Taiwán: South German Credit es el segundo dataset elegido en el informe, pero todavía no está
incorporado a `TFG_SHAP_credit_scoring.ipynb`. Ese notebook busca automáticamente el `.xls` de
UCI (o la copia `.csv` de Kaggle) en `data/default+of+credit+card+clients/`; la ruta se puede
fijar a mano en la variable `RUTA_DATOS`.

## Entorno

El proyecto usa [uv](https://docs.astral.sh/uv/) y Python 3.9:

```bash
uv sync
uv run python -m ipykernel install --user --name tfg-shap --display-name "TFG SHAP"
uv run jupyter lab code/TFG_SHAP_credit_scoring.ipynb
```

Para ejecutar el notebook completo sin abrirlo:

```bash
cd code
uv run jupyter nbconvert --to notebook --execute --inplace TFG_SHAP_credit_scoring.ipynb
```
