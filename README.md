# Prueba_Lulo_Bank
Este repositorio contiene los resultados y los notebooks utilizados en la creación de la solución de la prueba técnica de Lulo Bank

La solución fue desarrollada en mayor parte en Databricks y otra parte en Google colab. 

## Cosas solucionadas en Databricks en la nube de Azure 

Nota: El proyecto completo de Databricks, se encuentra en la carpeta src, en la subcarpeta "7.Proyecto_Completo_Databricks".

Se intento simular un escenario real, de un proyecto de inteligencia de negocios que va desde la extracción de los datos hasta la carga de estos, en el que se definió un arquitectura de data lake con tres capas, primero se hizo la instalación de los puntos de montaje con le notebook "mount_adls_storage" que se encuentra en la carpeta src, para poder conectar Databricks con un data lake de segunda generación en la nube de azure, entonces se montaron tres puntos de montaje referentes a cada container, es decir, a cada capa y estas se nombraron raw, processed y presentation. En la carpeta denominada "Simulacion_Data_Lake", se encuentran todos los archivos que se fueron escribiendo en las distintas capas a medida que se fue haciendo el procesamiento de los datos. 

1.raw: En esta capa en la carpeta "json" se hizo la ingesta de los datos del API con el notebook "Notebook_Ingesta_Consultas_API", en formato json, hay 31 arhivos .json, uno por cada dia de Diciembre del 2020, ya que, dentro de la prueba solamente se pendía extraer los dias del mes de Diciembre del año mencionado. 

2.processed: En esta capa en una carpeta denominada Sabana_inicial, se guardó un archivo denominado Sabana_inicial.csv, este archivo es el producto de leer todos los .json de raw y convertirlo en un único dataframe, es decir, se anexaron todos los json y se consolidaron en un formato tabular. 

Posteriormente, se construyeron cuatro dataframes y se les hizo su respectivo profiling y se genéro el archivo .html para cada dataframe y estos archivos .html, se guardaron en la capa de processed en una carpeta denominada "Profiling_Dataframes", junto con su respectivo PDF, en el que se presenta un análisis del perfilamiento realizado. 

Luego, se leyó el archivo de Sabana_inicial.csv, y se hicieron procesos de transformación sobre los datos con los notebooks, "3.Embedde_show", "4.Embedded_show_Web_Channel", "5.Embedded_show_Net_Work" y "Series", con cada uno de estos notebooks se escribió un archivo .csv en processed. Acá se hicieron las primeras transformaciones, para quitar registros vacíos, definir tipos de datos y eliminar duplicados, con el fin de construir tablas de dimensiones y de hechos. Los resultados de estas primeras ETL's, estan en las carpeta de  Simulacion_Data_Lake/Procesados y se guardaron como archivos de extensión .csv. Los notebooks, con los que se hicieron estos procesos, se encuentran en la carpeta src/5.Notebooks_Transformaciones_Sabana_Inicial.  

3.presentation: Consecutivamente, se leyeron los .csv de Simulacion_Data_Lake/Procesados y se procedio a hacer las últimas transformaciones y hacer un upsert para cada tabla, con el fin de hacer el cargue de los datos definitivos en la capa de presentation. Acá se utilizó, el notebook de Delta_Tables, en el que se definio la estructura de las tablas a cargar. Y posteriormente, con los notebooks, Dim_Genero, Dim_Net_Work, Dim_Show, Dim_Tiempo, Dim_Web_Channel y Fac_Series, se hizo la carga de cada una de las tablas, en formato de Delta Table, en la capa de presentation, ya con este paso los datos quedaron listos para consumir y realizar por ejemplo, proyectos de analítica descriptiva como reportes en Power BI. Los notebooks, utilizados para este paso, se encuentran en la carpeta src/6.Notebooks_Cargue_datos_modelo. 

Por último, como un pequeño valor agregado, se hizo una versión demo de un reporte en Power BI, para calcular los indicadores solicitados por el área del negocio. 

## Cosas solucionadas en Google colab en la nube de Google
 
Para esta parte tome los archivos .csv que guarte en Simulacion_Data_lake/processed/Procesados, estos archivos los cargue en una base datos denominada BD_Series y la construcción de esta base de datos, se hizo con el notebook 4_Base_datos_SQLite, que se encuentra en la carpeta src/8.Notebook_Base_datos_SQL_Lite. 

Espero haber sido claro con la exposición de lo realizado, en el repositorio, se encuentran todos los notebooks utilizados y las salidas de estos. Espero les guste el desarrollo ejecutado y gracias por la oportunidad de dejarme participar en el proceso de selección. Por último, quedo atento a pasos a seguir y a sustentar lo realizado con el finde recibir retroalimentación, para también aprender de las cosas que tengan oportunidad de mejora, ya que, el ejercicio me pareció muy interesante.

Muchas gracias por todo,
Juan David Ramírez Ávila 







