---
title: "Encuentro Agile-Python BCN"
author: "Ignasi Fosch"
slug: "agile-python-bcn-meetup"
date: 2013-05-29T23:00:00

tags: ["Agile", "Python", "Scrum"]
---

El grupo de `Python Barcelona`_ de Meetup_ organiza reuniones monográficas sobre temas relacionados con Python_. En esta ocasión, se hicieron presentaciones sobre metodologías de desarrollo.

<!--more-->


Introducción al desarrollo de software àgil con *Scrum*
-------------------------------------------------------

`Alex Ballarin`_ presentó la primera charla, que introducía metodologías ágiles poniendo como ejemplo Scrum. También presentó el grupo de Meetup_ recién creado `Barcelona Scrum`_. La charla fue bastante introductoria, basándose en una `guía de una página`_ creada para la ocasión.

Una de las herramientas más interesantes que comentó Alex es el `burndown chart`_ que muestra el progreso del proyecto ideal relacionado con las horas invertidas en el mismo.

Alex también comentó el `planning poker`_ que consiste en una técnica muy utilizada para la estimación aproximada sin incluir desviaciones personales. Otra herramienta muy extendida, ésta para el control de las tareas, es `Kanban`_, mucho más conocida, que consiste en disponer de un panel en el que cada estadio del desarrollo de una tarea se representa como una columna, por la que la tarea, que suele representarse con un *post-it*, va avanzando hasta que llega a la columna de tareas completadas. Para ésta técnica es muy importante tener claro lo que significa que la tarea está completada, lo que se llama *Definition of Done*, y que consiste en el conjunto de condiciones técnicas para que una tarea se considere completada y, en caso de usar *Kanban*, poderla poner en la última columna.

Development work-flow at Splendia
---------------------------------

`Christof Damian`_ explicó cómo funciona el método de desarrollo, su flujo de trabajo, en Splendia_. Hasta hace relativamente poco tiempo utilizaban waterfall_, pero empezaron a aplicar algunas técnicas como `code review`_. Utilizan Github para aprovechar la funcionalidad de *Pull Request* que les da, al mismo tiempo que pueden ver los cambios introducidos en la misma página web. Cuando otro desarrollador revisa el PR puede utilizar los comentarios para indicar lo que le gusta, o los comentarios que quiera hacer.

Christof también contó cómo hacen integración contínua. Tienen un servicio de *Jenkins* conectado al repositorio en `Github`_ que corre los tests y añade comentarios con los resultados de la ejecución de éstos. Finalmente, tienen un sistema automatizado que, dependiendo de los comentarios y de los resultados de los tests, añade los cambios a la rama principal.

En cuanto al sistema de control de versiones, que, evidentemente es git_, utilizan tres ramas, la que tienen en Github_, donde se hacen los *code reviews*. Cuando un conjunto de cambios se aprueban en el *code review*, se llevan los cambios a una rama de desarrollo, vinculada a otro proceso de *Jenkins* donde se ejecutan, de nuevo, los tests unitarios, estáticos y funcionales, para lo que Christof indica que utilizan Cucumber_. Finalmente, cuando *Jenkins* considera que los tests se satisfacen tras aplicar los cambios, éstos se llevan a la rama estable, donde se hace un despliegue en un entorno controlado sobre el que se realiza el testeo manual.

En su charla, Christof destacó que han ganado en comodidad para los desarrolladores, especialmente al hacer los *code reviews* y permite a la empresa tener las nuevas funcionalidades integradas rápidamente. También comentó que siendo *Jenkins* una herramienta muy conocida por los desarrolladores, ha resultado muy sencillo integrarla con `Github`_ para establecer éste proceso.

Testing and continuous integration
----------------------------------

`Thasso Griebel`_ explicó la importancia que tiene el concepto de *Continous Integration* en el mundo de las metodologías ágiles. Tanto definiendo un simple flujo de trabajo consistente en ejecutar todos los tests con éxito y subir el código, como si se utiliza el `branching model`_, es necesario que los tests necesarios para poder subir el código se ejecuten lo suficientemente rápido. En el caso de Thasso, necesita ejecutar los tests unitarios, de integración y funcionales en varios sistemas operativos y plataformas.

Thasso comentó la existencia de varias herramientas bastante interesantes (como Bamboo_, BuildBot_ o TeamCity_), aunque utiliza Jenkins_ sobre el que utilizan muchos módulos para ampliar las funcionalidades, como, por ejemplo, ejecutar los tests en equipos remotos con otros sistemas, plataformas, llamado Shining Panda.

My personal Python best practices
---------------------------------

`Paweł Piotr Przeradowski`_ habló sobre algunas técnicas que utiliza al programar en Python_:

- PEP8_ que es un conjunto de reglas de estilo orientadas a mejorar la legibilidad del código, que se pueden seleccionar y validar con la herramienta ``pep8`` y que se puede integrar directamente con editores y entornos de desarrollo.
- pyflakes_ es una herramienta que detecta partes del código que no se utilizan en ningún caso. También consiste en una herramienta de línea disponible para algunos editores.
- `McCabe`_ es una herramienta para analizar la complejidad que el código presenta. Ésta complejidad, llamada ciclomática, consiste en el número de caminos que el código puede tomar, según las situaciones que se planteen.
- py.test_ es una librería de unit testing que Paweł prefiere por, entre otras características, permitir crear tests más eficientes con menos código que otras librerías.

.. _`Python Barcelona`: http://www.meetup.com/python-185/
.. _Meetup: http://www.meetup.com
.. _Python: http://www.python.org/
.. _`Alex Ballarin`: http://es.linkedin.com/in/alexballarin
.. _`Barcelona Scrum`: http://www.meetup.com/Barcelona-Scrum-English/
.. _`guía de una página`: http://www.meetup.com/Barcelona-Scrum-English/
.. _`burndown chart`: 
.. _`planning poker`: 
.. _`Kanban`: 
.. _`Christof Damian`: http://christof.damian.net/
.. _Splendia: http://www.splendia.com/
.. _waterfall: http://es.wikipedia.org/wiki/Desarrollo_en_cascada
.. _`code review`: http://es.wikipedia.org/wiki/Revisi%C3%B3n_de_c%C3%B3digo
.. _git: http://git-scm.org
.. _Github: http://github.com
.. _Cucumber: http://cukes.info
.. _`Thasso Griebel`: 
.. _`branching model`: http://nvie.com/posts/a-successful-git-branching-model/
.. _Bamboo: http://www.atlassian.com/software/bamboo/overview
.. _BuildBot: http://buildbot.net/
.. _TeamCity: http://www.jetbrains.com/teamcity/
.. _Jenkins: http://jenkins-ci.org
.. _`Paweł Piotr Przeradowski`: http://es.linkedin.com/pub/pawe%C5%82-piotr-przeradowski/69/787/b7b
.. _PEP8: https://pypi.python.org/pypi/pep8
.. _pyflakes: https://pypi.python.org/pypi/pyflakes
.. _`McCabe`: https://pypi.python.org/pypi/mccabe
.. _py.test: http://pytest.org/latest/
