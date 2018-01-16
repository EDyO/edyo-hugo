---
title: "¿Hay consenso en el consenso?"
author: "Daniel Aresté"
slug: "hay-consenso-consenso"
date: 2016-08-11T09:00:00

tags: ["Básicos", "Algoritmos"]
---

.. image:: /images/55bed744-5fa6-11e6-93ee-f037e8f7b624.jpg
   :alt: Students
   :align: right
   :width: 125px
   :height: 125px

Imaginad un grupo de alumnos que toma apuntes en clase, anotando todo lo que un profesor dice. 
Este profesor, a menos que le indiquen lo contrario, no se detiene y asume que sus palabras llegan correctamente a todos los estudiantes. 
Si hay algún despistado, siempre puede preguntar al de al lado *("oye, ¿qué acaba de decir?")* sin interrumpir la clase.

<!--more-->


Pero ¿y si se despista más de uno a la vez? Siendo uno de los alumnos, 
¿cómo puedo estar seguro de que el compañero de al lado no estaba también en babia y me va a dar información errónea? 
Podría preguntarle a dos o tres compañeros, y me quedo con lo que diga la mayoría. Pero… ¿a cuántos es suficiente preguntar? 
¿Los elijo aleatoriamente, o me voy a preguntar a uno de los empollones? ¿Son cien por cien fiables los empollones?

¿Qué ocurre si no hablamos de un despiste de dos o tres, sino de una moto ruidosa que ha pasado por la calle 
y que ha hecho que casi la mitad de alumnos no llegue a oír la última frase del profe? 
¿Hay alguna forma de ponernos de acuerdo mientras seguimos apuntando lo que el profe dice, 
o habrá que pedirle al profe que pare la clase un rato mientras comparamos nuestras notas y llegamos a un acuerdo?

No parece trivial diseñar un sistema de organización (**algoritmo**) para garantizar que estos alumnos (**nodos**) 
dispongan en todo momento de unos apuntes (**datos**) consistentes y completos, ¿verdad? Especialmente ante despistes 
(**caídas de nodos**) o motos ruidosas (**problemas de red**). Más difícil aún si además tenemos que hacerlo sin interrumpir la clase
(**indisponibilidad de servicio**).

Lo que acabamos de presentar es conocido como el `problema del consenso`_, el aspecto fundamental a resolver 
en cualquier sistema distribuido que almacene información. De forma simplificada, 
el consenso se puede definir como la capacidad de una red de nodos no fiables de almacenar un estado común de forma fiable. 
Este problema quitó muchas horas de sueño a muchos investigadores, hasta que `Leslie Lamport`_, en 1989, presentó `Paxos`_ y lo resolvió.

El éxito indiscutible de Paxos...
=================================

Lamport desarrolló una familia de protocolos que resolvían definitivamente el problema del consenso. 
Digo definitivamente, porque Paxos no solamente parecía funcionar; estaba formalmente demostrado, 
prueba de la que otros algoritmos ad-hoc carecían.

En 1998, después de publicarse con mucho éxito en la revista `ACM Transactions on Computer Systems`_, 
Paxos pasó a ser sinónimo de consenso: prácticamente cualquier sistema distribuido lo utilizaba, 
y las universidades lo empezaron a enseñar.

Hoy en día, Paxos se usa en la arquitectura base de ciertos servicios comerciales (quizás os suene **AWS** o **Azure**)
y conocidos proyectos open source (el sistema de storage distribuido **Ceph**, la base de datos orientada a grafos **Neo4j**, 
o el gestor de clusters **Mesos**, por poner algunos ejemplos). Google, aunque con ciertas modificaciones, 
lo usa como base para **Chubby**, su servicio de DLM (Distributed Lock Manager).

Podríamos pensar que Paxos acabó con toda la investigación y desarrollo en el área del consenso. 
No hubiera sido extraño; al fin y al cabo, existiendo una solución definitiva a un problema, ¿qué más se necesita?

... y su oscuro secretillo.
===========================

En 2013, Diego Ongaro y John Ousterhout, investigadores de Standford, presentaron un nuevo algoritmo de consenso llamado `Raft`_.
Al igual que Paxos, Raft solucionaba el consenso de forma completa y probada, pero... 
¿qué necesidad había de trabajar de nuevo sobre un problema ya resuelto?

Ongaro y Ousterhout, con este trabajo, pretendían señalar al rey desnudo y sacar a la luz 
lo que ya en los círculos reducidos de investigadores era un secreto a voces: 
Paxos es condenadamente complejo y difícil de entender. 
Tanto, que se considera que solamente un puñado de investigadores en el mundo lo comprende en su totalidad. 
Los propios autores de Raft, en el `paper`_ original, explican que solamente después de pasar un año investigando Paxos 
y tratando de implementarlo lograron comprenderlo completamente. Repito: unos tíos de Standford. Un año entero para entenderlo.

La razón de ser de Raft fue la inteligibilidad. Los autores quisieron diseñar un algoritmo intuitivo, sencillo de entender 
y fácil de explicar, para así poder contribuir a que con él se construyeran sistemas más robustos. 
La idea subyacente es que si es fácil de entender, es más probable implementarlo sin errores.

Parece que lo lograron; a pesar de su corta vida, Raft es ya muy exitoso. 
Como ejemplos de proyectos conocidos que lo implementen, tenemos **etcd** (un sistema de almacenamiento distribuido de pares clave-valor),
**Consul** (una herramienta de Service Discovery) o **OpenDaylight** (un controlador de red SDN), 
lista a la que seguro se irán sumando muchos otros en el futuro. 

¿Cuál de los dos algoritmos va a ser el que monopolice el consenso en el futuro? Aunque parece que Raft arranca con fuerza, 
habrá que esperar y ver la tendencia. Lo que es seguro es que, cuando tratamos con el consenso, es mejor no inventar; 
el problema es tan complejo que es mejor acudir al mundo académico y usar algoritmos ya probados. 
El hecho de tratar de inventar tu propia solución al problema te puede llevar por derroteros bastante vergonzosos. 
O si no, que se lo pregunten a los desarrolladores de **MongoDB** 
(¿habéis oído hablar de problemas de integridad de datos en el producto? `Adivinad por qué`_).

Por último, os dejo con esta fantástica `animación interactiva`_ que muestra cómo funciona Raft y demuestra sus virtudes en términos
de claridad y simplicidad. ¡Disfrutadla!

.. _`problema del consenso`: https://en.wikipedia.org/wiki/Consensus_(computer_science)
.. _`Leslie Lamport`: https://en.wikipedia.org/wiki/Leslie_Lamport
.. _`Paxos`: https://en.wikipedia.org/wiki/Paxos_(computer_science)
.. _`Raft`: https://en.wikipedia.org/wiki/Raft_(computer_science)
.. _`paper`: https://raft.github.io/raft.pdf
.. _`ACM Transactions on Computer Systems`: http://dl.acm.org/citation.cfm?id=279229
.. _`Adivinad por qué`: https://aphyr.com/posts/322-call-me-maybe-mongodb-stale-reads
.. _`animación interactiva`: http://thesecretlivesofdata.com/raft/
