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
[COVID-19_20200411.html](https://emi-sstcdapp.unavarra.es/COVID-19/COVID-19_20200411.html)

Para los análisis posteriores al 07/04/2020, se ha incluido la variable que recoge los casos activos en cada comunidad, la cuál excluye a los pacientes que se han recuperado o han fallecido.

Archivos anteriores: [ver directorio](https://emi-sstcdapp.unavarra.es/COVID-19/)

_NOTA: Para las comunidades de Castilla-La Mancha y Madrid las variables "hospitalizados" y "UCI", para esta última también en Castilla y León y Galicia, son datos de prevalencia (personas ingresadas a fecha de hoy). Es decir, no reflejan el total de personas que han sido hospitalizadas o ingresadas en UCI a lo largo del periodo de notificación._


### Validación de las predicciones (_actualizado el 12/04/2020_)

__Tabla 1:__ Promedios de los errores relativos (%) en las predicciones a 1 día por Comunidad Autónoma.

|                   | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|-----:|-----:|-----:|-----:|
|Andalucía          |  1.01|  2.07|  1.12|  6.47|
|Aragón             |  1.05|  4.70|  1.17|  4.51|
|Asturias           |  1.53|  4.93|  1.39|  4.08|
|Baleares           |  1.34|  5.88|  2.39|  2.66|
|C. Valenciana      |  1.13|  2.02|    * |    * |
|Canarias           |  1.48|  5.82|  2.42|  3.94|
|Cantabria          |  0.96|  6.23|  0.65|  3.08|
|Castilla-La Mancha |  1.44|  1.59|  2.43|  2.52|
|Castilla y León    |  1.01|  1.82|    * |  1.83|
|Cataluña           |  1.33|  1.47|  1.87|  2.51|
|Extremadura        |  1.92|  4.14|    * |    * |
|Galicia            |  0.96|  3.23|  1.90|  3.14|
|La Rioja           |  1.37|  2.72|  1.67|  3.04|
|Madrid             |  1.14|  0.78|  1.16|  0.95|
|Murcia             |  0.84| 11.17|  5.13|  3.64|
|Navarra            |  1.29|  3.43|  2.24|  2.17|
|País Vasco         |  1.21|  1.40|  1.08|  1.29|
|ESPAÑA             |  0.81|  0.93|    * |  1.46|


__Tabla 2:__ Promedios de los errores relativos (%) en las predicciones a 2 días por Comunidad Autónoma.

|                   | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|------:|------:|------:|------:|
|Andalucía          |   3.26|   4.11|   3.73|   9.97|
|Aragón             |   3.12|  10.38|   3.13|   9.79|
|Asturias           |   3.07|   8.55|   3.83|   8.58|
|Baleares           |   3.64|  10.28|   6.56|   6.40|
|C. Valenciana      |   3.25|   4.70|     * |     * |
|Canarias           |   2.73|  12.81|   4.62|   8.49|
|Cantabria          |   1.91|  12.59|   1.95|   6.54|
|Castilla-La Mancha |   3.62|   2.63|   5.40|   4.98|
|Castilla y León    |   2.62|   4.10|     * |   4.05|
|Cataluña           |   3.17|   3.93|   4.38|   3.32|
|Extremadura        |   3.24|   7.90|     * |     * |
|Galicia            |   3.16|   7.42|   4.58|   7.78|
|La Rioja           |   2.89|   4.06|   3.74|   5.86|
|Madrid             |   3.41|   1.94|   3.26|   2.53|
|Murcia             |   2.34|  18.40|   9.75|   7.10|
|Navarra            |   2.79|   6.30|   3.99|   4.37|
|País Vasco         |   3.07|   3.11|   2.83|   2.59|
|ESPAÑA             |   2.55|   2.68|     * |   1.64|

*_Datos no disponibles debido al cambio de criterio en la contabilización de los casos (acumulados en vez de prevalencia)._


## Referencias
[Etxeberria, J., Goicoa, T., Ugarte, M.D., and Militino, A.F. (2014). Evaluating space-time models for short-term cancer mortality risk predictions in small areas. _Biometrical Journal_, __56(3)__, 383-402.](https://doi.org/10.1002/bimj.201200259)

[Rue, H., Martino, S., & Chopin, N. (2009). Approximate Bayesian inference for latent Gaussian models by using integrated nested Laplace approximations. _Journal of the Royal Statistical Society: Series B_, __71(2)__, 319-392.]( https://doi.org/10.1111/j.1467-9868.2008.00700.x)

[Ugarte, M.D., Adin, A., Goicoa, T., and Militino, A.F. (2014). On fitting spatio-temporal disease mapping models using approximate Bayesian inference. _Statistical Methods in Medical Research_, __23(6)__, 507-530.](https://doi.org/10.1177/0962280214527528)
