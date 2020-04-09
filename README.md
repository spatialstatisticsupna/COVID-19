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
[COVID-19_20200408.html](https://emi-sstcdapp.unavarra.es/COVID-19/COVID-19_20200408.html)

Archivos anteriores: [ver directorio](https://emi-sstcdapp.unavarra.es/COVID-19/)

_NOTA: Para las comunidades de Castilla-La Mancha y Madrid las variables "hospitalizados" y "UCI", para esta última también en Castilla y León y Galicia, son datos de prevalencia (personas ingresadas a fecha de hoy). Es decir, no reflejan el total de personas que han sido hospitalizadas o ingresadas en UCI a lo largo del periodo de notificación._


### Validación de las predicciones (_actualizado el 09/04/2020_)

__Tabla 1:__ Promedios de los errores relativos (%) en las predicciones a 1 día por Comunidad Autónoma.

|                   | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|-----:|-----:|-----:|-----:|
|Andalucía          |  1.19|  2.16|  1.25|  8.19|
|Aragón             |  1.20|  5.44|  1.39|  5.11|
|Asturias           |  1.66|  5.33|  1.64|  4.27|
|Baleares           |  1.51|  7.17|  2.69|  3.29|
|C. Valenciana      |  1.20|  1.99|   *  |    * |
|Canarias           |  1.56|  6.95|  2.69|  4.98|
|Cantabria          |  0.95|  7.27|  0.76|  3.91|
|Castilla-La Mancha |  1.35|  1.56|  2.68|  2.33|
|Castilla y León    |  1.06|  2.21|    * |  2.25|
|Cataluña           |  1.39|  1.72|  2.34|  3.17|
|Extremadura        |  1.98|  4.87|   *  |    * |
|Galicia            |  1.07|  3.88|  2.26|  4.06|
|La Rioja           |  1.16|  3.37|  1.98|  3.83|
|Madrid             |  1.26|  0.71|  1.41|  1.06|
|Murcia             |  1.00| 11.60|  6.13|  4.30|
|Navarra            |  1.21|  4.20|  1.99|  2.78|
|País Vasco         |  1.25|  1.51|  1.30|  1.66|
|ESPAÑA             |  0.89|  0.99|    * |  1.79|


__Tabla 2:__ Promedios de los errores relativos (%) en las predicciones a 2 días por Comunidad Autónoma.

|                   | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|------:|------:|------:|------:|
|Andalucía          |   4.19|   4.42|   4.65|  13.15|
|Aragón             |   4.04|  12.70|   3.80|  11.08|
|Asturias           |   4.15|  10.12|   4.63|   9.76|
|Baleares           |   3.95|  12.46|   8.09|   8.43|
|C. Valenciana      |   3.70|   4.75|     * |     * |
|Canarias           |   2.86|  15.28|   5.22|  10.82|
|Cantabria          |   2.02|  15.30|   2.71|   8.38|
|Castilla-La Mancha |   3.27|   2.98|   5.86|   5.08|
|Castilla y León    |   3.17|   4.58|     * |   5.22|
|Cataluña           |   3.40|   4.66|   5.46|   4.01|
|Extremadura        |   4.01|   9.03|     * |     * |
|Galicia            |   3.98|   8.62|   5.76|  10.13|
|La Rioja           |   3.08|   4.13|   4.61|   7.58|
|Madrid             |   3.50|   1.89|   3.74|   3.21|
|Murcia             |   2.59|  18.63|  10.96|   8.21|
|Navarra            |   3.36|   7.20|   4.10|   5.67|
|País Vasco         |   3.66|   3.44|   3.43|   3.29|
|ESPAÑA             |   2.75|   2.83|     * |   1.52|

*_Datos no disponibles debido al cambio de criterio en la contabilización de los casos (acumulados en vez de prevalencia)._


## Referencias
[Etxeberria, J., Goicoa, T., Ugarte, M.D., and Militino, A.F. (2014). Evaluating space-time models for short-term cancer mortality risk predictions in small areas. _Biometrical Journal_, __56(3)__, 383-402.](https://doi.org/10.1002/bimj.201200259)

[Rue, H., Martino, S., & Chopin, N. (2009). Approximate Bayesian inference for latent Gaussian models by using integrated nested Laplace approximations. _Journal of the Royal Statistical Society: Series B_, __71(2)__, 319-392.]( https://doi.org/10.1111/j.1467-9868.2008.00700.x)

[Ugarte, M.D., Adin, A., Goicoa, T., and Militino, A.F. (2014). On fitting spatio-temporal disease mapping models using approximate Bayesian inference. _Statistical Methods in Medical Research_, __23(6)__, 507-530.](https://doi.org/10.1177/0962280214527528)
