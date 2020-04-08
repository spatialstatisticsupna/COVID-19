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
[COVID-19_20200406.html](https://emi-sstcdapp.unavarra.es/COVID-19/COVID-19_20200406.html)

Archivos anteriores: [ver directorio](https://emi-sstcdapp.unavarra.es/COVID-19/)

_NOTA: Para las comunidades de Castilla y León, Castilla-La Mancha, Madrid y Comunidad Valenciana las variables "hospitalizados" y "UCI", para esta última también en Galicia, son datos de prevalencia (personas ingresadas a fecha de hoy). Es decir, no reflejan el total de personas que han sido hospitalizadas o ingresadas en UCI a lo largo del periodo de notificación._


### Validación de las predicciones

__Tabla 1:__ Promedios de los errores relativos (%) en las predicciones a 1 día por Comunidad Autónoma.

|                   | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|-----:|-----:|-----:|-----:|
|Andalucía          |  1.34|  2.42|  1.42|  9.12|
|Aragón             |  1.32|  5.92|  1.56|  5.40|
|Asturias           |  1.82|  5.70|  1.86|  4.58|
|Baleares           |  1.56|  6.75|  2.99|  3.65|
|C. Valenciana      |  1.21|  2.20|  3.42|  1.99|
|Canarias           |  1.66|  7.32|  3.02|  5.39|
|Cantabria          |  1.00|  8.02|  0.83|  4.27|
|Castilla-La Mancha |  1.50|  1.71|  2.87|  2.29|
|Castilla y León    |  1.11|  2.21|  1.95|  2.48|
|Cataluña           |  1.55|  1.75|  2.57|  3.58|
|Extremadura        |  2.13|  5.27|  6.37|  6.15|
|Galicia            |  1.20|  3.88|  2.39|  4.46|
|La Rioja           |  1.06|  3.39|  2.15|  4.17|
|Madrid             |  1.20|  0.73|  1.42|  1.12|
|Murcia             |  1.03| 11.96|  6.80|  4.75|
|Navarra            |  1.25|  4.34|  1.86|  3.18|
|País Vasco         |  1.32|  1.50|  1.41|  1.74|
|ESPAÑA             |  0.93|  1.01|  1.90|  1.82|


__Tabla 2:__ Promedios de los errores relativos (%) en las predicciones a 2 días por Comunidad Autónoma.

|                   | Casos confirmados | Fallecidos | Hospitalizados | UCI |
|:------------------|------:|------:|------:|------:|
|Andalucía          |   4.84|   4.29|   5.37|  13.89|
|Aragón             |   4.56|  14.17|   4.34|  11.46|
|Asturias           |   4.38|  10.90|   4.98|  11.21|
|Baleares           |   4.47|  12.29|   9.22|   9.70|
|C. Valenciana      |   3.90|   5.47|   7.81|   5.18|
|Canarias           |   3.21|  16.20|   5.98|  11.68|
|Cantabria          |   1.97|  17.51|   3.00|   9.54|
|Castilla-La Mancha |   3.51|   3.44|   4.65|   5.14|
|Castilla y León    |   3.47|   4.46|   4.62|   5.99|
|Cataluña           |   3.59|   5.08|   6.22|   4.11|
|Extremadura        |   4.30|  10.24|   8.56|  14.36|
|Galicia            |   4.55|   8.40|   6.53|  11.71|
|La Rioja           |   2.84|   4.73|   5.36|   8.84|
|Madrid             |   3.83|   2.01|   4.06|   3.09|
|Murcia             |   2.99|  20.03|  11.82|   8.82|
|Navarra            |   3.42|   7.46|   3.88|   6.08|
|País Vasco         |   3.83|   3.48|   3.74|   3.53|
|ESPAÑA             |   3.09|   3.14|   2.90|   2.59|



## Referencias
[Etxeberria, J., Goicoa, T., Ugarte, M.D., and Militino, A.F. (2014). Evaluating space-time models for short-term cancer mortality risk predictions in small areas. _Biometrical Journal_, __56(3)__, 383-402.](https://doi.org/10.1002/bimj.201200259)

[Rue, H., Martino, S., & Chopin, N. (2009). Approximate Bayesian inference for latent Gaussian models by using integrated nested Laplace approximations. _Journal of the Royal Statistical Society: Series B_, __71(2)__, 319-392.]( https://doi.org/10.1111/j.1467-9868.2008.00700.x)

[Ugarte, M.D., Adin, A., Goicoa, T., and Militino, A.F. (2014). On fitting spatio-temporal disease mapping models using approximate Bayesian inference. _Statistical Methods in Medical Research_, __23(6)__, 507-530.](https://doi.org/10.1177/0962280214527528)
