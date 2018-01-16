---
title: "512000 es el número que se contará..."
author: "Daniel Aresté"
slug: "512000-numero-contara"
date: 2014-08-13T20:30:00

tags: ["Redes", "Crónica"]
---

...y el número de la cuenta será 512000.

Hecho el obligatorio homenaje a la `Santa Granada de Antioquía`_ de los Monty Python, pongámonos serios y veamos por qué dedicamos un artículo a este número.

¿Os iba mal Internet ayer? No estabais solos. En algún momento de la mañana empezaron a haber problemas graves en la mayoría de los ISPs de todo el mundo, que afectaron tanto a empresas como a particulares. 

El mundo de la tecnología está lleno de ejemplos de diseños que, o bien por limitaciones del momento, o bien por no imaginar crecimientos exponenciales, provocan problemas de escalabilidad en el futuro; algunos de los más conocidos son el **efecto 2000** o el **agotamiento de direcciones IPv4**. A esta lista de umbrales superados ya podemos añadir uno nuevo: ayer, por primera vez en la historia, se superaron las **512000 entradas en la tabla de rutas de Internet**.

No obstante, antes de seguir hablando de dicha tabla necesitamos hablar de cómo está organizado Internet.

<!--more-->


Sistemas Autónomos
==================

Internet está administrativamente segmentado en Sistemas Autónomos (AS), que son en esencia entidades que agrupan prefijos IP públicos y los anuncian al resto del mundo. Aunque cualquiera puede `solicitar un AS`_, los grandes propietarios son empresas u organizaciones cuya actividad central o negocio tiene que ver con la presencia en Internet. Así, estaríamos hablando de ISPs o grandes compañías como Google o Amazon.

`Aquí`_ puedes obtener información del AS de tu ISP, así como de los prefijos IP de los cuales es propietario el mismo. En este `otro ejemplo`_ verás la lista de AS y prefijos IP propiedad de Google.

La tabla de rutas de Internet
=============================

Los AS interconectan unos con otros creando un gigantesco `grafo`_ donde cada AS es un nodo. Para que podáis vislumbrar la complejidad del conjunto, en este `ejemplo`_ tenéis el subgrafo de cómo uno de los AS de Microsoft (izquierda, AS8075) interconecta con sus vecinos más cercanos. Os dejo el ejercicio de intentar imaginar el grafo completo sabiendo que el número actual de ASes registrados supera los 80.000.

Internet funciona porque somos capaces de mover información entre dos AS cualesquiera (por ejemplo, el de tu ISP y el de Google cuando consultas tu correo en Gmail). A esto se le llama enrutamiento, y funciona gracias a que cada uno de los AS dispone de un mapa o tabla de rutas que le indica cómo comunicar con cualquier otro nodo. Así, no existe una sola tabla de rutas de Internet, sino tantas como ASes. Las tablas se mantienen al día gracias al protocolo `BGP`_, que esencialmente intercambia información con los AS vecinos para estar al día de cambios topológicos (recordad que los AS están en manos privadas, que tienen potestad para realizar cambios en cualquier momento) y crear, modificar o eliminar entradas en la tabla.

Dos vecinos tendrán tablas de rutas similares, mientras que las de dos ASes en extremos opuestos del planeta diferirán completamente. No obstante, lo que sí es más o menos parecido es su tamaño, que viene creciendo casi `exponencialmente`_ desde los 90 y que ayer por primera vez superó los 512.000 prefijos de media.

El número maldito
=================

Ya por fin tenemos todo lo necesario para explicar qué pasó ayer. Los chicos de bgpmon.net tienen un `análisis`_ técnico excelente que aquí resumiremos.

Ayer, a las 7:48 de la mañana, el ISP Verizon anunció (parece ser que por un error de configuración) **15.000 nuevos prefijos** a través de dos de sus AS. Inmediatamente, estas entradas empezaron a propagarse por el resto de Internet, provocando un tamaño medio de tabla de 513.000 registros.

Aunque esto no es problema para los AS que disfrutan de hardware más moderno, los routers más viejos no pudieron con esto. Por ejemplo, el veterano router `Cisco 6500`_ es un tanque que podemos encontrar en cientos de ASes, pero que por defecto **no permite cargar más de 512.000 prefijos** en memoria y deja el dispositivo inconsistente al alcanzar ese límite.

Cisco ofrecía `una solución`_ para incrementar ese tamaño a un millón, pero implicaba reiniciar el router. Muchos de los administradores de red se afanaron en aplicarla en sus viejos routers, pero siendo en muchos casos hardware que llevaba años sin reiniciarse, había **defectos ocultos** en discos o memorias de arranque que hicieron que el equipo **no sobreviviera al reinicio**. Eso acentuó los problemas.

Por suerte, Verizon corrigió rápido su error y esos prefijos fueron retirados, con lo cual la tabla de rutas volvió a su tamaño habitual. Aunque es inevitable que la tabla alcance de nuevo los 512.000 registros, esperemos que este pequeño susto haya hecho reaccionar a los administradores de red afectados y modernicen su infraestructura.

Internet, tan robusto y a la vez tan frágil...

.. _`Santa Granada de Antioquía`: https://www.youtube.com/watch?v=MPzWtI6uaJk&t=2m16s
.. _`solicitar un AS`: http://www.ripe.net/lir-services/resource-management/allocations-and-assignments/request-an-as-number
.. _`Aquí`: http://bgp.he.net/
.. _`otro ejemplo`: http://bgp.he.net/search?search%5Bsearch%5D=google&commit=Search
.. _`grafo`: http://es.wikipedia.org/wiki/Grafo
.. _`ejemplo`: http://bgp.he.net/AS8075#_graph4
.. _`BGP`: http://es.wikipedia.org/wiki/Border_Gateway_Protocol
.. _`exponencialmente`: http://www.cidr-report.org/cgi-bin/plota?file=%2fvar%2fdata%2fbgp%2fas2.0%2fbgp-active%2etxt&descr=Active%20BGP%20entries%20%28FIB%29&ylabel=Active%20BGP%20entries%20%28FIB%29&with=step
.. _`análisis`: http://www.bgpmon.net/what-caused-todays-internet-hiccup/
.. _`Cisco 6500`: http://www.cisco.com/c/en/us/products/switches/catalyst-6500-series-switches/literature.html
.. _`una solución`: http://www.cisco.com/c/en/us/support/docs/switches/catalyst-6500-series-switches/117712-problemsolution-cat6500-00.html


