# Siniestros-viales-CABA

![Logo buenos aires](https://pbs.twimg.com/profile_images/1371512308602654724/u7KbPhSL_400x400.jpg)

# Proyecto Siniestros Viales
## Juan Esteban García.
## Email: juanestebangarciarodriguez@gmail.com
## Usuario GitHub: juesga1987
## Información al interior del repositorio:
1. Carpeta entregables: 

2. 

# Introducción

### En este proyecto, asumí el rol consultor especialista en data analitycs contratado por el gobierno de la ciudad de Buenos Aires, cuyo objetivo es analizar a profundidad los datos al respecto de las fatalidades u homicdios en accidentes de transito con la información historica que comprende los años del 2016 a 2021. Como fin ultimo se busca que dicho analisis permita a las autoridades de transporte tomar medidas para disminuir la cantidad de fatalidades en via publica y oriente en terminos de las estrategias que sean aplicables y ayuden a cumplir las metas establecidas a este respecto.

### Como material de trabajo nos proveen con un Dataset oficial que contiene información relevante sobre los homicidios en siniestros viales. 

### Como esquema metodologico para el desarrollo de nuestro proyecto, contamos con las siguientes etapas:

a. Realizar un ETL del dataset: Para el proceso de depuracion se uso Python. Entre otros se inputo cuando era posible las filas sin data "SD". Los tipos de datos fueron organizados tomando gran importancia las fechas. Posteriormente se aplico un merge entre el dataset "Hechos" y "Victimas" para consolidar toda la informacion necesaria en un archivo de texto que se usara para el EDA.

b. Analisis exploratorio de datos (EDA): Nos permite como consultores entender las variables y las relaciones entre las mismas en terminos estadisticos y cualitativos. De este proceso nace el enfoque de la presentación posterior y la definición de key aspects.

c. Presentación interactiva: Escogimos la herramienta Power BI para la creación de vicualizaciones potentes e intuitivas cuyo fin es exponer la problematica y soportar las estrategias y acciones sugeridas de nuestra parte. Vale la pena anotar que en el dashboard se podran observar metricas especificas solicitadas por el cliente.

# Descripción del Problema

## Contexto

### A pesar de la adopción en los ultimos años de teconologias por parte del departamento de transporte de la ciudad, las fatalidades relacionadas con siniestros viales siguen siendo una de las principales causas de muerte, con este inquietante panorama el gobierno de la ciudad ha disponibilizado para nosotros la data recogido en los ultimos años, pues se ha percatado que a pesar de ciertas mejorias en los indicadores, todavia hay mucho camino por recorrer.

### Nuestra labor sera de una forma concisa y precisa concluir al respecto de los datos y ademas precisar el camino a seguir, incluyendo acciones que combinen metodos tradicionales de control y seguridad en las vias con tecnologias que puedan influir de manera contundente en el numero de accidentes fatales.

# Resumen del trabajo y sus etapas

## ETL

### Esta etapa es fundamental pues de ella depende la calidad del EDA y trabajo posterior. Nos entregaron un archivo de excel con varias hojas que contenian los datasets y los diccionarios de terminos. Procedimos a separar las hojas "Hechos" y "Victimas" con el fin de trabajar en cada una de ellas de forma separada.

### Hechos:

a. Encontramos que las columnas "Altura" y "Cruce" tenian bastantes celdas sin informacion, sin embargo en la data encontramos la latitud y longitud, por lo que estas dos columnas inicialmente nombradas no fueron tenidas en cuenta para el trabajo.

b. Se separo en longitud y latitud plana la columna "XY (CABA)".

c. Se eleimino la columna "Hora" pues era redundante ya que contabamos con la franja horaria, a esta ultima se le cambio el tipo de dato a int.

### Victimas:

a. Se encontraron algunos ID's repetidos, por ello se analizo la causa y se determino que esto correspondia a que hay accidentes donde se presentar multiples fatalidades por lo que en la data se observa una linea por fallecido. Dado esto concluimos que los ID's repetidos realmente no lo son.

b. En la columna "Rol" se encontraron 11 filas sin data "SD". Dado que en proporciones el Rol Conductor es el de mayor preponderancia, se inputo esa clasificacion en las filas faltantes.

c. La columna "Victima" tambien presentaba la misma dificultadad, para ser congruentes como a los faltantes en "Rol" se asigno conductor, en "Victima" identificamos que la proporci[on de motos es muy alta, por lo que la probabilidad apunta a que si el Rol fue asignado como conductos en el accdiente la victima fue una moto.

d. El "Sexo" era otra columnna con faltantes, al analizarla la proporcion de hombres y mujeres es bastante desigual, siengo el sexo preponderante el masculino. A las filas faltantes se asigno este registro.

e. Para la asignaci[on de falatantes en la columna "Edad" se saco el promedio por sexo y de acuerdo a este se asigno a las celdas de acuerdo al sexo la edad promedio resultante.

f. Las fechas de fallecimiento faltantes se diligenciaron usando la fecha del accidente. Normalmente segun nos indican los datos los accidentes fatales causan la muerte de forma inmediata o con poca diferencia de horas frente al acaecimiento del hecho, por esto motivo cuando faltaba la fecha de fallecimiento se inputo la fecha del accidente.

### Merge:

a. Sabiendo que en la mayoria de los casos la culpabilidad la tiene el AUTO y analizando los tipos de victimas para los casos donde no conocemos el acusado, podemos inferir que en gran parte esos accidentes de deberon a un auto. Procederemos a inputar en la columna acusado para los 25 casos faltantes como responsable el AUTO.

b. En las columnas latitud y longitud identificamos celdas que a pesar de no estar vacias unicamente contienen un punto, vamos a proceder a reeemplazar el mismo por un espacio vacio. No las eliminaremos pues a pesar de no tener la ubicacion exacta del accidente no quiero afectar el conteo ni distribucion de otras variables.

c. Pensando en una matriz de correlacion posterior. Procedimos a realizar un mapeo de las columnas con variables categoricas de relevancia. Se crearon entonces columnas con dicho proceso para: Rol, Victima, Sexo, Participantes.

### Para finalizar se guardo la informacion resultante en en el archivo .CSV llamado "hechosyvictimas".

## Análisis Exploratorio de los datos (EDA)
### Para llevar a cabo el EDA se genero en primera instancia el reporte de la libreria Pandas Profiling. Sin embargo y a pesar de tener el reporte a la mano se procedio posteriormente a analizar mediante graficos propios la data de la siguiente forma:

-	Estadisticas descriptivas: Media, desviación standard, percentiles, minimo y maximo.
  
-	Correlación entre variables.
  
-	Analisis univariado, bivariado y multivariado.
  
-	Outliers de variables.

### Los graficos mediante los cuales se realizo el analisis fueron:

- Correlación entre variables.
- Estadistica descriptiva.
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
- Proporción de victimas por sexo.
- Victimas por comuna por categoría.
- Victimas por comuna por sexo.
- Relación acusado y víctima.
- Acusado por año / Categoría.

### Las conclusiones especificas para cada grafico las puede encontrar en el notebook llamado EDA que se dejara en el repositorio. Sin embargo expondre las conclusiones generales:

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

### La presentación realizada a traves de la herramienta PowerBi busca exponer la problematica de los homicidios como consecuencia de siniestros viales fatales, los posibles causantes y soluciones a traves de acciones. Por ello se comienza exponiendo a traves de KPI´s la evolución semestre a semestre de de las victimas fatales por cada 100.000 habitantes, para el año 2.021 la disminución registrada fue del 23.7% por encima del 10% meta propuesto por el gobierno de la ciudad. Adicionalmente se propone un KPI que nos indique de 2016 a 2021 cual ha sido la evolución promedio geometrica de la tendencia de accidentes, el resultado global nos indica que en terminos anuales para los años incluidos en la muestra se han logrado reducir las fatalidades en 10.3%.

### El analisis continua con las victimas por categoría que nos proporcionan la relación mas relevante sobre el grupo de actores viales sobre el cual deben centrarse las acciones. En la ciudad de Buenos Aires son las motos y los peatones, esta información se compara con los responsables con mas incidencia en los accidentes, que serian las autos particulares y los vehiculos de carga. En terminos generales mueren los conductores en mayor medida y los peatones. El sexo preponderante para las victimas en el Masculino, investigue al respecto y esto puede explicarse pues unicamente el 28% de las licencias que se expiden a mujeres. Expondremos una grafica esclarecedora obtenida del siguiente vinculo de Infobae https://www.infobae.com/inhouse/2022/12/13/movilidad-y-genero-solo-el-28-de-las-licencias-de-conducir-emitidas-en-un-ano-corresponde-a-mujeres/:

![Mujeres](https://cloudfront-us-east-1.images.arcpublishing.com/infobae/QDYH3RNV5ZGOJFFIEUROHBVWEA.jpg)

### Se identifico que de acuerdo a las franjas horarias las horas en que mas se presentan accidentes fatalaes son entre las 5am y las 8am, hora en que se moviliza la mayor cantidad de vehiculos y peatones pues las personas se dirigen a sus lugares de trabajo, es interesante que por locaización en la ciudad es la comuna 1 la de mayor incidencia de accidentes fatales,  comuna que por cierto alberga la mayor cantidad de sitios turisticos y centros de trabajo en Buenos Aires.

### Habiendo expuesto el panorama del analisis se determinan las siguientes posibles acciones:

1. A pesar que hay regulación al respecto del uso de elementos de protección por parte de motociclistas las autoridades son laxas a la hora de exigir el uso de caso. Hoy en dia existen camaras con alta tecnologia que pueden identficar si un motocilicsta lleva casco y de no ser asi puede ser multado mediante la detección de la placa del vehiculo. Esta acción combinada con autoridades que hagan cumplir la norma tendria un efecto positivo en los fallecimientos de motociclistas. Sin embargo las acciones dirigidas a la importancia del autocuidado en un actor tan vulnerable en la via deben darse masivamente.
   
2. Con respecto a las localizaciones geograficas con mayor indicencia de accidentes y teniendo en cuenta que Buenos Aires recibe un gran numero de turistas proponemos:

- En la comuna No.1 deben instalarse avisos en ingles con el fin que los turistas en su mayoria peatones interactuen de forma mas adecuada con las vias y de esta forma evitar accidentes donde ellos esten involucrados.
- Hay semaforos que pueden ser programados y que faltando algunos segundos para cambiar comienzan a titilar, indicando con suficiente anticipación a los conductores que deben frenar o a los peatones cuando pueden realmente cruzar. La instalación de los mismos a probado incidir en la reducción de accidentes de manera notoria.

3. En Argentina es obligatorío llevar el RTO (Revisión tecnica obligatoria). Este se exige a los vehiculos que circulan por la via publica. Sin embargo la capacidad de la policia de transite suele ser limitada frente a los vehiculos que circulan, logrando unicamente inspeccionar una pequeña muestra de la población global. Considerando que los responsables de los accidentes en su mayoria son los autos particulares y los vehiculos de carga, se propone aprovechar la digitalización del documento instalando camaras con la capacidad de identificar de acuerdo a la placa del vehiculo si el mismo cumple con la condición de tener actualizado dicho certificado, de esta forma si no se cumple con esta condición se impone una multa de transito y se exige inmediatamente al infractor que proceda con la inspección del vehiculo para emitir el RTO o de lo contrario sera inmovilizado.

Segun el Camara de centros de inspección vehicular, cito:

La importancia de la VTV/RTO se agiganta al repasar las estadísticas internacionales que, divididas en tres factores básicos de accidentología, arrojan los siguientes porcentajes respecto de las causas de los accidentes de tránsito:

Las que tienen origen en las fallas atribuibles al factor humano son entre el 70 y el 75 por ciento
Las que se deben a defectos del vehículo, entre un 22  y un 25 por ciento
Las originadas en fallas de la vía pública o fenómenos ambientales, entre un 5 y un 7 por ciento.

fuente: http://www.cciv.com.ar/contenidos/2017/10/10/Editorial_2870.php#:~:text=La%20Revisi%C3%B3n%20T%C3%A9cnica%20Obligatoria%20(RTO,largo%20de%20su%20vida%20%C3%BAtil.

4. Por ultimo como se observan franjas horarias donde se dan la mayoria de los accidentes. El pie de fuerza debe incrementarse a dichas horas, maximizando el recurso humano y asi incrementar los controles viales.

### Como se puede observar nuestras recomendaciones se basan en el aprovechamiento de la tecnología disponible que en conjunto con las acciones de control humanas ciertamente tendran incidencia en la cantidad de accidentes fatales.






