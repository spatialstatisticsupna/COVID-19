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
[COVID-19_20200415.html](https://emi-sstcdapp.unavarra.es/COVID-19/COVID-19_20200415.html)

Para los análisis posteriores al 07/04/2020, se ha incluido la variable que recoge los casos activos en cada comunidad, la cuál excluye a los pacientes que se han recuperado o han fallecido.

Archivos anteriores: [ver directorio](https://emi-sstcdapp.unavarra.es/COVID-19/)

_NOTA: Para las comunidades de Castilla-La Mancha y Madrid las variables "hospitalizados" y "UCI", para esta última también en Castilla y León y Galicia, son datos de prevalencia (personas ingresadas a fecha de hoy). Es decir, no reflejan el total de personas que han sido hospitalizadas o ingresadas en UCI a lo largo del periodo de notificación._


### Validación de las predicciones (_actualizado el 16/04/2020_)

__Tabla 1:__ Promedios de los errores relativos (%) en las predicciones a 1 día por Comunidad Autónoma.

|                   | Casos Activos | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|-----:|-----:|-----:|-----:|-----:|
|Andalucía          |  1.11|  1.01|  2.37|  1.03|  5.35|
|Aragón             |  1.25|  1.08|  3.80|  1.17|  3.59|
|Asturias           |  2.16|  1.41|  4.19|  1.27|  3.29|
|Baleares           |  4.41|  1.11|  4.70|  2.07|  2.13|
|C. Valenciana      |  1.59|  0.98|  1.66| 1.49*| 2.34*|
|Canarias           |  2.34|  1.23|  4.73|  2.00|  3.24|
|Cantabria          |  1.80|  0.89|  5.19|  0.75|  2.79|
|Castilla-La Mancha |  1.84|  1.18|  1.53|  2.41|  2.34|
|Castilla y León    |  1.23|  0.86|  1.46| 0.43*|  1.14|
|Cataluña           |  1.62|  1.35|  1.19|  1.46|  2.10|
|Extremadura        |  2.62|  1.86|  3.30| 1.82*| 7.15*|
|Galicia            |  0.41|  0.83|  2.98|  1.70|  2.51|
|La Rioja           |  5.13|  1.79|  2.43|  1.58|  2.41|
|Madrid             |  1.65|  1.04|  0.60|  1.39|  1.10|
|Murcia             |  4.05|  0.95|  9.01|  4.20|  3.09|
|Navarra            |  1.07|  1.09|  2.78|  1.76|  1.59|
|País Vasco         |  2.52|  1.00|  1.48|  0.98|  1.09|
|ESPAÑA             |  0.59|  0.71|  0.75|      |      |


__Tabla 2:__ Promedios de los errores relativos (%) en las predicciones a 2 días por Comunidad Autónoma.

|                   | Casos Activos | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|------:|------:|------:|------:|------:|
|Andalucía          |   1.19|   2.76|   4.50|   3.11|   8.16|
|Aragón             |   1.63|   2.99|   8.20|   2.82|   7.17|
|Asturias           |   3.28|   2.64|   7.00|   3.44|   6.57|
|Baleares           |   7.71|   3.00|   7.94|   5.06|   4.72|
|C. Valenciana      |   2.43|   2.77|   3.66|  3.32*|  4.16*|
|Canarias           |   4.65|   2.34|  10.00|   3.73|   6.78|
|Cantabria          |   3.08|   1.99|   9.94|   2.03|   5.89|
|Castilla-La Mancha |   3.63|   2.93|   2.42|   5.53|   4.26|
|Castilla y León    |   1.60|   2.08|   3.30|  1.36*|   1.81|
|Cataluña           |   3.08|   2.90|   3.00|   3.45|   2.89|
|Extremadura        |   5.60|   3.48|   5.92|  4.23*| 13.34*|
|Galicia            |   0.82|   2.75|   6.51|   3.72|   5.89|
|La Rioja           |   5.80|   3.22|   3.86|   3.54|   4.57|
|Madrid             |   3.61|   2.90|   1.55|   3.36|   2.54|
|Murcia             |   6.65|   2.24|  14.90|   7.69|   5.74|
|Navarra            |   1.90|   2.47|   4.75|   3.30|   3.12|
|País Vasco         |   5.69|   2.71|   3.09|   2.51|   2.23|
|ESPAÑA             |   0.77|   2.20|   2.09|      |      |


*_Datos calculados teniendo en cuenta las predicciones posteriores al 08/04 debido al cambio de criterio en la contabilización de los casos (acumulados en vez de prevalencia)._


## Referencias
[Etxeberria, J., Goicoa, T., Ugarte, M.D., and Militino, A.F. (2014). Evaluating space-time models for short-term cancer mortality risk predictions in small areas. _Biometrical Journal_, __56(3)__, 383-402.](https://doi.org/10.1002/bimj.201200259)

[Rue, H., Martino, S., & Chopin, N. (2009). Approximate Bayesian inference for latent Gaussian models by using integrated nested Laplace approximations. _Journal of the Royal Statistical Society: Series B_, __71(2)__, 319-392.]( https://doi.org/10.1111/j.1467-9868.2008.00700.x)

[Ugarte, M.D., Adin, A., Goicoa, T., and Militino, A.F. (2014). On fitting spatio-temporal disease mapping models using approximate Bayesian inference. _Statistical Methods in Medical Research_, __23(6)__, 507-530.](https://doi.org/10.1177/0962280214527528)
