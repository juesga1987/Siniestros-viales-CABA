# Siniestros-viales-CABA

![Logo buenos aires](https://pbs.twimg.com/profile_images/1371512308602654724/u7KbPhSL_400x400.jpg)

# Proyecto Siniestros Viales
## Juan Esteban García.
## Email: juanestebangarciarodriguez@gmail.com
## Usuario GitHub: juesga1987
## Información al interior del repositorio:

1. README
2. ETL (Notebook Jupyter)
3. EDA (Notebook Jupyter)
4. Achivo PowerBi con dashboard.
5. Imagen del Dashboard.

# Introducción

### En este proyecto, asumí el rol consultor especialista en data analitycs contratado por el gobierno de la ciudad de Buenos Aires, cuyo objetivo es analizar a profundidad los datos al respecto de las fatalidades u homicidios en accidentes de tránsito con la información histórica que comprende los años del 2016 a 2021. Como fin último se busca que dicho análisis permita a las autoridades de transporte tomar medidas para disminuir la cantidad de fatalidades en vía pública y oriente en términos de las estrategias que sean aplicables y ayuden a cumplir las metas establecidas a este respecto.

### Como material de trabajo nos proveen con un Data set oficial que contiene información relevante sobre los homicidios en siniestros viales. 

### Como esquema metodológico para el desarrollo de nuestro proyecto, contamos con las siguientes etapas:

a. Realizar un ETL del data set: Para el proceso de depuración se usó Python. Entre otros se imputó cuando era posible las filas sin data "SD". Los tipos de datos fueron organizados tomando gran importancia las fechas. Posteriormente se aplicó un merge entre el data set "Hechos" y "Victimas" para consolidar toda la información necesaria en un archivo de texto que se usara para el EDA.

b. Análisis exploratorio de datos (EDA): Nos permite como consultores entender las variables y las relaciones entre las mismas en términos estadísticos y cualitativos. De este proceso nace el enfoque de la presentación posterior y la definición de key aspects.

c. Presentación interactiva: Escogimos la herramienta Power BI para la creación de visualizaciones potentes e intuitivas cuyo fin es exponer la problemática y soportar las estrategias y acciones sugeridas de nuestra parte. Vale la pena anotar que en el dashboard se podrán observar métricas especificas solicitadas por el cliente.

# Descripción del Problema

## Contexto

### A pesar de la adopción en los últimos años de tecnologías por parte del departamento de transporte de la ciudad, las fatalidades relacionadas con siniestros viales siguen siendo una de las principales causas de muerte, con este inquietante panorama el gobierno de la ciudad ha disponibilizado para nosotros la data recogida en los últimos años, pues se ha percatado que, a pesar de ciertas mejorías en los indicadores, todavía hay mucho camino por recorrer.

### Nuestra labor será de una forma concisa y precisa concluir al respecto de los datos y además precisar el camino a seguir, incluyendo acciones que combinen métodos tradicionales de control y seguridad en las vías con tecnologías que puedan influir de manera contundente en el número de accidentes fatales.

# Resumen del trabajo y sus etapas

## ETL

### Esta etapa es fundamental pues de ella depende la calidad del EDA y trabajo posterior. Nos entregaron un archivo de Excel con varias hojas que contenían los data sets y los diccionarios de términos. Procedimos a separar las hojas "Hechos" y "Victimas" con el fin de trabajar en cada una de ellas de forma separada en python.

### Hechos:

a. Encontramos que las columnas "Altura" y "Cruce" tenían bastantes celdas sin información, sin embargo, en la data encontramos la latitud y longitud, por lo que estas dos columnas inicialmente nombradas no fueron tenidas en cuenta para el trabajo.

b. Se separo en longitud y latitud plana la columna "XY (CABA)".

c. Se elimino la columna "Hora" pues era redundante ya que contábamos con la franja horaria, a esta última se le cambio el tipo de dato a int.

### Victimas:

a. Se encontraron algunos ID's repetidos, por ello se analizó la causa y se determinó que esto correspondía a que hay accidentes donde se presentar múltiples fatalidades por lo que en la data se observa una línea por fallecido. Dado esto concluimos que los ID's repetidos realmente no lo son.

b. En la columna "Rol" se encontraron 11 filas sin data "SD". Dado que en proporciones el Rol Conductor es el de mayor preponderancia, se imputó esa clasificación en las filas faltantes.

c. La columna "Victima" también presentaba la misma dificultad, para ser congruentes como a los faltantes en "Rol" se asignó conductor, en "Victima" identificamos que la proporción de motos es muy alta, por lo que la probabilidad apunta a que si el Rol fue asignado como conductos en el accidente la víctima fue una moto.

d. El "Sexo" era otra columna con faltantes, al analizarla la proporción de hombres y mujeres es bastante desigual, siendo el sexo preponderante el masculino. A las filas faltantes se asignó este registro.

e. Para la asignación de faltantes en la columna "Edad" se sacó el promedio por sexo y de acuerdo con este se asignó a las celdas de acuerdo con el sexo la edad promedio resultante.

f. Las fechas de fallecimiento faltantes se diligenciaron usando la fecha del accidente. Normalmente según nos indican los datos los accidentes fatales causan la muerte de forma inmediata o con poca diferencia de horas frente al acaecimiento del hecho, por esto motivo cuando faltaba la fecha de fallecimiento se imputó la fecha del accidente.

### Merge:

a. Sabiendo que en la mayoría de los casos la culpabilidad la tiene el AUTO y analizando los tipos de víctimas para los casos donde no conocemos el acusado, podemos inferir que en gran parte esos accidentes de debieron a un auto. Procederemos a imputar en la columna acusado para los 25 casos faltantes como responsable el AUTO.

b. En las columnas latitud y longitud identificamos celdas que a pesar de no estar vacías únicamente contienen un punto, vamos a reemplazar el mismo por un espacio vacío. No las eliminaremos pues a pesar de no tener la ubicación exacta del accidente no quiero afectar el conteo ni distribución de otras variables.

c. Pensando en una matriz de correlación posterior. Procedimos a realizar un mapeo de las columnas con variables categóricas de relevancia. Se crearon entonces columnas con dicho proceso para: Rol, Victima, Sexo, Participantes.

### Para finalizar se guardó la información resultante en el archivo .CSV llamado "hechosyvictimas".

## Análisis Exploratorio de los datos (EDA)
### Para llevar a cabo el EDA se uso python y se generó en primera instancia el reporte de la librería Pandas Profiling. Sin embargo y a pesar de tener el reporte a la mano se procedió posteriormente a analizar mediante gráficos propios la data de la siguiente forma:

-	Estadísticas descriptivas: Media, desviación standard, percentiles, mínimo y máximo.
  
-	Correlación entre variables.
  
-	Análisis univariado, bivariado y multivariado.
  
-	Outliers de variables.

### Los gráficos mediante los cuales se realizó el análisis fueron:

- Correlación entre variables.
- Estadística descriptiva.
- Distribución accidentes por año y por mes.
- Coincidencia Fecha de fallecimiento vs fecha de accidente.
- Muertes por mes.
- Outliers Victimas.
- Victimas por categoría.
- Outliers victimas por franja horaria.
- Outliers victimas por franja horaria por categoría.
- Victimas por año.
- Outliers edad por tipo de sexo.
- Victimas por sexo año.
- Proporción de víctimas por sexo.
- Victimas por comuna por categoría.
- Victimas por comuna por sexo.
- Relación acusado y víctima.
- Acusado por año / Categoría.

### Las conclusiones específicas para cada grafico las puede encontrar en el notebook llamado EDA que se dejara en el repositorio. Sin embargo, expondré las conclusiones generales:

1. Las variables más relacionadas son las fechas del accidente y las fechas de fallecimiento, de esta correlación se puede inferir que la mayoría de los accidentes causan una muerte inmediata o en las siguientes horas o días.

2. Los roles y las victimas también se relacionan esto pues el rol que asume una persona en un accidente de tránsito se puede directamente relacionar con la víctima del accidente.

3. Las muertes por año y mes nos indican que hay ciertos meses del año donde se dan más accidentes fatales, estos son noviembre, diciembre y enero. El análisis de las muertes por mes corrobora esta conclusión. Otra inferencia que podemos hacer es que durante el año 2.020 se evidencian que en los meses más difíciles de la Pandemia hubo una reducción significativa de las fatalidades. A partir del 2.018 se ve que hay una tendencia clara a la disminución de accidentes fatales, lo que indica que las medidas tomadas por las autoridades han sido efectivas.

5. La mayoría de las víctimas son de sexo masculino y son motociclistas. De igual forma son los autos particulares los más acusados como responsables del homicidio.

6. En cuanto a la edad se evidencia que las victimas hombres tienen un rango de edad menos disperso y no es común ver víctimas de más de 80 años. Las mujeres tienen accidentes fatales a una edad más tardía y es más común que se accidenten mujeres en edades de 80 años en adelante en comparación con los hombres.

7. Las franjas horarias y las victimas nos indican que la mayoría de los accidentes fatales se dan en la hora pico de la mañana, hora en que la mayoría de las personas se desplazan a sus trabajos. Por categoría se ve que las motos son los tipos de victima que se accidentan en un rango más amplio de horas.

8. Las fatalidades por comuna se dan principalmente en aquellas que son altamente turísticas o concentran la mayoría de la población trabajadora. Las motos mantienen una tendencia de fatalidad en todas las comunas, sin embargo, los peatones son víctimas en aquellas turísticas o centros de trabajo.

9. Las victimas con mayor incidencia son las motos y los peatones. Frente a los acusados que son los autos particulares, los carros de carga y los pasajeros.

10. A pesar de que se dan outliers o datos atípicos en términos de la edad, las franjas horarias y el número de víctimas cuando se analizan a razón de la lógica no son casos que necesiten ser revisados o contrastados.
  
## Dashboard y presentación de resultados

### La presentación realizada a través de la herramienta PowerBi busca exponer la problemática de los homicidios como consecuencia de siniestros viales fatales, los posibles causantes y soluciones a través de acciones. Por ello se comienza exponiendo a través de KPI´s la evolución semestre a semestre de las víctimas fatales por cada 100.000 habitantes, para el año 2.021 la disminución registrada fue del 23.7% por encima del 10% meta propuesto por el gobierno de la ciudad. Adicionalmente se propone un KPI que nos indique de 2016 a 2021 cual ha sido la evolución promedio geométrica de la tendencia de accidentes, el resultado global nos indica que en términos anuales para los años incluidos en la muestra se han logrado reducir las fatalidades en 10.3%.

### El análisis continuó con las victimas por categoría que nos proporcionan la relación más relevante sobre el grupo de actores viales sobre el cual deben centrarse las acciones. En la ciudad de Buenos Aires son las motos y los peatones, esta información se compara con los responsables con más incidencia en los accidentes, que serían los autos particulares y los vehículos de carga. En términos generales mueren los conductores  y los peatones. El sexo preponderante para las víctimas en el Masculino, investigué al respecto y esto puede explicarse pues únicamente el 28% de las licencias que se expiden a mujeres. Expondremos una gráfica esclarecedora obtenida del siguiente vinculo de Infobae:  https://www.infobae.com/inhouse/2022/12/13/movilidad-y-genero-solo-el-28-de-las-licencias-de-conducir-emitidas-en-un-ano-corresponde-a-mujeres/:

![Mujeres](https://cloudfront-us-east-1.images.arcpublishing.com/infobae/QDYH3RNV5ZGOJFFIEUROHBVWEA.jpg)

### Se identifico que de acuerdo con las franjas horarias las horas en que más se presentan accidentes fatales son entre las 5am y las 8am, hora en que se moviliza la mayor cantidad de vehículos y peatones pues las personas se dirigen a sus lugares de trabajo, es interesante que por localización en la ciudad es la comuna 1 la de mayor incidencia de accidentes fatales, comuna que por cierto alberga la mayor cantidad de sitios turísticos y centros de trabajo en Buenos Aires.

### Habiendo expuesto el panorama del análisis se determinan las siguientes posibles acciones:

1. A pesar de que hay regulación al respecto del uso de elementos de protección por parte de motociclistas las autoridades son laxas a la hora de exigir el uso de caso. Hoy en día existen cámaras con alta tecnología que pueden identificar si un motociclista lleva casco y de no ser así puede ser multado mediante la detección de la placa del vehículo. Esta acción combinada con autoridades que hagan cumplir la norma tendría un efecto positivo en los fallecimientos de motociclistas. Sin embargo, las acciones dirigidas a la importancia del autocuidado en un actor tan vulnerable en la vía deben darse masivamente.
   
2. Con respecto a las localizaciones geográficas con mayor incidencia de accidentes y teniendo en cuenta que Buenos Aires recibe un gran número de turistas proponemos:

- En la comuna No.1 deben instalarse avisos en ingles con el fin que los turistas en su mayoría peatones interactúen de forma más adecuada con las vías y de esta forma evitar accidentes donde ellos estén involucrados.
- Hay semáforos que pueden ser programados y que faltando algunos segundos para cambiar comienzan a titilar, indicando con suficiente anticipación a los conductores que deben frenar o a los peatones cuando pueden realmente cruzar. La instalación de estos ha probado incidir en la reducción de accidentes de manera notoria.

3. En Argentina es obligatorio llevar el RTO (Revisión técnica obligatoria). Este se exige a los vehículos que circulan por la vía pública. Sin embargo, la capacidad de la policía de transito suele ser limitada frente a los vehículos que circulan, logrando únicamente inspeccionar una pequeña muestra de la población global. Considerando que los responsables de los accidentes en su mayoría son los autos particulares y los vehículos de carga, se propone aprovechar la digitalización del documento instalando cámaras con la capacidad de identificar de acuerdo a la placa del vehículo si el mismo cumple con la condición de tener actualizado dicho certificado, de esta forma si no se cumple con esta condición se impone una multa de tránsito y se exige inmediatamente al infractor que proceda con la inspección del vehículo para emitir el RTO o de lo contrario será inmovilizado.

Según el Cámara de centros de inspección vehicular, cito:

La importancia de la VTV/RTO se agiganta al repasar las estadísticas internacionales que, divididas en tres factores básicos de accidentología, arrojan los siguientes porcentajes respecto de las causas de los accidentes de tránsito:

Las que tienen origen en las fallas atribuibles al factor humano son entre el 70 y el 75 por ciento
Las que se deben a defectos del vehículo, entre un 22 y un 25 por ciento
Las originadas en fallas de la vía pública o fenómenos ambientales, entre un 5 y un 7 por ciento.

fuente: http://www.cciv.com.ar/contenidos/2017/10/10/Editorial_2870.php#:~:text=La%20Revisi%C3%B3n%20T%C3%A9cnica%20Obligatoria%20(RTO,largo%20de%20su%20vida%20%C3%BAtil.

4. Por último como se observan franjas horarias donde se dan la mayoría de los accidentes. El pie de fuerza debe incrementarse a dichas horas, maximizando el recurso humano y así incrementar los controles viales.

### Como se puede observar nuestras recomendaciones se basan en el aprovechamiento de la tecnología disponible que en conjunto con las acciones de control humanas ciertamente tendrán incidencia en la cantidad de accidentes fatales.







