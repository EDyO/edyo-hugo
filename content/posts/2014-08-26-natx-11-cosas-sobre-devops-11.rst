---
title: "11 cosas sobre DevOps (11): Mi tercer patrón DevOps favorito"
author: "Ignasi Fosch"
slug: "11-cosas-necesitas-saber-devops-11"
date: 2014-09-08T08:30:00

tags: ["Agile", "DevOps", "Empresa", "Entrega Contínua", "Integración Contínua", "Pruebas", "Seguridad", "QA"]
---

.. image:: /images/estandarizacion.jpg
   :alt: Bucle de retroalimentación
   :align: left
   :class: border

Para finalizar esta serie de `Gene Kim`_, presentamos la traducción de su tercer patrón DevOps favorito. En este patrón, presenta el problema de la estandarización en los entornos donde los proyectos son desplegados, y cómo lidiar con ellos, aplicando una técnica ágil, tratando de no olvidar las necesidades de negocio.

<!--more-->


11. Mi tercer patrón DevOps favorito
------------------------------------

Otro problema que aparece a menudo es la falta de estandarización en el flujo de valor entre Desarrollo y Operaciones. Ejemplos de esto serían los despliegues realizados de forma distinta cada vez, o los entornos que reúnen diferentes propiedades. Cuando esto ocurre, no hay ninguna maestría en las configuraciones o procedimientos de la organización.

En este patrón, definimos procedimientos de despliegue reutilizables que puedan ser utilizados en todos los proyectos. Hay una solución muy elegante en las metodologías Ágiles para esto, en la que las actividades de despliegue se convierten en una historia de usuario. Por ejemplo, podríamos construir una historia de usuario reutilizable para Operaciones llamada 'Desplegar en un entorno de alta disponibilidad', la cual definiría los pasos exactos para construir el entorno, así como cuánto tiempo lleva, qué recursos se necesitan, etc.

Esta información puede, entonces, ser usada por los gestores de proyecto para integrar detalladamente las actividades de despliegue en el plan de proyecto. Por ejemplo, podríamos tener mucha confianza en el horario de despliegue si supiéramos que la historia 'Despliegue en un entorno de alta disponibilidad' ha sido ejecutada en quince ocasiones en el último año, llevando una media de tres días, con un margen de error de un día arriba o abajo.

Aún más, también ganamos confianza en que las actividades de despliegue están siendo debidamente integradas en cada proyecto de *software*. Reconociendo que ciertos proyectos de *software* requieren entornos únicos que Operaciones no soporta oficialmente, podemos permitir excepciones en las que esos entornos estén permitidos en producción, pero que sean soportados por alguien fuera de Operaciones, que consideraríamos entornos no soportados.

Haciendo esto, tenemos los beneficios de la estandarización de los entornos, es decir, variedad reducida, menores diferencias, soporte y mantenimiento confiable; mientras que permitimos los casos especiales que a veces el negocio requiere.

.. _`Gene Kim`: http://itrevolution.com/authors/gene-kim
