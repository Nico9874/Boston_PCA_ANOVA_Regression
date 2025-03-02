# Análisis del Mercado de Viviendas en Boston

## Descripción  
Este proyecto analiza el **mercado de viviendas en Boston** utilizando técnicas de **regresión lineal** para predecir el valor medio de las viviendas (**median_value**). Se aplican diversos métodos estadísticos como **ANOVA, PCA y correlaciones** para seleccionar las variables más relevantes y evaluar el desempeño del modelo en datos de prueba.

## Tecnologías utilizadas  
- **Lenguaje / Framework:** R  
- **Librerías o paquetes clave:**  
  - tidyverse  
  - dplyr  
  - MASS  
  - class  
  - corrplot  
  - ggplot2  
  - gridExtra  
  - GGally  
  - nortest  
  - lmtest  
  - olsrr  
  - vioplot  
- **Algoritmos o modelos utilizados:**  
  - ANOVA  
  - PCA  
  - Regresión Lineal Múltiple y Simple  

## Resultados clave  

### **Selección de Variables para el Modelo de Regresión**  
Se seleccionaron las siguientes variables por su relevancia estadística y conceptual:

| Variable                 | Justificación Estadística                                                 | Importancia Práctica                              |
|-------------------------|-------------------------------------------------------------------------|-------------------------------------------------|
| `rooms_squared_new`     | Correlación alta con median_value (0.718), p-valor ANOVA = 0.0274, carga alta en PCA (0.390) | Representa el tamaño ajustado de la vivienda    |
| `lower_status_log_new`  | Correlación negativa fuerte (-0.815), carga negativa en PCA (-0.506)    | Captura el impacto del nivel socioeconómico     |
| `urban_ratio`           | Carga positiva en PCA (0.416), correlación moderada con median_value (0.360) | Refleja el grado de urbanización                |
| `teacher_ratio_log_new` | p-valor ANOVA = 0.00872, correlación moderada (-0.503)                 | Representa la calidad educativa en la zona      |

### **Regresión Lineal Múltiple**  
- **Modelo:** `median_value ~ rooms_squared_new + lower_status_log_new + urban_ratio + teacher_ratio_log_new`  
- **Desempeño del modelo:**  
  - Explica el **77.03%** de la variabilidad en los precios de las viviendas.  
  - **Error estándar residual:** 4.38.  
  - **Todas las variables fueron estadísticamente significativas** (p < 0.05).  
- **Limitaciones detectadas en los residuos:**  
  - **Kolmogorov-Smirnov:** Los residuos **no siguen una distribución normal** (p < 0.05).  
  - **Breusch-Pagan:** Indica **heteroscedasticidad** (p = 0.015).  
  - **Durbin-Watson:** No se encontró autocorrelación en los residuos (p = 0.8686).  

### **Regresión Lineal Simple**  
- **Modelo:** `median_value ~ lower_status_log_new`  
- **Desempeño del modelo:**  
  - Explica el **68.91%** de la variabilidad en median_value.  
  - **Error estándar residual:** 5.08.  
  - El coeficiente de `lower_status_log_new` fue **negativo y significativo**.  

### **Validación del Modelo**  
- **Evaluación con conjunto de prueba (`data_test`)**:  
  - Explica el **71.86%** de la variabilidad en datos no vistos.  
  - **RMSE = 4.96**, **MAE = 3.55**.  
  - **Puntos influyentes detectados** mediante distancia de Cook, indicando posible inestabilidad del modelo.  

## Conclusión  
 **El modelo de regresión múltiple es adecuado para predecir `median_value`**, explicando un alto porcentaje de la variabilidad en los datos. Sin embargo, la falta de normalidad y homoscedasticidad en los residuos podrían afectar la precisión de las estimaciones.  
 **Para mejorar su aplicabilidad, se recomienda realizar transformaciones en las variables o considerar modelos más robustos** que permitan corregir estas limitaciones.
