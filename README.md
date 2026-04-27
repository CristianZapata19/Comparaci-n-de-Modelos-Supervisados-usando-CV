# Predicción de Precios de Bienes Raíces

## Descripción del Dataset

El dataset utilizado es **"Real Estate Price Prediction"**, disponible públicamente en plataformas como Kaggle. Contiene información sobre transacciones de bienes raíces en una zona específica de Taiwán.

**Características del dataset:**
- **Total de registros:** 414 transacciones
- **Variables predictoras (6 numéricas):**
  - `X1 transaction date`: Fecha de la transacción
  - `X2 house age`: Antigüedad de la casa (años)
  - `X3 distance to the nearest MRT station`: Distancia a la estación de MRT más cercana (metros)
  - `X4 number of convenience stores`: Número de tiendas de conveniencia cercanas
  - `X5 latitude`: Latitud de la ubicación
  - `X6 longitude`: Longitud de la ubicación
- **Variable objetivo:** `Y house price of unit area` (precio por unidad de área) - numérica continua

El dataset no presenta valores nulos y todas las variables son numéricas, lo que facilita su procesamiento.

## Objetivo del Trabajo

El objetivo principal es desarrollar y comparar modelos supervisados de regresión para predecir el precio por unidad de área de propiedades inmobiliarias, utilizando las 6 variables predictoras disponibles.

**Etapas del proyecto:**

1. **Preparación del dataset:**
   - División estratificada por cuantiles (70/15/15)
   - Estandarización de variables con StandardScaler

2. **Modelos evaluados:**
   - LinearRegression
   - Ridge (regularización L2, alpha=1.0)
   - Lasso (regularización L1, alpha=1.0)
   - DecisionTreeRegressor (max_depth=4)

3. **Evaluación:**
   - Métrica principal: RMSE (Root Mean Square Error)
   - Validación cruzada K-Fold (K=5)
   - Evaluación final en conjunto de prueba

## Principales Hallazgos y Conclusiones

### Resultados de los Modelos

| Modelo | Train RMSE | Val RMSE | Test RMSE | Train R2 | Test R2 |
|--------|------------|----------|-----------|----------|---------|
| LinearRegression | 7.96 | 8.54 | 12.11 | 0.6099 | 0.4351 |
| Ridge | 7.96 | 8.57 | 12.12 | 0.6102 | 0.4325 |
| Lasso | 8.75 | 9.55 | 12.51 | 0.5293 | 0.4019 |
| DecisionTreeRegressor | 5.14 | 9.11 | 10.90 | 0.8378 | 0.5427 |

### Validación Cruzada (K=5)

| Modelo | CV Mean RMSE | CV Std RMSE |
|--------|--------------|--------------|
| LinearRegression | 8.18 | 0.25 |
| Ridge | 8.17 | 0.26 |
| Lasso | 9.55 | 0.31 |
| DecisionTreeRegressor | 7.38 | 1.03 |

### Conclusiones Principales

1. **Mejor modelo:** El DecisionTreeRegressor presentó el mejor rendimiento en términos de capacidad predictiva general, con un Test RMSE de 10.90 y un Test R2 de 0.5427.

2. **Sobreajuste moderado:** Se evidenció un sobreajuste en el árbol de decisión, con una diferencia significativa entre su CV Mean RMSE (7.38) y su Test RMSE (10.90), lo que indica que el modelo capturó ruido específico de los datos de entrenamiento.

3. **Estabilidad de modelos lineales:** Los modelos lineales mostraron mayor estabilidad (menor desviación estándar en validación cruzada), aunque su rendimiento absoluto fue ligeramente inferior.

4. **Recomendaciones futuras:**
   - Ajustar hiperparámetros del árbol de decisión (reducir max_depth, aumentar min_samples_split)
   - Considerar modelos ensemble como Random Forest o Gradient Boosting
   - Incrementar el tamaño del dataset para mejorar la representatividad

**Conclusión final:** El DecisionTreeRegressor es válido como la mejor opción entre los modelos evaluados, pero su error real esperado en producción se aproxima más a 12.14 puntos de RMSE, siendo esta la métrica a considerar para la toma de decisiones.
