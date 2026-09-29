# Inferencia Bayesiana sobre un Parámetro Bernoulli

**Autor:** Matías Ccolque A.  
**Curso:** Machine Learning  
**Tarea:** 2


##  Descripción general

Este proyecto explora la **inferencia bayesiana** aplicada a la estimación de un parámetro desconocido `θ` en un modelo **Bernoulli**. El objetivo es analizar cómo la distribución posterior de `θ` evoluciona a medida que se incorpora más información (más observaciones), y cómo la **elección del prior** influye en dicha evolución.

Se trabaja con una muestra simulada de `n = 1000` observaciones Bernoulli con parámetro verdadero `θ_true = 0.7`, y se estudian cuatro priors conjugados distintos:

| Prior        | Interpretación                              |
|--------------|---------------------------------------------|
| `Beta(1,1)`  | Prior uniforme (sin información previa)     |
| `Beta(5,1)`  | Prior sesgado hacia valores altos de θ      |
| `Beta(1,5)`  | Prior sesgado hacia valores bajos de θ      |
| `Beta(10,10)`| Prior concentrado alrededor de θ = 0.5      |

---

##  Objetivos

1. **Implementar** el cálculo de la distribución posterior conjugada Beta-Bernoulli.
2. **Visualizar** cómo la posterior se concentra en torno al valor real `θ = 0.7` conforme crece el tamaño muestral `k`.
3. **Comparar** el efecto de distintos priors en la forma de la posterior.
4. **Analizar** la evolución de tres estimadores clave:
   - **Media posterior** (estimador bayesiano bajo pérdida cuadrática).
   - **MAP** (máximo a posteriori).
   - **MLE** (máximo verosímil, sin influencia del prior).
5. **Construir intervalos creíbles al 95 %** y observar su contracción con `k`.

---

##  Fundamento teórico

### Modelo
Para cada observación `X_i ~ Bernoulli(θ)`, con verosimilitud:

$$p(X \mid \theta) = \theta^{s}(1-\theta)^{k-s}$$

donde `s` es el número de éxitos y `k` el número de ensayos.

### Prior conjugado
Se usa un prior **Beta(α, β)**, conjugado del modelo Bernoulli, lo que permite obtener una posterior analítica:

$$p(\theta \mid X) = \text{Beta}(\alpha + s,\ \beta + k - s)$$

### Estimadores
- **Media posterior:** $\mathbb{E}[\theta \mid X] = \dfrac{\alpha + s}{\alpha + \beta + k}$
- **MAP:** moda de la distribución Beta posterior.
- **MLE:** $\hat{\theta}_{MLE} = \dfrac{s}{k}$
- **Intervalo creíble al 95 %:** cuantiles 0.025 y 0.975 de la Beta posterior.

---

## Análisis desarrollados

### 1. Posteriores por prior y tamaño muestral
Para cada prior se grafican las 8 posteriores correspondientes a `k ∈ {1, 5, 10, 25, 50, 100, 500, 1000}`, mostrando cómo la distribución se estrecha y se centra en `θ = 0.7`.

### 2. Comparación entre priors
Se contrastan los cuatro priors en dos escenarios: `k = 10` (poca información) y `k = 1000` (mucha información). Se observa que:

- Con **poca información**, el prior domina la forma de la posterior.
- Con **mucha información**, todas las posteriores convergen al mismo valor, evidenciando la **consistencia bayesiana** y el principio de que los datos superan la influencia del prior.

### 3. Evolución de estimadores
Para cada prior se grafica la evolución de:
- Media posterior
- MAP
- MLE
- Intervalo creíble al 95 %

Se observa que:
- El **MLE es más errático** en valores pequeños de `k` (incluso llegando a 0 o 1).
- La **media posterior** y el **MAP** son más estables gracias al efecto regularizador del prior.
- Conforme `k → 1000`, los tres estimadores convergen al valor real `θ = 0.7`.

##  Tecnologías utilizadas

- **Python 3**
- **NumPy** — simulación y operaciones vectorizadas
- **SciPy** — distribución Beta (`beta.pdf`, `beta.ppf`)
- **Matplotlib** — visualización de posteriores y estimadores

##  Conclusiones principales

1. La **conjugación Beta-Bernoulli** permite obtener la posterior de forma analítica, sin necesidad de métodos numéricos como MCMC.
2. El **prior pierde relevancia** a medida que crece el tamaño muestral: con `k = 1000` las cuatro posteriores son prácticamente idénticas.
3. La **media posterior** ofrece un compromiso natural entre la información previa y los datos observados.
4. El **MAP** puede comportarse de forma distinta a la media cuando la posterior es asimétrica (especialmente con priors sesgados y `k` pequeño).
5. El **MLE** es un caso límite de la posterior cuando el prior es no informativo o `k → ∞`.
6. Los **intervalos creíbles** se contraen rápidamente, reflejando la reducción de la incertidumbre sobre `θ`.


