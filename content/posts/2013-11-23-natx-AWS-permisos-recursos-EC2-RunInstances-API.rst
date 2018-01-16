---
title: "Permisos sobre recursos en RunInstances de EC2"
author: "Ignasi Fosch"
slug: "amazon-ws-ec2-runinstances-permisos-nivel-recursos"
date: 2013-11-23T12:15:00

tags: ["Amazon WS"]
---

`Amazon WS`_ ha anunciado que ha añadido, a la *API* RunInstances_ de EC2_, la posibilidad de gestionar permisos a nivel de recursos. RunInstances_ es la *API* principal y más común para crear nuevas instancias en EC2_, y ahora permite limitar ciertos aspectos de la creación por usuario.

<!--more-->


La nueva funcionalidad consiste en permitir la construcción de políticas IAM_ que permiten un mejor control sobre las instancias que los usuarios pueden crear. De este modo, por ejemplo, se podría restringir a los usuarios las *AMI* o *snapshots* que pueden utilizar para la creación de sus nuevos servidores. También permite controlar las subredes, *VPC* o los grupos de seguridad que pueden asignar a sus nuevas instancias.

Como con otros permisos a nivel de recurso, se pueden utilizar las etiquetas asignadas a los recursos, lo que permite escribir fácilmente políticas que controlen, por ejemplo, que ciertos usuarios sólo puedan crear instancias en el entorno de desarrollo.

.. _`Amazon WS`: http://aws.amazon.com/es/
.. _AWS: `Amazon WS`_
.. _RunInstances: http://docs.aws.amazon.com/AWSEC2/latest/APIReference/ApiReference-query-RunInstances.html
.. _EC2: http://aws.amazon.com/es/ec2/
.. _IAM: http://aws.amazon.com/es/iam/
