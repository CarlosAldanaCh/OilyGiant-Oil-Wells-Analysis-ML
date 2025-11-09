# Predicción de Beneficios y Selección de Región para Nuevos Pozos Petrolíferos – OilyGiant

## Objetivo del Proyecto

Este proyecto tiene como propósito identificar la **mejor región** para abrir **200 nuevos pozos petrolíferos**, optimizando el **beneficio esperado** y minimizando el **riesgo de pérdida (<2.5%)**.  
Se utiliza **regresión lineal** para la predicción de reservas y **bootstrapping** para la evaluación de riesgo.

---

## Contexto Empresarial

La empresa **OilyGiant** desea invertir **100 millones USD** en la perforación de 200 nuevos pozos.  
Cada pozo genera ingresos según su volumen de reservas estimado.

**Condiciones del negocio:**

- Inversión total: **100 millones USD**
- Ingreso por unidad (mil barriles): **4,500 USD**
- Punto de equilibrio: **111.1 unidades promedio por pozo**
- Riesgo máximo permitido: **2.5%**

---

## Metodología

1. **Carga y preparación de datos**

   - Archivos: `geo_data_0.csv`, `geo_data_1.csv`, `geo_data_2.csv`
   - División de datos: 75% entrenamiento / 25% validación
   - Escalamiento con `StandardScaler`

2. **Modelado predictivo**

   - Regresión Lineal mediante _Pipeline_ de `scikit-learn`
   - Evaluación con **RMSE** y comparación de volúmenes reales vs predichos

3. **Selección de pozos**

   - Se eligen los **200 pozos con mayor volumen predicho**
   - Se calcula el beneficio neto:
     ```
     beneficio = (suma de reservas reales × 4500) – 100,000,000
     ```

4. **Análisis de riesgo (Bootstrapping)**
   - 1000 iteraciones con muestreo aleatorio con reemplazo
   - Estimación del **beneficio promedio**, **intervalo de confianza del 95%** y **riesgo de pérdida**
   - Implementado con `scipy.stats.bootstrap`

---

## Resultados por Región

| Región   | RMSE | Beneficio Promedio (M USD) | Riesgo (%) | IC95% (M USD) |
| -------- | ---- | -------------------------- | ---------- | ------------- |
| Región 0 | 37.6 | 3.69                       | 8.5        | (-1.76, 8.86) |
| Región 1 | 0.89 | 4.54                       | 1.4        | (0.49, 8.46)  |
| Región 2 | 40.0 | 3.78                       | 6.0        | (-1.35, 8.82) |

**Región seleccionada:** **Región 1**

- Mayor beneficio promedio
- Riesgo más bajo (1.4%)
- Intervalo de confianza completamente positivo
- Excelente ajuste del modelo (RMSE ≈ 0.89)

---

## Conclusiones

La **Región 1** es la opción óptima para el desarrollo de pozos petrolíferos.  
Cumple con todas las condiciones de negocio:

- Riesgo < 2.5%
- Beneficio promedio positivo
- Rentabilidad estable validada con bootstrapping

El análisis demuestra que la rentabilidad no se debe al azar, sino a una tendencia consistente en los datos.

---

## Tecnologías Utilizadas

- Python 3.11
- pandas, numpy, scikit-learn, scipy
- matplotlib / seaborn
- Jupyter Notebook

---

## Estructura del Proyecto

````markdown
OilyGiant-Oil-Wells-Analysis/
│
├── data/ # Archivos CSV de las tres regiones
├── notebook/
└── OilyGiant_analysis.ipynb # Notebook principal
├── requirements.txt # Dependencias del proyecto
└── README.md

```

```
````
