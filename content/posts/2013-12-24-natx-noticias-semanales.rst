---
title: "Noticias semanales (Dic III)"
author: "Ignasi Fosch"
slug: "noticias-semanales-diciembre-2013-3"
date: 2013-12-24T12:00:00

tags: ["Amazon WS", "Cloud", "Python", "Eventos", "DevOps"]
---

.. image:: /images/Weekly-Newspaper.jpg
   :width: 213px
   :height: 141px
   :alt: La información semanal sobre lo que te interesa
   :align: right
   :class: border

Debido a que el ritmo de publicación de noticias se había incrementado hasta el punto de casi no tener tiempo para escribir nada más, en Entre Dev Y Ops vamos a probar publicar un sólo post semanal con las noticias más interesantes de cada semana.

<!--more-->


Kinesis ya está disponible para todos los clientes de Amazon
------------------------------------------------------------

AWS_ anunció el pasado martes que su servicio Kinesis_, del que ya comentamos algo en el artículo sobre el `re:Invent 2013`_, está disponible a todos los clientes.

CloudFront puede servir contenido sólo a ciertos países
-------------------------------------------------------

El pasado viernes, AWS_ anunció una nueva funcionalidad en CloudFront_. Llamada *Geo Restriction*, permite restringir el acceso al contenido publicado en CloudFront_ basándose en la ubicación geográfica de los usuarios. De este modo, contenido licenciado para ser mostrado en ciertos países, o software con código cuya distribución está prohibida en ciertos países, se puede servir mediante CloudFront_ utilizando esta funcionalidad.
Al usuario que no se le permite el acceso al contenido se le da una respuesta HTTP 403, cuyo aspecto se puede personalizar. La funcionalidad no implica coste adicional.
AWS_ ha organizado, el 4 de Febrero del próximo año, a las 18:00 UTC+1, un webinar_ sobre esta y otras novedades de CloudFront_.

Nueva generación de instancias con alto rendimiento en E/S en EC2
-----------------------------------------------------------------

También el pasado día 20, AWS_ anunció para los servicios EC2_ la disponibilidad inmediata del nuevo tipo de instancias I2, que corresponden a la nueva generación de alto rendimiento en E/S. Basadas en la última generación del procesador Intel Ivy Bridge, cada vCPU corresponde a un hyperthread hardware de un Intel Xeon E5-2670 v2. Disponibles en 4 tamaños distintos, llegan a las 32 vCPU y los 244 GB de RAM, mientras que utilizan discos SSD de 800 GB.
Hay que señalar que estas instancias sólo soportan AMIs con HVM. Siendo la família de instancias con mayor número de IOPS, son las indicadas tanto para sistemas transaccionales como para bases de datos NoSQL de alto rendimiento, como Cassandra o MongoDB.

Charlas, tutoriales y posters de la PyCon 2014
----------------------------------------------

Como indican en el `número 97`_ del semanario `Pycoder's Weekly`_, la `PyCon 2014`_, que se celebrará en Montréal del 9 al 17 de Abril del próximo año, ya ha hecho públicas las charlas, tutoriales y presentaciones que se realizarán, así como sus horarios_.

PuppetLabs lanza la nueva edición de su encuesta anual sobre DevOps
-------------------------------------------------------------------

De la mano de `Gene Kim`_, coautor de `The Phoenix Project`_, libro ya comentado_ en este blog, y `Jez Humble`_, coautor de `Continuous Delivery`_, PuppetLabs_ presenta la edición 2013 de su `encuesta anual sobre DevOps`_.

Conociendo los logs, nuestros amigos
------------------------------------

Comentan en el `DevOps Weekly`_, uno de los mejores artículos `sobre los registros`_, los logs. Indicando qué son, porqué son importales, y cómo utilizarlos en escala. Desde el diseño para sistemas distribuidos hasta el almacenaje y la minería de datos con procesos ETL, acabando con una genial lista de documentos y artículos para leer sobre la materia.

Las presentaciones y los vídeos de la Flowcon
---------------------------------------------

También en el `DevOps Weekly`_, anuncian la publicación de las presentaciones_ y vídeos_ de la Flowcon_, conferencia sobre despliegue contínuo que se celebraron en San Francisco el primero de Noviembre.

El próximo Monitorama se celebrará del 5 al 7 de Mayo
-----------------------------------------------------

Con ubicación en Portland, se celebrará el próximo Monitorama_, para el que, como anuncian en `DevOps Weekly`_, ya se ha abierto el plazo de entrega de documentación hasta finales de Febrero.

.. _`Amazon WS`: http://aws.amazon.com/es/
.. _AWS: `Amazon WS`_
.. _Kinesis: http://aws.amazon.com/es/kinesis/
.. _`re:Invent 2013`: http://www.entredevyops.es/posts/reInvent-2013-amazon-ws.html
.. _CloudFront: http://aws.amazon.com/es/cloudfront/
.. _webinar: https://attendee.gotowebinar.com/register/4139542886387230465?source=EMC1&sc_ichannel=EM&sc_icountry=Global&sc_icampaign_type=Launch&sc_icampaign=EM_92282750&ref_=10
.. _EC2: http://aws.amazon.com/es/ec2/
.. _`número 97`: http://us4.campaign-archive2.com/?u=9735795484d2e4c204da82a29&id=5f11d89cd4&e=661cd1b265
.. _`Pycoder's Weekly`: http://pycoders.us4.list-manage.com/subscribe?u=9735795484d2e4c204da82a29&id=64134e0a27
.. _`PyCon 2014`: https://us.pycon.org/2014/
.. _horarios: http://pycon.blogspot.ca/2013/12/talks-tutorials-and-poster-selections.html
.. _`Gene Kim`: https://twitter.com/RealGeneKim
.. _`The Phoenix Project`: http://itrevolution.com/books/phoenix-project-devops-book/
.. _comentado: http://www.entredevyops.es/posts/the-phoenix-project.html
.. _`Jez Humble`: https://twitter.com/jezhumble
.. _`Continuous Delivery`: http://www.amazon.es/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912
.. _PuppetLabs: http://puppetlabs.com
.. _`encuesta anual sobre DevOps`: http://www.surveygizmo.com/s3/1483785/DevOps-Survey-2013
.. _`DevOps Weekly`: http://devopsweekly.com/
.. _`sobre los registros`: http://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying
.. _presentaciones: http://flowcon.org/flowcon-sanfran-2013/schedule/index.jsp
.. _vídeos: http://www.youtube.com/channel/UCMk1sRo1hnTLMA3kpn6BVKg
.. _Flowcon: http://flowcon.org
.. _Monitorama: http://monitorama.com/#cfp
