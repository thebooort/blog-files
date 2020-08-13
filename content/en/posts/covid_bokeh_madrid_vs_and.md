---
author: "Bart"
title: "COVID19 + Bokeh: Madrid vs. Andalucía"
date: 2020-03-21T12:00:06+09:00
description: "Graficos sobre COVID19 usando bokeh"
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: Bart
authorEmoji: 👻
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
image: images/covid_plot/plot2.jpg
---

Este post continúa la serie sobre visualización del COVID-19. La motivación para hacerla no es otra que ocupar los ratos muertos de la cuarentena para aprender a crear gráficos interactivos con Bokeh.

Y de paso ofrecer un vistazo objetivo a los datos que nos llegan sobre la enfermedad. Sé que suena un poco raro pero ya que voy a estar dándole vueltas al tema, tener este enfoque objetivo me ayuda a sobrellevarlo. 

En cuanto depure los códigos los subo a github y tendréis el enlace aquí:

## COVID19- Madrid vs. Andalucía

Para este segundo post quise usar los datos del crecimiento en Madrid, para compararlos con Andalucía. 

La idea aquí era ver cómo de diferentes habían sido las escaladas de casos y ver cómo quedaban al representarlas la una frente a la otra.

De paso, hacer hincapié en opciones para personalizar. En particular me gusta mucho la opción 'mute' de la lenyenda, que te permite cambiar la opacidad de una de las líneas para visualizar mejor el resto. Os animo a probarla.

``` python
from bokeh.plotting import figure
p = figure()
p.legend.click_policy='mute'
# recordad que podéis personalizar cómo actúa en vuestra gráfica
p.circle(x='date', y='cases', muted_alpha = 0.2)

```

Aún no manejo los hovers bien (¿quizás es problema de cómo está estructurado el dataset?), asi que estoy optando por poner toda la información. Aunque repito que no me gusta el resultado. 

Por otra parte también quise ensayar la unión de dos gráficas, que quizás se veía mas explicativa. Y ojo que han cambiado la orden en Bokeh 2.0.0

``` python
from bokeh.plotting import figure
from bokeh.layouts import row
p = figure()
p1 = figure()
# y aqui la magia
show(row(p,p1))
```
La verdad que es bastante intuitivo. Aunque no esté 100% contento con las gráficos, aprender la librería, hacer cositas mas o menos chulas, y poder tirar de ella en el futuro, pinta muy bien. 

Lo cierto es que, además, le estoy cogiendo tirria al dark mode XD.

### Gráficos

#### Madrid
<iframe width="100%" height="700" src="/images/covid_plot/plot_madrid.html">
</iframe>



#### Andalucía
<iframe width="100%" height="700" src="/images/covid_plot/plot_andalucia(3).html">
</iframe>


#### M vs A (misma gráfica)
<iframe width="100%" height="700" src="/images/covid_plot/plot_andaluciavsmadrid.html">
</iframe>

#### M vs. A (gráficas diferentes)
 Aquí estña el último! Creo que es el que mejor ha quedado, donde he puesto mejor los hovers, y además he ocultado la toolbar si no estás sobre el gráfico!

<iframe width="1200" height="700" src="/images/covid_plot/plot_andaluciaymadrid.html">
</iframe>



### Data Source
Todos los datos están obtenidos de [Numeroteca COVID-19](https://code.montera34.com:4443/numeroteca/covid19)

### Librerías usadas
- [Bokeh](https://bokeh.org/)
- [Pandas](https://pandas.pydata.org/)
