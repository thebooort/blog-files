---
author: "Bart"
title: "Did confinement affect my sleep/exercise routine?"
date: 2020-04-06T12:00:06+09:00
description: "Analyzing sleep patterns before and during COVID19 quarentine"
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
- Machine Learning
series:
- Data Science
libraries:
- mathjax
image: images/cat.png
---
Image credit: [Javier Ezpeleta @javierezpeleta Unsplash](https://unsplash.com/photos/g1GOQsSd_iA)

# Did confinement affects my sleep routine?
Llevamos ya varias semanas de cuarentena y los ánimos varían mucho de un día a otro. Ultimamente han aparecido muchos artículos y estudios sobre el posible impacto del confinamiento en nuestros ritmos de vida. El tema me despertaba bastante curiosidad desde el principio, y da la casualidad de que por mis otros hobbies (trail running) tengo un reloj capaz de captar algunas de mis rutinas. En particular el reloj puede realizar mediciones de sueño, actividad física, pasos, etc. 

Evidentemente la actividad física se vió afectada por el confinamiento, reduciendo mis ejercicios y mis pasos diarios. Para que os hagáis una idea mis pasos han pasado de 14.149,2 de media diaria a sólo 1869,1. 

Si bien es cierto que cuando más ando, al salir a comprar para varios días, no me llevo el reloj para evitar tocarlo con las manos sucias, actualmente salgo 1 vez cada semana y media, con lo cual creo que no ayudan a la media en absoluto. 

También hay que tener en cuenta que al hacer ejercicio en casa (algo que hago entre 1 hora / 1hora y media al día), con los movimientos que practico, el reloj también cuenta pasos. Aún así, creo que gracias a eso solo he llegado un día a la cifra de 4000 pasos. 

En resumen, creo que el parámetro del que tengo menos idea es el del sueño, y es uno de los que destacan para evaluar mi posible productividad, descanso, concentración, o incluso estado anímico. 

## Getting the data

Para obtener los datos tiré de GPDR y solicité mis datos a la empresa de la cual viene mi reloj deportivo. Tardarón un par de días en darme los datos, pero a su favor, gestionaron bastante bien mi solicitud. 

Los datos se distribuyen de la siguiente manera (de su página web): 
- Sueño profundo
Cuando pasas a la fase de sueño profundo, los movimientos oculares y musculares se detienen por completo. La frecuencia cardiaca y el ritmo de tu respiración disminuyen. 

- Sueño ligero
El sueño ligero es la primera fase del sueño. Durante la fase de sueño ligero, los movimientos oculares y la actividad muscular se ralentizan. 

- Despierto

Para detectar estas fases el reloj hace uso del acelerómetro y el pulsómetro. En aquellos dispositivos con oxímetro también es tenido en cuenta, pero no es mi caso.


## Analyzing the data
Finalmente con los datos obtenidos, procedo a usar bokeh para un EDA. Dentro del mismo gráfico incluyo los datos de sueño total, de sueño profundo y sueño ligero. 

![Example image](/images/sueño_1.png)


Además de los datos en crudo, he marcado la franja de sueño saludable recomendada (7-8h). Como parte del análisis, he realizadao una pequeña regresión para intentar ver qué tendencia seguían los datos. 
Sin más información lo cierto es que son pocos datos y no es del todo representativa, pero creo que se puede intuir alguna conclusión de ella. 

## Conclusions!

Bueno viendo los datos soy optimista. He seguido de forma adecuada un rutina de sueño para evitar alterar mis ciclos y ritmos diarios. 

En parte estoy acostumbrado a realizar mis principales entrenamientos por la tarde-noche durante la semana. Estos horarios, al mantenerlos creo que me han ayudado a llegar cansado a la hora de dormir.

Es cierto que se intuye un leve subida de las horas de sueño, pero con menor cantidad de sueño profundo. Esto puede afectar a la calidad del sueño, pero las variaciones son tan sumamente mínimas, que no creo que tenga que preocuparme. 



