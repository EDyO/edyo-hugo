---
title: "Nuevas funcionalidades y noticias en Amazon WS"
author: "Ignasi Fosch"
slug: "nuevas-funcionalidades-amazon-ws"
date: 2013-11-05T00:15:00

tags: ["Amazon WS"]
---

.. image:: /images/AmazonWebservices.png
   :alt: AWS
   :align: right

Entre el jueves de la semana pasada y este lunes, `Amazon WS`_ publicó algunas noticias sobre nuevas funcionalidades en sus productos RDS_, Cloudfront_, y CloudWatch_. También reconocieron ciertos problemas en su actualización de versión menor de MySQL_ en RDS_, por lo que han detenido su calendario de aplicación de dicha actualización, aunque ofrecen a los usuarios que lo deseen, poderse actualizar.

<!--more-->


Cambios en el calendario de actualización de versión menor de MySQL en RDS
--------------------------------------------------------------------------

El pasado día 14, publicaron un calendario de actualización de las versiones menores de MySQL a 5.1.71, 5.5.33 y 5.6.13, respectivamente. Amazon_ ejecuta estos cambios manteniendo especial atención en las evoluciones de sus monitorizaciones. El pasado miércoles, día 30, observaron ciertos indicios que les llevaron a detener los procesos de actualización en todas las regiones, para revisarlo y reprogramar el resto de actualizaciones.

En caso que un usuario desee actualizar, puede hacerlo manualmente, modificando su instancia cambiando la versión. Este cambio puede ser aplicado de forma inmediata o durante la siguiente ventana de mantenimiento. Esto causará un reinicio de la instancia. También es posible descartar la actualización automática seleccionando la respuesta 'No' en la opción '*Auto Minor Version Upgrade*'.

En caso de actualizarse, recomiendan comprobar la compatibilidad y el correcto funcionamiento de las aplicaciones con las nuevas versiones menores. Para más información, siempre se puede consultar la `documentación de RDS sobre las versiones de MySQL`_

Nueva funcionalidad de copia de un snapshot de RDS entre regiones
-----------------------------------------------------------------

El sábado pasado, anunciaban que la copia de *snapshots* de base de datos, para los tres motores soportados (Oracle, SQL Server y MySQL) permitía hacerlo de una región a otra, con lo que es posible copiar un *snapshot* a otra región y levantar una nueva instancia en dicho destino. El funcionamiento es, como es habitual, tanto desde la consola de gestión como utilizando las correspondientes llamadas API, o, por lo tanto, los correspondientes comandos CLI.

Dado que las copias pueden tardar cierto tiempo, recomiendan la configuración y suscripción de `eventos de bases de datos`_ para conocer el momento en el que los datos se han copiado.

En cuanto al coste, se cobrará el coste de traspaso de región a región, que es inferior al del tráfico de Internet, y el coste de almacenamiento en la región destino. Como las copias de *snapshots*, son incrementales una vez se ha realizado la primera, los costes subsecuentes siempre serán inferiores. Para saber más recomiendan leer la `Guía de usuario de Amazon RDS`_.

Nuevas ubicaciones de servicio para CloudFront
----------------------------------------------

Amazon_ ha abierto tres ubicaciones más para mejorar el servicio de CloudFront_: Atlanta, en los EE.UU., Londres, en el Reino Unido, y Frankfurt, en Alemania. Con estas, ya son 46 las ubicaciones totales con las que cuenta este servicio en todo el mundo. Con cada nueva ubicación, la latencia en el servicio de los contenidos desciende, mejorando el rendimiento que obtienen los usuarios finales. En caso de estar ya usando CloudFront, no es necesario realizar ninguna acción. En el caso que sea conveniente, se servirán los contenidos directamente desde estas nuevas ubicaciones.

Aprovecharon para presentar el webinario_ sobre CloudFront_ que han organizado para el próximo día 7, a las 19:00, hora española. También indican que en el `AWS re:Invent`_ tendrán lugar las siguientes charlas sobre CloudFront:

* `Aceleración dinámica de contenido`_.
* `Streaming bajo demanda y en directo`_.
* `Uso de las caches para escalar aplicaciones`_.

Búsqueda y navegación por las métricas de CloudWatch
----------------------------------------------------

Finalmente, la última noticia es sobre las mejoras introducidas en el servicio CloudWatch_. Junto a las mejoras de rendimiento que permitirán a las métricas cargarse con mayor velocidad, se ha creado, dentro de la consola de gestión, un `cuadro de mando de Amazon CloudWatch`_ que permite encontrar métricas introduciendo solamente un término o navegar por categorías de métricas_ hasta encontrar la que se está buscando.

.. _`Amazon WS`: http://aws.amazon.com/es/
.. _Amazon: `Amazon WS`_
.. _AWS: `Amazon WS`_
.. _RDS: http://aws.amazon.com/es/rds/
.. _MySQL: http://mysql.com/
.. _`documentación de RDS sobre las versiones de MySQL`: http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_MySQL.html#MySQL.Concepts.VersionMgmt
.. _`eventos de bases de datos`: http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Events.html?channel=EM&Campaign_Type=Launch&Campaign_id=33361880&ref_=pe_411040_33361880_7
.. _`Guía de usuario de Amazon RDS`: http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html
.. _CloudFront: http://aws.amazon.com/es/cloudfront/
.. _webinario: https://event.on24.com/eventRegistration/EventLobbyServlet?target=registration.jsp&eventid=700642&sessionid=1&key=ED5FF854BD9C2081E4B26E38DC496A4C&partnerref=WN&channel=EM&Campaign_Type=Launch&Campaign_id=40553290&ref_=7&partnerref=EM_40553290&sourcepage=register
.. _`AWS re:Invent`: http://reinvent.awsevents.com/
.. _`Aceleración dinámica de contenido`: https://portal.reinvent.awsevents.com/connect/sessionDetail.ww?SESSION_ID=2033&channel=EM&Campaign_Type=Launch&Campaign_id=40553290&ref_=8&partnerref=EM_40553290
.. _`Streaming bajo demanda y en directo`: https://portal.reinvent.awsevents.com/connect/sessionDetail.ww?SESSION_ID=1156&channel=EM&Campaign_Type=Launch&Campaign_id=40553290&ref_=9&partnerref=EM_40553290
.. _`Uso de las caches para escalar aplicaciones`: https://www.portal.reinvent.awsevents.com/connect/sessionDetail.ww?SESSION_ID=1215&channel=EM&Campaign_Type=Launch&Campaign_id=40553290&ref_=10&partnerref=EM_40553290
.. _CloudWatch: http://aws.amazon.com/es/cloudwatch/
.. _`cuadro de mando de Amazon CloudWatch`: http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/finding_metrics_with_cloudwatch.html?channel=EM&Campaign_Type=Launch&Campaign_id=39180040&ref_=pe_411040_39180040_10
.. _métricas: http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/supported_services.html?channel=EM&Campaign_Type=Launch&Campaign_id=39180040&ref_=pe_411040_39180040_9
