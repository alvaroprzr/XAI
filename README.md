# Explicabilidad de modelos de caja negra en *credit scoring*

Trabajo de Fin de Grado del Grado en Ciencia e Ingeniería de Datos (Universidade da Coruña).

Se estudia hasta qué punto las explicaciones SHAP de un modelo de caja negra (XGBoost)
son estables y coherentes cuando se aplican a la concesión de crédito, tomando como
referencia una regresión logística entrenada sobre los mismos datos.

## Estructura del repositorio

```
.
├── code/
│   ├── TFG_analisis_datasets.ipynb     # análisis de los cinco datasets candidatos
│   └── TFG_SHAP_credit_scoring.ipynb   # experimento usando shap sobre el dataset de Taiwán
├── data/                               # datasets (no versionados, ver más abajo)
├── documentos/
│   └── Documento_TFG_agosto_revisado.docx   # boceto, previo a los informes
├── informes/
│   └── Informe_fase_inicial_TFG.docx        # informe de la fase inicial
├── README.md
├── pyproject.toml / uv.lock            # dependencias fijadas
└── .python-version                     # Python 3.9
```

`TFG_analisis_datasets.ipynb` explora los cinco datasets candidatos y produce las cifras que
después se recogen en el informe: tamaño, número y tipo de variables, definición y tasa de la
variable objetivo, desequilibrio, valores perdidos, inventario de ficheros y anomalías de
codificación.
Se necesitan los cinco datasets descargados si se quiere ejecutar.

## Datos

Los datasets no se incluyen en el repositorio. Deben descargarse y dejarse en `data/`:

| Dataset | Fuente | Carpeta esperada |
|---|---|---|
| Default of Credit Card Clients (principal elección) | [UCI #350](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients) | `data/default+of+credit+card+clients/` |
| South German Credit | [UCI #573](https://archive.ics.uci.edu/dataset/573/south+german+credit) | `data/south+german+credit+update/` |
| Give Me Some Credit | [Kaggle](https://www.kaggle.com/c/GiveMeSomeCredit) | `data/GiveMeSomeCredit/` |
| Home Credit Default Risk | [Kaggle](https://www.kaggle.com/c/home-credit-default-risk) | `data/home-credit-default-risk/` |
| Lending Club | [Kaggle](https://www.kaggle.com/datasets/wordsforthewise/lending-club) | `data/lending-club/` |

El experimento usa solo el de Taiwán, en `TFG_SHAP_credit_scoring.ipynb`.

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
