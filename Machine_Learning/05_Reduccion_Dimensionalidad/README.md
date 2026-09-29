# Tarea 5 ML: Reducción de Dimensionalidad

Estudio de métodos de reducción de dimensionalidad lineal (PCA, Kernel PCA, Fisher LDA) y no lineal (Isomap, t-SNE, UMAP) aplicados al dataset Heart Failure Prediction.

## Contenido

- **`Tarea_5_Machine_Learning.pdf`**: Documento con el desarrollo completo.

## Resumen

1. PCA sobre variables numéricas estandarizadas (d* = 5 componentes para 90% de varianza).
2. Kernel PCA con kernels RBF y polinomial.
3. Fisher LDA para separación supervisada de clases.
4. Isomap, t-SNE y UMAP con análisis de sensibilidad a hiperparámetros.

## Hallazgos Principales

- **PCA:** PC1 y PC2 explican 52% de la varianza; solapamiento entre clases.
- **Fisher LDA:** Mejor separación que PC1 en una sola dimensión.
- **UMAP:** Mayor pureza por clase en sus proyecciones (especialmente con `min_dist=0.0`).
- **t-SNE:** Clusters compactos, óptimo con `perplexity=30`.
- **Isomap:** Menor separación entre clases.

## Conclusión

- **Visualización:** t-SNE y UMAP son los más informativos.
- **Interpretabilidad:** Fisher LDA es el más útil.
- **Clasificación:** SVM con kernel RBF sobre variables originales sigue siendo la mejor referencia.

