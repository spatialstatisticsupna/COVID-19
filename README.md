# COVID-19
Este repositorio contiene mapas descriptivos de la situación diaria acumulada y predicciones a corto plazo de la expansión de la enfermedad por el coronavirus SARS-CoV-2 (COVID-19) en las Comunidades Autónomas de España (excepto Ceuta y Melilla). Los resultados se actualizan diariamente en función de los datos publicados por el Ministerio de Sanidad.

## Fuente de los datos

- [Ministerio de Sanidad, Consumo y Bienestar Social](https://www.mscbs.gob.es/profesionales/saludPublica/ccayes/alertasActual/nCov-China/situacionActual.htm)
- [Instituto de Salud Carlos III](https://covid19.isciii.es/)


## Metodología

Los modelos utilizados para la predicción de las variables (número de casos confirmados, número de fallecimientos, número de enfermos hospitalizados, número de ingresos en UCI -todas ellas acumuladas-) son modelos espacio-temporales (modelos mixtos de Poisson) diseñados para el análisis de datos de conteo en áreas pequeñas. Han sido utilizados para suavizar tasas y riesgos en enfermedades crónicas fundamentalmente y para predecir a corto plazo la carga de cáncer, entre otras aplicaciones (ver por ejemplo Etxeberria et al, 2014). Por ello, no son posiblemente los modelos más adecuados para el estudio de datos de una pandemia. Sin embargo hemos comprobado que las predicciones a muy corto plazo (a uno y dos días) funcionan razonablemente bien y por ello los hemos utilizado para predecir casos en las variables anteriormente mencionadas en las Comunidades Autónomas españolas (a excepción de Canarias, Ceuta y Melilla).  Canarias y el conjunto de España se han analizado por separado, mediante un modelo de regresión de Poisson que modeliza el tiempo mediante un paseo aleatorio de orden dos. 

Los modelos espacio-temporales utilizados están descritos en Ugarte et al. (2014) e incorporan dependencia espacial mediante el uso de efectos aleatorios que siguen distribuciones tipo CAR (en concreto para modelizar la dependencia espacial hemos usado la distribución de Leroux y coautores).  Para modelizar la dependencia temporal se han utilizado paseos aleatorios de orden dos. La dependencia espacio-temporal se ha modelizado con cuatro tipos distintos de interacciones (tipo I, II, III y IV). El ajuste de todos los modelos analizados y la inferencia correspondiente se ha llevado a cabo con INLA (Rue et al., 2009) utilizando la librería [R-INLA](http://www.r-inla.org/).

Se han utilizado diversos criterios para seleccionar el mejor modelo en términos de complejidad y bondad de ajuste (DIC and WAIC) así como dos reglas que permiten evaluar la capacidad predictiva del modelo: el log-score y la regla de de Dawid–Sebastiani (DSS).



## Resultados
Los mapas descriptivos con los datos diarios actualizados y las predicciones a corto plazo para las Comunidades Autónomas españolas están disponibles en el siguiente enlace:
[COVID-19_20200409.html](https://emi-sstcdapp.unavarra.es/COVID-19/COVID-19_20200409.html)

Archivos anteriores: [ver directorio](https://emi-sstcdapp.unavarra.es/COVID-19/)

_NOTA: Para las comunidades de Castilla-La Mancha y Madrid las variables "hospitalizados" y "UCI", para esta última también en Castilla y León y Galicia, son datos de prevalencia (personas ingresadas a fecha de hoy). Es decir, no reflejan el total de personas que han sido hospitalizadas o ingresadas en UCI a lo largo del periodo de notificación._


### Validación de las predicciones (_actualizado el 10/04/2020_)

__Tabla 1:__ Promedios de los errores relativos (%) en las predicciones a 1 día por Comunidad Autónoma.

|                   | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|-----:|-----:|-----:|-----:|
|Andalucía          |  1.09|  2.21|  1.19|  7.62|
|Aragón             |  1.10|  5.02|  1.25|  5.09|
|Asturias           |  1.65|  5.29|  1.51|  4.35|
|Baleares           |  1.41|  6.49|  2.40|  2.93|
|C. Valenciana      |  1.15|  1.99|    * |    * |
|Canarias           |  1.60|  6.53|  2.62|  4.66|
|Cantabria          |  0.96|  6.90|  0.72|  3.47|
|Castilla-La Mancha |  1.37|  1.68|  2.71|  2.48|
|Castilla y León    |  1.02|  2.15|    * |  2.10|
|Cataluña           |  1.49|  1.69|  2.15|  2.82|
|Extremadura        |  1.88|  4.87|    * |    * |
|Galicia            |  1.03|  3.86|  2.03|  3.61|
|La Rioja           |  1.20|  3.11|  1.85|  3.56|
|Madrid             |  1.29|  0.72|  1.26|  1.03|
|Murcia             |  0.98| 11.67|  5.93|  4.07|
|Navarra            |  1.23|  4.14|  2.29|  2.56|
|País Vasco         |  1.23|  1.42|  1.17|  1.53|
|ESPAÑA             |  0.91|  0.99|  *   |  1.60|

__Tabla 2:__ Promedios de los errores relativos (%) en las predicciones a 2 días por Comunidad Autónoma.

|                   | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|------:|------:|------:|------:|
|Andalucía          |   3.74|   4.29|   4.19|  11.72|
|Aragón             |   3.59|  11.24|   3.34|  10.65|
|Asturias           |   3.66|   9.58|   4.19|   9.41|
|Baleares           |   3.80|  11.93|   7.24|   7.56|
|C. Valenciana      |   3.52|   4.58|     * |     * |
|Canarias           |   2.62|  14.43|   4.79|  10.00|
|Cantabria          |   2.08|  14.12|   2.42|   7.51|
|Castilla-La Mancha |   3.19|   2.77|   5.87|   5.24|
|Castilla y León    |   2.91|   4.60|     * |   4.64|
|Cataluña           |   3.39|   4.57|   4.83|   3.58|
|Extremadura        |   3.54|   8.86|     * |     * |
|Galicia            |   3.66|   8.52|   5.23|   9.11|
|La Rioja           |   3.33|   4.25|   4.21|   6.98|
|Madrid             |   3.73|   1.91|   3.55|   2.81|
|Murcia             |   2.60|  18.80|  10.43|   7.61|
|Navarra            |   3.02|   7.16|   3.64|   5.06|
|País Vasco         |   3.57|   3.03|   3.09|   3.11|
|ESPAÑA             |   2.74|   2.79|    *  |   1.60|

*_Datos no disponibles debido al cambio de criterio en la contabilización de los casos (acumulados en vez de prevalencia)._


## Referencias
[Etxeberria, J., Goicoa, T., Ugarte, M.D., and Militino, A.F. (2014). Evaluating space-time models for short-term cancer mortality risk predictions in small areas. _Biometrical Journal_, __56(3)__, 383-402.](https://doi.org/10.1002/bimj.201200259)

[Rue, H., Martino, S., & Chopin, N. (2009). Approximate Bayesian inference for latent Gaussian models by using integrated nested Laplace approximations. _Journal of the Royal Statistical Society: Series B_, __71(2)__, 319-392.]( https://doi.org/10.1111/j.1467-9868.2008.00700.x)

[Ugarte, M.D., Adin, A., Goicoa, T., and Militino, A.F. (2014). On fitting spatio-temporal disease mapping models using approximate Bayesian inference. _Statistical Methods in Medical Research_, __23(6)__, 507-530.](https://doi.org/10.1177/0962280214527528)
