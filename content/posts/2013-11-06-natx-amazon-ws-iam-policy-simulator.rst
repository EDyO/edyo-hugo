---
title: "Amazon WS ha presentado el simulador de políticas de IAM"
author: "Ignasi Fosch"
slug: "amazon-ws-presenta-iam-policy-simulator"
date: 2013-11-06T23:00:00

tags: ["Eventos", "Amazon WS", "Seguridad"]
---

.. image:: /images/iam.jpg
   :width: 183px
   :height: 123px
   :alt: Seguridad mejorada en Amazon WS IAM
   :class: border
   :align: left

Esta semana `Amazon WS`_ ha publicado una nueva funcionalidad para su servicio IAM_, con el que intenta mejorar el despliegue de configuraciones de seguridad algo más complejas, asegurando que no afecten al funcionamiento de la infraestructura. El servicio IAM_ es el que permite administrar el modo en que los usuarios se autentican y acceden a los servicios que se hayan contratado con `Amazon WS`_. La aplicación de políticas complejas pueden poner en peligro el funcionamiento del sistema desplegado.

<!--more-->


Ya hace cierto tiempo que es posible gestionar políticas de acceso a los distintos recursos, de modo que, por ejemplo, un usuario pueda acceder a un *bucket* de S3_ pero no a otros *buckets* o servicios. Ciertas configuraciones de estas políticas pueden volverse bastante complicadas. Además, es posible que estas políticas, de estar mal aplicadas, pudieran bloquear el funcionamiento de los servicios más críticos.

El producto que `Amazon WS`_ ha publicado, llamado `IAM Policy Simulator`_, permite verificar lo que ocurriría de aplicar un nuevo conjunto de políticas a los servicios en producción. `Amazon WS`_ también ha hecho público un vídeo_ en el que lo explican con más detalle. Otra fuente de información interesante es el `blog de seguridad de Amazon WS`_.

.. _`Amazon WS`: http://aws.amazon.com/es/
.. _IAM: http://aws.amazon.com/es/iam/
.. _S3: http://aws.amazon.com/es/s3/
.. _`IAM Policy Simulator`: http://docs.aws.amazon.com/IAM/latest/UsingPolicySimulatorGuide/iam-policy-simulator-guide.html
.. _vídeo: http://www.youtube.com/watch?v=1IIhVcXhvcE&feature=youtu.be&channel=EM&Campaign_Type=Launch&Campaign_id=34866820&ref_=8
.. _`blog de seguridad de Amazon WS`: http://blogs.aws.amazon.com/security/?channel=EM&Campaign_Type=Launch&Campaign_id=34866820&ref_=pe_411040_34866820_10
