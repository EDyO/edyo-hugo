---
title: "Reunión de Junio de Sudoers BCN"
author: "Ignasi Fosch"
slug: "reunion-de-junio-de-sudoers-bcn"
date: 2013-06-04T20:37:37

tags: ["Eventos", "Sudoers BCN", "MongoDB", "Go"]
---

`Sudoers BCN`_
--------------

De nuevo, como cada mes, se realizó la reunión del grupo de Sudoers BCN, en la que Jordi Soucheiron habló sobre MongoDB, y Ignacio Torres hizo lo propio sobre Go.

<!--more-->


`MongoDB para sysadmins`_
-------------------------

`Jordi Soucheiron`_ explicó que MongoDB_ es una base de datos NoSQL, de 10gen_, quién también da soporte, orientada a documentos (JSON), con escalado horizontal (sharding) y alta disponibilidad (replicación). Permite actualizaciones atómicas pero no soporta transacciones ni incluye un lenguaje como SQL, puesto que utiliza JSON para realizar las consultas. Algunos de sus principales usos son:

- Almacenar ficheros, como se haría con S3, aproximadamente,
- Almacenar logs, como, por ejemplo, backend de logstash
- En sistemas de cola, como RabbitMQ..
- Data mining/Big Data, como storage, y herramienta de MapReduce.

Despliegues
```````````

El despliegue de desarrollo es con un sólo nodo, no hay *sharding* ni *HA*. El despliegue pequeño tiene un maestro y varios esclavos, de modo que permite HA, pero no hay *sharding*. Opcionalmente, se puede tener un retraso entre el nivel de actualización de uno de los esclavos para permitir recuperar errores lógicos. Esto debería alcanzar varios miles de inserts por segundo. El despliegue avanzado tiene una composición mucho más compleja: Hay un grupo de servidores, llamados de configuración (*config servers*) que conocen la ubicación de cada información en cada servidor. Luego hay otros grupos de nodos, separados en *shards*, que corresponde a cada partición. Estos *shards* se componen de una instalación basada en el despliegue pequeño, por lo que cada *shard* es autónomo, altamente disponible y permite tener nodos retrasados. El punto de fallo para un *shard* es que se estropeen tanto el nodo maestro como los esclavos. Jordi comentó que se habían llegado a hacer instalaciones de 30-40 *shards*. Además, al poder elegir la clave de distribución, se pueden tener distribuidas las lecturas y escrituras en cada *shard*. El tipo de replicación es configurable, así como las colecciones que se mantienen en *shard* y la clave que las distribuye. Los clientes se conectan a un proceso llamado ``mongos`` que es el que consulta a los *config servers* para saber a qué *shard* y qué nodo debe consultar. La desventaja es que siempre se necesitan tres servidores de configuración y que es una solución bastante más compleja que las otras.

En cuanto a las copias de seguridad, Jordi explicó que tiene una instrucción que permite volcar los datos a ficheros BSON. Aunque se puede hacer en caliente, ellos lo utilizan en los nodos que tienen retrasados para hacer una copia periódica. Relacionado al rendimiento, Jordi destacó el tamaño de los índices, pero sobretodo recomendó utilizar los *update in-place* antes que reescribir el documento entero. Para la medida de los documentos, se puede configurar un porcentaje sobre el tamaño original para que se reserve espacio para que el documento pueda crecer, pero comentó que no parece que se utilice mucho. Para la monitorización, utilizan consultas formateadas con JSON sobre uno de los nodos de cada *replica-set*, que les responde con un resumen del estado. También comentó que existen módulos y guiones para Nagios y otros sistemas similares que lo permiten gestionar con bastante facilidad.

Finalmente, hizo una demostración en la que, sobre una máquina virtual, instalaba tres nodos de mongoDB que contenían un solo *shard*, creando tres directorios y arrancando tres procesos mongoDB uno en cada directorio, con tres puertos distintos. Luego, se conectó a uno de los nodos, y, utilizando un documento JSON, lo inicializó. Tras esto, le indicó la existencia de los otros dos nodos y éstos se configuraron y replicaron automáticamente. Con esto hecho, se puede acceder a una interfaz de gestión vía HTTP/REST que permite visualizar el estado del *shard* y los correspondientes nodos.

`Go y el Zen de Python`_
------------------------

`Ignacio Torres`_ nos introdujo, a partir de la presentación de `Andrew Gerrand`_, en el mundo de Go_, un lenguaje de programación que apareció en 2009, con las siguientes características:

- Simple de leer y aprender.
- Tipado estático pero permitiendo ser usado como dinámico.
- Compilado en código máquina nativo, con un ciclo de desarrollo rápido.
- Funcionalidades especiales para la concurrencia a nivel del lenguaje. Puede interactuar directamente con Erlang.
- Librería estándar con esteroides y expansible.
- Muchas y buenas librerías.
- Código abierto con licencia BSD.

Algunos usos habituales serían:

- Demonios de servidor
- Herramientas de línea de comandos
- Aplicaciones web
- Juegos
- Aplicaciones científicas

Un factor muy importante que Ignacio destacó, es que Go es un lenguaje con sintaxis C, pero sin los peores aspectos de éste, que sigue la filosofía de Python. Hay que destacar que cualquier función puede convertirse en un método de un tipo, añadiéndolo sin necesidad de crear un heredero. Permite múltiples interfaces de forma muy sencilla. No hay ``this`` o ``self``, se hace referencia con un nombre elegido en el prototipo del método. La visibilidad de los elementos se define por el uso de mayúsculas y minúsculas. No hay subclases, decoradores, iteradores, excepciones, etcétera. La gestión de errores es explícita. El espacio de nombres de los paquetes es plano. Para reforzar la legibilidad de código, evitando los *one-liners*, no hay encadenamientos para las listas ni operador condicional ternario.

En cuanto al despliegue, el resultado de la compilación es un binario enlazado estáticamente, por lo que no hay que preocuparse por las dependencias. En lo relativo a la concurrencia, no hay que preocuparse del bloqueo, puesto que el compilador lo tiene en cuenta, y el código se ejecuta en paralelo con poco coste adicional (no hay GIL).

.. _`Sudoers BCN`: http://sudoers-barcelona.wikia.com/wiki/Sudoers_Barcelona_Wiki
.. _`MongoDB para sysadmins`: http://www.slideshare.net/jordixou/mongo-db-22441879
.. _`Jordi Soucheiron`: https://twitter.com/jordixou
.. _MongoDB: http://www.mongodb.org/
.. _10gen: http://www.10gen.com/
.. _`Go y el Zen de Python`: http://www.tux21b.org/public/go-python-zen.html#1
.. _`Ignacio Torres`: https://twitter.com/itorres
.. _Go: http://golang.org
.. _`Andrew Gerrand`: http://andrewgerrand.com

