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

## Análisis Exploratorio de los Datos Modelo de recomendacion (EDA)
### Se realizo un EDA de los datos del dataframe games pues de alli se extrajeron los datos  para el desarrollo de modelo de recomendación como era solicitado por la empresa, vale la pena aclarar que el archivo usado para el modelo de recomendación es simplement un dataframe con la información justamente necesario para ejecutarlo de acuerdo a a las variables identificadas como mas relevantes.
### Se analizaron las variables mas relevantes del dataset con base en el modelo de recomendación item a item o juego a juego. Con base en el EDA se determino que el mismo debia ser realizado con el desarrollador y el genero pues determinaban en mayor medida la selección de un juego en particular.
### El EDA se realizo de forma grafica mayoritariamente pues definitivamente hace los datos mas amenos y faciles de entender para el usuario final de la informacion, se usaron:
-	Barras.
-	Barras compiladas.
-	Boxplot.
-	Tortas.
## Modelo ML de recomendación
### Después de preparar los datos y realizar el EDA, entrenamos el modelo de recomendación basado en la similaridad del coseno que es una medida de similitud entre dos vectores que como producto arroja la relacion entre los mismos en referencia a una variable dada, como lo mencionamos anteriormente en mi caso, se determino que un juego (item) estaba intimamente ligado al genero y el desarrollador. 
### La librería Scikit-Learn proporciona los metodos para la creacion de la matriz o vectores (TfidVectorizer) y el metodo de coseno de similaridad (cosine_similarity). En este paso y dadas las limitaciones de procesamiento de nuestro host Render se tomo una muetra del 12% original del DataSet, que permite hacer el deploy y generar la matriz de resultados. Esta es la minima muestra que asegura un resultado de recomendación.
### Adicionalmente fue necesario eliminar algunos generos cuya importancia en la muestra y cantidad de juegos no era relevante, esto con fines el deployment.
### Finalmente a traves de una función que considerara no arrojar como recomendación el mismo item (Juego) introducido como variable de entrada y la no repeticion de recomendaciones se obtienen los 5 items mejor valorados recomendados.




