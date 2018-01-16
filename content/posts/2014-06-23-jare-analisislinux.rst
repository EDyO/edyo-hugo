---
title: "Análisis de rendimiento de Linux"
slug: "analisis-rendimiento-linux"
date: 2014-06-23T03:14:00

tags: ["Linux", "Unix", "Rendimiento", "Herramientas", "Sistemas Operativos"]
author: "Javier Arellano"
description: ""
---

.. image:: /images/linuxperftools_1000.png
   :width: 650px
   :height: 376px
   :alt: resumen de herramientas de Brendan Gregg
   :align: center
   :class: border
   
Brendan Gregg ha escrito una serie de artículos y documentos agrupados en `Linux Performance <http://www.brendangregg.com/linuxperf.html>`_ donde se investigan los cuellos de botella de los sistemas Unix y Linux. 

<!--more-->


Realiza una exposición de las herramientas más útiles en los distintos sistemas operativos y de su equivalencia en su `piedra Rosetta <http://www.brendangregg.com/USEmethod/use-rosetta.html>`_ sobre los sistemas Linux, Solaris, Freebsd y Mac OSX, así como de un método llamado USE para el diagnóstico de problemas. 

Una de las partes más interesantes que he visto ha sido el resumen de las herramientas según la localización del problema en la imagen que acompaña a este artículo.

También de las charlas que acompañan al artículo hay una llamada *What Linux can learn from Solaris performance and vice-versa* realizada el febrero de 2014 en la `SCaLE 12x <https://www.socallinuxexpo.org/scale12x/>`_ tiene como punto de origen un programa Perl ejecutado en un Linux y en un SmartOS (Basado en Illumos), el mismo programa con el mismo hardware tiene una variación de 5% entre un sistema y el otro. Durante la charla trata de averiguar como verificar el rendimiento de la máquina realizando un recorrido por todas las partes funcionales del sistema, utilizando diversas herramientas y realizando comparaciones entre ellas para ver que se puede aplicar de Solaris en Linux y que puede aprender Solaris de Linux. 

Se trata pues, de una charla imprescindible para aquellas personas que necesiten investigar cuellos de botella en sus sistemas, y también las personas que quieran profundizar en el comportamiento de las máquinas.
