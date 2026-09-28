# Predicción de Ratings de Reseñas Amazon con Regresión Regularizada

Implementación desde cero y comparación de modelos de regresión lineal 
(MCO, Ridge, Lasso, ElasticNet) para predecir la calificación (1-5 estrellas) 
de reseñas de instrumentos musicales en Amazon.

## Objetivo
Predecir el `rating` de una reseña a partir de:
- verified_purchase
- helpful_vote
- length_of_review
- month, year (en la versión extendida)

## Técnicas aplicadas
- Regresión Lineal por Mínimos Cuadrados Ordinarios (implementación propia con NumPy)
- Ridge (regularización L2)
- Lasso (regularización L1)
- ElasticNet (L1 + L2)
- Escalamiento con StandardScaler
- Análisis de correlación entre features

## Resultados principales
| Modelo     | MSE Train | MSE Test | R² Test |
|------------|-----------|----------|---------|
| MCO        | 1.641     | 1.635    | 0.009   |
| Ridge      | 1.638     | 1.631    | 0.012   |
| Lasso      | 1.638     | 1.632    | 0.011   |
| ElasticNet | 1.638     | 1.631    | 0.012   |

*El bajo R² sugiere que las variables numéricas por sí solas explican poco 
el rating — se requeriría NLP sobre el texto de la reseña.*

## Aprendizajes clave
- Los ratings están fuertemente sesgados hacia 4-5 estrellas (promedio 4.25)
- La regularización apenas mejora el MCO porque el modelo base ya es simple
- El escalamiento no cambia el rendimiento del MCO (invariancia a escala)