---
title: "ELB de Amazon WS balancea entre zonas de disponibilidad"
author: "Ignasi Fosch"
slug: "amazon-ws-elb-balancea-entre-zonas"
date: 2013-11-10T08:00:00

tags: ["Amazon WS"]
---

.. image:: /images/AmazonWebservices.png
   :alt: AWS
   :align: left

El pasado jueves, día 7 de noviembre, `Amazon WS`_ anunció que su servicio ELB_ pasaría a permitir balancear entre instancias que se encontraran en zonas de disponibilidad distintas, mejorando el mantenimiento y rendimiento de las aplicaciones, que ya no requerirán esfuerzos adicionales por parte de los clientes. También hará el despliegue de las aplicaciones más sencillo.

<!--more-->


Hasta ahora, el servicio ELB_ balanceaba a los clientes sólo entre las instancias de una misma zona de disponibilidad, dejando al servicio DNS_ la tarea de repartir las peticiones de los usuarios entre las zonas. Éste comportamiento podía causar diferencias de carga entre las instancias de distintas zonas. Además, si no se disponía del mismo número de instancias funcionando en cada una de las zonas, las peticiones podían distribuirse entre un número menor de servidores.

La nueva funcionalidad `requiere ser activada manualmente`_, pero una vez hecho, el balanceador repartirá equitativamente las peticiones entre todas las instancias configuradas.

.. _`requiere ser activada manualmente`: http://docs.aws.amazon.com/ElasticLoadBalancing/latest/DeveloperGuide/TerminologyandKeyConcepts.html?channel=EM&Campaign_Type=Launch&Campaign_id=47667000&ref_=pe_411040_47667000_7&#request-routing
.. _DNS: http://es.wikipedia.org/wiki/Domain_Name_System
.. _`Amazon WS`: http://aws.amazon.com/es/
.. _Amazon: `Amazon WS`_
.. _AWS: `Amazon WS`_
.. _ELB: http://aws.amazon.com/es/elb/
