---
title: "Crónica de el Orchestrate 2017"
author: "Ignasi Fosch"
slug: "cronica-orchestrate-2017"
date: 2017-04-29T19:50:00

tags: ["DevOps", "Eventos", "Herramientas", "Integración Contínua"]
---

<img src='/images/bb4decaa-0e40-11e7-9007-41080697e259.png' alt='AWS Lambda' class='align-right' height='75' width='200'/>

El pasado 6 de Abril tuvo lugar, en [CodeWorks], el [Orchestrate 2017], un evento sobre DevOps, que ya [anunciamos].
De la mano de [blended.io], el evento trató principalmente sobre [Kubernetes], contenedores, microservicios y testeo.

Esta es una crónica del evento, esperamos que os guste!

<!--more-->


En primer lugar, habló [Luke Bond], sobre el concepto de [Operators] en [Kubernetes], un tema presentado en un [conocido artículo] de [CoreOS].
Los operadores son controladores de [Kubernetes] que implementan la lógica específica de aplicaciones *stateful* de forma que se pueden gestionar confiablemente.
Lo interesante del concepto es que plantea la posibilidad de desplegar y gestionar bases de datos en el cluster [Kubernetes].

Tras esto, [Andrew Martin] habló sobre cómo las tecnologías de contenedores interactúan con la seguridad.
Empezando con una revisión de los últimos ataques que han ido apareciendo, para explicar cómo el uso de contenedores puede ayudar o, en ocasiones, complicar la implementación de la seguridad.
Aunque los conceptos de seguridad no han evolucionado mucho, las herramientas se están viendo complementadas con utilidades específicas para usar con contenedores.

Por motivos logísticos, hubo un cambio en el programa, y [Samuel Cozannet], de [Ubuntu], explicó de qué modo herramientas como [Juju], [MAAS], o [snaps] se pueden utilizar para desplegar aplicaciones sobre clusters de contenedores.
Aunque no se habló mucho de Tensorflow, el planteamiento encajaba con su uso, pero también debería ser posible usarlo para otros tipos de aplicaciones.

Tras la comida, [Snadeep Dinesh] presentó el uso de [Kubernetes Federation], [StatefulSets] y otros mecanismos de [Kubernetes] para desplegar microservicios a nivel global.
Siendo un tema que venía a encajar con el de los [Operators], podría haber sido interesante tenerlos seguidos, incluso en orden inverso.

Luego, [Guillem Hernández] explicó cómo [Jenkins] puede utilizar [Pipelines] para automatizar el testeo funcional.
No deja de sorprender cómo [Groovy] ha encontrado en éste tema un [buen caso de uso].

Finalmente, [Jon Nordby] charló sobre por qué, por las características de rendimiento de distintas aplicaciones, poniendo como ejemplo [MsgFlo] y [GuvScale], el uso de sistemas de mensajes y colas, como [RabbitMQ], puede ser tan interesante.

[Codeworks]: https://codeworks.me
[Orchestrate 2017]: https://ti.to/blended/orchestrate-2017/en
[anunciamos]: http://www.entredevyops.es/posts/orchestrate-2017.html
[blended.io]: https://blended.io
[Kubernetes]: https://kubernetes.io/
[Luke Bond]: https://github.com/lukebond
[Operators]: https://coreos.com/operators/
[conocido artículo]: https://coreos.com/blog/introducing-operators.html
[CoreOS]: https://coreos.com/
[Andrew Martin]: https://twitter.com/sublimino?lang=es
[Samuel Cozannet]: https://twitter.com/samnco_23?lang=es
[Ubuntu]: https://www.ubuntu.com/
[Juju]: https://www.ubuntu.com/cloud/juju
[MAAS]: https://maas.io/
[snaps]: https://www.ubuntu.com/desktop/snappy
[Snadeep Dinesh]: https://twitter.com/sandeepdinesh?lang=es
[Kubernetes Federation]: https://kubernetes.io/docs/user-guide/federation/
[StatefulSets]: https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/
[Guillem Hernández]: https://twitter.com/guillemhs?lang=es
[Jenkins]: https://jenkins.io/
[Pipelines]: https://jenkins.io/doc/book/pipeline/
[Groovy]: http://groovy-lang.org/
[buen caso de uso]: https://jenkins.io/solutions/pipeline/
[Jon Nordby]: https://twitter.com/jononor?lang=es
[Msgflo]: https://github.com/msgflo/msgflo
[GuvScale]: https://guvscale.com/
[RabbitMQ]: https://www.rabbitmq.com/
