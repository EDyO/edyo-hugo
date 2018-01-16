---
title: "Amazon WS re:Invent 2013"
author: "Ignasi Fosch"
slug: "reInvent-2013-amazon-ws"
date: 2013-11-25T21:00:00

tags: ["Eventos", "Amazon WS"]
---

.. image:: /images/AmazonWebservices.png
   :alt: AWS
   :align: right

Del día 12 al 15 de noviembre, tuvo lugar, en Las Vegas, el `re:Invent`_, de `Amazon WS`_. Siendo el mayor evento sobre el *cloud* de AWS_, esta edición contempló sesiones técnicas, sesiones formativas de entrenamiento, laboratorios de práctica y consultas técnicas con ingenieros y clientes expertos. Aunque nuestra asistencia fue imposible, este artículo contiene un resumen de las novedades que anunciaron.

<!--more-->


Nuevos servicios
----------------

Amazon WorkSpaces
~~~~~~~~~~~~~~~~~

Se diría que con la intención de introducirse en el mercado de servicios como `VMware Horizon View`_, `Amazon WS`_ ha anunciado su nuevo servicio WorkSpaces_. Éste nuevo servicio consiste en un sistema de escritorio completamente gestionado, más conocido como VDI_. Con él los usuarios pueden, desde sus portátiles, iPad, Kindle Fire, o tabletas Android, acceder a un sistema de escritorio personalizado, homogéneo y desde cualquier ubicación.

Amazon AppStream
~~~~~~~~~~~~~~~~

Éste otro servicio, aunque podría confundirse con el primero, es un poco distinto. En realidad consiste en disponer de aplicaciones ejecutándose en sistemas en el *cloud* con las que los usuarios interactúan desde sus dispositivos. De este modo, las aplicaciones pueden utilizar los recursos de computación de la nube, con independencia de los dispositivos que los usuarios estén utilizando. AppStream_ incluye un *SDK* que soporta *streaming* desde Microsoft Windows 2008 R2 a dispositivos con FireOS, Android, iOS y Microsoft Windows. Para 2014 está planificado ofrecer una *SDK* para Mac OS X.

Amazon CloudTrail
~~~~~~~~~~~~~~~~~

CloudTrail_, servicio que todavía se encuentra en beta, consiste, simplemente, en un servicio que registra todas las llamadas *API* que se producen con la cuenta AWS_, almacenándolas en ficheros en S3_. De este modo se puede realizar un seguimiento de todas las acciones administrativas que se han producido. El servicio registra:

* La identidad del usuario
* El momento de la llamada
* La dirección IP utilizada
* Los parámetros de la petición
* Los elementos de la respuesta

El servicio registra tanto las llamadas *API* generadas desde la consola de gestión web, los *SDK*, las herramientas de línea de comandos y otros servicios AWS_ de más alto nivel, como CloudFormation_.

Amazon Kinesis
~~~~~~~~~~~~~~

Kinesis_ consiste en un servicio de recopilación y procesado de flujos de datos en tiempo real a escala masiva. Su capacidad permite recoger y procesar cientos de terabytes de datos por hora desde cientos de miles de orígenes distintos. Utilizando este servicio se pueden escribir aplicaciones que procesen la información en tiempo real recibida de páginas web, información financiera y de márqueting, instrumentación de fabricación, medios sociales, registros operacionales o mediciones de datos. Se pueden construir cuadros de mandos en tiempo real, capturar excepciones de aplicaciones generando las alertas correspondientes, ofreciendo recomendaciones o tomar decisiones de negocio o operacionales. Además puede almacenar los datos en otros servicios como S3_, DynamoDB_ o Redshift_.

Nuevas instancias de EC2
------------------------

En el evento `re:Invent`_, además, se presentaron dos nuevos tipos de instancias de EC2_:

G2
~~

Diseñada para aplicaciones que requieran capacidades de cálculo para gráficos 3D, está equipada con una *GPU* `NVIDIA GRID`_, ofrece 8 *vCPU*, 15 GB de *RAM* y un disco *SSD* de 60 GB. Permite el uso de almacenamiento *EBS* y el rendimiento de sus interfaces de red es alto.

C3
~~

Esta familia basa su capacidad de computación en los chips de alto rendimiento de `Intel Xeon E5`_. Además, se provisionan con almacenamiento basado en *SSD*. Son la família de instancias que proporcionan la menor relación precio/rendimiento de computación y disponen de capacidades de comunicaciones más avanzadas. Mejoran la latencia entre instancias, tienen menor *jitter* y un rendimiento en paquetes por segundo significativamente más alto.

Funcionalidades en servicios ya existentes
------------------------------------------

En esta ocasión, AWS_ presentó nuevas funcionalidades en tres servicios ya existentes:

PostgreSQL ya está soportado en RDS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Con todos sus tipos de datos y sus funciones de compresión de información, búsqueda textual y de consultas geoespaciales, RDS_ incluye con PostgreSQL_ sus típicas funcionalidades como el despligue multizona, recuperación a punto en el tiempo, *snapshots* de la base de datos, copia de *snapshots* entre regiones, aprovisionamiento de *IOPS*, y soporte *VPC*.

Redshift también dispone de *snapshots* entre regiones
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

AWS_ ha anunciado la disponibilidad de la función de copia de *snapshots* entre regiones para el servicio Redshift_. La copia de *snapshots* entre regiones es una gran funcionalidad en los servicios de AWS_, sobretodo para aquellos usuarios que trabajan en ubicaciones muy distanciadas. Al permitir hacer una copia de un *snapshot* de una base de datos en una región a otra región, pudiendo levantar otra instancia, es posible tener un sistema de copia de seguridad muy eficiente.

Mejoras y optimizaciones en el Trusted Advisor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

AWS_ ha incluido mejoras significativas en su `Trusted Advisor`_, como la visualización del ahorro mensual, o un análisis del beneficio de utilizar volúmenes *EBS* con aprovisionamiento de *IOPS*. También han retocado el interfaz de usuario para simplificar la visualización y su utilización.

`Trusted Advisor`_ es un cuadro de mando, disponible para clientes con planes de soporte *Business* y *Enterprise*, que ofrece comprovaciones y recomendaciones sobre la infraestructura en uso en AWS_ dentro de cuatro apartados:

* Optimización de coste
* Seguridad
* Tolerancia a fallos
* Rendimiento

.. _`Amazon WS`: http://aws.amazon.com/es/
.. _AWS: `Amazon WS`_
.. _`re:Invent`: http://reinvent.awsevents.com/index.html
.. _`VMware Horizon View`: http://www.vmware.com/es/products/horizon-view/
.. _WorkSpaces: http://aws.amazon.com/workspaces/
.. _VDI: http://es.wikipedia.org/wiki/Virtualizaci%C3%B3n_de_escritorio
.. _AppStream: http://aws.amazon.com/appstream/
.. _CloudTrail: http://aws.amazon.com/cloudtrail/
.. _S3: http://aws.amazon.com/s3/
.. _CloudFormation: http://aws.amazon.com/cloudformation/
.. _Kinesis: http://aws.amazon.com/kinesis/
.. _DynamoDB: http://aws.amazon.com/es/dynamodb/
.. _Redshift: http://aws.amazon.com/es/redshift/
.. _EC2: http://aws.amazon.com/es/ec2/
.. _`NVIDIA GRID`: http://www.nvidia.es/object/grid-vdi-desktop-virtualisation-es.html
.. _`Intel Xeon E5`: http://www.intel.com/content/www/us/en/processors/xeon/xeon-processor-5000-sequence.html
.. _RDS: http://aws.amazon.com/es/rds/
.. _PostgreSQL: http://www.postgresql.org/
.. _`Trusted Advisor`: https://aws.amazon.com/es/premiumsupport/trustedadvisor/
