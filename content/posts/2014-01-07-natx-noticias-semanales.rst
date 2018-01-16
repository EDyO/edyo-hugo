---
title: "Noticias semanales (Ene I)"
author: "Ignasi Fosch"
slug: "noticias-semanales-enero-2014-1"
date: 2014-01-07T21:00:00

tags: ["Recursos", "Herramientas", "Chef", "Puppet", "Pruebas", "TDD", "Entrega Contínua", "Monitorización", "Automatización"]
---

.. image:: /images/Weekly-Newspaper.jpg
   :width: 213px
   :height: 141px
   :alt: La información semanal sobre lo que te interesa
   :align: right
   :class: border

En primer lugar, ¡Feliz Año Nuevo a todos! Tras las fiestas, las comilonas, los encuentros familiares y los regalos, aquí están las primeras noticias de 2014. Podréis encontrar herramientas, como una especie de Vagrant_ para Docker_, un servicio complementario para vuestro Nagios_ y vuestra cuenta de Pagerduty_, o un nuevo panel para Graphite_, así como explicaciones sobre cobertura de testeo de código para Chef_ o un interesante blog sobre lo último de Puppet_, junto con artículos sobre SDN_, el despliegue contínuo agresivo o la importancia de la infraestructura como código para la automatización. Disfrutad del commienzo de año.

<!--more-->


Fig, un Vagrant para Docker
---------------------------

La gente de Orchard_, un proveedor de hospedaje con Docker_, ha hecho pública su herramienta para la automatización de despliegues, llamada Fig_. Siendo una suerte de Vagrant_ para Docker_, la introducción que han publicado parece muy interesante, sobretodo para la preparación de entornos de desarrollo.

Cómo controlar las alertas con Flapjack
---------------------------------------

Quizás más útil para un ISP o un proveedor de hosting, Flapjack_ puede ser un interesante aliado de los sistemas de monitorización, parecido a Pagerduty_ en algunos aspectos, puede complementarlo para facilitar la gestión de alertas a equipos diferenciados. En cualquier caso, un nuevo juguete al que echar un vistazo.

Otro *dashboard* para Graphite
------------------------------

Es bastante habitual que aparezcan paneles e interfaces para Graphite_, lo que ya no es tan habitual es que sean tan completos en funcionalidad como Graph-explorer_, que, además, es de Vimeo_. A parte de que utiliza GEQL_, permitiendo crear gráficos aún más fácilmente, facilita la identificación de las unidades, facilita la agregación en línea, y otras muchas funcionalidades.

Cobertura de tests con Chef
---------------------------

`Seth Vargo`_, uno de los componentes de los equipos de Berkshelf_ y ChefSpec_, así como uno de los evangelizadores de Chef_, ha escrito un interesante artículo sobre cómo gestionar la `cobertura de los tests`_ sobre las recetas, permitiendo identificar incluso los recursos que no se han comprobado.

Las novedades de Puppet
-----------------------

El blog `Puppet on the edge`_, de `Henrik Lindberg`_, es un blog dedicado a destacar las novedades que el equipo de Puppet_ va añadiendo, antes de que lleguen a las manos de los más avezados administradores. Un buen candidato para vuestro lector de RSS.

Cambios de paradigma en la virtualización y las comunicaciones
--------------------------------------------------------------

`Greg Ferro`_, autor del blog EtherealMind_, ha publicado un artículo_, en respuesta a una duda de un lector, sobre el cambio del paradigma de la virtualización de redes y su acercamiento a las SDN_. Aunque no es en gran profundidad, puede hacer reflexionar a muchos sobre la utilización de las filosofías Agile y DevOps en el mundo del *networking*.

El despliegue contínuo de los grandes
-------------------------------------

En `Infinite Duo`_ hacen un superficial, aunque interesante, repaso_ al despliegue contínua ultraagresivo que hacen algunos grandes como Google_, Amazon_ o Facebook_. Con un vídeo explicativo para cada caso, puede ser curioso ver cómo estar publicando las nuevas versiones de forma constante puede no ser una idea tan loca, como algunos piensan.

¿Porqué nos dedicamos a esto?
-----------------------------

`Aaron Nichols`_, autor del blog `Operation Bootstrap`_, ha escrito una interesante reflexión_ sobre lo que, podéis estar seguros, piensan muchos administradores de sistemas y DevOps, en relación a esta nuestra profesión. A destacar el émfasis que hace en el hecho del perfil generalista tan común en Ops.

La relación entre IaC y la automatización
-----------------------------------------

Kief_, consultor especializado en entrega contínua de software, ha escrito un artículo sobre automatización_ y la importancia de combinarla con la gestión de la infraestructura como código.


.. _Vagrant: http://vagrantup.com
.. _Docker: https://docker.io
.. _Nagios: http://www.nagios.org/
.. _Pagerduty: http://www.pagerduty.com/
.. _Graphite: http://graphite.wikidot.com/
.. _Chef: http://www.getchef.com/chef/
.. _Puppet: http://puppetlabs.com/
.. _SDN: http://en.wikipedia.org/wiki/Software-defined_networking
.. _Orchard: https://orchardup.com/
.. _Fig: http://orchardup.github.io/fig/
.. _Flapjack: http://flapjack.io/
.. _Graph-explorer: http://vimeo.github.io/graph-explorer/
.. _Vimeo: http://vimeo.com
.. _GEQL: https://github.com/vimeo/graph-explorer/wiki/GEQL
.. _`Seth Vargo`: https://sethvargo.com/
.. _Berkshelf: http://berkshelf.com
.. _ChefSpec: https://github.com/sethvargo/chefspec
.. _`cobertura de los tests`: https://sethvargo.com/chef-recipe-code-coverage/
.. _`Puppet on the edge`: http://puppet-on-the-edge.blogspot.co.uk/
.. _`Henrik Lindberg`: https://plus.google.com/103020081690083867959
.. _`Greg Ferro`: http://etherealmind.com/author/gregferro/
.. _EtherealMind: http://etherealmind.com
.. _artículo: http://etherealmind.com/server-performance-network-agents-software-routers-and-networking/
.. _`Infinite Duo`: http://infiniteundo.com
.. _repaso: http://infiniteundo.com/post/71540519157/continuous-delivery-is-mainstream
.. _Google: http://google.com
.. _Amazon: http://amazon.com
.. _Facebook: http://facebook.com
.. _`Aaron Nichols`: https://twitter.com/anichols
.. _`Operation Bootstrap`: http://opsbs.com
.. _reflexión: http://www.opsbs.com/2013/09/why-i-infracode/
.. _`Kief`: https://twitter.com/kief
.. _`automatización`: http://kief.com/infrastructure-as-code-versus-automation.html
