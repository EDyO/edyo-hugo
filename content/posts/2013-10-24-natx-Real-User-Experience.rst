---
title: "Rendimiento Web: Real User eXperience"
author: "Ignasi Fosch"
slug: "rendimiento-web-real-user-experience"
date: 2013-10-28T16:45:00

tags: ["Eventos", "Herramientas", "Rendimiento"]
---

.. image:: /images/performance.jpg
   :width: 180px
   :height: 135px
   :alt: Medición de tiempos (Foto: William Warby)
   :align: left
   :class: border
   :target: http://www.flickr.com/photos/wwarby/

El pasado jueves tuvo lugar, en las oficinas que CanteraTech_ tiene en  Barcelona, un encuentro del grupo de Meetup_ de `Barcelona Web Performance`_ en el que `Marc Loan`_ habló sobre su proyecto *Real User eXperience*, o RUX. Desarrollado y utilizado desde 2008 para detectar y analizar los problemas que los usuarios puedan experimentar durante la navegación de un sitio web, incluso cuando éstos no llamen al servicio de atención al cliente. Este proyecto, además, se convirtió en el proyecto de fin de carrera de Marc.

<!--more-->


RUX: Real User eXperience
-------------------------

Como explicó Marc, el proyecto se realizó para poder atender problemas que los usuarios detectaban en la página web, sin que percibieran el problema, a no ser que el usuario llamaba a su servicio de atención.
Este proyecto se inició en 2008 para aportar:

* Control en tiempo real de las incidencias.
* Mejoras en la calidad de la aplicación.
* Reducción del tiempo de investigacion de los errores, al recibirlo todo en el momento de producirse, antes de que los usuarios llamasen.
* Recuperación de la información útil para los desarrolladores.
* Análisis de la estadística de los errores para encontrar tendencias.
* Registro de la actividad de los usuarios, permitiendo detectar el entorno que causa el error.
* Diagnóstico del funcionamiento de los servicios. Es una especie de web status.

En su entorno, el contenido se sirve desde una granja de servidores web. Estos servidores registran todo en un servidor centralizado utilizando el servicio ``syslog``. Sobre los registros de las peticiones y de los errores, que se actualizan tras cada petición, se ejecuta un proceso *ETL* que analiza su contenido y lo carga en una base de datos. Esta base de datos, que tiene un diseño ROLAP para permitir crear cubos de análisis OLAP, es consultada por el sistema que crearon para obtener la información que necesita.

.. _CanteraTech: http://www.cantera-tech.com/es/
.. _Meetup: http://www.meetup.com/
.. _`Barcelona Web Performance`: http://www.meetup.com/Barcelona-Web-Performance-Group/
.. _`Marc Loan`: http://marcloan.cat/
