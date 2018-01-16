---
title: "11 cosas sobre DevOps (6): Las áreas de los patrones"
author: "Ignasi Fosch"
slug: "11-cosas-necesitas-saber-devops-6"
date: 2014-05-03T23:25:00

tags: ["Agile", "DevOps", "Empresa", "Entrega Contínua", "Integración Contínua"]
---

.. image:: /images/change-ahead.png
   :alt: Cambio en adelante
   :align: left

El siguiente apartado que `Gene Kim`_ trata, destaca las áreas en las que los patrones DevOps operan. Éstas áreas fueron descritas en el libro `DevOps Cookbook`_. Éstas áreas unen, de formas diferente, tres conceptos altamente importantes de todo equipo de IT: Producción, Desarrollo y Operaciones.

<!--more-->


6. ¿Cuáles son las áreas de los patrones de DevOps?
---------------------------------------------------

Para el libro `DevOps Cookbook`_, dividimos [*]_ los patrones DevOps en cuatro áreas:

  * Área 1: Extender Desarrollo en Producción:

    Ésta área incluye extender las funciones de integración y entrega contínua en Producción, integrando a QA y Seguridad en el flujo de trabajo, asegurando la disponibilidad para Producción del código y el entorno.
  * Área 2: Crear retroalimentación de Producción a Desarrollo:

    Creando una línea temporal completa con los eventos de Desarrollo y Operaciones para ayudar a la resolución de problemas, incluyendo a Desarrollo en reuniones *post-mortem* sin búsqueda de culpabilidad, permitiendo a los desarrolladores obtener ellos mismos lo que necesitan, donde sea posible, y creando radiadores de información que muestren cómo las decisiones locales afectan las metas globales.
  * Área 3: Incrustar Desarrollo en Operaciones:

    Permitiendo poner a Desarrollo en la cadena de escalado a Producción, asignando recursos de Desarrollo a la gestión de problemas de Producción ayudando a disminuir deuda técnica, y creando una formación cruzada entre Operaciones y Desarrollo que permita reducir la cantidad de escalados.
  * Área 4: Incrustar Operaciones en Desarrollo:

    Ofreciendo incrustar recursos de Operaciones en Desarrollo de modo que puedan servir de enlace; crear historias de usuario reutilizables en Operaciones; y definiendo requerimientos no funcionales que puedan reutilizarse entre proyectos.

`Patrick Debois`_, uno de los coautores de `DevOps Cookbook`_, escribió más detalladamente sobre esto `aquí`_.

.. [*] La primera persona hace referencia al autor del original.

.. _`Gene Kim`: http://itrevolution.com/authors/gene-kim/
.. _`DevOps Cookbook`: http://www.realgenekim.me/devops-cookbook/
.. _`Patrick Debois`: https://twitter.com/patrickdebois
.. _`aquí`: http://www.jedi.be/blog/2012/05/12/codifying-devops-area-practices/
.. _`#11cosasdevops`: https://twitter.com/search?q=%2311cosasdevops
