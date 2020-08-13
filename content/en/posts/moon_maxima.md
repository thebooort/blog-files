---
author: "Bart"
title: "20 años y 20 horas"
date: 2020-05-08T12:00:06+09:00
description: "Sobre la luna, Delaunay , Deprit y el inicio del álgebra computacional"
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: Bart
categories:
- Science Communication
- Comunicación Científica
tags: 
- Comunicación
- Comunicación Científica
- Ciencia
- Divulgación 
- Matemáticas
- Algebra
- Computación
- Computación Matemática
series:
- Comunicación Científica
- Divulgación científica
libraries:
- mathjax
image: images/moon.png
---

<figure>
  <img src="/images/blackboard.png"  />
</figure>

# 20 años y 20 horas

Quiero invitarte a reflexionar: ¿dónde estabas hace 20 años?

Echar la vista atrás tanto tiempo puede ser complicado, pero es necesario para el tema que queremos tratar hoy. En un periodo tan largo caben muchas experiencias, tanto buenas como malas. Incluso, dependiendo del lector, ese período puede que abarque toda su existencia. 

Y antes de que empieces a sentir vértigo por lo rápido que pasa la vida y lo viejo/a que te encuentras, quiero que te quedes con esa visión de la enorme cantidad de tiempo que suponen 20 años, 175.200 horas. 

20 años fueron los que Charles Eugène Delaunay (1816-1872), matemático francés, necesitó para calcular la órbita de la luna, intentando mejorar los intentos de sus predecesores, Laplace y Le Verrier. 

Este periodo se dividió en dos etapas de 10 años, una para hacer las cuentas y otra para verificarlas. En 1847, con la públicación de su metodología en la revista de la Academia francesa de París, se daba el pistoletazo de salida a una prueba calculística que iba a requerrir mucho de Delaunay. 

La primera parte del rompecabezas para calcular la órbita de la luna fue una aproximación. Delaunay consideró las órbitas de la luna y la tierra eran elípticas y se encontraban en planos diferentes. Posteriormente añadió las perturbaciones producidas por el Sol y otros planetas, hasta obtener un sistema Hamiltoniano (un sistema de ecuaciones diferenciales que describe el movimiento de la luna). El primer paso estaba dado. 

Tener el sistema y poder usarlo o resolverlo eran cosas muy distintas. La única opción que le quedó a Delanay (y que sigue siendo utilizada en muchas ocasiones hoy en día) fue traducir su sistema diferencial a una expresión en suma de potencias.
Siendo parcos en palabras, Delaunay pasó de resolver un sistema de ecuaciones a calcular una suma de muchisimos términos. ¿Dónde está el truco? Los coeficientes de esos términos debían ser obtenidos a mano mediante transformaciones algebraicas, y cuánta más exactitud quería, más términos debía poner (y por tanto, más coeficientes y más cáclulos a mano). Llegó hasta orden 7, lo que se traduce en 478 términos, los cuales tenían por coeficientes polinomios que también debían ser calculados. 

En 1867, Charles publica su segundo tomo de resultados, concluyendo su periplo celeste. Sin embargo, los resultados, aunque acertados, no tenían la precisión que Delaunay esperaba, con márgenes de error de hasta 100km. ¿Fue un esfuerzo en bano? ¿Se había equivocado Delaunay? 

Tardaríamos casi 100 años en saber que pasó. 

El problema de encontrar el fallo en el trabajo de Delaunay era cuantitativo. A Delaunay le había llevado unos 10 años comprobar todos sus cálculos. Sin la perspectiva de que encontrar el error mejorase sus resultados enormente, nadie iba perder 10 años de su vida sin garantías.

Además, hubo más intentos tras Delaunay. Intentos que mejoraron sus resultados y avanzaron nuestra comprensión de la mecanica celeste y la luna. 

Asi que para resolver el misterio hubo que esperar a una de las grandes revoluciones del siglo XX: el algebra computacional y el cálculo simbólico (vamos, que le cargamos el muerto a un ordenador, que no se queja). 

Hasta 1960 los ordenadores que existían se llevaban bastante bien con las cuentas. Sumas, restas, matrices... lo que en matemática aplicada conocemos como cálculo numérico. Dentro de este área, podemos atacar el problema de la órbita lunar a traves de la integración numérica (usando las funciones de nuestro sistema y operaciones básicas). Desgraciadamente las aproximaciones analíticas (como la de Delaunay) que requieren transformar nuestro sistema con manipulaciones algebraicas complejas, y aunque nos dan una mejor comprensión de lo que está pasando, no eran programables en un ordenador. 

Lo que nos permite el algebra computacional es justo eso, manipular las expresiones, trabajar con ellas, con los símbolos de la matemática. Y gracias a ello resolvimos el misterio de Delaunay. 

André Deprit (1926-2006), fue uno de esos matemáticos pioneros que consiguió que el ordenador hablase el lenguaje matemático. Junto con J.M.A. Danby y Arnold Rom  desarrollan un paquete matemático: MAO - Mechanized Algebraic Operations. Este paquete fue un precursor en su clase, potenciando el desarrollo de muchos otros lenguajes de cálculo simbólico (como Macsyma, el abuelo de wxMaxima o Mathematica, sin el que muchos estudiantes no pueden vivir hoy en día). Para mostrar las bondades de su trabajo, Deprit y su equipo debían escoger un problema interesante.

Gracias a la transformación explícita basada en series de Lie, Deprit y sus colaboradores pudieron replicar todas las transformaciones algebraicas del trabajo de Delaunay, consiguieron que el ordenador hablase nuestro mismo lenguaje, con variables, coeficientes y cálculos itnermedios. Y todo ello, para descubrir que casi al final del sumatorio, Delanay había confundido un 33/16 por un 23/16. Un fallo lo tiene cualquiera. 

20 horas de computación bastaron para encontrar un error en un trabajo de 20 años.

20 horas que sirvieron para mostrar la potencia de los nuevos lenguajes de cálculo simbólico, y la importancia que iban a tener en los años venideros. 



## Notas 

Delaunay no sólo trabajó en mecánica celeste. Su trabajo como matemático se ve reflejado en otras áreas. Muestra de ello es un artículo publicado en 1841, donde demuestra que las  únicas  superficies  de  revolución  con  curvatura media  constante,  son  las  superficies obtenidas por rotación de las ruletas cónica. Estas superficies se denominan actualmente, en  su  honor,  superficies  de  Delaunay.



# Bibliografía
- La columna de la Academia (La Verdad, 9 de abril de 2016) https://www.um.es/geometria/files/Delaunay.pdf
- Tony Hurlimann. 1999. Mathematical Modeling and Optimization: An Essay for the Design of Computer-Based Modeling Tools. Kluwer Academic Publishers, USA.
- Introduction à la théorie de la Lune de Delaunay https://journals.openedition.org/bibnum/683
- H S Dumas, K R Meyer, D S Schmidt. 1995. Hamiltonian Dynamical Systems: History, Theory, and Applications. The IMA Volumes in Mathematics and its Applications, Springer.
- Deprit A, Henrard J, Rom A. Lunar Ephemeris: Delaunay's Theory Revisited. Science. 1970 Jun 26;168(3939):1569-70.
- Nota Necrologica: Prof.  Dr.  Andre Deprit http://www.raczar.es/webracz/ImageServlet?mod=publicaciones&subMod=revistas&car=revista61&archivo=p181.pdf


# Images credit: 

- Cabecera:  Joseph D.M. White's Youtube channel https://www.youtube.com/watch?v=ugxRx7alXb4&feature=emb_logo

- Photo by Neven Krcmarek on Unsplash: https://unsplash.com/photos/9dTg44Qhx1Q


