# deficit-expectativas-tasa-referencia-bcrp

 

Predicción de Expectativas Empresariales usando Indicadores Macroeconómicos (2015–2025)

Modelos Lineales, Regularización, Ensemble Methods y Redes Neuronales

Integrantes del equipo:

Carmen Crisanto, César Jair

Miranda Sánchez, Alex Abraham Patrick

Prado Chafloque, Sarai Elizabeth

Reátegui Zapata, Joaquín Alejandro


Este repositorio reúne el trabajo final del curso Introducción a la Ciencia de Datos y Machine Learning con Python (ICD). El proyecto se desarrolló por etapas, por lo que aquí se incluyen todas las entregas parciales. El resultado final se encuentra en el notebook T4_INTEGRADO_FINAL (1).ipynb, donde se integra todo el análisis, el modelamiento y la comparación de resultados.

El objetivo principal es construir y evaluar modelos capaces de predecir las expectativas empresariales a corto (3 meses) y largo plazo (12 meses) utilizando información macroeconómica y financiera del Perú. Se enfatiza el rol del déficit fiscal, la tasa de referencia del BCRP, el riesgo país (EMBIG Perú) y el gasto no financiero como posibles determinantes de estas expectativas.

Además de la predicción, el proyecto busca interpretar los factores económicos que influyen en el comportamiento de las expectativas y analizar cómo los efectos fiscales y monetarios se transmiten en el tiempo. Un reto importante es que, en el contexto peruano, las expectativas suelen ser altamente persistentes; por ello, encontrar modelos que superen la simple inercia se convierte en un aporte valioso del trabajo.

Datos y variables

Los datos fueron descargados directamente desde la API estadística del BCRP y cubren el periodo 2015–2025, con frecuencia mensual.

Variables principales

deficit_fiscal: déficit fiscal acumulado 12 meses, % del PBI.

exp_eco_3m: expectativas empresariales de la economía a 3 meses.

exp_eco_12m: expectativas empresariales de la economía a 12 meses.

tasa_ref: tasa de referencia del BCRP.

gasto_no_financiero: gasto público no financiero total, como indicador de impulso fiscal.

embig_pe: EMBIG Perú, usado como medida de riesgo país y condiciones financieras externas.

Variables ingenierizadas

Para capturar mejor la dinámica temporal y los rezagos de la transmisión económica se construyen:

Rezagos de todas las series a 1 y 3 meses.
Variaciones mensuales.
Transformaciones e interacciones orientadas a mejorar estacionariedad y reducir ruido.
Estas permiten modelar de forma más realista la persistencia, los efectos rezagados y las relaciones heterogéneas entre déficit fiscal, gasto no financiero, riesgo país, tasa de referencia y expectativas empresariales.

Estructura del proyecto:

Trabajo 1 (EDA): Se realizó una exploración inicial de las series base —déficit fiscal, tasa de referencia y expectativas empresariales— para identificar patrones, anomalías y relaciones preliminares, antes de incorporar posteriormente el gasto no financiero y el EMBIG Perú. El análisis muestra un déficit fiscal persistente y creciente, en un contexto de reiterados incumplimientos de las reglas fiscales, junto con correlaciones negativas entre déficit y expectativas, sugiriendo un posible efecto adverso sobre la confianza empresarial. Además, se observa que las expectativas a 12 meses son más estables que las de 3 meses, lo que indica que el corto plazo responde con mayor fuerza a shocks transitorios.

Trabajo 2 (Baseline): Se implementaron modelos lineales como baseline para predecir expectativas en dos targets: a 3 y 12 meses. Se utilizó un baseline ingenuo (media histórica) y dos modelos OLS: uno simple con solo déficit fiscal y otro extendido que incorpora tasa de referencia, EMBIG Perú y gasto no financiero. La evaluación, basada en una división temporal 75/25, TimeSeriesSplit y métricas MSE junto con diagnósticos de residuos, mostró que los OLS presentan bajo poder explicativo y autocorrelación, por lo que sirven principalmente como punto de referencia para comparar con modelos más complejos.

Trabajo 3 (Modelos Complejos): Tras los resultados del Trabajo 2, donde los modelos lineales no lograron superar la inercia de las propias expectativas, en esta etapa se buscó evaluar modelos con mayor capacidad predictiva. Se añadió un baseline tipo random walk (H=1) y, sobre esa referencia, se entrenaron modelos más complejos —Ridge, Lasso, Random Forest y XGBoost— usando variables ingenierizadas y validación temporal (RidgeCV, LassoCV, GridSearchCV). La comparación por MSE mostró que en ambos targets (3 y 12 meses) el Lasso fue el mejor modelo, seleccionando las variables clave para capturar tanto shocks de corto plazo como tendencias más estructurales de largo plazo.

Trabajo 4 (MLP y análisis causal) Se incluyó un DAG para representar relaciones causales entre variables. Además, se entrenaron redes neuronales MLP para capturar las relaciones no lineales entre déficit fiscal, tasa de referencia y expectativas empresariales. Se detalló la arquitectura, funciones de activación, escalado de datos y la optimización de hiperparámetros. Los resultados mostraron mejoras significativas sobre el baseline, especialmente para el horizonte de 3 meses, y comparables a los mejores modelos previos para 12 meses.

Instrucciones de ejecución

Requisitos:

Python 3.11 o superior
pip y virtualenv recomendados

# 1. Clonar el repositorio

git clone https://github.com/patrick8ms-wq/deficit-expectativas-tasa-referencia-bcrp
cd deficit-expectativas-tasa-referencia-bcrp

# 2. Crear e instalar dependencias

pip install -r requirements.txt

# 3. Ejecutar el notebook principal

jupyter notebook notebook/T4_INTEGRADO_FINAL (1).ipynb

El notebook descarga los datos desde la API del BCRP, realiza el EDA, entrena los modelos y muestra las métricas y gráficos principales.

Principales librerías

pandas, numpy – manejo y transformación de datos.
matplotlib, seaborn – visualización.

scikit-learn – modelos lineales, ML clásicos (Ridge, Lasso, RF, etc.), MLP, GridSearchCV.

xgboost – modelos de gradient boosting.

statsmodels – regresión OLS, pruebas estadísticas y diagnósticos.

requests – conexión a la API del BCRP.

openpyxl – lectura/escritura de archivos Excel.

Las versiones exactas están en requirements.txt.


 
