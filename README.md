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
[COVID-19_20200422.html](https://emi-sstcdapp.unavarra.es/COVID-19/COVID-19_20200422.html)

Para los análisis posteriores al 07/04/2020, se ha incluido la variable que recoge los casos activos en cada comunidad, la cuál excluye a los pacientes que se han recuperado o han fallecido.

Archivos anteriores: [ver directorio](https://emi-sstcdapp.unavarra.es/COVID-19/)

_NOTA: Para las comunidades de Castilla-La Mancha y Madrid las variables "hospitalizados" y "UCI", para esta última también en Castilla y León y Galicia, son datos de prevalencia (personas ingresadas a fecha de hoy). Es decir, no reflejan el total de personas que han sido hospitalizadas o ingresadas en UCI a lo largo del periodo de notificación._


### Validación de las predicciones (_actualizado el 17/04/2020_)

__Tabla 1:__ Promedios de los errores relativos (%) en las predicciones a 1 día por Comunidad Autónoma.

|                   | Casos Activos | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|-----:|-----:|-----:|-----:|-----:|
|Andalucía          |  1.22|  0.96|  2.25|  1.00|  5.16|
|Aragón             |  1.27|  1.15|  3.62|  1.21|  3.59|
|Asturias           |  2.03|  1.40|  4.21|  1.26|  3.19|
|Baleares           |  3.96|  1.10|  4.50|  2.00|  2.12|
|C. Valenciana      |  1.49|  0.93|  1.60| 1.33*| 2.07*|
|Canarias           |  2.09|  1.16|  4.49|  1.87|  3.04|
|Cantabria          |  1.84|  0.84|  4.95|  0.78|  2.62|
|Castilla-La Mancha |  2.11|  1.24|  1.49|  2.60|  2.31|
|Castilla y León    |  1.24|  0.89|  1.42| 0.53*|  1.12|
|Cataluña           |  1.62|  1.27|  1.19|  1.46|  2.10|
|Extremadura        |  2.54|  1.80|  3.18| 1.70*| 6.65*|
|Galicia            |  0.39|  0.81|  2.83|  1.61|  2.51|
|La Rioja           |  4.61|  1.87|  2.43|  1.52|  2.26|
|Madrid             |  1.61|  0.98|  0.59|  1.34|  1.13|
|Murcia             |  3.82|  1.02|  8.73|  3.97|  2.96|
|Navarra            |  1.24|  1.08|  3.94|  1.66|  1.49|
|País Vasco         |  2.27|  0.96|  1.38|  0.96|  1.03|
|ESPAÑA             |  0.59|  0.67|  0.75|      |      |


__Tabla 2:__ Promedios de los errores relativos (%) en las predicciones a 2 días por Comunidad Autónoma.

|                   | Casos Activos | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|------:|------:|------:|------:|------:|
|Andalucía          |   1.65|   2.68|   4.23|   2.97|   7.81|
|Aragón             |   1.74|   2.94|   7.67|   2.80|   7.17|
|Asturias           |   3.13|   2.57|   7.07|   3.46|   6.24|
|Baleares           |   6.81|   2.85|   7.46|   4.76|   4.50|
|C. Valenciana      |   2.35|   2.62|   3.47|  3.04*|  4.27*|
|Canarias           |   4.08|   2.21|   9.40|   3.57|   6.41|
|Cantabria          |   3.75|   1.89|   9.42|   2.08|   5.59|
|Castilla-La Mancha |   3.57|   2.94|   2.48|   5.49|   4.23|
|Castilla y León    |   1.49|   1.96|   3.17|  1.32*|   1.69|
|Cataluña           |   3.08|   2.88|   3.00|   3.45|   2.89|
|Extremadura        |   5.64|   3.47|   5.70|  3.73*| 12.18*|
|Galicia            |   0.75|   2.57|   6.18|   3.70|   5.67|
|La Rioja           |   8.00|   3.82|   3.78|   3.34|   4.27|
|Madrid             |   3.21|   2.82|   1.48|   3.21|   2.56|
|Murcia             |   7.66|   2.21|  14.27|   7.44|   5.49|
|Navarra            |   1.88|   2.36|   5.89|   3.09|   2.92|
|País Vasco         |   5.51|   2.54|   3.00|   2.37|   2.11|
|ESPAÑA             |   0.77|   2.08|   2.09|       |      |


*_Datos calculados teniendo en cuenta las predicciones posteriores al 08/04 debido al cambio de criterio en la contabilización de los casos (acumulados en vez de prevalencia)._


## Referencias
[Etxeberria, J., Goicoa, T., Ugarte, M.D., and Militino, A.F. (2014). Evaluating space-time models for short-term cancer mortality risk predictions in small areas. _Biometrical Journal_, __56(3)__, 383-402.](https://doi.org/10.1002/bimj.201200259)

[Rue, H., Martino, S., & Chopin, N. (2009). Approximate Bayesian inference for latent Gaussian models by using integrated nested Laplace approximations. _Journal of the Royal Statistical Society: Series B_, __71(2)__, 319-392.]( https://doi.org/10.1111/j.1467-9868.2008.00700.x)

[Ugarte, M.D., Adin, A., Goicoa, T., and Militino, A.F. (2014). On fitting spatio-temporal disease mapping models using approximate Bayesian inference. _Statistical Methods in Medical Research_, __23(6)__, 507-530.](https://doi.org/10.1177/0962280214527528)
