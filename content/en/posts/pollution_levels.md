---
author: "Bart"
title: "El aire que respiramos durante el confinamiento"
date: 2020-04-08T12:00:06+09:00
description: "Evolución de los niveles de polución en Granada durante la cuarentena"
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: Bart
categories:
- coding
- Data Science
tags: 
- Visualization
- Data
- COVID19
- Python
- Pollution
- Ecology
- Air Quality
series:
- Data Science
libraries:
- mathjax
image: images/polucion.png
---
Image credit: [Ivan Aleksic @ivalex Unsplash](https://unsplash.com/photos/WrYM0tBbYj0)

# ¿Cómo afecta el confinamiento a los niveles de polución?

Durante la cuarentena que estamos viviendo la reducción de la movilidad de las personas es evidente. 
Ligada a esta disminución del tránsito de vehiculos particulares, vehiculos de transporte público y algunas maquinarias pertenecientes a servicios que se encuentran inactivos, muchos [medios se han hecho eco de la disminución en los niveles de polución ambiental](https://www.sciencealert.com/here-s-what-covid-19-is-doing-to-our-pollution-levels). Es más, al ser COVID una enfermedad que afecta a las vías respiratorias, ya hay algunos analisis que relacionan la polución del aire con tasas de moratilidad mas altas por COVID.

Por este motivo me pareció interesante estudiar el caso de la ciudad en la que resido: Granada(España).

La evidencia muestra que los niveles de polución han bajado, pero ¿cómo sabemos esto?.
Para contestar a esto vamos a tomar dos enfoques: primero, conocer qué buscamos en el aire para mediar su calidad, y, segundo, conocer alguna técnica que nos ofrezca los datos necesarios para nuestro análisis.

## ¿Qué buscamos?
La [calidad del aire](http://www.troposfera.org/conceptos/calidad-aire/) se mide en relación a la presencia y cantidad de determinados contaminantes en el aire. Los principales contaminantes monitorizados suelen estar determinados por la legislación vigente, que también determina qué baremos se utilizan para evaluar cada uno. 

Aun así, hay una [gran variedad de contaminantes](http://movil.asturias.es/portal/site/medioambiente/menuitem.1340904a2df84e62fe47421ca6108a0c/?vgnextoid=daca2ae109539210VgnVCM10000097030a0aRCRD&vgnextchannel=761ab1cc11b6a110VgnVCM1000006a01a8c0RCRD&i18n.http.lang=es) sobre los cuales existe un conseso (en cuanto a su peligrosidad) y que son monitorizados habitualmente en estaciones medidoras de calidad del aire (habitualmente en ciudades). Algunos ejemplos son:
- $NO_2$ y en general los óxidos de nitrógeno. Estos se producen como consecuencia del uso de combustibles fósiles como petróleo, carbón o gas natural. Es un contaminante muy perjudicial.
- $CO_2$ y $CO$ su origen antropogénico es debido a la combustión incompleta de materias orgánicas (gas, carbón, madera, etc.), en especial los carburantes de los automóviles.

A estos habría que sumarles otros como las particulas en suspensión ($PM_5$ o $PM_10$ según su tamaño), el Ozono, el Dióxido de azufre, etc. 

Despúes de consultar diversas páginas y leer las noticias sobre polución y COVID, me quedaba claro que sería muy interesante comprobar los niveles de NO_2, pues tienen una clara relación con las actividades de transporte y su uso está muy extendido como parámetro que mide la calidad del aire. 

## Getting the data

¿Cómo obtenemos los datos? Esencialmente los datos sobre los contaminantes se pueden encontrar en internet vía dos posibles orígenes. 

Por una parte muchos de estos datos se originan en estaciones de medición locales. Estas permiten una obtención de datos directamente de nucleos urbanos particulares, con una cantidad de datos relativamente pequeña. La parte negativa es que dependes de los sensores de la estación. En mi caso, Granada tiene varias estaciones, pero por ejemplo no pude encontrar datos de Ozono o de las partículas en suspensión. 

La otra opción es usar datos de satélite. Aunque hay datos bastante actualizados sobre estas mediciones, habitualmente pesan bastante (puesto que se parten solo regiones grandes como Europa o America del Norte), y ahora mismo mi conexión de internet no da para tanto. 

Particularizando esta última opción, si os véis valientes en Europa tenempos el TROPOMI, un instrumento de monitorización de la trposfera que tiene datos de NO2 que forma parte del [Sentinel-5 de la Agencia Espacial Europea](https://sentinel.esa.int/web/sentinel/missions/sentinel-5). 

Finalmente, para mi análisis me dicidí por usar datos de las estaciones locales, aunque solo encontré de NO2, al menos son datos oficiales y de un volumen manejable para tratarlos. Como extra también tuve acceso al histórico de otros años, para así compararlo. Toda la información la saqué de la [Agencia Medioambiental Europea](https://www.eea.europa.eu/themes/air).

## Analyzing the data

La verdad es que los datos no estaban en la mejor versión posible. Además fue un poco lioso conseguirlos. Aún así, con un poco de preprocesado obtuve lo que buscaba.

Lo único a destacar durante esta fase es la conversion a dato tipo fecha que necesitas para plotear datos pertenecientes a series temporales: 

```python
no2_df_2020['date'] = pd.to_datetime(no2_df_2020['date_time'])
no2_df_2019['date'] = pd.to_datetime(no2_df_2019['date_time'])
```

En este aspecto ospuede ayudar strftime, pues que en muchas ocasiones os vais a encontrar fechas en formatos muy diferentes. Es habitual tambien que algunas librerías requieran el formato de año-mes-dia , o mes-dia-año, para todas estas ocasiones con strftime podéis salir del paso.
(El ejemplo es de otro código pero así os haceís una idea de como usarlo)
```python
df['date'] = pd.to_datetime(df["date"].dt.strftime('%d/%m/%Y'))
```

Y bueno, como ya sabéis empecé a usar bokeh hace poco, asi que esto era una situación perfecta para poner a prueba mis conocimientos.

## Plot

<iframe width="100%" height="700" src="/images/plot_no2.html">
</iframe>

He marcado con verde ( no lo había usado antes) el nivel de contaminante que la OMS considera seguro (en media al año).

Para ello he usado la funcionalidad BoxAnnotation, que además puede personalizarse un monton y se puede usar con fechas de inicio y fin: 

```python
low_box = BoxAnnotation(top=40, fill_alpha=0.1, fill_color='green')
top_box = BoxAnnotation(bottom=40, top=80, fill_alpha=0.1, fill_color='red')
p1.add_layout(low_box)
p1.add_layout(top_box)
```
Añadí el marcaje del día en el que se inicia la cuarentena. Además saqué la leyenda fuera, porq dentro del gráfico molestaba bastante: 

```python
from bokeh.models import Legend
legend = Legend(items=[
    ("2020"   , [r1,r2]),
    ("2019" , [r3, r4]),

], location="center")

p1.add_layout(legend, 'right')
```

## Conclusions!

Si bien es cierto que en abril hay un descenso en los dos años (puede que la lluvia ayude), veníamos de un febrero muy caluroso y sin apenas lluvia, por lo tanto veníamos de una situación negativa. También se puede observar que ya de por sí nos encontrabamos en un punto muy bueno, menor al del año pasado. Me llama la atención un pequeño repunte (quizas por el mayor uso de coches unipersonales para ir al trabajo en lugar de transporte público?), con todo, estamos lejos de los niveles del año pasado. No olvidemos tampoco que estamos representando un promedio semanal, con lo que captamos eventos que han podido pasar durante la semana completa.

A mitad del encierro hay una gran bajada que nos deja en un nivel muy bajo y posiblemente relacionada con la mayor restricción de circulación. Llegamos a un punto muy inferior a otros años por la misma fecha, lo que parece indicar que sí que se debe a causas antropológicas. Además es un buen indice de que la gente se está tomando en serio la cuarentena :) y que aunque sea por unos días, estamos respirando un aire más limpio.





