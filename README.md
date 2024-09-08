# TFM_yeast_dna
## Proyecto de Imputación de Variantes Genéticas Faltantes en Genes de Levaduras con Métodos de Machine Learning

Este proyecto explora varios enfoques para la **imputación de valores faltantes** en datos genéticos de levaduras, utilizando distintas técnicas de aprendizaje automático. Se implementan tres tipos principales de arquitecturas: métodos **basados en estadística**, **árboles de decisión**, y **redes neuronales profundas**.

El proyecto está inspirado en el trabajo disponible en [SCDA](https://github.com/work-hard-play-harder/SCDA), un repositorio que presenta un método de imputación basado en **Sparse Convolutional Denoising Autoencoders** para la imputación genotípica. Dado que este repositorio ofrece un código transparente y completamente reproducible, se decidió utilizar como base este proyecto para implementar y comparar distintos métodos de imputación mediante **Machine Learning** (ML).

### Enfoques Implementados

En el proyecto se han implementado los siguientes enfoques:

1. **Métodos estadísticos:**
   - **K-Nearest Neighbors (KNN)**: Un enfoque clásico basado en la proximidad entre muestras para imputar valores faltantes.

2. **Métodos basados en árboles:**
   - **Random Forest (RF)**: Un modelo basado en múltiples árboles de decisión que se entrena para predecir de manera conjunta o columna por columna.
   - **XGBoost**: Un método de boosting que mejora los árboles de decisión incrementales para lograr una mayor precisión en la predicción.

3. **Métodos basados en redes neuronales:**
   - **Autoencoder con capa de atención**: Una versión mejorada del autoencoder tradicional que incluye una capa de atención para mejorar la imputación al enfocarse en las características más importantes de los datos.

### Datos Utilizados

Los datos utilizados en este proyecto consisten en **variantes genéticas** (representadas por los valores 1 y 2) en distintos genes de levaduras para diferentes individuos. Los conjuntos de datos en formato comprimido que se emplean tanto para el **entrenamiento** como para el **test** son los siguientes:

- `ML_yeast_dna_imputation/data/raw/yeast_genotype_train.txt.zip`
- `ML_yeast_dna_imputation/data/raw/yeast_genotype_test.txt.zip`

En el notebook `ML_yeast_dna_imputation/notebooks/preprocessing.ipynb` se realiza el **preprocesamiento** de los datos, generando conjuntos de **train** y **test reducidos**, además de subconjuntos de test con diferentes niveles de pérdida de datos (10%, 20%, 30%, 40%). Estos conjuntos de datos se guardan en formato `.parquet` en la carpeta `ML_yeast_dna_imputation/data/processed` para su uso en los diferentes modelos implementados.

---

## Estructura del Proyecto

El proyecto está organizado en los siguientes directorios:

### **`data/`** 
Contiene los datos de entrada y salida:

- **`data/generated/`**: Subcarpetas específicas para cada modelo, con los datasets imputados por cada método.
- **`data/processed/`**: Conjuntos de datos preprocesados y reducidos, listos para ser utilizados en el entrenamiento y prueba de los modelos.
- **`data/raw/`**: Archivos comprimidos con los datos originales de gran dimensionalidad.

### **`models/`** 
Subcarpetas para cada arquitectura donde se almacenan los modelos entrenados en formato `.h5`.

### **`notebooks/`** 
Contiene todos los notebooks utilizados, organizados por tarea y/o arquitectura:

- **`notebooks/original_SDCA/`**: Notebooks originales del modelo **Sparse Convolutional Denoising Autoencoder (SDCA)** para el entrenamiento y test.
- **`notebooks/reduced_SDCA/`**: Notebooks con el modelo **SDCA** utilizando el conjunto de datos reducido.
- **`notebooks/KNN_yeast.ipynb`**: Notebook donde se implementa el entrenamiento y test con **KNN** para la imputación.
- **`notebooks/RF_unique_model.ipynb`**: Notebook donde se entrena y prueba un modelo de **Random Forest** tradicional, entrenando un solo modelo para todo el conjunto de datos.
- **`notebooks/RF_yeast.ipynb`**: Notebook donde se entrena un **Random Forest** para predecir valores faltantes en columnas individuales del conjunto de test, utilizando un modelo independiente por cada columna.
- **`notebooks/XGBoost.ipynb`**: Notebook donde se realiza el entrenamiento y prueba con el modelo de **XGBoost**.
- **`notebooks/attention_autoencoder_yeast.ipynb`**: Implementación de un **autoencoder con atención** para imputar valores faltantes en el conjunto de datos reducido.
- **`notebooks/attention_autoencoder_yeast_amplified.ipynb`**: Variante del autoencoder con atención, utilizando una arquitectura más compleja o parámetros ajustados para mejorar la imputación.

---

## Ejecución del Proyecto

### Preprocesamiento
1. Ejecutar el notebook `preprocessing.ipynb` para generar los conjuntos de **train** y **test reducidos**, así como los conjuntos de test con diferentes niveles de pérdida de datos.
2. Los datos preprocesados se guardarán en la carpeta `data/processed/` en formato `.parquet`.

### Entrenamiento y Evaluación de Modelos
1. Ejecutar los notebooks correspondientes a cada método de imputación:
   - **KNN**: `notebooks/KNN_yeast.ipynb`
   - **Random Forest (con un solo modelo)**: `notebooks/RF_unique_model.ipynb`
   - **Random Forest (por columnas)**: `notebooks/RF_yeast.ipynb`
   - **XGBoost**: `notebooks/XGBoost.ipynb`
   - **Autoencoders con Atención**: `notebooks/attention_autoencoder_yeast.ipynb` y `notebooks/attention_autoencoder_yeast_amplified.ipynb`
   
2. Los modelos entrenados se almacenarán en la carpeta `models/` en formato `.h5`.
2. Los datasets imputados se almacenarán en la carpeta `data/generates` en el subdirectorio correspondiente a cada arquitectura, en formato .parquet.

### Evaluación Comparativa
- Los resultados de la imputación se evaluarán en términos de métricas como **accuracy**, **F1-score**, **precision**, y **recall**, y se compararán entre los diferentes enfoques (comparativa realizada en el documento de desarrollo del TFM).

---





