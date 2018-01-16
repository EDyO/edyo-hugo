---
title: "11 cosas sobre DevOps (8): Infosec y QA"
author: "Ignasi Fosch"
slug: "11-cosas-necesitas-saber-devops-8"
date: 2014-06-08T03:35:00

tags: ["Agile", "DevOps", "Empresa", "Entrega Contínua", "Integración Contínua", "Pruebas", "Seguridad", "QA"]
---

.. image:: /images/chaos-monkey.png
   :alt: Chaos Monkey
   :align: right

El octavo punto de `Gene Kim`_ sobre DevOps trata sobre cómo se integran las áreas de Seguridad informática y calidad en los flujos de trabajo de DevOps. Aunque parezca algo muy complejo de hacer, es también algo que conviene comprender correctamente para poder realizar de la forma más adecuada. Es decir, sin perder el sentido de tener procesos de calidad y seguridad, ni afectar al esfuerzo realizado para disponer de las funcionalidades en el tiempo requerido para mantener la competitividad de la organización.

<!--more-->


8. ¿Cómo se integran Seguridad informática y QA en el flujo de trabajo de DevOps?
---------------------------------------------------------------------------------

Los altos ritmos de despliegue del flujo de trabajo de DevOps ponen una enorme presión sobre los equipos de QA y Seguridad informática. Hay que considerar el caso en el que Desarrollo está haciendo diez despliegues diarios, mientras que Seguridad requiere tiempos de espera de cuatro meses para completar las revisiones de seguridad de la aplicación. A simple vista, se observa una falta de coincidencia entre el ritmo de despliegues y el de revisiones de seguridad.

Un ejemplo del riesgo expuesto por despliegues insuficientemente comprobados es el famoso caso del `fallo de Dropbox en 2011`_, en el que la autenticación quedó desactivada durante cuatro horas, permitiendo a usuarios no autorizados acceder a toda la información almacenada.

La buena noticia para QA y Seguridad es que las organizaciones capaces de sostener ritmos altos de despliegues, suelen usar integración contínua y otras prácticas relacionadas con la entrega contínua, que a menudo incluyen la práctica religiosa del testeo contínuo. Dicho en otras palabras, cada vez que se va a integrar el código, se ejecutan pruebas automatizadas y cualquier problema que aparezca debe ser corregido para continuar, del mismo modo que si el código no compila.

Mediante la inclusión de las pruebas funcionales, de integración y de seguridad en las operaciones diarias de Desarrollo, los defectos se detectan y resuelven en menor tiempo que nunca.

Hay un número creciente de herramientas de seguridad informática, como `Gauntlet`_ y `Security Monkey`_, que ayudan a testear objetivos de seguridad en los proceses de desarrollo y producción.

Una preocupación habitual genuina es que las herramientas de análisis estático de código requieren demasiado tiempo para ejecutarse que harían que los tiempos de los procesos de testeo e integración tardasen horas o incluso días en completarse. En esos casos, Seguridad debería designar los módulos específicos sobre los que se delegan las funcionalidades de seguridad (cifrado, autenticación, etc.). Cada vez que se modifican esos módulos, se ejecutan los tests completos, de otro modo, el despliegue puede continuar.

Una última nota: hemos [*]_ observado que los flujos de DevOps a menudo tienen más dependencia en la detección y recuperación, que en el testeo unitario estándard. En otras palabras, en el desarrollo de software empaquetado, que dificulta el despliegue de cambios y parches, QA depende mucho del testeo del código para cumplir la funcionalidad antes de ser empaquetado. Por otro lado, cuando el software se entrega como un servicio y los defectos pueden ser resueltos muy rápidamente, QA puede reducir su dependencia en el testeo, y concentrarse en la monitorización de producción para detectar problemas, tanto como se puedan resolver rápidamente.

La recuperación rápida de errores de código puede ser mejorada con la inclusión de *feature flags*, o activadores de funcionalidades, que activan y desactivan funcionalidades del código mediante opciones de configuración, en lugar del despliegue de la versión anterior.

Depender en la detección y recuperación para QA es obviamente, mucho más aplicable cuando lo peor que puede ocurrir es la pérdida de funcionalidad o del rendimiento requerido. Sin embargo, cuando el riesgo es de perder confidencialidad, integridad entre los sistemas o datos, la dependencia no se debe poner en la detección y recuperación, sino que debe ser testeado antes de desplegar el código, para evitar un incidente de seguridad genuino.

Seguiremos escribiendo más sobre cómo codificamos los nuevos patrones de QA y Seguridad en el blog.

.. [*] La primera persona hace referencia al autor del original.

.. _`Gene Kim`: http://itrevolution.com/authors/gene-kim/
.. _`fallo de Dropbox en 2011`: http://news.techworld.com/security/3287206/dropbox-admits-it-suffered-serious-password-failure/)/
.. _`Gauntlet`: http://gauntlt.org/
.. _`Security Monkey`: https://github.com/Netflix/SimianArmy
.. _`#11cosasdevops`: https://twitter.com/search?q=%2311cosasdevops
