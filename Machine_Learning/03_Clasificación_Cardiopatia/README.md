# Tarea3_ML_Clasificacion_Cardiopatia

Análisis de modelos de Machine Learning para predecir cardiopatías usando Regresión Logística, KNN, Naive Bayes, LDA y Perceptrón.

## Contenido

- **`Tarea3ML.ipynb`**: Notebook con el desarrollo completo.

## Resumen

1. Preprocesamiento y división de datos (80/20 y 60/40).
2. Modelo baseline con Regresión Logística.
3. Curvas ROC y cálculo de AUC.
4. Optimización de hiperparámetros con `GridSearchCV`.
5. Análisis de coeficientes y normas.
6. Comparación con otros clasificadores.
7. Selección de características (categóricas, numéricas, todas).

## Hallazgos Principales

- `ST_Slope_Up` es la variable más influyente.
- Gaussian NB y LDA superan ligeramente a la Regresión Logística.
- Usar todas las variables da el mejor rendimiento.
- `class_weight={0:1, 1:5}` mejora el Recall (reduce Falsos Negativos).

