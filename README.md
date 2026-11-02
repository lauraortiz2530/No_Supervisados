# Aprendizaje No Supervisado: hábitos de vida y bienestar físico

**Autora:** Laura Ortiz Franco

---

## Tabla de contenido

1. [Objetivo](#objetivo)
2. [Dataset](#dataset)
3. [Variables incluidas](#variables-incluidas)
4. [Metodología](#metodología)
5. [Resultados](#resultados)
6. [Conclusiones](#conclusiones)

---

## Objetivo

Identificar posibles patrones y agrupamientos dentro de datos sobre hábitos de vida y bienestar físico, mediante técnicas de aprendizaje no supervisado como PCA y K-Means.

---

## Dataset

El conjunto de datos utilizado se titula **"Health and Lifestyle Data for Regression"**, disponible públicamente en [Kaggle](https://www.kaggle.com/datasets/sidharth178/health-and-lifestyle-data-for-regression).

Contiene información sobre hábitos de vida y bienestar físico de diferentes individuos. Las variables incluyen factores como edad, ejercicio, dieta, sueño, consumo de alcohol y tabaco, entre otros.

Se utilizó un conjunto de datos limpio y exclusivamente numérico, cumpliendo con los requerimientos del trabajo (5–10 variables).

---

## Variables incluidas

| Variable                | Descripción                                      | Tipo     |
|-------------------------|--------------------------------------------------|----------|
| **Age**                 | Edad del individuo (en años)                     | Numérica |
| **BMI**                 | Índice de masa corporal (kg/m²)                  | Numérica |
| **Exercise_Frequency**  | Frecuencia de ejercicio semanal (días/semana)    | Numérica |
| **Diet_Quality**        | Puntuación de calidad de la dieta (escala 1–10)  | Numérica |
| **Sleep_Hours**         | Promedio de horas de sueño por día               | Numérica |
| **Smoking_Status**      | Nivel de consumo de tabaco (escala 0–10)         | Numérica |
| **Alcohol_Consumption** | Nivel de consumo de alcohol (escala 0–10)        | Numérica |
| **Health_Score**        | Puntuación general de salud (escala 0–100)       | Numérica |

---

## Metodología

### 1. Preparación de los datos
- **Estandarización:** todas las variables fueron escaladas mediante `StandardScaler` para evitar sesgos por diferencias de magnitud.

### 2. Reducción de dimensionalidad y visualización
- **Análisis PCA:** se aplicó Análisis de Componentes Principales y se generó un *scree plot* que muestra la proporción de varianza explicada por cada componente. Las dos primeras componentes capturan la mayor parte de la información y se usaron para proyectar los datos en un plano bidimensional.
- **Visualización de patrones:** se realizó un diagrama de dispersión con las dos primeras componentes principales para observar posibles agrupamientos naturales.

### 3. Selección de variables
- Se aplicó un análisis de correlación y un modelo Random Forest para identificar las variables con mayor relevancia sobre `Health_Score`.
- Las variables menos significativas fueron eliminadas.

### 4. Agrupamiento con K-Means
Se aplicó el algoritmo sobre tres versiones del dataset:

| Versión | Descripción |
|---------|-------------|
| Original | Dataset sin transformaciones adicionales |
| PCA | Dataset reducido a 2 componentes |
| Variables seleccionadas | Dataset tras la selección de variables |

En cada caso se probaron distintos valores de K (2 a 6), evaluando los resultados con el **método del codo** y el **Silhouette Score**.

---

## Resultados

| Versión del dataset | Silhouette Score | Observación |
|---------------------|------------------|-------------|
| PCA (K = 2) | ~0.39 | Mejor separación entre grupos |
| Original | ~0.15 | Estructura menos definida |
| Variables seleccionadas | ≈ 0.13 | No mejoró sustancialmente el agrupamiento |

- El número óptimo de clusters fue **K = 2** en general, lo que indica la existencia de dos grupos principales en los datos.

---

## Conclusiones

El PCA fue el método más efectivo para representar y agrupar los datos de forma interpretable, mientras que la selección de variables no aportó mejoras relevantes a la calidad del agrupamiento.