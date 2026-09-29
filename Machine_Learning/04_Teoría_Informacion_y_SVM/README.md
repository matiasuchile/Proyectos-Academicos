# Tarea 4 ML: Teoría de la Información y SVM

Análisis de selección de modelos mediante AIC, BIC e información mutua, junto con Máquinas de Soporte Vectorial (SVM) aplicados al dataset `heart.csv` para predecir falla cardíaca.

## Contenido

- **`Tarea_4_Machine_Learning.pdf`**: Documento con el desarrollo completo.

## Resumen

1. Marco teórico de entropía, información mutua y divergencia KL.
2. Criterios de información AIC y BIC.
3. Selección de variables vía información mutua (M1, M2, M3).
4. Cálculo de AIC/BIC para Regresión Logística y LDA.
5. SVM: margen duro, margen suave, formulación dual y kernels.
6. SVM con hiperparámetros por defecto y optimización con GridSearchCV.

## Modelos Comparados

| Modelo | Descripción |
|--------|-------------|
| M1 | Todas las variables (15 tras dummy encoding) |
| M2 | Top 5 variables por información mutua |
| M3 | 5 variables con menor información mutua |
| LDA | Análisis Discriminante Lineal |
| SVM | Kernel RBF optimizado |

## Hallazgos Principales

- **M1** es preferido por AIC y BIC (mejor ajuste compensa mayor complejidad).
- **SVM con kernel RBF** obtiene el mejor rendimiento predictivo: AUC-test = 0.9464, F1-test = 0.8986.
- La configuración por defecto de `SVC` (RBF, C=1) ya es óptima para este dataset.
- Existe tensión entre AIC/BIC (favorecen parsimonia) y métricas de test (favorecen flexibilidad).

