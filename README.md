# deficit-expectativas-tasa-referencia-bcrp


Trabajo 3 — PCA y Modelos Predictivos

En el Trabajo 3 se amplía el análisis realizado previamente incorporando nuevas variables, aplicando Análisis de Componentes Principales (PCA) y comparando modelos predictivos usando validación cruzada para series de tiempo.
El objetivo central es entender mejor la relación entre las expectativas empresariales, el déficit fiscal y la tasa de referencia del BCRP, y evaluar qué tan bien diferentes modelos pueden anticipar su comportamiento.

Este incluye:
Limpieza y consolidación de datos macroeconómicos.
Construcción de nuevas variables (rezagos, diferencias, transformaciones).
Aplicación de PCA como herramienta de diagnóstico y visualización.
Entrenamiento y comparación de dos modelos: un modelo regularizado (Ridge o Lasso) y un modelo Random Forest o XGBoost.
Validación con TimeSeriesSplit, evitando mezclar información futura.
Reporte de métricas y conclusiones sobre desempeño predictivo.


Datos usados
Los datos provienen de la API estadística del BCRP, cubriendo el periodo 2015–2025.

Variables principales:

Fecha: periodo mensual.

Deficit_Fiscal: déficit fiscal acumulado a 12 meses en % del PBI.

Expect_3m: expectativas empresariales a 3 meses.

Expect_12m: expectativas empresariales a 12 meses.

Tasa_Referencia: tasa de referencia del BCRP.

Variables añadidas en este trabajo:

Rezagos de cada serie (lag1, lag2, etc.).

Variaciones mensuales.

Transformaciones para mejorar estacionariedad.

Estas variables adicionales permiten capturar persistencia temporal y la manera en que los efectos económicos se transmiten con rezagos.



PCA — Análisis de Componentes Principales
El PCA se utiliza como una herramienta para:

Identificar correlaciones fuertes entre variables.

Revisar problemas de multicolinealidad.

Visualizar la estructura de los datos en menor dimensión.

Analizar la varianza explicada por cada componente.

El notebook incluye:
Scree plot.

Biplot.

Cálculo de varianza acumulada.

Así se evalúan cuántos componentes serían útiles como entrada para los modelos.


Modelos implementados
El trabajo incluye la comparación de dos modelos:

1. Modelo regularizado
Ridge o Lasso.

Este modelo se ajusta usando RidgeCV/LassoCV, que permiten encontrar automáticamente el valor óptimo de λ.

3. Modelo de ensamble
Random Forest o XGBoost.

Se ajustan usando GridSearchCV, y se documentan los hiperparámetros del grid, por qué se probaron y cuáles fueron los óptimos.

Validación

Ambos modelos se validan con TimeSeriesSplit, lo cual es clave para evitar “leakage” temporal.
La métrica principal es el MSE.



Instrucciones de ejecución

1. Tener instalado: Python 3.11 o superior
   
2. Clonar el repositorio
   git clone https://github.com/patrick8ms-wq/deficit-expectativas-tasa-referencia-bcrp
   cd deficit-expectativas-tasa-referencia-bcrp
   
3. Instalar dependencias con requirements.txt:
   pip install -r requirements.txt
   
4. Ejecutar el notebook:
   jupyter notebook notebook/trabajo3.ipynb


Las librerías usadas en el notebook incluyen:
pandas

numpy

matplotlib

seaborn

scikit-learn

statsmodels

requests

openpyxl

xgboost

El archivo requirements.txt del repositorio contiene las versiones exactas.





Resultados

1. Naive baseline

El baseline consiste en predecir que el valor actual será igual al del mes previo. Sirve como referencia para evaluar si los modelos realmente añaden poder predictivo.

Horizonte	MSE Baseline
3 meses	4.09
12 meses	8.40

2. Resultados por modelo

2.1 Horizonte 3 meses (exp_eco_3m)
Modelo, test MSE
Baseline	(4.09):	Modelo más preciso. Difícil de superar.
Random Forest (7.75): Mejor dentro de ML, pero no supera al baseline.
XGBoost (10.29): Sobreajuste, rendimiento limitado.
Lasso	(11.10):	Elimina ruido, pero sigue lejos del baseline.
Ridge	(21.22):	Afectado por multicolinealidad en la matriz de predictores.

Ningún modelo supera al baseline. Las expectativas a 3 meses dependen casi por completo de su propio valor rezagado. La serie muestra una estructura autorregresiva muy fuerte.


2.2 Horizonte 12 meses (exp_eco_12m)
Modelo, test MSE

Lasso	(7.08): Mejor modelo. El único que supera al baseline.

Baseline	(8.40):	Punto de referencia.

Ridge	(20.90).	Nuevamente afectado por multicolinealidad.

XGBoost	(30.70):	Problemas de generalización.

Random Forest	(35.18):	Sobreajuste.

A diferencia del horizonte de 3 meses, Lasso sí mejora el baseline, la regularización L1 logra filtrar el ruido y seleccionar las variables macro-financieras realmente relevantes a este horizonte.

3. Importancia de variables
   
Random Forest — Horizonte 3 meses

Las variables con mayor importancia fueron:
exp_eco_3m_l1 (82%)

exp_eco_3m_l3

gasto_no_financiero_l3

deficit_x_tasa

embig_pe_l1

El modelo depende casi exclusivamente del rezago 1, lo cual explica por qué no puede superar al baseline.

Lasso — Horizonte 12 meses
Lasso seleccionó un número reducido de predictores:

exp_eco_12m_l1

Interacciones fiscales (déficit x tasa / embig)

Lags de EMBIG y gasto público

Esto sugiere que a horizontes más largos, las expectativas incorporan información macrofinanciera.


En conclusión,
- Para horizontes cortos (3M), la serie se comporta casi como un random walk, por lo que los modelos no lineales ni penalizados agregan valor.
- Para horizontes largos (12M), los modelos lineales penalizados funcionan mejor, especialmente Lasso, que maneja bien muestras pequeñas y el ruido.
- Random Forest y XGBoost tienen bajo desempeño debido al tamaño reducido de la muestra y a la alta estructura temporal de los datos.
- La regularización L1 (Lasso) resulta muy efectiva en contextos macroeconómicos con pocas observaciones y alta correlación entre predictores.





 
