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
[COVID-19_20200413.html](https://emi-sstcdapp.unavarra.es/COVID-19/COVID-19_20200413.html)

Para los análisis posteriores al 07/04/2020, se ha incluido la variable que recoge los casos activos en cada comunidad, la cuál excluye a los pacientes que se han recuperado o han fallecido.

Archivos anteriores: [ver directorio](https://emi-sstcdapp.unavarra.es/COVID-19/)

_NOTA: Para las comunidades de Castilla-La Mancha y Madrid las variables "hospitalizados" y "UCI", para esta última también en Castilla y León y Galicia, son datos de prevalencia (personas ingresadas a fecha de hoy). Es decir, no reflejan el total de personas que han sido hospitalizadas o ingresadas en UCI a lo largo del periodo de notificación._


### Validación de las predicciones (_actualizado el 14/04/2020_)

__Tabla 1:__ Promedios de los errores relativos (%) en las predicciones a 1 día por Comunidad Autónoma.

|                   | Casos Activos | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|-----:|-----:|-----:|-----:|-----:|
|Andalucía          |  0.62|  1.01|  2.47|  1.13|  5.92|
|Aragón             |  1.10|  1.01|  4.29|  1.10|  3.92|
|Asturias           |  2.31|  1.47|  4.38|  1.28|  3.66|
|Baleares           |  4.55|  1.19|  5.30|  2.18|  2.35|
|C. Valenciana      |  1.77|  1.08|  1.82| 1.64*| 2.18*|
|Canarias           |  3.04|  1.35|  5.31|  2.19|  3.44|
|Cantabria          |  1.16|  0.97|  5.47|  0.71|  2.92|
|Castilla-La Mancha |  1.69|  1.29|  1.44|  2.53|  2.53|
|Castilla y León    |  1.10|  0.90|  1.63| 0.47*|  0.75|
|Cataluña           |  1.24|  1.29|  1.32|  1.63|  2.21|
|Extremadura        |  2.83|  1.96|  3.64| 2.31*| 7.99*|
|Galicia            |  0.51|  0.91|  3.16|  1.79|  2.83|
|La Rioja           |  3.26|  1.22|  2.78|  1.73|  2.67|
|Madrid             |  1.70|  1.05|  0.69|  1.35|  0.98|
|Murcia             |  3.18|  0.82| 10.05|  4.60|  3.41|
|Navarra            |  1.20|  1.24|  3.12|  1.99|  1.84|
|País Vasco         |  2.73|  1.11|  1.52|  1.08|  1.13|
|ESPAÑA             |  0.51|  0.75|  0.84|      |      |


__Tabla 2:__ Promedios de los errores relativos (%) en las predicciones a 2 días por Comunidad Autónoma.

|                   | Casos Activos | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|------:|------:|------:|------:|------:|
|Andalucía          |   1.03|   3.03|   4.56|   3.55|   9.36|
|Aragón             |   1.09|   3.03|   9.48|   2.91|   8.31|
|Asturias           |   3.83|   2.85|   7.57|   3.62|   7.30|
|Baleares           |   6.50|   3.34|   9.13|   5.71|   5.51|
|C. Valenciana      |   2.03|   3.08|   4.06|  3.90*|  4.86*|
|Canarias           |   3.95|   2.51|  11.27|   4.19|   7.47|
|Cantabria          |   2.06|   2.17|  10.98|   1.93|   6.22|
|Castilla-La Mancha |   3.60|   3.25|   2.33|   5.74|   4.46|
|Castilla y León    |   1.75|   2.33|   3.66|  1.66*|   1.57|
|Cataluña           |   2.97|   3.16|   3.37|   3.79|   2.98|
|Extremadura        |   5.18|   3.52|   6.79|  6.29*| 15.23*|
|Galicia            |   0.61|   3.04|   6.88|   4.18|   6.67|
|La Rioja           |   3.89|   2.84|   4.30|   3.84|   5.22|
|Madrid             |   3.74|   3.13|   1.77|   3.02|   2.35|
|Murcia             |   4.46|   2.30|  16.71|   8.42|   6.36|
|Navarra            |   1.69|   2.60|   5.38|   3.70|   3.64|
|País Vasco         |   6.16|   3.03|   3.30|   2.75|   2.32|
|ESPAÑA             |   0.58|   2.45|   2.34|       |       |

*_Datos calculados teniendo en cuenta las predicciones posteriores al 08/04 debido al cambio de criterio en la contabilización de los casos (acumulados en vez de prevalencia)._


## Referencias
[Etxeberria, J., Goicoa, T., Ugarte, M.D., and Militino, A.F. (2014). Evaluating space-time models for short-term cancer mortality risk predictions in small areas. _Biometrical Journal_, __56(3)__, 383-402.](https://doi.org/10.1002/bimj.201200259)

[Rue, H., Martino, S., & Chopin, N. (2009). Approximate Bayesian inference for latent Gaussian models by using integrated nested Laplace approximations. _Journal of the Royal Statistical Society: Series B_, __71(2)__, 319-392.]( https://doi.org/10.1111/j.1467-9868.2008.00700.x)

[Ugarte, M.D., Adin, A., Goicoa, T., and Militino, A.F. (2014). On fitting spatio-temporal disease mapping models using approximate Bayesian inference. _Statistical Methods in Medical Research_, __23(6)__, 507-530.](https://doi.org/10.1177/0962280214527528)
