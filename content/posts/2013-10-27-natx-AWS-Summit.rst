---
title: "Crónica del AWS Summit Barcelona 2013"
author: "Eduardo Bellido Bellido, Ignasi Fosch"
slug: "aws-summit-barcelona-2013"
date: 2013-10-27T20:00:00

tags: ["Eventos", "Amazon WS", "Cloud"]
---

.. image:: /images/AmazonWebservices.png
   :alt: AWS
   :align: right

Este pasado jueves `Amazon WS`_ celebró en Barcelona un Summit_ para ofrecer una visión de sus tecnologías *cloud*, casos prácticos de empresas, su aplicación para escenarios de *Big Data*, copias de seguridad y *Disaster Recovery*, así como aspectos de seguridad. El evento pudo seguirse en Twitter con el hashtag `#awssummit`_.

<!--more-->


Un Paseo por las Nubes: El *Cloud* for AWS
------------------------------------------

Carlos Conde, Director del equipo de arquitectos de AWS, fue el encargado de `abrir el evento`_. Nos mostró las ventajas de utilizar los servidos de Amazon WS y como tienen en cuenta y escuchan a sus clientes a la hora de crear y desplegar nuevos servicios. También pudimos ver el especular crecimiento que han tenido desde su creación, siendo en la actualidad el mayor proveedor de servicios *cloud*, manteniendo una ventaja abismal respecto a sus competidores actuales.

Seguridad y cumplimiento de normativas en el *Cloud*
----------------------------------------------------

Charla donde se expuso el punto de vista en cuanto a seguridad se refiere en Amazon WS, así como algunas buenas prácticas al respecto. También nos mostraron las diferentes certificaciones que dispone Amazon WS, garantía de que nuestros datos están seguros en la nube y que podemos confiar en la privacidad de los mismos.

*Cloud* Híbrida y Aplicaciones empresariales en AWS
---------------------------------------------------

En esta última charla antes del descanso para el almuerzo, varios clientes españoles mostraron como habían utilizado los `servicios de Amazon WS`_ dentro de sus empresas y los motivos que les llevaron a tomar esta decisión.

Las empresas invitadas fueron:

* `Mapfre`_, que utiliza los servicios de Amazon WS para realizar los cálculos de solvencia requeridos para el cumplimiento de la normativa europea actual, todo con el objetivo de minimizar costes en *HPC*.

* `Miquel Alimentació Grup`_, que con el objetivo de ganar en competitividad en un mercado tan exigente, y siendo en la actualidad los sistemas informáticos una pieza clave para tal fin, deciden apostar por Amazon WS.

* `IE Business School`_, que han migrado sus sistemas de *IT* a la nube, todo con el propósito de garantizar el mejor servicio posible a los estudiantes que han escogido este centro para llevar a cabo sus estudios. En esta ocasión presenciamos dos ponencias, una desde un punto de vista puramente empresarial, y la otra más técnica, ya que el encargado de presentarla fue uno de los miembros del equipo de Administradores de Sistemas.

Soluciones de *Disaster Recovery* en AWS
----------------------------------------

La charla empezó describiendo las soluciones que AWS_ puede ofrecer a la recuperación de desastres, que se centraron en :

* El uso de servicios de almacenamiento a corto plazo, como S3_ o EBS_, y a largo plazo, como Glacier_.
* Servicios de comunicaciones, es decir, diferentes formas de establecer conexión con los servicios en la nube, como `Direct connect`_ o VPC_.

Finalmente detalló cuatro patrones de arquitecturas de *DR*:

*Backup & Restore*
~~~~~~~~~~~~~~~~~~

Este patrón consiste en tener una infraestructura en producción, de la que se van haciendo copias de seguridad, guardándolas en S3_, la última, y en Glacier_, las anteriores. Cuando algo le sucede a producción, se genera una nueva infraestructura sobre la que se restaura la última copia y, utilizando el DNS, se redirige el tráfico. Sus principales ventajas son que es muy simple, tiene una barrera técnica muy baja, y que su coste es suficientemente efectivo.
Una variación de esto, cuando la infraestructura está en instalación propios, pasaría por utilizar un `Storage Gateway`_, que es un sistema virtualizado que permite conectar los dispositivos y sistemas de almacenamientos locales a S3_. RDS_ pueden combinarse con estos escenarios. Utilizando estas técnicas, Amazon consiguió reducir sus tiempos de restauración de 15 horas a 2'5.

*Pilot light*
~~~~~~~~~~~~~

Es muy similar al anterior, pero, en este caso, la nueva infrastructura se encuentra parcialmente arrancada, recibiendo actualizaciones de los datos. Ante una situación de contingencia, la infraestructura alternativa escala para soportar la carga y, utilizando `Route 53`_, se redirige el tráfico.

*Hot Standby Architecture*
~~~~~~~~~~~~~~~~~~~~~~~~~~

Ambas infraestructuras están en funcionamiento simultáneo, pero sólo una recibe el tráfico productivo. Su principal ventaja es que se restaura muy rápido, pero su coste es el doble.

*Multi-site solution mixing AWS and on-premise*
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Para cuando el tiempo de caída es crítico, esta solución permite reducirlo al mínimo, aunque requiere escalabilidad. La instalación principal no puede soportar todo el tráfico posible. El funcionamiento de este patrón es similar al anterior, pero ambas infraestructuras reciben tráfico de producción.

Continuous Deployment
---------------------

En esta charla se explicó cómo disponer las herramientas para poder hacer despliegue continuo en Amazon WS. El uso de CloudFormation_ puede permitir la automatización de estos entornos. Sus casos de uso podrían ser entornos de test, o de pruebas de carga, de *A/B testing*, de cálculo y análisis de datos o para arquitecturas orientadas al coste.

Big Data
--------

Finalmente, se `comentaron casos de uso`_ de empresas españolas que utilizando recursos de AWS_, están realizando sus operaciones de análisis, *Business Intelligence* o *Big Data*. Los productos más interesantes fueron Redshift_, que consiste en un servicio de almacén de datos en la nube, o `Elastic Map Reduce`_ para el análisis.

.. _`abrir el evento`: http://es.slideshare.net/AmazonWebServices/aws-summit-barcelona-opening-keynote
.. _`servicios de Amazon WS`: http://es.slideshare.net/AmazonWebServices/aws-summit-barcelona-hybrid-enterprise-apps
.. _`comentaron casos de uso`: http://es.slideshare.net/AmazonWebServices/aws-summit-barcelona-data-analysis-on-aws
.. _`Amazon WS`: http://aws.amazon.com/es/
.. _Summit: https://aws.amazon.com/es/aws-summit-2013/barcelona/
.. _AWS: `Amazon WS`_
.. _`#awssummit`: https://twitter.com/search?q=%23awssummit
.. _`Mapfre`: http://www.mapfre.es/
.. _`Miquel Alimentació Grup`: http://www.miquel.es/
.. _`IE Business School`: http://www.ie.edu/business-school/
.. _S3: http://aws.amazon.com/es/s3/
.. _EBS: http://aws.amazon.com/es/ebs/
.. _Glacier: http://aws.amazon.com/es/glacier/
.. _`Direct connect`: http://aws.amazon.com/es/directconnect/
.. _VPC: http://aws.amazon.com/es/vpc/
.. _`Storage Gateway`: http://aws.amazon.com/es/storagegateway/
.. _RDS: http://aws.amazon.com/es/rds/
.. _CloudFormation: http://aws.amazon.com/es/cloudformation/
.. _`Route 53`: http://aws.amazon.com/es/route53/
.. _Redshift: http://aws.amazon.com/es/redshift/
.. _`Elastic Map Reduce`: http://aws.amazon.com/es/elasticmapreduce/
