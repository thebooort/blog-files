---
author: "Bart"
title: "COVID19 + Bokeh - Mapas!"
date: 2020-03-22T12:00:06+09:00
description: "Graficos sobre COVID19 usando bokeh"
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: Bart
categories:
- coding
tags: 
- COVID19
- Python
- Visualization
series:
- COVID19 visualization
libraries:
- pandas
- bokeh
- geopandas
image: images/covid_plot/plot.jpg
---
Este post continúa la serie sobre visualización del COVID-19. La motivación para hacerla no es otra que ocupar los ratos muertos de la cuarentena para aprender a crear gráficos interactivos con Bokeh.

Y de paso ofrecer un vistazo objetivo a los datos que nos llegan sobre la enfermedad. Sé que suena un poco raro pero ya que voy a estar dándole vueltas al tema, tener este enfoque objetivo me ayuda a sobrellevarlo. 

En cuanto depure los códigos los subo a github y tendréis el enlace aquí: 

## COVID19 - Gráficos de Europa

Para cerrar (por ahora) esta introducción que me estoy haciendo a la biblioteca Bokeh, quería aportar luz sobre la evolución de la enfermedad por el mundo. 

Ni por estudios ni por trabajo, nunca me ha tocado trabajar con datos geográficos. Es por eso que quería llenar un poco la laguna que tengo a la hora de representarlos gráficamente. He visto que bokeh es un excelente recurso para eso, asi que me he lanzado a sacarle partido. 

En esta ocasión estoy siguiendo un [tutorial de Shivangi Patel](https://towardsdatascience.com/a-complete-guide-to-an-interactive-geographical-map-using-python-f4c5197e23e0).

El tutorial está estupendo y sirve no solo como introducción para plotear mapas si no también para cómo hacerlo en Bokeh y como usar Bokeh para generar un minidashboard en el que los datos vayan actualizandose. 

Esto último, requiere de un server que lamentable mente no tengo, asi que os dejo un su lugar un video del resultado. 

Por otra parte, he aprovechado para trabajar con geopandas y empaparme un poco del tema de datos geográficos. Lamentablemente el dataset consultado usaba un GEOID un tanto raro, que no he conseguido acoplar correactamente al archivo shapes (no usa el estandar de codificacion de países de 3 letras, y no coincide con los que he visto de 2 letras), con lo que la info de algunos países a pesar de tenerla, no está visible. 

En cualquier caso, como introducción, contento con los resultados.

### Graficos

#### Gráfico interactivo de casos y muertes 
Aquí aproveche para manejar pestañas y ofrecer en el mismo grafico la posibilidad de consultar ambas variables en el mundo. Probé con los hover, pero no me encajaron mucho y decidí que esta era la mejor opción.

<iframe width="100%" height="700" src="/images/covid_plot/my_first_map.html">
</iframe>

#### Gráfico interactivo de casos y muertes 
Finalmente añadí la interacción al gráfico de manera que se acualice a cada paso. La verdad que el data set ha mostrado ser insuficiente, con muchos valores perdidos. No obstante, creo que el caso de Italia (podéis hacer zoom :) ) se ve bastante bien como empeora el color. 

Os dejo por aquí el video del resultado 

{{< youtube eGs_CDpOdSE >}}

#### Extra: El dashboard de la Johns Hopkins University
Por último aprovecho para dejaros el dashboard de la Johns Hopkins University, que está muy currado y con la info al día.

<iframe width="650" height="400" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" title="2019-nCoV" src="/gisanddata.maps.arcgis.com/apps/Embed/index.html?webmap=14aa9e5660cf42b5b4b546dec6ceec7c&extent=77.3846,11.535,163.5174,52.8632&zoom=true&previewImage=false&scale=true&disable_scroll=true&theme=light"></iframe>

### Data Source
Todos los datos están obtenidos de [ECDC COVID-19](https://www.ecdc.europa.eu/en/publications-data/download-todays-data-geographic-distribution-covid-19-cases-worldwide)

### Librerías usadas
- [Bokeh](https://bokeh.org/)
- [Pandas](https://pandas.pydata.org/)
- [GeoPandas](https://geopandas.org/)

#### Con esta parte creo que aparco de momento esta serie de COVID+Bokeh en pos de hacer algún post sobre otras herramientas. No obstante, no descarto volver en breve, el tema de la visualización me gusta mucho. 

