---
title: "2014, el año de las vulnerabilidades"
author: "Eduardo Bellido Bellido"
slug: "2014-vulnerabilidades"
date: 2014-10-26T21:30:00

tags: ["Seguridad"]
---

.. image:: /images/security.jpg
   :alt: Securidad
   :align: left
   :class: border

Este año 2014 se ha convertido en un verdadero calvario para los administradores de sistemas y los responsables de seguridad de muchas empresas, sobretodo las que proporcionan servicios en Internet. A falta de dos meses para que finalice el año, ya son tres las vulnerabilidades graves detectadas que nos han puesto en jaque. Hablamos de Heartbleed_, Shellshock_ y Poodle_.

<!--more-->


Si bien es cierto que tanto **Heartbleed** como **Shellshock** son fallos de implementación o de código, en la librería OpenSSL_ y en el intérprete de comandos Bash_, respectivamente, no es así con **Poodle**, que es un fallo del propio diseño del protocolo (que ya tiene 18 años de antigüedad).

Hay que tener en cuenta, que gracias a que ambos proyectos son *Software Libre/Open Source*, es posible que cualquier especialista, voluntario, o cualquier que se precie, tenga la posibilidad de auditar el código fuente y detectar futuros incidentes como los vividos en los últimos meses.

Recordemos también el nacimiento de la `Core Infrastructure Initiative`_, proyecto creado por grandes empresas relacionadas con Internet (Google, IBM o Intel, por citar algunas) con el beneplácito de la `Linux Foundation`_, con el fin de proporcionar fondos para garantizar que este tipo de *software* tan crítico quede libre, en la manera de posible, de este tipo de fallos tan graves.

Para acabar, dado el creciente aumento en proporcionar cifrado en las conexiones HTTP, recomendar la herramienta_ que proporcionan en `Qualys SSL Labs`_ para verificar el grado de seguridad en cuanto a la implementación de SSL/TLS, así como verificar que hemos corregido estas vulnerabilidades citadas además de muchas otras. Un enlace que conviene tener siempre a mano en nuestros marcadores.

.. _Heartbleed: https://en.wikipedia.org/wiki/Heartbleed
.. _Shellshock: https://en.wikipedia.org/wiki/Shellshock_(software_bug)
.. _Poodle: https://en.wikipedia.org/wiki/Transport_Layer_Security#POODLE_attack
.. _OpenSSL: https://www.openssl.org
.. _Bash:  http://www.gnu.org/software/bash/bash.html
.. _Linux Foundation: http://www.linuxfoundation.org/
.. _Core Infrastructure Initiative: http://www.linuxfoundation.org/programs/core-infrastructure-initiative
.. _Qualys SSL Labs: https://www.ssllabs.com
.. _herramienta: https://www.ssllabs.com/ssltest/
