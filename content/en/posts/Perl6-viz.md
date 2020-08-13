---
author: "Bart"
title: "How to visualize a github repository evolution in time"
date: 2020-03-23T12:00:06+09:00
description: "Video sobre la evolución del repo de documentación de Perl6"
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: Bart
authorEmoji: 👻
tags: 
- Github
- Repository
- Visualization
- Perl6
- Raku
libraries:
- Gource
categories:
- coding
image: images/repo.png
---
¡Ojo! Perl6 ya "no existe", oficalmente el lenguaje ahora se llama ¡Raku! :)

## Perl6 Documentation 

Durante un breve periodo de tiempo estuve estudiando la evolución en las contribuciones a los repositorios de código. En muchas ocasiones se dice que este tipo de contribuciones siguen leyes de potencias, pero habitualmente esta afirmación va apoyada únicamente por un par de fits de distribuciones a los datos, sin contraste de hipótesis o comparación con otras posibles distribuciones. Aunque ya me meteré en este costal más adelante, lo cierto es que analizar las contribuciones a cualquier repositorio es siempre interesante. 

Y como ya sabéis, el tema de la visualización me gusta bastante, por lo que, documentándome para el trabajo que antes os mencionaba, encontré [Gource](https://gource.io/). 
Y como por aquel entonces también estaba escribiendo cosillas para la documentación de Perl6 (en particular su [sección sobre simulación de Ecuaciones diferenciales](https://docs.raku.org/language/math#Numerical_integration_of_ordinary_differential_equations)) decidí probar a ver que pasaba al usar esta herramienta con ese repo. 

Los resultados gustaron mucho, y subieron el video a los [updates semanales de Perl6](https://p6weekly.wordpress.com/2019/05/06/2019-17-18-three-months-to-riga/) :).

Os animo a usar Gource en vuestros proyectos de software libre, es un curioso gráfico que puede llamar la atención de los usuarios y ser útil a la hora de mostrar vuestro repo (o la actividad en el mismo).

### Video

{{< youtube mvGhZutr2_s >}}


### Data Source
[Repositorio de la documentacion de Perl6](https://github.com/Raku/doc) a fecha de creación del video.

### Software usado
- [Gource](https://gource.io/)

