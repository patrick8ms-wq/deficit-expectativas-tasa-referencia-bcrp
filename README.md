# deficit-expectativas-tasa-referencia-bcrp


Trabajo 3 — PCA y Modelos Predictivos

Em el Trabajo 3 se amplía el análisis realizado previamente incorporando nuevas variables, aplicando Análisis de Componentes Principales (PCA) y comparando modelos predictivos usando validación cruzada para series de tiempo.
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

2. Modelo de ensamble
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







 
