# Myopia-Prediction
Prediction of different types of myopia with several different Machine/Deep learning models using a dataset made by medical students from UNAV

## Project Structure & Phases

The project is sequentially structured into the following development blocks:

### 1. Data Preprocessing & Cleaning
* Initial analysis of missing values and dataset dimensions.
* Controlled merging of predictor variables (`X_train`) and labels (`Y_train`) to ensure consistency during the cleaning process.
* Strict removal of irrelevant or empty columns (such as `fecha` and any features with more than 40% missing values, e.g., `hº act.cerca sem`).

### 2. Part 1: Binary Myopia Classification (PyTorch Modeling)
* **Objective:** Predict whether a student has myopia or not (column `M`: YES/NO).
* **Architecture:** A sequential Artificial Neural Network (ANN) built from scratch using **PyTorch** (`nn.Sequential`, `nn.Linear`, `nn.LeakyReLU`, `nn.Dropout`).
* **Optimization:** Used `BCEWithLogitsLoss` while configuring the `pos_weight` parameter to mitigate class imbalance (which follows an approximate 2-to-1 ratio). Implemented the Adam optimizer with weight decay (`weight_decay`).
* **Validation:** Applied **Stratified K-Fold Cross Validation (5 Folds)** to guarantee statistical robustness.
* **Ensemble Model:** Designed a final soft-voting strategy that averages the probabilities of the 5 models trained during cross-validation, achieving high predictive stability.

### 3. Part 2: High Myopia Prediction (MM)
* **Objective:** Specifically classify cases of high myopia ("Miopía Magna", representing more than six diopters).
* **Model:** A **Random Forest** classifier (`RandomForestClassifier`) with balanced class weights.
* **Imbalance Techniques:** Implemented oversampling techniques via **SMOTE** (`imblearn`) to address the severe shortage of positive High Myopia cases.
* **Clinical Adjustment:** Manually optimized the decision threshold (probability > 0.20) to make the model more sensitive and aggressive when detecting positive cases within a medical context.

### 4. Part 3: Multiclass Prediction of Combined Variables
* **Objective:** Hierarchical classification of combined profiles (`Combo`).
* **Model:** A **Random Forest** scaled to 1,000 estimators (`n_estimators=1000`) with unconstrained depth and native balancing to capture complex, multidimensional patterns.

### 5. Part 4: Complete Sequential Inference Pipeline
* **Objective:** Construction of an integrated hierarchical system that stacks the predictive outputs from previous phases.
* **Logic:** Utilizes the PyTorch model's prediction to initially differentiate between healthy and myopic patients, subsequently applying the High Myopia classifier and a final optimized Random Forest (`max_depth=5`) to subclassify the remaining categories.
* **Final Inference:** Automated generation of the comprehensive predictions, formatted and ready to be exported into flat files (`predicciones_grupo.txt`).

## Technologies & Libraries Used

* **Deep Learning Framework:** PyTorch (`torch`, `torch.nn`, `torch.optim`)
* **Machine Learning Libraries:** Scikit-Learn (`sklearn.ensemble`, `sklearn.model_selection`, `sklearn.metrics`)
* **Sampling Techniques:** Imbalanced-Learn (`imblearn.over_sampling.SMOTE`)
* **Data Processing:** Pandas, NumPy
* **Data Visualization:** Matplotlib, Seaborn
--------------------------------------------------------------------------------------------------------------------------------------------------

## Estructura y Fases del Proyecto

El trabajo está estructurado de manera secuencial siguiendo los siguientes bloques de desarrollo:

### 1. Preprocesamiento y Limpieza de Datos
* Análisis inicial de valores faltantes y dimensiones de los conjuntos de datos.
* Fusión controlada de variables predictoras (`X_train`) y etiquetas (`Y_train`) para asegurar consistencia en la limpieza.
* Eliminación estricta de columnas irrelevantes o vacías (como `fecha` y aquellas con más de un 40% de valores nulos, por ejemplo, `hº act.cerca sem`).

### 2. Parte 1: Clasificación Binaria de Miopía (Modelado con PyTorch)
* **Objetivo:** Predecir si el estudiante presenta miopía o no (columna `M`: YES/NO).
* **Arquitectura:** Red Neuronal Artificial (ANN) secuencial construida desde cero utilizando **PyTorch** (`nn.Sequential`, `nn.Linear`, `nn.LeakyReLU`, `nn.Dropout`).
* **Optimización:** Uso de `BCEWithLogitsLoss` configurando el parámetro `pos_weight` para mitigar el desbalanceo de clases (proporción aproximada 2 a 1). Optimizador Adam con decaimiento de peso (`weight_decay`).
* **Validación:** Implementación de **Stratified K-Fold Cross Validation (5 Folds)** para asegurar la robustez estadística.
* **Modelo Ensamble:** Estrategia de votación final (Voting) que promedia las probabilidades de los 5 modelos entrenados en la validación cruzada, alcanzando una alta estabilidad predictiva.

### 3. Parte 2: Predicción de Miopía Magna (MM)
* **Objetivo:** Clasificar de manera específica los casos de miopía magna (más de seis dioptrías).
* **Modelo:** Clasificador **Random Forest** (`RandomForestClassifier`) con pesos de clase balanceados.
* **Técnicas de Balanceo:** Implementación de técnicas de sobremuestreo mediante **SMOTE** (`imblearn`) debido a la escasez crítica de casos positivos de Miopía Magna.
* **Ajuste Clínico:** Optimización manual del umbral de decisión (probabilidad > 0.20) para volver el modelo más sensible y agresivo en la detección de casos positivos en el entorno médico.

### 4. Parte 3: Predicción Multiclase de Variables Combinadas
* **Objetivo:** Clasificación jerárquica de perfiles combinados (`Combo`).
* **Modelo:** **Random Forest** escalado a 1000 estimadores (`n_estimators=1000`) con profundidad libre y balanceo nativo para capturar patrones multidimensionales complejos.

### 5. Parte 4: Pipeline Secuencial de Inferencia Completo
* **Objetivo:** Construcción de un sistema jerárquico integrado que combina las salidas predictivas de las fases anteriores.
* **Lógica:** Utiliza la predicción del modelo de PyTorch para discernir inicialmente entre sanos y miopes, aplicando posteriormente el clasificador de Miopía Magna y un Random Forest final optimizado (`max_depth=5`) para subclasificar las categorías restantes.
* **Inferencia Final:** Generación automatizada de las predicciones completas listas para exportación a archivos planos (`predicciones_grupo.txt`).

## Tecnologías y Librerías Utilizadas

* **Framework de Deep Learning:** PyTorch (`torch`, `torch.nn`, `torch.optim`)
* **Librerías de Machine Learning:** Scikit-Learn (`sklearn.ensemble`, `sklearn.model_selection`, `sklearn.metrics`)
* **Técnicas de Muestreo:** Imbalanced-Learn (`imblearn.over_sampling.SMOTE`)
* **Procesamiento de Datos:** Pandas, NumPy
* **Visualización Gráfica:** Matplotlib, Seaborn
