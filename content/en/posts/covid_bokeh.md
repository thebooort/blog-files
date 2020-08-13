---
author: "Bart"
title: "COVID19 + Bokeh"
date: 2020-03-19T12:00:06+09:00
description: "Graficos sobre COVID19 usando bokeh"
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: Bart
authorEmoji: 👻
tags: 
- COVID19
- Python
- Visualization
series:
- COVID19 visualization
libraries:
- pandas
- bokeh
categories:
- coding
image: images/covid_plot/plot.jpg
---
Este post comienza una serie sobre visualización del COVID-19. La motivación para hacerla no es otra que ocupar los ratos muertos de la cuarentena para aprender a crear gráficos interactivos con Bokeh.

Y de paso ofrecer un vistazo objetivo a los datos que nos llegan sobre la enfermedad. Sé que suena un poco raro pero ya que voy a estar dándole vueltas al tema, tener este enfoque objetivo me ayuda a sobrellevarlo. 

En cuanto depure los códigos los subo a github y tendréis el enlace aquí:

## COVID19- El caso de Andalucía

Comenzamos con el gráfico que primero vino a mi cabeza. Mi idea era obtener los datos de las provincias andaluzas, pero, hasta la fecha de subir este post, no encontraba más que los de las comunidades autónomas. 

En este caso, el ejercicio me llevó a comenzar de cero con Bokeh. Un gráfico tan sencillo como ese sirve para iniciarte en los aspectos básicos de la librería, de los cuales destaco:

- Hovers: son las capas de visualización que te dan información sobre un punto cuando pasas el raton por encima

- Curdoc: importada desde bokeh.io, te permite cambiar el estilo del grafico (a modo dark jeje)

- Manejo de TOOLS: que indica que herramientas quieres que presente el gráfico interactivo para ser manipulado. En mi caso:
``` python
TOOLS = 'crosshair,save,pan,box_zoom,reset,wheel_zoom'
plot = figure(tools=TOOLS)
```
- Plot de datos temporales: Hubo que hacer algún reajuste sobre el tipo de datos y luego indicarle a bokeh que estabamos trabajando con esto en su creacion: 
``` python
plot = figure(x_axis_type='datetime', tools=TOOLS)
```
Finalmente opté por crear mi primer gráfico con puntos y líneas. 

### Graficos
<iframe width="100%" height="700" src="/images/covid_plot/plot_andalucia(3).html">
</iframe>


### Data Source
Todos los datos están obtenidos de [Numeroteca COVID-19](https://code.montera34.com:4443/numeroteca/covid19)

### Librerías usadas
- [Bokeh](https://bokeh.org/)
- [Pandas](https://pandas.pydata.org/)
