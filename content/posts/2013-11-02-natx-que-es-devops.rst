---
title: "¿Qué es DevOps?"
author: "Ignasi Fosch"
slug: "que-es-devops"
date: 2013-11-02T10:00:00

tags: ["DevOps", "Automatización", "Filosofía"]
---

.. image:: /images/show-me-the-devops.png
   :width: 250
   :height: 135
   :alt: ¿DevOps? ¿Y eso qué es?
   :class: border
   :align: right

Desde la primera vez que oí hablar de DevOps, hace casi 3 años, pasó cierto tiempo en el que, en mi mente, se formaban ideas equivocadas sobre a lo que se refería. Con el tiempo, he ido comprendiendo el concepto pero, al mismo tiempo, cada vez he ido conociendo a más gente con el mismo problema. Este artículo intenta aclarar el concepto para que nadie más se pregunte *¿Qué es esto del DevOps?*

<!--more-->


Breve historia de DevOps
------------------------

El término DevOps se populariza a raíz de los primeros eventos `DevOps Days`_ que se suceden en Bélgica desde 2009, y que se han ido extendiendo de forma global. Su aparición está estrechamente relacionada con:

* La adopción de la filosofía de producción ajustada, o lean_, a nivel empresarial, y de las metodologías ágiles, o agile_, en los equipos de desarrollo.
* La demanda de incrementar el ratio de publicación de nuevas versiones de los productos.
* La amplia oferta de infraestructuras de virtualización y computación en la nube.
* El incremento del uso de herramientas para la automatización de los centros de datos y de las herramientas de configuración.

Su principal objetivo es promover un conjunto de procesos y métodos para mejorar la comunicación y la colaboración entre departamentos.

Durante todo este tiempo, el movimiento DevOps se ha desplazado sobre los siguientes puntos:

1. Definición: Evidentemente, uno de los intereses fue concretar a qué se refería. Aún hay, de vez en cuando, bastantes discusiones sobre este tema.
2. Despliegue y aprovisionamiento: Centrándose en la presión constante del resto de departamentos de producción, concretar cómo se puede conectar el desarrollo, integración y despliegue continuos, a fin de satisfacer las necesidades y expectativas del negocio. Una consecuencia de esta etapa es la enorme evolución que las herramientas de integración y despliegue continuos han sufrido en los últimos años.
3. Monitorización: En este campo se han centrado enormes esfuerzos por mantener el control sobre los aspectos realmente importantes de la producción y operación del producto. Un claro símbolo de esto, son los *hashtags* `#monitoringsucks`_ y `#monitoringlove`_ que guiaron las discusiones en Twitter y provocaron la aparición de los eventos Monitorama_ y `Monitorama EU`_.

¿Qué no es DevOps?
------------------

Durante estos últimos 4 años, DevOps ha sido definida incorrectamente en muchas ocasiones, dando ideas incorrectas a mucha gente de entrada. Éstos son algunos de los conceptos que suelen confundirse con DevOps:

* *DevOps es utilizar herramientas como X*: DevOps es una filosofía relacionada con la comunicación y colaboración entre los distintos equipos o departamentos implicados. Aunque es habitual que se utilice un amplio espectro de herramientas, no es fundamental, no es lo que define DevOps.
* *DevOps es que desarrolladores y operaciones hagan las mismas tareas*: Aunque suele ocurrir que los componentes de los equipos tienen perfiles bastante mixtos, no se trata de concentrar las tareas en uno u otro equipo.
* *DevOps es un nuevo rol o perfil laboral*: Como en el caso anterior, tampoco es cierto que se pueda definir un nuevo equipo o departamento, ni tampoco un perfil laboral concreto. DevOps es una filosofía, por lo que es posible que en una oferta de trabajo interese mencionar que la empresa la aplica, pero eso no configura, sin más, un puesto de trabajo.

¿Cómo definir DevOps?
---------------------

Llegados a este punto, muchos se preguntarán cómo definir, entonces, DevOps. DevOps es una filosofía que apoya y promueve la colaboración y comunicación entre los distintos departamentos y equipos implicados en el desarrollo de un producto o servicio. Usualmente, es una extensión natural de los conceptos *lean* y *agile*, y que se aplica en relación a las operaciones, especialmente las tecnológicas.

Por ejemplo, cuando en los procesos de concepción, diseño y desarrollo, se implica correcta y convenientemente a las personas que van a estar implicadas, se está aplicando la filosofía DevOps. Si uno de los equipos es apartado para, pongamos, evitar que pueda poner trabas y obstáculos, la filosofía DevOps se está dejando de aplicar. Así, alguien que pone obstáculos y trabas, pero no ofrece alternativas, acuerdos o soluciones, no está aplicando DevOps.

.. _`DevOps Days`: http://devopsdays.org
.. _lean: http://es.wikipedia.org/wiki/Lean_manufacturing
.. _agile: http://es.wikipedia.org/wiki/Desarrollo_%C3%A1gil_de_software
.. _`#monitoringsucks`: https://twitter.com/search?q=%23monitoringsucks&src=typd&f=realtime
.. _`#monitoringlove`: https://twitter.com/search?q=%23monitoringlove&src=typd&f=realtime
.. _Monitorama: http://monitorama.com
.. _`Monitorama EU`: http://monitorama.eu
