---
title: "Review del paper What Is DevOps?"
author: "David Acacio"
slug: "review-paper-what-is-devops"
date: 2013-12-07T20:14:00

tags: ["Reseña", "Paper", "DevOps", "Opinión"]
---

.. image:: /images/what_is_devops_paper.jpg
   :width: 93
   :height: 125
   :alt: Paper What Is DevOps?
   :class: border
   :align: left

Buscando por Amazon libros sobre DevOps fui a dar un con un paper que tanto su título y precio enseguida llamaron mi atención. El paper en cuestión es `What Is DevOps?`_ de Mike Loukides y su precio es 0 €. 

Es un paper ameno, haciendo referencia a diversas fuentes, que para los dominadores de la lengua de Shakespeare se lee de manera rápida en apenas 15 minutos. 

<!--more-->


Lo primero a destacar es la manera en que el autor presenta el DevOps más allá de su definición: empieza repasando las diferentes fases por la que ha pasado el programador/administrador de sistemas. Desde los primeros informáticos que vestían batas blancas y era la misma persona la que se encargaba de desarrollar y operar el sistema, pasando por la segmentación de roles, que se precipitó con la aparición de la micro informática, hasta llegar a la última evolución: el DevOps.

De manera constante nos va poniendo ejemplos haciendo referencias a diversas compañías (`O'Reilly`_, `Netfilx`_, `Amazon`_) así como de diferentes autores que han colaborado, o colaboran, para llegar a entender el DevOps tal como lo entendemos hoy en día.

Tampoco quiero entrar a comentar todos los puntos del paper, ya que dada su brevedad no haría más que hacer innecesaria su lectura, pero sí que quiero resaltar algunas de las frases que más me han llamado la atención:

 * [...] mumbling obscure command-line incantations is a appropiate way to fix problems.

 * If you're going to do operations reliably, you need to make it reproducible and programmatic.

 * So infrastructure had to become code.

 * The new sysadmin won't power down a machine, replace a failing disk dirve, reboot, and restore from backup; he'll write software to detect a misbehaving EC2 instance automatically, destroy the bad instance, spin up a new one, and configure it, all without interrupting service.

 * The use of metrics to monitor system performance is another respect in which system administration has evolved.

 * it's important not to divorce developers from the consequences of their work since the fires are frequently set by their code.

Una lectura más que recomendable para entender el DevOps y el origen de éste.

.. _`What Is DevOps?`: http://www.amazon.com/What-DevOps-Mike-Loukides-ebook/dp/B0084HJB56/ref=sr_1_2?s=digital-text&ie=UTF8&qid=1386441697&sr=1-2 
.. _`web de Amazon`: http://www.amazon.com/What-DevOps-Mike-Loukides-ebook/dp/B0084HJB56/ref=sr_1_2?s=digital-text&ie=UTF8&qid=1386441697&sr=1-2
.. _`O'Reilly`: http://www.oreilly.com/
.. _`Netfilx`: https://signup.netflix.com/global
.. _`Amazon`: http://www.amazon.com/
