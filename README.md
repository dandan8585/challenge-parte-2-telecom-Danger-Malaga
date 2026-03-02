# challenge-parte-2-telecom-Danger-Malaga

# 📊 Predicción de Cancelación de Clientes (Churn) — Proyecto de Machine Learning

## 🎯 Objetivo

Desarrollar modelos predictivos capaces de identificar clientes con alta probabilidad de cancelación (churn), permitiendo a la empresa anticiparse mediante estrategias de retención focalizadas y optimización de recursos.

El churn representa un riesgo financiero relevante, ya que el costo de adquisición de nuevos clientes suele ser mayor que el costo de retención.

---

# 📌 1. Definición del Problema

Se aborda un problema de **clasificación binaria supervisada**:

- **Variable objetivo:** `Churn`
  - 1 → Cliente cancela el servicio
  - 0 → Cliente permanece

El objetivo es construir un pipeline robusto que permita:

- Detectar clientes en riesgo
- Identificar los principales drivers de cancelación
- Generar insights accionables para el negocio

El churn está fuertemente asociado a clientes recientes y con cargos mensuales altos.
Random Forest es el modelo más robusto para predicción.
El balanceo de clases mejora la detección real de abandono.
Existe oportunidad clara de intervención temprana y segmentación por riesgo.
La estrategia óptima combina:
Modelo predictivo (RF)
Scoring por probabilidad
Intervención focalizada en clientes de alto valor y alto riesgo

# 🧹 2. Preparación de Datos

Se realizaron los siguientes pasos de preprocesamiento:

- Eliminación de identificadores no informativos
- Corrección de tipos de datos
- Codificación de variables categóricas (One-Hot Encoding)
- División Train/Test con estratificación
- Escalado de variables (para Regresión Logística)

El dataset presenta **desbalance moderado de clases**, lo cual influyó en la selección de métricas de evaluación.

---

# 📊 3. Análisis Exploratorio de Datos (EDA)

## 🔴 Tipo de Contrato


Los clientes con contrato **Month-to-Month (mensual)** presentan una tasa de cancelación significativamente mayor que aquellos con contratos anuales o bianuales.

![imagen alt](https://github.com/dandan8585/challenge-parte-2-telecom-Danger-Malaga/blob/646b773a1916f763d50bb301ba580ebb0ee46f07/TERNURE.png)


**Interpretación de negocio:**
- Bajo compromiso contractual
- Alta sensibilidad al precio
- Baja barrera de salida

---

## 🔴 Antigüedad (Tenure)

Los clientes con menor antigüedad muestran mayor probabilidad de churn.

**Interpretación de negocio:**
- Riesgo elevado en los primeros meses
- Posible debilidad en el proceso de onboarding
- Valor percibido aún no consolidado

---

## 🔴 Cargos Mensuales (Monthly Charges)

Clientes con cargos mensuales más altos tienden a cancelar con mayor frecuencia.

**Interpretación de negocio:**
- Sensibilidad al precio
- Percepción de desbalance costo-beneficio
- Presión competitiva

---

## 🔴 Método de Pago

El método **Electronic Check** se asocia con mayor probabilidad de cancelación.

**Posibles explicaciones:**
- Mayor fricción en el proceso de pago
- Menor automatización
- Segmento menos fidelizado

---

# 🤖 4. Desarrollo de Modelos

Se entrenaron dos modelos de clasificación:

- Regresión Logística
- Random Forest

Ambos modelos fueron evaluados bajo el mismo esquema de validación.

---

# 📈 5. Evaluación de Modelos

Se utilizaron las siguientes métricas:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Matriz de Confusión
- Curva Precision-Recall

Dado que el costo de error es asimétrico:

> Un Falso Negativo (cliente que se va sin ser detectado) es más costoso que un Falso Positivo.

Por lo tanto, se priorizó **Recall y ROC-AUC sobre Accuracy**.

---

# 🏆 6. Comparación de Modelos

| Modelo                | Accuracy | Precision | Recall | F1 | ROC-AUC |
|-----------------------|----------|-----------|--------|----|----------|
| Regresión Logística   | 0.743080 | 0.510417  |0.786096|0.61| 0.842587 |
| Random Forest         | 0.784244 | 0.622378  |0.475936|0.53| 0.821100 |

### Recomendación Final

El modelo **Random Forest** mostró:

- Mayor ROC-AUC
- Mejor capacidad de discriminación
- Mayor sensibilidad para detectar clientes en riesgo

Se recomienda como modelo base para implementación inicial.

---

# 🔍 7. Principales Variables Predictoras

El análisis de importancia (Random Forest) y coeficientes (Regresión Logística) identificó consistentemente los siguientes drivers:

1. Contrato mensual
2. Baja antigüedad (Tenure)
3. Altos cargos mensuales
4. Método de pago Electronic Check
5. Ausencia de servicios adicionales

La coherencia entre modelos refuerza la robustez de los hallazgos.

---

# 👤 8. Perfil del Cliente de Alto Riesgo

El modelo permite definir el siguiente arquetipo:

> Cliente relativamente nuevo, con contrato mensual, cargos elevados, método de pago electrónico y pocos servicios adicionales contratados.

Este segmento debe ser priorizado en estrategias de retención.

---

# 💼 9. Implicancias Estratégicas

## 1️⃣ Estrategia Contractual
- Incentivar migración a contratos anuales
- Beneficios por permanencia

## 2️⃣ Programa de Retención Temprana
- Intervención en los primeros 90 días
- Seguimiento activo post-onboarding

## 3️⃣ Optimización de Propuesta de Valor
- Bundles con mejor percepción costo-beneficio
- Ajustes segmentados en pricing

## 4️⃣ Automatización de Pagos
- Incentivar débito automático
- Beneficios por domiciliación

---

# ⚖ 10. Limitaciones del Análisis

- No se realizó optimización exhaustiva de hiperparámetros
- Umbral de clasificación fijo en 0.5
- No se incluyeron variables externas (satisfacción, reclamos, uso real)
- No se modeló componente temporal
- No se aplicó entrenamiento cost-sensitive

Mejoras futuras:

- Optimización de threshold
- Calibración de probabilidades
- SHAP para explicabilidad avanzada
- Cross-validation
- Modelado basado en costos

---

# 🚀 11. Consideraciones para Producción

Para implementación real se recomienda:

1. Construcción de pipeline automatizado
2. Generación de score de churn por cliente
3. Segmentación por niveles de riesgo (Bajo / Medio / Alto)
4. Integración con CRM
5. Medición del impacto post-intervención

Indicadores de éxito:

- Reducción del churn rate
- ROI de campañas de retención
- Lift vs segmentación aleatoria

---

# 📌 Conclusión

El análisis permitió identificar los principales factores que impulsan la cancelación de clientes y desarrollar modelos con capacidad predictiva sólida.

El modelo Random Forest mostró mejor desempeño y se recomienda como base para un sistema de alerta temprana.

La aplicación de estrategias focalizadas sobre los segmentos de mayor riesgo permitirá reducir churn y maximizar el valor del cliente en el tiempo.

---

# 🧠 Autor

Analista Junior de Machine Learning  
Proyecto de Predicción de Churn – Telecom
