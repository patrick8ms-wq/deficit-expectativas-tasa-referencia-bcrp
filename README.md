# deficit-expectativas-tasa-referencia-bcrp


Trabajo 4 - Predicción de Expectativas Empresariales

Este proyecto busca predecir las expectativas económicas a 3 y 12 meses usando variables macroeconómicas y financieras. Se llevó a cabo en varias etapas integrando exploración de datos, modelos lineales y no lineales, ensambles y redes neuronales.

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



Trabajo 1 (EDA)
Se realizó una exploración minuciosa de los datos para identificar patrones, anomalías y relaciones entre variables. Se seleccionaron las variables más relevantes para los modelos posteriores, destacando el déficit fiscal y la tasa de referencia como posibles predictores de las expectativas empresariales.

Trabajo 2 (Baseline)
Se implementó un modelo lineal, una regresión OLS, como referencia, evaluando su desempeño en las expectativas a 3 y 12 meses. Este baseline permitió establecer un punto de comparación para modelos más complejos y entender la persistencia de las expectativas.

Trabajo 3 (Modelos Complejos)
Se probaron modelos como Ridge, Lasso, Random Forest y XGBoost para mejorar la predicción. Así, se realizaron comparaciones de su desempeño mediante MSE y se seleccionó el modelo con mejor balance entre error y generalización. 

Trabajo 4 (MLP y análisis causal)
Se incluyó un DAG para representar relaciones causales entre variables. 
Además, se entrenaron redes neuronales MLP para capturar las relaciones no lineales entre déficit fiscal, tasa de referencia y expectativas empresariales. Se detalló la arquitectura, funciones de activación, escalado de datos y la optimización de hiperparámetros. Los resultados mostraron mejoras significativas sobre el baseline, especialmente para el horizonte de 3 meses, y comparables a los mejores modelos previos para 12 meses.


Instrucciones de ejecución

1. Tener instalado: Python 3.11 o superior
   
2. Clonar el repositorio
   git clone https://github.com/patrick8ms-wq/deficit-expectativas-tasa-referencia-bcrp
   cd deficit-expectativas-tasa-referencia-bcrp
   
3. Instalar dependencias con requirements.txt:
   pip install -r requirements.txt
   
4. Ejecutar el notebook:
   jupyter notebook notebook/T4_FINAL.ipynb


Las librerías usadas en el notebook incluyen:

pandas: manipulación y limpieza de datos, manejo de dataframes.

numpy: operaciones numéricas, arrays, reshaping.

matplotlib.pyplot: visualización básica de gráficos.

seaborn: gráficos estadísticos y series temporales.

scikit-learn: machine learning

MLPRegressor: redes neuronales para regresión.

LinearRegression: modelo lineal base (baseline).

StandardScaler: escalado de variables.

GridSearchCV: búsqueda de hiperparámetros.

mean_squared_error y r2_score: métricas de evaluación.

statsmodels: modelos estadísticos, regresión lineal y pruebas estadísticas.

requests: descarga de datos.

openpyxl: lectura de Excel.

xgboost: modelos de ensamble tipo gradient boosting.

El archivo requirements.txt del repositorio contiene las versiones exactas.









 
