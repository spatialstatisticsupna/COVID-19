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
[COVID-19_20200410.html](https://emi-sstcdapp.unavarra.es/COVID-19/COVID-19_20200410.html)

Archivos anteriores: [ver directorio](https://emi-sstcdapp.unavarra.es/COVID-19/)

_NOTA: Para las comunidades de Castilla-La Mancha y Madrid las variables "hospitalizados" y "UCI", para esta última también en Castilla y León y Galicia, son datos de prevalencia (personas ingresadas a fecha de hoy). Es decir, no reflejan el total de personas que han sido hospitalizadas o ingresadas en UCI a lo largo del periodo de notificación._


### Validación de las predicciones (_actualizado el 11/04/2020_)

__Tabla 1:__ Promedios de los errores relativos (%) en las predicciones a 1 día por Comunidad Autónoma.

|                   | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|-----:|-----:|-----:|-----:|
|Andalucía          |  1.05|  2.16|  1.16|  6.94|
|Aragón             |  1.02|  4.97|  1.24|  4.92|
|Asturias           |  1.58|  4.99|  1.43|  4.39|
|Baleares           |  1.42|  5.84|  2.50|  2.85|
|C. Valenciana      |  1.19|  2.04|    * |    * |
|Canarias           |  1.57|  6.09|  2.58|  4.20|
|Cantabria          |  0.92|  6.49|  0.65|  3.13|
|Castilla-La Mancha |  1.42|  1.63|  2.52|  2.51|
|Castilla y León    |  1.06|  1.96|    * |  1.95|
|Cataluña           |  1.42|  1.52|  2.04|  2.65|
|Extremadura        |  2.01|  4.48|    * |    * |
|Galicia            |  0.95|  3.51|  1.97|  3.46|
|La Rioja           |  1.34|  2.95|  1.80|  3.34|
|Madrid             |  1.17|  0.77|  1.26|  0.94|
|Murcia             |  0.91| 11.46|  5.62|  4.01|
|Navarra            |  1.33|  3.77|  2.32|  2.39|
|País Vasco         |  1.18|  1.45|  1.16|  1.42|
|ESPAÑA             |  0.83|  1.00|    * |  1.52|


__Tabla 2:__ Promedios de los errores relativos (%) en las predicciones a 2 días por Comunidad Autónoma.

|                   | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|------:|------:|------:|------:|
|Andalucía          |   3.51|   4.40|   4.00|  10.68|
|Aragón             |   3.23|  10.77|   3.14|  10.38|
|Asturias           |   3.33|   8.95|   3.95|   9.22|
|Baleares           |   3.70|  10.82|   6.85|   6.96|
|C. Valenciana      |   3.21|   4.67|     * |     * |
|Canarias           |   2.78|  13.53|   4.77|   9.20|
|Cantabria          |   2.03|  13.28|   2.15|   6.82|
|Castilla-La Mancha |   3.41|   2.55|   5.74|   5.43|
|Castilla y León    |   2.65|   4.40|     * |   4.36|
|Cataluña           |   3.46|   4.34|   4.60|   3.33|
|Extremadura        |   3.25|   8.49|     * |     * |
|Galicia            |   3.40|   8.04|   4.90|   8.33|
|La Rioja           |   3.00|   4.21|   3.81|   6.36|
|Madrid             |   3.68|   2.02|   3.33|   2.64|
|Murcia             |   2.55|  18.84|  10.32|   7.52|
|Navarra            |   2.75|   6.85|   3.74|   4.68|
|País Vasco         |   3.35|   3.07|   2.90|   2.81|
|ESPAÑA             |   2.71|   2.80|     * |   1.55|

*_Datos no disponibles debido al cambio de criterio en la contabilización de los casos (acumulados en vez de prevalencia)._


## Referencias
[Etxeberria, J., Goicoa, T., Ugarte, M.D., and Militino, A.F. (2014). Evaluating space-time models for short-term cancer mortality risk predictions in small areas. _Biometrical Journal_, __56(3)__, 383-402.](https://doi.org/10.1002/bimj.201200259)

[Rue, H., Martino, S., & Chopin, N. (2009). Approximate Bayesian inference for latent Gaussian models by using integrated nested Laplace approximations. _Journal of the Royal Statistical Society: Series B_, __71(2)__, 319-392.]( https://doi.org/10.1111/j.1467-9868.2008.00700.x)

[Ugarte, M.D., Adin, A., Goicoa, T., and Militino, A.F. (2014). On fitting spatio-temporal disease mapping models using approximate Bayesian inference. _Statistical Methods in Medical Research_, __23(6)__, 507-530.](https://doi.org/10.1177/0962280214527528)
