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
[COVID-19_20200412.html](https://emi-sstcdapp.unavarra.es/COVID-19/COVID-19_20200412.html)

Para los análisis posteriores al 07/04/2020, se ha incluido la variable que recoge los casos activos en cada comunidad, la cuál excluye a los pacientes que se han recuperado o han fallecido.

Archivos anteriores: [ver directorio](https://emi-sstcdapp.unavarra.es/COVID-19/)

_NOTA: Para las comunidades de Castilla-La Mancha y Madrid las variables "hospitalizados" y "UCI", para esta última también en Castilla y León y Galicia, son datos de prevalencia (personas ingresadas a fecha de hoy). Es decir, no reflejan el total de personas que han sido hospitalizadas o ingresadas en UCI a lo largo del periodo de notificación._


### Validación de las predicciones (_actualizado el 13/04/2020_)

__Tabla 1:__ Promedios de los errores relativos (%) en las predicciones a 1 día por Comunidad Autónoma.

|                   | Casos Activos | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|-----:|-----:|-----:|-----:|-----:|
|Andalucía          |  0.72|  1.01|  2.29|  1.20|  6.24|
|Aragón             |  0.95|  0.98|  4.63|  1.12|  4.19|
|Asturias           |  2.29|  1.46|  4.69|  1.37|  3.89|
|Baleares           |  4.12|  1.28|  5.60|  2.33|  2.49|
|C. Valenciana      |  1.64|  1.09|  1.90| 1.91*| 2.47*|
|Canarias           |  1.68|  1.39|  5.42|  2.32|  3.73|
|Cantabria          |  1.27|  0.98|  5.78|  0.71|  3.05|
|Castilla-La Mancha |  1.39|  1.36|  1.47|  2.68|  2.39|
|Castilla y León    |  1.12|  0.97|  1.72| 0.45*|  0.85|
|Cataluña           |  1.37|  1.32|  1.35|  1.73|  2.34|
|Extremadura        |  2.00|  1.90|  3.87| 2.81*| 8.18*|
|Galicia            |  0.38|  0.92|  3.14|  1.92|  2.94|
|La Rioja           |  3.74|  1.29|  2.87|  1.71|  2.90|
|Madrid             |  1.78|  1.09|  0.74|  1.25|  1.05|
|Murcia             |  1.72|  0.88| 10.73|  4.73|  3.52|
|Navarra            |  1.00|  1.20|  3.18|  2.07|  1.99|
|País Vasco         |  2.86|  1.16|  1.49|  1.10|  1.20|
|ESPAÑA             |  0.44|  0.79|  0.91|  $-$ |  $-$ |


__Tabla 2:__ Promedios de los errores relativos (%) en las predicciones a 2 días por Comunidad Autónoma.

|                   | Casos Activos | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|------:|------:|------:|------:|------:|
|Andalucía          |   1.06|   3.01|   4.08|   3.49|   9.65|
|Aragón             |   1.03|   3.10|   9.95|   2.99|   9.06|
|Asturias           |   3.00|   2.93|   8.20|   3.74|   7.88|
|Baleares           |   5.89|   3.50|   9.89|   5.97|   5.89|
|C. Valenciana      |   2.28|   3.14|   4.37|  4.32*|  5.68*|
|Canarias           |   3.00|   2.60|  12.12|   4.39|   8.03|
|Cantabria          |   2.11|   2.08|  11.68|   1.85|   6.43|
|Castilla-La Mancha |   3.97|   3.55|   2.49|   5.58|   4.59|
|Castilla y León    |   1.45|   2.40|   3.82|  1.64*|   1.66|
|Cataluña           |   2.85|   3.11|   3.66|   4.02|   3.15|
|Extremadura        |   4.31|   3.30|   7.32|  8.04*| 15.90*|
|Galicia            |   0.54|   3.13|   6.97|   4.20|   7.07|
|La Rioja           |   4.19|   2.95|   4.14|   3.68|   5.58|
|Madrid             |   3.95|   3.33|   1.85|   3.16|   2.34|
|Murcia             |   3.17|   2.28|  17.63|   8.90|   6.65|
|Navarra            |   1.74|   2.59|   5.72|   3.89|   3.98|
|País Vasco         |   6.28|   3.13|   3.15|   2.68|   2.46|
|ESPAÑA             |   0.64|   2.52|   2.46|   $-$ |   $-$ |


*_Datos calculados teniendo en cuenta las predicciones posteriores al 08/04 debido al cambio de criterio en la contabilización de los casos (acumulados en vez de prevalencia)._


## Referencias
[Etxeberria, J., Goicoa, T., Ugarte, M.D., and Militino, A.F. (2014). Evaluating space-time models for short-term cancer mortality risk predictions in small areas. _Biometrical Journal_, __56(3)__, 383-402.](https://doi.org/10.1002/bimj.201200259)

[Rue, H., Martino, S., & Chopin, N. (2009). Approximate Bayesian inference for latent Gaussian models by using integrated nested Laplace approximations. _Journal of the Royal Statistical Society: Series B_, __71(2)__, 319-392.]( https://doi.org/10.1111/j.1467-9868.2008.00700.x)

[Ugarte, M.D., Adin, A., Goicoa, T., and Militino, A.F. (2014). On fitting spatio-temporal disease mapping models using approximate Bayesian inference. _Statistical Methods in Medical Research_, __23(6)__, 507-530.](https://doi.org/10.1177/0962280214527528)
