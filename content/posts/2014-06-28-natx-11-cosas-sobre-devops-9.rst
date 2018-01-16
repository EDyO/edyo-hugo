---
title: "11 cosas sobre DevOps (9): Mi primer patrón DevOps favorito"
author: "Ignasi Fosch"
slug: "11-cosas-necesitas-saber-devops-9"
date: 2014-06-29T03:35:00

tags: ["Agile", "DevOps", "Empresa", "Entrega Contínua", "Integración Contínua", "Pruebas", "Seguridad", "QA"]
---

.. image:: /images/automation.jpeg
   :alt: Automatización
   :align: right

En el noveno punto, `Gene Kim`_ inicia el tramo final de los once puntos, en el que presentará los patrones de DevOps que más le gustan. En este caso, destaca la importancia de la automatización y de su implantación en las primeras etapas del proyecto.

<!--more-->


9. Mi primer patrón DevOps favorito
-----------------------------------

Demasiado a menudo en los proyectos de desarrollo de software, el equipo de desarrollo acaba empleando todo el tiempo de la planificación en el desarrollo de funcionalidades. Esto no deja tiempo suficiente para tratar los asuntos de Operaciones. Lo que lleva a tomar atajos de forma sucesiva en la definición, creación y comprobación de todo en lo que el código se basa, incluyendo las bases de datos, los sistemas operativos, la red, la virtualización y demás. Ésta es, sin duda, una de las principales causas de la tensión perpetua entre Desarrollo y Operaciones, y sus correspondientes resultados subóptimos. Las consecuencias de esto son bien conocidas:

* Entornos con definiciones y especificaciones inadecuadas.
* Procedimientos de despliegue irrepetibles.
* Incompatibilidades entre el código desplegado y el entorno.

En este patrón, crearemos los entornos al principio del proceso de desarrollo y aplicaremos un política que fuerce probar el código y el entorno juntos. Cuando el equipo de desarrollo utiliza un proceso ágil se puede hacer algo muy sencillo y elegante. De acuerdo con *Agile*, se supone que, al final de cada iteración disponemos de código entregable y funcional. Modificaremos este objetivo para incluir que al final de la iteración no sólo tengamos el código listo, sinó también el entorno en el que se desplegará, desde el primer sprint. En lugar de responsabilizar a Operaciones de crear un entorno productivo que se ajuste a las especificacions, se construirá un proceso de creación del entorno automatizado. Este mecanismo creará el entorno de producción, pero también los entorno para desarrollo y QA.

Haciendo que los entornos, y las herramientas para crearlos, estén disponibles pronto, quizás antes de que el proyecto empiezo, los desarrolladores y QA pueden ejecutar y testear su código en entornos consistentes y estables, con una desviación controlada del entorno de producción. Además, manteniendo esta desviación entre los distintos entornos lo más reducida posible, encontraremos y resolveremos temas de interoperatibilidad entre el código y el entorno mucho antes del despliegue en producción. Idealmente, el mecanismo de despliegue que hemos construido estará completamente automatizado. Las herramientas que se pueden utilizar incluyen *shell scripts*, Puppet, Chef, Solaris Jumpstart, Redhat Kickstart, Debian Preseed, etc.

.. _`Gene Kim`: http://itrevolution.com/authors/gene-kim/
