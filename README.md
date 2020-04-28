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
[COVID-19_20200427.html](https://emi-sstcdapp.unavarra.es/COVID-19/COVID-19_20200427.html)



Archivos anteriores: [ver directorio](https://emi-sstcdapp.unavarra.es/COVID-19/)

_NOTAS_: 

1. Para la comunidad de Madrid las variables "hospitalizados" y "UCI", para esta última también en Galicia, son __datos de prevalencia__ (personas ingresadas a fecha de hoy). Es decir, no reflejan el total de personas que han sido hospitalizadas o ingresadas en UCI a lo largo del periodo de notificación.

2. Para los análisis posteriores al 07/04/2020, se ha incluido la variable que recoge los __casos activos__ en cada comunidad, la cuál excluye a los pacientes que se han recuperado o han fallecido.

3. Para los análisis posteriores al 15/04/2020, se ha incluido el mapa con la __tasa de letalidad__ (nº de fallecidos / nº de casos positivos) y su evolución en el tiempo. 

4. Para los análisis posteriores al 23/04/2020, los datos de casos confirmados corresponden al __total de personas con test positivo incluyendo PCR y positivos a test de anticuerpos__ (suma de las variables `PCR+` y `TestAc+` facilitadas por el Instituto de Salud Carlos III).


## Referencias
[Etxeberria, J., Goicoa, T., Ugarte, M.D., and Militino, A.F. (2014). Evaluating space-time models for short-term cancer mortality risk predictions in small areas. _Biometrical Journal_, __56(3)__, 383-402.](https://doi.org/10.1002/bimj.201200259)

[Rue, H., Martino, S., & Chopin, N. (2009). Approximate Bayesian inference for latent Gaussian models by using integrated nested Laplace approximations. _Journal of the Royal Statistical Society: Series B_, __71(2)__, 319-392.]( https://doi.org/10.1111/j.1467-9868.2008.00700.x)

[Ugarte, M.D., Adin, A., Goicoa, T., and Militino, A.F. (2014). On fitting spatio-temporal disease mapping models using approximate Bayesian inference. _Statistical Methods in Medical Research_, __23(6)__, 507-530.](https://doi.org/10.1177/0962280214527528)
