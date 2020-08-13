---
author: "Bart"
title: "CO₂ emissions per capita in history: a bar chart race"
date: 2020-03-29T12:00:06+09:00
description: "Probando Flourish para hacer graficos dinámicos"
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: Bart
categories:
- Visualization
tags: 
- Flourish
- Visualization
- Data
- Bar Chart Race
series:
- DataViz
libraries:
- Flourish
- mathjax
image: images/co2.png
---

# Bar chart race

Siguiendo un poco el interés que me suscita la representación visual de datos, aprovechando la cuarentena me puse a descubrir la mejor forma de hacer una "carrera de gráficos de barras". 

Este tipo de visualización ha cogido fama últimamente. Más que por su su utilidad a la hora de analizar los datos, por su forma atractiva y visual de presentar la información, haciéndola muy apetecible al público en general y prestándose a ofrecer videos interesantes fáciles de consumir. 

Por esta razón, y aprovechando para adquirir nuevos conocimientos que me pueden ser útiles en el futuro, me puse a replicar este tipo de visualización gráfica. El objetivo de estos posts no es solo aprender herramientas nuevas o rebuscar códigos interesantes, también ser capaz de ofrecer un gráfico final vistoso que sea consumible.

## Opciones
Buscando por internet encontré varias opciones para relizar este tipo de gráficos. 
- Python: Python siempre sale a relucir sea cual sea tu requerimiento. En esta ocasión encontré posts en [TowardsDataScience](https://towardsdatascience.com/bar-chart-race-in-python-with-matplotlib-8e687a5c8a41) donde te explicaban paso a paso como conseguir el efecto. Aún así, los resultados que veía, si bien per se eran interesantes, no llegaban al resultado final que estaba buscando. 
- Tableau: Tableau es otro clásico de la visualización utilizado por muchas empresas con una opción gratuita en [Tableau Public](https://public.tableau.com/en-us/s/) con un gran potencial para realizar gráficos interactivos de todo tipo y con buen acabado. Algunos de los ejemplos que ví con esta herramienta no me llegaron a captar la atención, por lo que decidí dejar su aprendizaje para más tarde (tengo pendiente ponerme con él).
- Flourish: Llegamos finalmente a [Flourish](https://flourish.studio/). Flourish es otra herramienta que se puede gestionar online que ofrece muchas y variadas visualizaciones. Encontré esta herramienta debido a una de las gráficas que se publicaron en un periódico online. Ojeándola me gustó mucho su acabado y decidí darle una oportunidad para el objetivo que tenía.

## Datos y preprocesado
Una vez que escogí Flourish, quedaba elegir qué datos quería representar. Como llevaba tiempo trabajando con casos de COVID-19 decidí alejarme un poco de esta dinámica y buscar alguna fuente de datos interesante. 

Casi por casualidad ese día estuve comentando los datos sobre las disminuciones de contaminación atmosférica de las grandes ciudades debido al confinamiento. Asi que las emisiones de $CO_2$ rondaban mi mente, y aunque había relación con el COVID19, el aspecto ecológico me atraía bastante. 

Encontrar dataset buenos sobre cualquier tema es complicado, más aún temás ecológicos/climáticos. Por suerte en ensta ocasion cuento con [OurWorldInData](https://ourworldindata.org/per-capita-co2) fuente de datasets de todo tipo con muchisima información y bien formateados. Decidí elegir las emisiones de $CO_2$ por persona. Esencialmente, para calcular la contribución del ciudadano promedio de cada país a las emisiones totales de $CO_2$ se dividen sus emisiones totales por su población, obteniendo las medidas en tonelaadas por usuario por año.

Estas emisiones juegan un papel fundamental dentro de los objetivos climáticos de los años venideros y, como dicen en la web: gracias a las reconstrucciones históricas, están disponibles para todo el mundo desde mediados del siglo XVIII.

Esto nos permite captar tendencias globales, casos concretos con cifras muy altas y analizar quienes son los principales emisores de $CO_2$

Una vez descargamos los datos y los exportamos a Flourish, tenemos un par de problemas:
- Formato de los datos: Los datos se encuentran por fecha y pais, pero, para repesentarlos como queremos necesitamos que se muestren como una serie temporal. Con ese fin, simplemente mapeamos los distintos años y creamos columnas con cada país.
 
- Datos perdidos y nuevos paises: Algunos países no poseen todos los datos, en estos casos hemos optado por hacer una media entre el año posterior del que tenemos datos y el año anterior del cual tenemos datos. No es una solución ideal, pero como este tipo de gráfico no acaba representando toda la información, mas tarde nos cercioramos de que ninguno de los países en los cuales hicimos este procesado sale en el gráfico final. Para aquellos países que no tienen datos hasta un determinado año, la información se completa con ceros.

Una vez solventados estos dos problemas, toqueteamos las opciones de Flourish hasta que nos convenza el diseño.

## Resultado final

### Grafico interactivo

Este es el resultado final. Un gran acabado, muy contento con el resultado ¡y es interactivo!

<div class="flourish-embed flourish-bar-chart-race" data-src="visualisation/1711011"><script src="https://public.flourish.studio/resources/embed.js"></script></div>


### Video

Este tipode gráficos también quedan vistosos en video, aquí os dejo el resultado con musiquita:

{{< youtube byDiAC9Xvug >}}

### Conclusiones curiosas

Por un lado destacan aquellos paises que son grandes productores de crudo, sobre todo aquellos con una población pequeña (Qatar , Kuwait...). Por otra parte destaca un pico en Brunei a mediados del siglo XX, este pico da para mucho y debería escribir un post sobre él. 

Dicho esto, creo que los resultados son mas que satisfactorios, una herramienta interesante y habilidades de manejo que pueden serme útiles si necesito tirar de graficos animados e interactivos con formatos que otras librerías no tienen (o cuesta mucho implementar).

