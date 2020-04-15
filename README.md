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
[COVID-19_20200414.html](https://emi-sstcdapp.unavarra.es/COVID-19/COVID-19_20200414.html)

Para los análisis posteriores al 07/04/2020, se ha incluido la variable que recoge los casos activos en cada comunidad, la cuál excluye a los pacientes que se han recuperado o han fallecido.

Archivos anteriores: [ver directorio](https://emi-sstcdapp.unavarra.es/COVID-19/)

_NOTA: Para las comunidades de Castilla-La Mancha y Madrid las variables "hospitalizados" y "UCI", para esta última también en Castilla y León y Galicia, son datos de prevalencia (personas ingresadas a fecha de hoy). Es decir, no reflejan el total de personas que han sido hospitalizadas o ingresadas en UCI a lo largo del periodo de notificación._


### Validación de las predicciones (_actualizado el 15/04/2020_)

__Tabla 1:__ Promedios de los errores relativos (%) en las predicciones a 1 día por Comunidad Autónoma.

|                   | Casos Activos | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|-----:|-----:|-----:|-----:|-----:|
|Andalucía          |  0.63|  1.04|  2.47|  1.09|  5.68|
|Aragón             |  1.04|  0.96|  4.01|  1.04|  3.69|
|Asturias           |  2.32|  1.48|  4.11|  1.25|  3.46|
|Baleares           |  5.04|  1.19|  4.98|  2.15|  2.23|
|C. Valenciana      |  1.58|  1.03|  1.78| 1.61*| 1.90*|
|Canarias           |  2.68|  1.29|  5.00|  2.03|  3.34|
|Cantabria          |  1.29|  0.92|  5.40|  0.73|  2.90|
|Castilla-La Mancha |  2.01|  1.22|  1.48|  2.55|  2.38|
|Castilla y León    |  1.22|  0.87|  1.54| 0.46*|  0.84|
|Cataluña           |  1.58|  1.35|  1.26|  1.55|  2.16|
|Extremadura        |  2.54|  1.87|  3.40| 2.18*| 7.68*|
|Galicia            |  0.47|  0.86|  3.12|  1.68|  2.63|
|La Rioja           |  3.15|  1.20|  2.61|  1.67|  2.48|
|Madrid             |  1.75|  1.06|  0.64|  1.42|  1.11|
|Murcia             |  2.98|  0.82|  9.46|  4.32|  3.16|
|Navarra            |  1.14|  1.17|  2.90|  1.87|  1.71|
|País Vasco         |  2.50|  1.05|  1.43|  1.01|  1.15|
|ESPAÑA             |  0.61|  0.76|  0.80|      |      |


__Tabla 2:__ Promedios de los errores relativos (%) en las predicciones a 2 días por Comunidad Autónoma.

|                   | Casos Activos | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|------:|------:|------:|------:|------:|
|Andalucía          |   0.86|   2.85|   4.73|   3.31|   8.68|
|Aragón             |   1.55|   2.99|   8.81|   2.81|   7.67|
|Asturias           |   3.23|   2.63|   7.08|   3.46|   6.87|
|Baleares           |   7.61|   3.12|   8.49|   5.34|   5.09|
|C. Valenciana      |   2.48|   2.98|   3.89|  3.27*|  4.19*|
|Canarias           |   5.35|   2.44|  10.70|   3.91|   7.05|
|Cantabria          |   2.33|   2.12|  10.37|   1.97|   6.05|
|Castilla-La Mancha |   3.27|   3.07|   2.24|   5.63|   4.40|
|Castilla y León    |   1.59|   2.22|   3.47|  1.51*|   1.52|
|Cataluña           |   2.86|   2.92|   3.14|   3.63|   2.82|
|Extremadura        |   5.79|   3.54|   6.27|  4.76*| 14.40*|
|Galicia            |   0.94|   2.96|   6.76|   3.88|   6.22|
|La Rioja           |   3.97|   2.78|   4.12|   3.73|   4.82|
|Madrid             |   3.77|   3.03|   1.66|   3.36|   2.38|
|Murcia             |   5.48|   2.12|  15.70|   7.99|   5.95|
|Navarra            |   2.17|   2.65|   5.06|   3.55|   3.36|
|País Vasco         |   5.94|   2.88|   3.17|   2.66|   2.27|
|ESPAÑA             |   0.59|   2.28|   2.19|       |       |

*_Datos calculados teniendo en cuenta las predicciones posteriores al 08/04 debido al cambio de criterio en la contabilización de los casos (acumulados en vez de prevalencia)._


## Referencias
[Etxeberria, J., Goicoa, T., Ugarte, M.D., and Militino, A.F. (2014). Evaluating space-time models for short-term cancer mortality risk predictions in small areas. _Biometrical Journal_, __56(3)__, 383-402.](https://doi.org/10.1002/bimj.201200259)

[Rue, H., Martino, S., & Chopin, N. (2009). Approximate Bayesian inference for latent Gaussian models by using integrated nested Laplace approximations. _Journal of the Royal Statistical Society: Series B_, __71(2)__, 319-392.]( https://doi.org/10.1111/j.1467-9868.2008.00700.x)

[Ugarte, M.D., Adin, A., Goicoa, T., and Militino, A.F. (2014). On fitting spatio-temporal disease mapping models using approximate Bayesian inference. _Statistical Methods in Medical Research_, __23(6)__, 507-530.](https://doi.org/10.1177/0962280214527528)
