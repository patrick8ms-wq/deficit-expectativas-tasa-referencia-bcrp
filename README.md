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

