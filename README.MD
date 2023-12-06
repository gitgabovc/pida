<center><h1 style="text-align:center">PROYECTO DE DATA ANALIST DE SINIESTRO VIALES EN CABA</h1></center>


Ciudad Autónoma de Buenos Aires (CABA), siendo una de las áreas urbanas más grandes de Argentina, enfrenta desafíos significativos relacionados con la seguridad vial debido a la alta densidad de tráfico. Este entorno urbano congestionado y dinámico puede contribuir a una incidencia considerable de accidentes de tránsito.

## Recopilación y Análisis de Datos

Las autoridades locales suelen llevar a cabo la recopilación y el análisis de datos relacionados con accidentes de tráfico. Estos esfuerzos buscan comprender las tendencias, identificar áreas problemáticas y desarrollar estrategias de prevención efectivas. La información recopilada proporciona una base para la toma de decisiones informada y la implementación de medidas destinadas a mejorar la seguridad vial.

## Impacto Social y Económico

Los accidentes de tránsito no solo representan una amenaza para la seguridad de los ciudadanos, sino que también tienen un impacto significativo en la sociedad y la economía en general. Entre las consecuencias se incluyen pérdidas humanas, lesiones, costos médicos, daños a la propiedad y congestión del tráfico. Estos aspectos subrayan la importancia de abordar la seguridad vial de manera integral.

## Proyecto de Análisis Exploratorio

Con el objetivo de abordar la problemática de los accidentes de tránsito, se lleva a cabo un proyecto que incluye:

1. **Análisis Exploratorio de Datos:**
   - Se explora la información proporcionada por el gobierno de CABA para comprender la naturaleza y las características de los accidentes.

2. **Limpieza de Datos y Transformaciones:**
   - Se realiza una limpieza de la información recopilada y se aplican transformaciones necesarias para obtener datos claros y valiosos.

3. **Extracción de Información Valiosa:**
   - Se extraen insights y patrones relevantes que pueden ser fundamentales para la formulación de estrategias de prevención.

4. **Recomendaciones para la Seguridad Vial:**
   - Se ofrecen recomendaciones basadas en los hallazgos del análisis exploratorio y la información extraída.

5. **Key Performance Indicators (KPI):**
   - Se presentarán KPI que permitirán evaluar el cumplimiento de los objetivos de seguridad vial a lo largo del tiempo.

Este enfoque integral busca no solo entender la problemática de los accidentes de tránsito en CABA, sino también proponer soluciones efectivas y medir el progreso a través de indicadores clave a lo largo de los años.

## Limpieza de datos y transformaciones

Los datos de víctimas fatales en CABA fueron extraídos de **https://data.buenosaires.gob.ar/dataset/victimas-siniestros-viales**, la cual nos proporciona información desde el año 2012 hasta el 2021, incluyendo datos sobre las víctimas, edad, fecha del accidente, género, etc.

Estos datos fueron procesados en el archivo **01-ETL.ipynb**. En primer lugar, se verificó la calidad de los datos, buscando valores incoherentes, duplicados y nulos.

Inicialmente, se identificó que había 696 registros en la página "Hechos" del archivo Excel extraído, mientras que en la página de "Víctimas" se tenían 717 registros. Algunos de estos valores faltantes estaban representados por "SD" y otros estaban en blanco.

Dado que los datos estaban en mayúsculas, se decidió convertirlos a minúsculas para una mayor consistencia y ademas cambiar el tipo de dato para los valores que sean numericos a enteros o decimales

Las páginas "Hechos" y "Víctimas" estaban relacionadas; uno, dos o tres registros de víctimas pertenecían a un hecho relacionado mediante un identificador (id). Se procedió a unirlos, y en la tabla de "Hechos" se tenía el número de víctimas, el cual se modificó a un valor igual a 1 al realizar esta operación de merge.

Durante esta combinación de registros, se identificaron registros con atributos que representaban la misma información. Se verificó que ambas fueran idénticas, pero se encontraron algunos registros que no lo eran. Al analizar más a fondo estos datos, se evidenció un registro incorrecto en el cual los datos pertenecientes a acusados estaban en "Víctimas" y viceversa. Se procedió a intercambiarlos y se verificó que dos registros estaban combinados debido a que ocurrió en este accidente con dos víctimas, por lo que se separaron para que cada víctima sea un registro independiente.

En los registros existían comunas con el valor 0, lo cual era peculiar ya que las comunas van del 1 al 15. Al analizar esto, se identificó que estos valores estaban presentes porque no se tenía la coordenada exacta del lugar y estos incidentes ocurrieron en autopistas, uniendo diferentes comunas. Por este motivo, no se podía asignar una comuna específica.

Las columnas de las horas en que ocurrieron los accidentes fatales presentaban valores nulos, y se procedió a rellenar estos valores mediante la mediana, ya que esta es la mejor representante para estos datos debido a su coeficiente de variabilidad superior al 50%. Este mismo proceso se llevó a cabo con la columna de edad de la víctima.

Adicionalmente, se añadieron columnas que ayudan a agrupar los datos, graficar y elaborar KPI. Se incluyó una columna "semestre", extraída del año en que ocurrió el accidente fatal, se creó la columna "dia_semana" que representa el nombre literal del día del accidente y, por último, la columna del "Rango etario", la cual agrupa las edades en diferentes categorías.

## Análisis Exploratorio de Datos

**1. Evolucion de los accidentes en los diferentes años**
<p align="center">
  <img src="src/1-eda.png" alt="Descripción de la imagen">
</p>
    - Se puede evidenciar que se tiene informacion desde los años 2016 y 2021 sobre las victimas fatales.<br>
    - Entre el año 2016 y 2018 se puede ver cambios pequeños en la cantidad de victimas fatales.<br>
    - Para el año 2019 y 2020 existe una disminucion significativa en la cantidad de vistimas fatales con respecto a los años anteriores, esto puede deberse principalmente a que se entro a una pandemia y las personas no podian salir de sus casas<br>
    - En el año 2021 se puede ver un aumento significativo y esto puede deberse a que se debio permitir una disminucion de las restricciones de salida debido a los efectos de la pandemia<br>