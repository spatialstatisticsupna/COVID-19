# COVID-19
Este repositorio contiene mapas descriptivos de la situación diaria acumulada y predicciones a corto plazo de la expansión de la enfermedad por el coronavirus SARS-CoV-2 (COVID-19) en las Comunidades Autónomas de España. Los resultados se actualizan diariamente en función de los datos publicados por el Ministerio de Sanidad.

## Fuente de los datos

- [Ministerio de Sanidad, Consumo y Bienestar Social](https://www.mscbs.gob.es/profesionales/saludPublica/ccayes/alertasActual/nCov-China/situacionActual.htm)
- [Instituto de Salud Carlos III](https://covid19.isciii.es/)
- Datos disponibles en el GitHub de [Datadista](https://github.com/datadista/datasets/tree/master/COVID%2019)


## Metodología

Los modelos utilizados para la predicción de las variables (número de fallecimientos, número de ingresos, número de casos confirmados, número de enfermos hospitalizados -todas ellas acumuladas-) son modelos espacio-temporales diseñados para el análisis de datos de conteo en áreas pequeñas. Han sido utilizados esencialmente para suavizar tasas y riesgos en enfermedades crónicas fundamentalmente y para predecir a corto plazo la carga de cáncer, entre otras aplicaciones (Etxeberria et al, 2014). Por ello, no son posiblemente los modelos más adecuados para el estudio de datos de una pandemia. Sin embargo hemos comprobado que las predicciones a muy corto plazo (a uno y dos días) funcionan razonablemente bien y por ello los hemos utilizado para predecir casos en las variables anteriormente mencionadas en las comunidades autónomas españolas (a excepción de Canarias, Ceuta y Melilla).  Canarias se ha analizado por separado, mediante un modelo de splines.

Los modelos utilizados incorporan dependencia espacial mediante el uso de efectos aleatorios que siguen distribuciones tipo CAR. La dependencia temporal se incorpora utilizando splines con distintos tipos de penalizaciones. Además se tiene en cuenta la dependencia espacio-temporal con cuatro tipos distintos de interacciones (tipo I, II, III y IV). La inferencia de todos los modelos analizados se ha llevado a cabo con INLA (ver por ejemplo Ugarte et al., 2014).

La selección del mejor modelo se ha realizado utilizando la regla de de Dawid–Sebastiani (DSS) (Dawid and Sebastiani, 1999).


## Resultados
Los mapas descriptivos con los datos diarios actualizados y las predicciones a corto plazo para las Comundidades Autónomas de España están disponibles en el siguiente enlace:
[INSERTAR ENLACE]()


## Referencias
[Etxeberria, J., Goicoa, T., Ugarte, M.D., and Militino, A.F. (2014). Evaluating space-time models for short-term cancer mortality risk predictions in small areas. _Biometrical Journal_, __56(3)__, 383-402.](https://doi.org/10.1002/bimj.201200259)

[Riebler, A., Held, L., and Rue, H. (2012). Estimation and extrapolation of time trends in registry data - borrowing strength from related populations. _Institute of Mathematical Statistics_, __6(1)__, 304-333.](https://doi.org/10.1214/11-AOAS498)

[Ugarte, M.D., Adin, A., Goicoa, T., and Militino, A.F. (2014). On fitting spatio-temporal disease mapping models using approximate Bayesian inference. _Statistical Methods in Medical Research_, __23(6)__, 507-530.](https://doi.org/10.1177/0962280214527528)
