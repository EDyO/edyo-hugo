---
title: "11 cosas sobre DevOps (3): En qué difiere de ITIL o de ITSM"
author: "Ignasi Fosch"
slug: "11-cosas-necesitas-saber-devops-3"
date: 2014-04-01T09:35:00

tags: ["Agile", "DevOps", "Entrega Contínua", "Automatización", "Desarrollo", "Empresa", "Integración Contínua"]
---

.. image:: /images/bridge-building.png
   :alt: Change vs Trouble
   :align: left

El tercer punto sobre DevOps que propone `Gene Kim`_ es la relación con ITIL_ y ITSM_, dos conjuntos de prácticas y disciplinas para la gestión de operaciones IT, muy extendidas, especialmente en las grandes empresas.
Como en las dos anteriores entregas, esperamos que os unáis al debate en Twitter, con el *hashtag* `#11cosasdevops`_.

<!--more-->


3. ¿Cómo difiere DevOps de ITIL o de ITSM?
------------------------------------------

Aunque la mayoría de gente ve DevOps como un contragolpe a ITIL_ o a ITSM_, yo [*]_ tengo una visión distinta. ITIL y ITSM son mejores codificaciones de los procesos de negocio que forman la base de las operaciones IT. De hecho, describen muchas de las capacidades que las operaciones IT necesitan tenen en orden para dar soporte al flujo de trabajo al estilo DevOps.

El resultado de aplicar metodologías ágiles y la integración contínua en el equipo de desarrollo genera, como salida, las versiones liberadas, que son la entrada para el equipo de operaciones. Para acomodar la rápida cadencia de publicación de versiones asociada con DevOps, muchas áreas de los procesos ITIL requieren estar automatizados, especialmente los procesos de cambio, configuración y liberación.

La meta de DevOps no es sólo incrementar el ritmo de cambio, sino desplegar exitosamente nuevas funcionalidades en producción, sin causar caos ni interrumpir otros servicios, permitiendo la detección y corrección cuando ocurran. Esto se añade a las disciplinas ITIL de diseño de servicio y gestión de incidentes y problemas.

.. [*] La primera persona hace referencia al autor del original.

.. _`Gene Kim`: http://itrevolution.com/authors/gene-kim/
.. _ITIL: http://es.wikipedia.org/wiki/Information_Technology_Infrastructure_Library
.. _ITSM: http://es.wikipedia.org/wiki/Gesti%C3%B3n_de_servicios_de_tecnolog%C3%ADas_de_la_informaci%C3%B3n
.. _`#11cosasdevops`: https://twitter.com/search?q=%2311cosasdevops
.. _`The DevOps Cookbook`: http://itrevolution.com/books/devops-cookbook/
