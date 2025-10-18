# deficit-expectativas-tasa-referencia-bcrp

Este proyecto en Python utiliza datos abiertos del Banco Central de Reserva del Perú (BCRP) para explorar la relación entre el déficit fiscal, las expectativas empresariales de corto (3 meses) y largo plazo (12 meses), y la tasa de referencia como herramienta de política monetaria.  

El análisis incluye la conexión al API del BCRP, la limpieza y transformación de los datos, así como la construcción de gráficos que muestran cómo la política fiscal y la política monetaria interactúan y afectan la confianza empresarial.  

A través de gráficos comparativos e interpretación de resultados, el proyecto abarca:  
- La respuesta de las expectativas empresariales frente al déficit fiscal.  
- La volatilidad de las expectativas a corto plazo frente a las de largo plazo.  
- El rol de la tasa de referencia como mecanismo de transmisión en la economía.  

Fuente de los datos:
Los datos provienen de la API de estadísticas del **BCRP**.  
El rango considerado va de **2015 a 2025**.

Variables principales:
- Fecha: Periodo en formato `Mes.Año` (ejemplo: `Ene.2015`).  
- Deficit_Fiscal: Resultado fiscal acumulado 12 meses, expresado como % del PBI.  
- Expect_3m: Expectativas empresariales a 3 meses (índice de confianza empresarial).  
- Expect_12m: Expectativas empresariales a 12 meses (índice de confianza empresarial).  
- Tasa_Referencia: Tasa de referencia de política monetaria fijada por el BCRP (%).  


Objetivos

1. Comprender la evolución temporal de las principales variables macroeconómicas.
2. Evaluar la relación entre inflación, tipo de cambio y crecimiento económico.
3. Estimar modelos econométricos que expliquen la dinámica entre las series ya mencionadas.


Librerías usadas

- `pandas`, `numpy` manejo de datos y series temporales  
- `matplotlib`, `seaborn`  visualización  
- `statsmodels`, `scikit-learn`  estimación de modelos econométricos  
- `requests`, `openpyxlcarga` lectura de datos desde Excel y conexión a la web  

Instrucciones de ejecución

1. Tener instalado: Python 3.11 o superior
2. Descargar el repositorio:
   https://github.com/patrick8ms-wq/deficit-expectativas-tasa-referencia-bcrp.git
4. Instalar dependencias con requirements.txt:
 pip install -r requirements.txt
6. Ejecutar el notebook:
jupyter notebook T2_ML_G6.ipynb

Decisiones de modelado:

-Frecuencia temporal: todas las series se ajustan al primer día del mes.

-Limpieza de datos: se eliminan filas vacías o con formatos inconsistentes de fecha para estandarizar.

-Transformación: se convierten los nombres de meses a valores numéricos.

-Unificación de series: se realiza un merge por la columna Fecha para conservar el rango completo de observaciones.

-Estandarización de columnas: se renombran las variables para mantener consistencia.

-Almacenamiento final: los resultados se guardan en un archivo CSV (series_consolidadas.csv).

-Modelo econométrico: se estiman regresiones lineales simples y múltiples para explorar relaciones entre las expectativas, el déficit fiscal y la tasa de referencia.





 
