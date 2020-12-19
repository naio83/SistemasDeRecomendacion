#### El siguiente proyecto siguio los pasos de la competencia [challenge_de_ZonJobs](https://www.kaggle.com/c/postulaciones-zonajobs-fcen-2020/leaderboard) que pretende predecir aquellos avisos laborales (10 en orden descendente de relevancia) a los que se van a postular una serie de usuarios.
Metrica: [NDCG](https://www.kaggle.com/c/airbnb-recruiting-new-user-bookings/overview/evaluation) (Normalized discounted cumulative gain)
Score publico: 0.00839


### Baselines:
Se basaron en la generacion de modelos al azar, donde se buscaba poder recomendar a un usuario avisos
que hayan tenido alguna condicion, por ejemplo ser a los que mas se postularon, etc.
Sirvio de base para tener un piso de comparacion con el resto de los modelos.
Tabien es busco hacer algun modelo combinado buscando un aviso para un usuario con un algoritmo de prediccion
y luego buscar los avisos mas parecidos a el con un metodo bastante rudimentario, que no supero al azar.

### Modelos:
Se basaron en la utilizacion de LightFM para el scoreo de los distintos avisos para cada usuario, hubo
muchas combinaciones, pero se podrian resumir en las siguientes dos (A y B) teniendo en cuenta algunas salvedades:

1) Los avisos que se utilizan para el analisis son los validos, es decir no todos sino aquellos que tienen
fecha de inicio y fin de publicacion.
2) Para el caso de valores nas o nulos en los datasets se opto por completar con vacio, la moda de la columna
u algun otro metodo dependiendo del caso.
3) Se recorto el universo de postulantes para los que eran acordes al problema.
4) Hay usuarios/postulantes que estaban en train y test y otros que solo en train o solo en test. Con lo cual el 
problema se partio en dos, como predecir a los que estaban solo en test y que hacer con los que estaban
en ambos lados.
5) No se debe predecir a un postulante un aviso que al que ya se haya postulado.
6) Los avisos validos son los que estan activos en Abril de 2018.


#### A) Postulantes solo en test utilizando avisos "random" + LightFM:
Se itero varias veces generando avisos random para los postulantes que solo estaban en test, 
teniendo en cuenta las salvedades antes mencionadas. Dando cierta inteligencia a esta busqueda de avisos,
como ser cantidad minima de postulaciones, fechas, etc.
Para los postulantes que estaban tanto en train como en test se utilizo LightFM para encontrar los 10
avisos.

#### B) LightFM para todos los postulantes de Test:
Para esta opcion, que fue la que mejor resultado obtuvo se realizo una busqueda del 100% de los postulantes
de test utilizando LightFM, variando los hiperparametros para obtener los mejores resultados.


Se presentan 3 archivos:
#### baseline.ipynb : 
Cuenta con las primeras pruebas y los baselines.
#### expl_etl.ipynb : 
Analisis exploratorio y ejecucion de ETLs para la creacion de archivos que seran utilizados
en el modelo final.
#### modelo_lightfm.ipynb : 
Modelo final, que refleja lo construido segun las salvedades y el punto (B)


#### Conclusiones:
- Si bien se realizaron numerosas corridas para obtener predicciones, algunas de ellas que llegaron a tardar
casi 12 horas corridas, el modelo final es uno que se puede correr de punta a punta en 20 minutos en una
maquina local.
- Contar con metrica al momento de hacer tantas pruebas es fundamental.
- Se utilizaron opciones al manejo puro de data sets en Pandas para el manejo de los datos para optimizar
tiempos de corrida, por ejemplo el uso de Sets, Diccionarios, Listas, etc.

##### Ambiente:
- Visual Studio Code 1.51.1
- Python 3.7.5
- Ubuntu 18.04.3 LTS
- Intel Core i7 (4 core, 8 threads), 16GB de Ram.


