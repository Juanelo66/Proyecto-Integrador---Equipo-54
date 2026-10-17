# Perfiles antioxidantes en fresas

**Proyecto Integrador — Equipo 54**

Análisis de datos e ingeniería de características para estudiar las relaciones entre el manejo orgánico del suelo, el estado nutricional de las plantas y la producción y calidad de las fresas (*Fragaria × ananassa*) de los cultivares Donna y Dream.

## Descripción del proyecto

Este proyecto utiliza técnicas de ciencia de datos para explorar información experimental relacionada con cuatro tratamientos de manejo orgánico del suelo y sus posibles asociaciones con las propiedades del suelo, la nutrición foliar, los indicadores de color RGB y las características productivas, fisicoquímicas y nutricionales de las fresas.

El trabajo sigue la metodología **CRISP-ML(Q)**, comenzando con el análisis exploratorio de datos (EDA) y continuando con la ingeniería de características (*Feature Engineering*).

## Objetivo general

Analizar las relaciones entre los tratamientos orgánicos del suelo, las propiedades edáficas, el estado nutricional de las plantas y los indicadores de producción y calidad del fruto, mediante técnicas de análisis de datos y aprendizaje automático.

### Objetivos específicos

- Explorar la distribución, calidad y comportamiento de las variables experimentales.
- Comparar descriptivamente los tratamientos orgánicos y los cultivares Donna y Dream.
- Identificar posibles asociaciones entre propiedades del suelo, nutrición foliar, índices RGB y características del fruto.
- Construir y transformar características relevantes para el análisis agronómico.
- Aplicar métodos de selección y extracción de características para reducir la dimensionalidad de los datos.
- Preparar conjuntos de datos para las futuras etapas de modelado predictivo.

## Tratamientos experimentales

Se consideran cuatro tratamientos orgánicos, cuya correspondencia con los códigos experimentales fue confirmada por la responsable del estudio.

| Código | Tratamiento | Descripción |
|---|---|---|
| T1 | Compost | Enmienda orgánica basada en compost. |
| T2 | N-rich | Enmienda orgánica rica en nitrógeno. |
| T3 | RCW-HD / WR-HD | Residuos leñosos de poda aplicados en dosis alta (15 kg/m²). |
| T4 | RCW-LD | Residuos leñosos de poda aplicados en dosis baja (7.5 kg/m²). |

## Estructura del repositorio

```text
Proyecto-Integrador---Equipo-54/
│
├── .idea/                         # Archivos de configuración del IDE
│
├── data/
│   └── raw/                       # Archivos originales del experimento
│       ├── alldata_polyphenols.xlsx
│       ├── Anthocyanins.xlsx
│       ├── Antiox_data.xlsx
│       ├── Dataset_final_leaf.xlsx
│       ├── Dataset_final_suelo.xlsx
│       ├── harvests.xlsx
│       ├── Sampling May 2023.xlsx
│       ├── Table polyphenols.xlsx
│       └── VitC_MarinaPerez.xlsx
│
├── docs/                          # Documentación del proyecto
│
├── notebook/
│   ├── Análisis exploratorio de datos.ipynb
│   └── Feature_Engineering.ipynb
│
├── outputs/                       # Resultados generados por los notebooks
│   ├── feature_engineering/
│   │   ├── figuras/
│   │   ├── auditoria_transformaciones.csv
│   │   ├── comparacion_subconjuntos.csv
│   │   ├── diccionario_derivadas.csv
│   │   ├── pca_cargas.csv
│   │   ├── pca_varianza.csv
│   │   ├── ranking_f_rendimiento.csv
│   │   ├── resumen_preparacion_crisp_ml.csv
│   │   ├── train_depurado.csv
│   │   ├── test_depurado.csv
│   │   ├── train_pca.csv
│   │   ├── test_pca.csv
│   │   ├── train_top_12.csv
│   │   ├── test_top_12.csv
│   │   ├── train_top_16.csv
│   │   ├── test_top_16.csv
│   │   ├── train_top_20.csv
│   │   ├── test_top_20.csv
│   │   └── variables_descartadas.csv
│   │
│   ├── correlation_master_full.png
│   ├── correlation_master_spearman.csv
│   └── ...                        # Otros resultados del EDA
│
└── README.md
```

## Datos utilizados

Los datos experimentales provienen de nueve archivos Excel almacenados en `data/raw/`.

Estos archivos contienen mediciones relacionadas con:

- **Suelo:** propiedades químicas, disponibilidad de nutrientes e indicadores microbiológicos.
- **Hojas:** concentraciones minerales, indicadores nutricionales y mediciones realizadas en distintos momentos.
- **Color foliar:** índices derivados de información RGB.
- **Producción:** rendimiento comercial y otras variables de cosecha.
- **Calidad del fruto:** características fisicoquímicas, contenido de vitamina C, polifenoles, antocianinas y actividad antioxidante.

El conjunto analítico integrado contiene **32 observaciones correspondientes a dos cultivares, cuatro tratamientos y cuatro réplicas**, con una agrupación provisional de 16 parcelas experimentales.

## Metodología

El desarrollo del proyecto se organiza siguiendo CRISP-ML(Q).

### 1. Análisis Exploratorio de Datos (EDA)

**Notebook:** `notebook/Análisis exploratorio de datos.ipynb`

Se realiza la integración y exploración de los datos originales, incluyendo:

- Revisión de estructura, tipos de datos y valores faltantes.
- Estadística descriptiva y visualización de distribuciones.
- Comparaciones exploratorias por tratamiento y cultivar.
- Análisis de correlaciones entre variables de suelo, hojas y fruto.
- Exploración de patrones multivariantes.

Los resultados correspondientes se almacenan en `outputs/`. Las figuras utilizadas en las libretas se guardan en `outputs/figures/`.

### 2. Ingeniería de Características (Feature Engineering)

**Notebook:** `notebook/Feature_Engineering.ipynb`

La preparación de datos contempla tres bloques principales.

**Construcción de características:** generación de nuevas variables a partir de mediciones existentes, discretización descriptiva y codificación de variables categóricas mediante One-Hot Encoding.

**Normalización y transformación:** imputación de valores faltantes, transformación Yeo-Johnson y estandarización mediante StandardScaler.

**Selección y extracción:** aplicación de filtros de varianza, duplicación y correlación; selección supervisada mediante puntuación F; construcción de subconjuntos de características; y reducción dimensional mediante PCA.

Los principales resultados obtenidos son:

| Indicador | Resultado |
|---|---:|
| Observaciones analíticas | 32 |
| Características derivadas | 25 |
| Variables numéricas candidatas | 89 |
| Variables transformadas con Yeo-Johnson | 25 |
| Variables numéricas depuradas | 85 |
| Variables categóricas codificadas | 6 |
| Componentes principales seleccionados | 12 |
| Varianza acumulada del PCA | 85.93% |

Se generan diferentes matrices de características, que se almacenan en `outputs/feature_engineering/` para su posterior evaluación.

### 3. Modelado predictivo — Próxima etapa

En etapas posteriores se contempla construir un modelo de referencia (*baseline*) para evaluar la viabilidad predictiva del problema, comparar algoritmos y optimizar sus configuraciones.

Esta fase todavía no forma parte de los resultados presentados.

## Requisitos y herramientas

El proyecto utiliza Python 3 y notebooks de Jupyter.

Las principales bibliotecas utilizadas son:

- `pandas` y `numpy`: procesamiento y manipulación de datos.
- `matplotlib` y `seaborn`: visualización.
- `scipy`: análisis estadístico.
- `scikit-learn`: transformación, escalamiento, selección de características y PCA.
- `openpyxl`: lectura de archivos Excel.

### Instalación

Clonar el repositorio:

```bash
git clone <URL_DEL_REPOSITORIO>
cd Proyecto-Integrador---Equipo-54
```

Crear y activar un entorno virtual:

**Windows**

```bash
python -m venv .venv
.venv\Scripts\activate
```

**macOS / Linux**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Instalar las dependencias:

```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn openpyxl jupyter
```

## Ejecución del proyecto

1. Verificar que los nueve archivos Excel originales se encuentren en `data/raw/`.
2. Abrir `notebook/Análisis exploratorio de datos.ipynb` para consultar o reproducir el análisis exploratorio.
3. Abrir `notebook/Feature_Engineering.ipynb` para ejecutar la ingeniería de características.
4. Ejecutar las celdas en orden, comenzando por la configuración técnica inicial.
5. Consultar los archivos y figuras generados en `outputs/`.

Se recomienda ejecutar cada notebook con un kernel limpio para verificar su reproducibilidad.

## Consideraciones y limitaciones

El conjunto de datos es reducido, por lo que los resultados deben interpretarse principalmente con fines exploratorios.

Además, las observaciones pueden compartir unidades experimentales, por lo que será necesario respetar la estructura de parcelas durante las evaluaciones posteriores.

Las asociaciones encontradas no deben interpretarse automáticamente como relaciones causales. Asimismo, la reducción dimensional mediante PCA no garantiza una mejora del rendimiento predictivo.

## Estado del proyecto

| Etapa | Estado |
|---|---|
| Análisis exploratorio de datos | Completado |
| Ingeniería de características | Implementada |
| Modelo de referencia (*baseline*) | Pendiente |
| Comparación de modelos | Pendiente |
| Optimización de hiperparámetros | Pendiente |

## Equipo

**Equipo 54 — Proyecto Integrador**

Proyecto académico de ciencia de datos aplicado al estudio de fresas bajo diferentes tratamientos de manejo orgánico del suelo.