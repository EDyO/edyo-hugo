---
title: "Las conferencias OpenNebulaConf 2015"
author: "Javier Arellano"
slug: "OpenNebula_2015"
date: 2015-11-10T21:00:00

tags: ["OpenNebula", "Cloud"]
---

Del 20 al 22 de octubre del 2015 tuvo lugar en Barcelona el `OpenNebulaConf 2015`_. Antes de nada me gustaría aclarar que esta no es una simple noticia, sino que se trata de un artículo de opinión ya que pude assistir los tres días gracias a la invitación que nos ofreció la organización y por mucho que quisiera, no podría separar mis experiencias de lo que formalmente sería la noticia, una vez aclarado este tema, relataré sin hacer un resumen exhaustivo de las charlas, haciendo una separación entre el taller del primer día y los dos días siguientes que fueron las charlas en sí.

<!--more-->


Taller
------

El primer día empezaba con 3 talleres que se realizaban de forma simultánea a partir de las 14:00. Los talleres eran un "Iniciación" , "Avanzado" y uno especial sobre Centos. Dado mi nulo conocimiento del producto me apunte al de iniciación. Ante todo quiero aclarar que no tenia conocimientos sobre OpenNebula_ pero si que he trabajado mucho con OpenStack. 

El taller se compone de 2 máquinas virtuales que nos repartieron en el momento (aunque varios días antes ya nos habían avisado y yo ya las tenia copiadas en el ordenador). En un articulo posterior explicaré este taller, ya que hablando con la organización me han dado permiso para poder distribuir el taller.

Entre las cosas que aprendi:

- Es un proyecto opensource, que se puede acceder en github
- Tiene una empresa "OpenNebula Systems" que trabaja en ello. 
- No tiene una version empresarial, sino que se sustentan con los desarrollos a medida y con el soporte a empresas
- Y la cosa que más me impactó: **Es super fácil**

Conferencias
------------

Las conferencias empezaban a las 9:00 y finalizaban a las 18:00, con una hora para comer y 2 pausas para el café y poder hacer networking. En estas pausas era el momento para ver las mesas de los sponsors, los cuales amablemente soportaban las preguntas que les hacíamos. 

Las charlas eran de 20-30 minutos, aunque ya desde el primer momento las horas empezaron a descuadrar, por lo que se usaron las últimas charlas como colchón de tiempo y se sacrificaron para poder finalizar a la hora marcada.

Unas de las tipologias de charlas fueron las *charlas rápidas* que se trataban de charlas máximo 5 minutos y 3 slides, y nos animaban a preparar estas charlas durante el evento y exponerlas al final del día. 

Podemos dividir las charlas en:

* **Organización**: muy interesantes ya que pudimos ver estado actual y el mapa de ruta que están preparando de mano de los propios creadores. Y alguna charla técnica con las últimas novedades o formas de trabajo, como por ejemplo el uso de docker. Entre estas charlas tambien contaría la última charla que fue prácticamente una mesa redonda, en la que preguntaron a los asistentes por necesidades de los usuarios y las fueron apuntando para añadirlas al roadmap. 

* **Usuarios**: exposiciones sobre el funcionamiento real de los sistemas donde trabajan y como usan OpenNebula_, lo que pude aprender a parte de unas muy buenas soluciones (como por ejemplo el uso de la MAC para aislar las máquinas), y tambien los movimientos dentro de los requerimientos, por ejemplo: una empresa que necesitaba el uso de GPU pidió un desarrollo a medida que hizo que otra empresa pudiese usar las tarjetas de forma directa y así pudieron usar unas tarjetas infiniband que no estaban disponibles en un principio.

	También pude ver un patrón común en los usos de OpenNebula_, ya que por un lado muchos usuarios venian representando equipos científicos y universidades, también se podía ver un uso de los mismos recursos, como por ejemplo el uso de ceph_ como el sistema de almacenamiento más extendido entre los asistentes.. 

	Como curiosidad: entre estas charlas habían una de devuan_ que se trata de una distribución debían sin systemd (hubo una ovación en la recepción del ponente)
	
* **Agregados**: También otro tipo de charla es la presentación de productos que aunque no tengan nada que ver con OpenNebula_ pero que pueden usarse como añadidos, como por ejemplo: ceph_ que es un sistema de ficheros, cdist_ y  quattor_ que son sistemas de configuración distribuidos, icinga_ monitorización, xen_ hipervisor de virtualización, etc.

Resumen
-------

Las ideas que extraigo es que OpenNebula_ es un sistema que simplifica mucho la administración, es robusto y manejable. Es decir, que todo lo contrario a OpenStack, ya que en nuestro anterior laboratorio de OpenStack instalamos la versión RDO de RedHat, que simplifica mucho la instalación. En cambio OpenNebula lleva la simplicidad como ADN. Pudiendo crear sistemas de una sola a miles de máquinas, tal y como nos enseñaron en la charlas, con la misma facilidad.

.. _xen: http://www.xenproject.org
.. _icinga: https://www.icinga.org
.. _quattor: http://www.quattor.org
.. _cdist: http://www.nico.schottelius.org/software/cdist/
.. _devuan: https://devuan.org
.. _ceph: http://ceph.com
.. _`OpenNebulaConf 2015`: http://2015.opennebulaconf.com
.. _OpenNebula: http://opennebula.org
