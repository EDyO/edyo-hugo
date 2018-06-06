---
title: "La promesa incompleta"
author: Ignasi Fosch
slug: "la-promesa-incompleta"
date: 2018-06-05T22:00:00
image: rocket-launch.jpg
---

<img src='/images/noops.jpg' alt='noops' class='align-left height='200' width='200'/>

Hace unos días, con un compañero desarrollador comentábamos un [artículo](https://medium.freecodecamp.org/how-we-serve-25m-api-calls-from-10-scalable-global-endpoints-for-150-a-month-911002703280) sobre un producto implementado usando sólo Serverless y que, por lo tanto, es NoOps.
Durante la conversación, me llamó la atención lo fácil que es confundir el significado de NoOps, así que decidí escribir este post.

Aunque es largo, espero que os guste ;)

<!--more-->

## La importancia de la definición

Si se busca NoOps en Internet y se lee con atención las explicaciones de lo que es, es fácil encontrarse con muchas definiciones, algunas diciendo más o menos lo mismo, pero otras poniendo matices o incluso significados muy personalizados y alejados de la realidad.

NoOps es un término que, al parecer, fue acuñado por [Mike Gualtieri](https://twitter.com/mgualtieri), Vicepresidente de [Forrester](https://go.forrester.com/), por allá en 2011… desde aquello ha llovido bastante.
Lo expuso en un [artículo](https://go.forrester.com/blogs/11-02-07-i_dont_want_devops_i_want_noops/) bastante controvertido, en el que proponía el término como *"No" + "Ops" = "NoOps"*.
No parecía una declaración de paz.

Aunque explicaba que, aunque los esfuerzos de los ingenieros de sistema que hacían funcionar la aplicaciones eran críticos, los desarrolladores de las aplicaciones deberían invertir más tiempo en acercarse al negocio, no al hardware.

Reconocía la necesidad de despliegues más rápidos y más seguros, pero él creía que DevOps era, en realidad, un paso atrás, y, en su lugar, proponía *NoOps*, con la misma meta de mejorar los despliegues pero implicando que los desarrolladores de las aplicaciones no necesitan mantener conversaciones con los ingenieros de operaciones… **nunca**.

Su plan implicaba que los, entonces novedosos, conceptos como *IaaS* y *PaaS* debían permitir a los desarrolladores no sólo levantar las instancias o VMs necesarias, sino gestionar las *releases*.

Esto fue la génesis de un debate que aún dura hoy, pero veamos un poco cómo evolucionó.

## La primera fase de NoOps

Como suele pasar, Internet hirvió con discusiones sobre el tema, y gurúes de aquí y allá salían defendiendo unas u otras opiniones.
Ni siquiera había dos bandos.

Incluso, algunos eran citados hablando del tema, a menudo, fuera de contexto. Por ejemplo, un año después, [Adrian Cockcroft](https://twitter.com/adrianco?lang=es) [publicó un artículo](http://perfcap.blogspot.com/2012/03/ops-devops-and-noops-at-netflix.html) en su blog aclarando que Netflix sí que seguía teniendo un equipo de operaciones, sólo que el funcionamiento había evolucionado con el pasar del tiempo.

O, otro ejemplo, [Lucas Carlson](https://twitter.com/cardmagic?lang=es), fundador de la, pronto extinta, [AppFog](https://www.ctl.io/appfog/), en 2012 [predecía](https://gigaom.com/2012/01/31/why-2013-is-the-year-of-noops-for-programmers-infographic/) que 2013 sería el año del NoOps.

Un poco más tarde, algunos [defendían](https://devops.com/noops-devops-disaster-waiting-happen/) la necesidad de mantener equipos de operaciones, eso sí con títulos del estilo de los del [Y2K](https://es.wikipedia.org/wiki/Problema_del_a%C3%B1o_2000).

## La segunda fase de NoOps

Mientras algunos [buscaban puntos intermedios](https://devops.com/future-devops-lie-noops/), otros empezaron a [ver en el Serverless](https://thenewstack.io/serverless-computing-growing-quickly/) el camino hacia el NoOps, y otros tantos [seguían defendiendo](https://blog.appdynamics.com/engineering/is-noops-the-end-of-devops-think-again/) la permanencia del concepto DevOps.

## El concepto

Tal y como ocurrió con DevOps, NoOps ha sido definido, [redefinido](https://www.techrepublic.com/article/noops-how-serverless-architecture-introduces-a-third-mode-of-it-operations/) y [asimilado](https://www.bmc.com/blogs/itops-devops-and-noops-oh-my/) de formas muy distintas.
En muchos casos, parece que ser NoOps, según la variable interpretación de quien lo usa para ello, es un beneficio de negocio.

Igualmente que con DevOps, no es una solución, no es una [herramienta](https://www.ibm.com/blogs/bluemix/2016/06/moving-devops-noops-microservice-architecture-bluemix/), sólo es una forma de trabajar en equipo.
Y, por supuesto, no significa que no haya nadie a cargo de las operaciones, sólo significa que es otra forma de llevarlas a cabo, que implica cambios en la forma de trabajar de [mucha gente](https://medium.com/@copyconstruct/the-death-of-ops-is-greatly-exaggerated-ff3bd4a67f24).
No sólo para los ingenieros de sistemas, sino también para los desarrolladores.

## Confusiones y errores

Sólo por poner algunas cosas claras:

- DevOps no es **sólo** desplegar. NoOps, tampoco.
- NoOps no es [impopular entre los ingenieros de sistemas](https://www.youtube.com/watch?v=ajT90pC3ris).
- DevOps, como NoOps, defienden la automatización, pero hay que ir con cuidado con las abstracciones.
- Seguro que hay negocios que pueden adoptar NoOps. Pero eso no significa que todos puedan.

## Conclusión

Uno no se siente capacitado para predecir si el cielo, en el futuro, va a ser de un color o de otro.
La experiencia nos debería decir que lo que existió, aunque hoy no sea necesario, no siempre desaparece del todo.
Si no, que se lo cuenten a los programadores de Cobol y RPG, o a los operadores de AS400.

Lo que sí que da la sensación es que estos cambios son evolutivos, no revolucionarios.
Y probablemente, no serán los últimos.

## Referencias

- [7 arguments against NoOps (Travis Greene, ?)](https://techbeacon.com/7-arguments-against-noops)
- [Reports Of The Impending Demise Of Operations Are Greatly Exaggerated (Damon Edwards, May 21, 2018)](https://www.rundeck.com/blog/reports-of-the-impending-demise-of-ops-are-greatly-exaggerated)
- [NoOps and DevOps: The dawn of a new methodology? (Vanessa Perciballi, Feb 1, 2018)](https://www.spindox.it/en/blog/noops-devops-dawn-new-methodology)
- [NoOps: How serverless architecture introduces a third mode of IT operations (Keith Townsend, Jan 19, 2018)](https://www.techrepublic.com/article/noops-how-serverless-architecture-introduces-a-third-mode-of-it-operations/)
- [DevOps vs NoOps (Irene Maida, Jan 18, 2018)](https://www.criticalcase.com/blog/devops-vs-noops.html)
- [What is NoOps and is It Real? (Peter Matthews, Aug 3, 2017)](https://www.ca.com/us/modern-software-factory/content/what-is-noops-and-is-it-real.html)
- [The Best DevOps is NoOps (Feras Hirzalla, Jul 31, 2017)](https://medium.com/buttercloud-labs/the-best-devops-is-noops-e99c83d4fdf0)
- [Everyone is not Ops (Cindy Sridharan, Jul 29, 2017)](https://medium.com/@copyconstruct/the-death-of-ops-is-greatly-exaggerated-ff3bd4a67f24)
- [ITOps, DevOps, and NoOps Explained (Stephen Watts, May 31, 2017)](https://www.bmc.com/blogs/itops-devops-and-noops-oh-my/)
- [Is NoOps the End of DevOps? Think Again (Jordan Bach, Apr 11, 2017)](https://blog.appdynamics.com/engineering/is-noops-the-end-of-devops-think-again/)
- [NoOps - Is this the end of DevOps as we know it? (Rotem Dafni, Oct 31, 2016)](https://www.stratoscale.com/blog/devops/noops-end-devops-know/)
- [NoOps (Kelsey Hightower @ DevOpsDays Portlang, Aug 21 2016)](https://www.youtube.com/watch?v=ajT90pC3ris)
- [Moving from DevOps to NoOps with a Microservice Architecture on Bluemix (Christopher Hambridge, Jun 29, 2016)](https://www.ibm.com/blogs/bluemix/2016/06/moving-devops-noops-microservice-architecture-bluemix/)
- [The Road to NoOps: Serverless Computing is Quickly Gaining Momentum (Mark Boyd, May 18, 2016)](https://thenewstack.io/serverless-computing-growing-quickly/)
- [Does the Future of Devops Lie in NoOps? (Michael Schmidt, Apr 28, 2016)](https://devops.com/future-devops-lie-noops/)
- [Why NoOps is a DevOps disaster waiting to happen (Peter Waterhouse, Dec 1, 2015)](https://devops.com/noops-devops-disaster-waiting-happen/)
- [Why 2013 is the year of 'NoOps' for programmers (Derrick Harris, Jan 31, 2012)](https://gigaom.com/2012/01/31/why-2013-is-the-year-of-noops-for-programmers-infographic/)
- [Ops, DevOps and PaaS (NoOps) at Netflix (Adrian Cockcroft, Mar 19, 2012)](http://perfcap.blogspot.com/2012/03/ops-devops-and-noops-at-netflix.html)
- [I Don't Want DevOps. I Want NoOps (Mike Gualtieri, Feb 8, 2011)](https://go.forrester.com/blogs/11-02-07-i_dont_want_devops_i_want_noops/)
