#### El siguiente proyecto siguio los pasos de la competencia [Meli_Data_Challenge_2020](https://ml-challenge.mercadolibre.com/) 
Obteniendo una posicion final Nro 64 entre los casi 200 competidores. 
Metrica: Promedio de NDCG (Normalized Discounted Cumulative Gain o Ganancia Acumulada Descontada y Normalizada).
Score privado: 0.23125

------
------

Se entregan los siguientes archivos:

## exploratorio.ipynb : 
Analisis exploratorio incial, revision de los datos, y load de los mismo.

## expl_etl.ipynb : 
Analisis exploratorio inicial, incursionando en el uso de gc.collect() para ir liberando del heap los dataFrames que no se usaron.

## base_line.ipynb : 
Distintos baselines en los que se fue iterando y ensamblando para obtener mejores resultados. A partir de este momendo practicamente se deja de trabajar con dataFrames y se empieza a 
utilizar listas, diccionarios y diccionarios de diccionarios por la mejor performance al trabajar con grandes cantidades de datos. 
Los Baselines fueron:

#### BL_1: 
Items mas vendidos del dominio mas visitado
#### BL_2: 
Ultimos Items Vistos
#### BL_3: 
Vistas Compras (Quienes vieron esto, compraron lo otro)
#### Ensamble_basico_1: 
Ultimos Items Vistos con relleno de los items mas vendidos
### Ensamble_basico_2: 
Ultimos Items Vistos con relleno de los vistas_compra

##### *Fue el que obtuvo el mejor score, sobre este se aplicaron varias mejoras para evitar lo mas posible el uso de random, pero los resultados siempre fueron similares sin mostrar una mejora considerable.*


## modelitos.ipynb : 
Se hicieron algunas mejoras al Ensamble_basico_1, como ser buscar items por pais, o en vez de utilizar el Dominio utilizar la Categoria. Los resultados en ambos casos no fueron muy diferentes a lo antes obtenido.

#### Modelito 1: 
Ultimos Items Vistos con relleno de los items mas vendidos del mismo pais
#### Modelito 2: 
Ultimos Items Vistos con relleno de los items mas vendidos de la "categoria" mas visitada por el usuario

## meli_perfiles.ipynb : 
Se busco crear una matriz de perfiles, la idea era pegarle al dominio del item. Entonces para cada dominio comprando, crear una matriz con todos los dominios y un flag 1 o 0 en cada posicion indicando si al haber comprando un item del Dominio X que dominios visito antes.
Luego se podria utilizar algun predictor como lgb para predicir el dominio basado en la matriz. El problema fue que si bien al momento de crear mediane listas y diccionarios la matriz del perfil (8 mil columnas x la cantidad de datos de Train), que es super esparza, al quererla transformar a dataframe para correr el modelo, dicha operacion superaba la memoria de la maquina loca.
Se penso en intentar algunos metodos de ir cortando el dataset, o procesando de a partes, pero el deadline de la competencia no permitio avanzar mucho mas.


#### Notas:
- Para el manejo de estos tipos de archivos se utlizaron diccionarios y listas para la optimizacion de tiempos de corrida.
- Se utilizó metrica local.

