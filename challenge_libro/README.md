#### El siguiente proyecto siguio los pasos de la competencia [challenge_Libros](https://www.kaggle.com/c/prediccion-de-opiniones-de-libros-fcen-2020/leaderboard) para la cual se busca predecir la opinión (de 1 a 10) que los usuarios del sitio quelibroleo.com van a tener sobre una serie de libros.
Metrica: Error cuadrático medio (RMSE).
Score publico: 1.48142


------
------

Se entregan los siguientes archivos:

## predict_surprise.ipynb : 
- Se utilizo la libreria Surprise, haciendo repetidas pruebas para encontrar los mejores hiperparamentros para los algoritmos [SVD, NMF, KNN], la estrategia para encontrar los mismos fue primero hacer un RandomizedSearchCV para ir acecando a los mejores valores y cuando el campos de opciones fue mas reducido utilizar un GridSearchCV para explorar exhaustivamente todos las posibilidades y encontrar la mejor combinacion.
- **En todas las pruebas realizadas el mejor modelo se produjo ejecutando SVD.**

## combinado_lgb.ipynb : 
- Una vez obtenidos los mejores hiperparametros con Surprise se continuo agregando dichas predicciones como columnas del data set, ademas de otras de interes comos ser idioma, anio, genero, etc. y ejecutar algoritmos de prediccion como LightGBM, para el cual hubo que realizar algunas etapas de feature engineering y pasado de datos a tipo category para que sean aceptadas por el algoritmo. Si bien se obtuvieron algunos resultados interesantes, este camino no se exploro mucho mas.




