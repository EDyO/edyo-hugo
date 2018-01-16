---
title: "Charlas en el DevOpsDays Barcelona 2013"
author: "Ignasi Fosch"
slug: "charlas-devopsdays-barcelona-2013"
date: 2013-10-12T20:13:00

tags: ["Eventos", "DevOps", "devopsdays"]
---

`devops days Barcelona 2013`_
-----------------------------

Como decíamos en nuestro último post, éstos dos últimos días, jueves y viernes, se ha celebrado en la `Fábrica de la Moritz`_ de Barcelona, el evento `devops days`_ en su edición de 2013. El evento en sí ha estado muy bien y bastante interesante. Con muchos asistentes, se podría decir que cerca de 100 personas, la posibilidad de hacer networking era muy interesante. Podréis encontrar todos los vídeos en `la página de vimeo`_.
El evento lo ha organizado `Rhommel Lamas`_, y ha contado con el patrocinio de `Moritz`_, `STR Sistemas`_, `Rakuten`_, `CA`_, `Telefónica I+D`_, `3Scale`_, y `GitHub`_. Realmente, conviene que este evento se repita y crezca, tanto en cantidad de asistentes, como de ponentes.

<!--more-->


Disciplined Agile Delivery
--------------------------

En esta charla, `Alex Ballarin`_ habló sobre la `Disciplined Agile Delivery`_, metodología ágil que integra también los conceptos de la filosofía DevOps y sobre la que podréis extender en profundidad en el libro_ correspondiente. Una de las principales diferencias respecto a otras metodologías más conocidas, es la inclusión e implicación de las áreas de sistemas y operaciones en la producción.

Enemigos de la entrega contínua
-------------------------------

`Isa M. Vilacides`_ explicó cuáles son los principales problemas que se han encontrado al intentar realizar entrega contínua, en inglés *continuous delivery*, en Wuaki.tv_. Por resumir un poco su presentación, habló de lo siguiente:

* Sobre el testeo:

  - Cuándo, qué y donde testear.
  - Cómo la gestión incorrecta del alcance y de la automatización llevan al testeo manual tradicional.
  - La importancia de definir claramente la titularidad del código y la formación en las herramientas de comunicación facilitan la resolución de los fallos.
  - La priorización de los fallos detectados se consigue evitando el pánico.


* Sobre la calidad de las pruebas:

  - Los tests deben ser estables, sus resultados nunca deberían ser falsos negativos.
  - La evolución de la cobertura de los tests debe ser tratada con cuidado y conocida al detalle.
  - El tiempo de ejecución no puede ser demasiado, puede ser necesario encontrar la forma de paralelizarlos.


* Sobre la falta de automatización:

  - Las pruebas unitarias, las de integración y las de aceptación, forman una pirámide en las que las primeras son la base y las últimas la cúspide.
  - Cuando sea posible, hay que automatizar el proceso de lanzamiento.


* Sobre la comunicación:

  - Debe existir comunicación a todos los niveles, especialmente el flujo de comunicación sobre la evolución del concepto del producto a lo que debería ser.
  - Un tipo especial de comunicación a tener muy en cuenta, es el que hace referencia a lo que ocurrirá a partir del lanzamiento.

Una perspectiva europea de la adopción de DevOps
------------------------------------------------

`Justin Vaughan-Brown`_ estuvo presentando un estudio de `CA`_ que presentaba el resultado de un estudio realizado sobre 1300 compañías de IT en 21 países europeos. En términos generales, el estudio mostraba bastantes aspectos curiosos.
Un ejemplo era que el conjunto de Portugal y España era en el que había un menor conocimiento del concepto DevOps, pero otros países con mejor resultado en ese aspecto, presentaban muy bajos índices de adopción o planificación de hacerlo.
Una de las conclusiones que presentó es que la automatización de las infrastructuras IT, las metodologías de desarrollo ágiles y la colaboración son los aspectos claves para la adopción de DevOps.

Pruebas de rendimiento continuas
--------------------------------

La charla que dió `Almudena Vivanco González`_ trató sobre el testeo de rendimiento, su historia, las claves de su aplicación, cómo mejorar sus tareas y su entorno y las herramientas que más utilizan.
Así, recomienda tener una idea clara de la visión y contexto del proyecto, entendiendo el sistema, así como el entorno del proyecto, adaptando la planifición de las construcciones para el rendimiento.

Los costes y beneficios de DevOps
---------------------------------

`Tom Levey`_ presentó una gran disertación sobre el valor de DevOps para las compañías. Un poco más concretamente, indicó que los objetivos que se marca DevOps, al estar alineados con los de la empresa, permiten que ésta obtenga mucho más de sus equipos técnicos, mejorando sus costes, optimizando sus gastos y maximizando los beneficios.

Incluso un negocio al por menor puede seguir la filosofía DevOps
----------------------------------------------------------------

Francesc Bernau explicó cómo Venca_, un negocio de venta al por menor, se enfrontó a la adaptación de su negocio al mercado móvil y cómo éste objetivo fué adaptando tanto el equipo técnico, como sus operacionas, al mismo tiempo que el enfoque, tanto en la dirección como en otros equipos, iba cambiando para adaptarse.

El camino hacia DevOps en Tuenti
--------------------------------

`Óscar San José`_ y `Víctor García`_ presentaron una explicación acerca de los cambios que el equipo de Tuenti_ ha realizado para adaptarse a la filosofía DevOps, creando una serie de herramientas y procedimientos que les permiten desarrollar, testear y desplegar más eficientemente.

.. _`devops days Barcelona 2013`: http://devopsdays.org/events/2013-barcelona/
.. _`devops days`: http://devopsdays.org
.. _`Fábrica de la Moritz`: https://plus.google.com/100068709387237553942/about?gl=ES&hl=en-ES
.. _`la página de vimeo`: http://vimeo.com/album/2565361
.. _`Rhommel Lamas`: http://rhommell.com/
.. _`Moritz`: http://www.moritz.com/
.. _`STR Sistemas`: http://www.strsistemas.com/
.. _`Rakuten`: http://www.rakuten.co.jp/
.. _`CA`: http://www.ca.com/es/lpg/appvelocity/home.aspx
.. _`Telefónica I+D`: http://www.tid.es/
.. _`3Scale`: http://www.3scale.net/
.. _`GitHub`: http://github.com/
.. _`Alex Ballarin`: http://es.linkedin.com/in/alexballarin
.. _`Disciplined Agile Delivery`: http://disciplinedagiledelivery.com/
.. _libro: http://www.amazon.com/Disciplined-Agile-Delivery-Practitioners-Enterprise/dp/0132810131
.. _`Isa M. Vilacides`: http://www.linkedin.com/in/vilacides
.. _Wuaki.tv: http://wuaki.tv
.. _`Justin Vaughan-Brown`: de.linkedin.com/pub/justin-vaughan-brown/0/493/9a1
.. _`Almudena Vivanco González`: es.linkedin.com/pub/almudena-vivanco/13/5b7/877
.. _`Tom Levey`: uk.linkedin.com/in/tlevey
.. _Venca: http://venca.com/
.. _`Óscar San José`: es.linkedin.com/pub/oscar-san-jose/2/886/a37
.. _`Víctor García`: es.linkedin.com/in/v1kt0r
.. _Tuenti: http://tuenti.com
