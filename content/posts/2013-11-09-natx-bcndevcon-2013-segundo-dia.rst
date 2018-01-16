---
title: "Segundo día en la BcnDevCon'13"
author: "Ignasi Fosch"
slug: "bcndevcon-2013-segundo-dia"
date: 2013-11-11T07:00:00

tags: ["Eventos", "BcnDevCon", "DevOps", "Escalabilidad", "Python", "Pruebas", "TDD"]
---

.. image:: /images/bcndevcon13.jpeg
   :width: 125px
   :height: 125px
   :alt: BcnDevCon13
   :class: border
   :align: right


El segundo día de la BcnDevCon_'13 estuvo plagado de charlas y actividades, el final del `Hackathon for education`_, Los concursos de Mario Kart y Street Fighter. El salón de RetroBarcelona_ fue muy visitado y la `Agile Station`_, coordinada por la gente de `Agile BCN`_, tuvo una actividad frenética, como el día anterior.

<!--more-->


Problemas de la escalabilidad
-----------------------------

`David Poblador`_, responsable de disponibilidad en Spotify_, explicó cómo su infraestructura, usuarios y servicios han crecido en los últimos cinco años. Su crecimiento, en datos resumidos, serían como sigue:

* 1000M de listas de reproducción, actualmente. En 2010, tenían 400M y añaden 2M cada día.
* De 20 servidores en 2008, pasaron a 1300 en 2011, y a más de 6000 en 2013.
* Se encuentran en 32 mercados, pero en 201 sólo estaban en 12 mercados.
* En 2010, el equipo de operaciones e infraestructura lo componían 10 personas, lo que provocó mucha deuda técnica. Ahora son diez veces más.
* Actualmente, tienen 4 centros de datos lógicos. Aunque algunos de éstos, se componen en algunos más, no están muy alejados entre ellos.
* Más de 20M canciones, y añaden 20000 nuevas diariamente.
* Más de 24M de usuarios activos.
* Más de 50 equipos creando nuevos componentes y productos.
* Alrededor de 100 sistemas de *backend*.

Estas condiciones de dimensión y crecimiento han provocado que recopilen mucho conocimiento aprendiendo al encontrarse con problemas que superar. Respecto al escalado de los centros de datos, destacó cierto puntos a tener en cuenta:

1. Cuando se es pequeño, es necesario admitir que siempre habrá alguien que sabrá y podrá montar centros de datos mejor que uno mismo.
2. Simplificar el proceso de adquisición. El contacto y trato con los proveedores es crítico.
3. Tener una unidad de capacidad para el aprovisionamiento. Consiste en una medida que contengan los servidores y el resto de infraestructura necesaria para su conexionado, que facilitará el aprovisionamiento y su conexionado. En su caso, la llaman *POD*, y consta de 44 racks casi llenos de servidores. 
4. Los centros de datos se están convirtiendo en un servicio poco habitual, debido a la utilización de cloud.

Hablando del escalado del *backend*, explicó cómo funciona su sistema. Los usuarios, con su cliente, se conectan a uno de una serie de servidores, llamados *Access Points*, mediante una única conexión TCP. El cliente pedirá las playlists, que el AP recuperará del sistema de *backend* correspondiente. Para poder escalar esta infraestructura, deben ser conscientes de sus límites, por ejemplo, si un AP puede atender 60K usuarios (es un valor hipotético), para atender 600K, serán necesarios más de 10 APs, para evitar problemas al caer uno de ellos.

Expuso el lema 'No intentes ser demasiado inteligente'. Como ingenieros, es frecuente que, al intentar resolver algun problema o necesidad, se intente cubrir con una respuesta completa, a menudo, mucho más allá de lo necesario. Por ejemplo, para identificar cuáles son los nodos que están dando servicios, decidieron utilizar el *DNS*. De este modo, disponían de un servicio ya construido que es simple, estándar y conocido. Lo utilizaron para funciones como:

* Registro de errores.
* Búsqueda de anillos de *DHT*.
* Descubrimiento de servicios (utilizan registros ``SRV``).
* Distribución de usuarios por zona geográfica.

No obstante, se encontraron con ciertos problemas:

* Los terminales iPhone, en todas sus versiones de iOS, tiene ciertos detalles como descartar todas las respuestas más allá del octavo registro. Muchos usuarios con iPhone acababan en un grupo pequeño de APs, que acababan saturándose.
* El uso de los DNS de Google, como 8.8.8.8, muy extendido en Europa, causó muchos usuarios europeos acabaran en APs de Estados Unidos.

Resolvieron estos protocolos dejando de utilizar el protocolo *DNS*. Utilizan un servicio que responde con estructuras JSON_ que pueden gestionar mejor.

El almacenamiento es otro punto de la infraestructura que conviene escalar convenientemente. Se encontraron con el caso de un servicio de *backend* que indexa las canciones. Sus índices, al principio, cabían en *RAM*, pero, cuando dejaron de hacerlo, su rendimiento pasó a depender de la velocidad de sus discos duros, unos pocos cientos de *IOPS*. Por lo que pasar a depender de discos *SSD* se convirtió en una necesidad que mejoraba el rendimiento de forma sencilla, y su coste dejó de considerarse caro. También se pueden utilizar unidades `Fusion IO`_, que proveen 25 veces la cantidad de *IOPS* de un *SSD* medio, pero todavía es bastante cara.

Un servicio muy pequeño, dedicado a mantener una copia de las páginas, necesitaba 32GB de RAM, de las que 2 eran para el sistema operativo, indexando en 10Gb, 10 millones de canciones. Por lo que un crecimiento de 20 millones de canciones debería ser soportable. El problema es que mantener los índices en memoria causaba, por el uso de las caches, que realmente ocupara 3 GB más, con lo que los 30 millones de canciones, no ocupaban 30GB sinó 39GB. La solución pasó por modificar el servicio para que utilizara la llamada ``posix_fadvise`` para evitar utilizar caché. También se puede organizar un mejor despliegue del índice en memoria. Otra opción podría haber utilizado ``mlock`` para restringir este caso.

La gestión de reintentos en las conexiones también es algo delicado. Cuando un cliente en Spotify_ pierde su conexión, o se vuelve muy lenta, empieza a reintentar, lo que llevará a saturar los APs. Para evitar esto, lo reintentan menos veces y aplicando un ascenso exponencial en el tiempo de espera de cada uno de los reintentos. Con esto la capacidad de conexiones de los APs pueden ser recuperadas a tiempo para seguir atendiendo.

También es importante el concepto "fallar tan rápido como sea posible", de forma que si los APs pierden conectividad con los *backends*, se lo comuniquen al cliente tan rápido como sea posible, para que busque alternativas o se conecte a otros APs. Hay situaciones en las que puede ser interesante que el cliente pueda aceptar una degradación del servicio sin fallar del todo.

Una de las cosas que hacen es utilizar usuarios reales para testear, por ejemplo, enviando un porcentaje de usuarios a un porcentaje de servidores. Suelen actualizar los clientes en bloques en distintos intervalos, de modo que pueden ir analizando cómo funciona todo.

Aunque son muy aficionados, han decidido automatizar sólo cuando sea necesario. Sí que tienen toda la infraestructura disponible como servicio, de modo que los equipos que trabajan en las distintas plataformas pueden servirse ellos mismos cuando lo necesitan.

En relación al crecimiento, han tenido que delegar la responsabilidad de la disponibilidad a los que están implicados en la plataforma. Son estos los que se encuentran con los problemas y, cuando no pueden resolverlos,ce piden reciben ayuda y consejo de la experiencia de los técnicos de operaciones. El equipo de operaciones se centra en extender la plataforma

Finalmente, es muy importante recordar que los incidentes no deben ocurrir dos veces. Cuando ocurre una vez, se establece la severidad, se reúnen a todos los implicados y se aplican, con urgencia, las soluciones oportunas.

Django Best Practices
---------------------

`David Arcos`_ dió una interesante charla sobre las mejores prácticas al utilizar Django_, un *framework* web muy conocido para Python_. En términos generales, concretó los siguientes puntos:

* Seguir la filosofía de Python_ y Django_ tanto como sea posible.
* No reinventar la rueda, permanecer sobre la espalda de los gigantes.
* Utilizar virtualenv_, con virtualenvwrapper_, para crear un entorno para cada proyecto, con todas sus diferentes dependencias, versiones distintas de las librerías, etc. Para instalar algo, utilizar ``pip``, que permite salvar las dependencias con sus versiones en un fichero, que se incluye con el resto del código, y utilizarlo para repetir la instalación en otro equipo.
* Aclarar la nomenclatura proyecto/aplicaciones de Django. Utilizar nombres cortos, de una sola palabra, obvios para las aplicaciones. Es mejor que éstas sean pequeñas y muchas, antes que pocas y grandes. Si lo que hace la aplicación necesita una frase, probablemente se puede hacer con más de una aplicación. No reinventar la rueda, utilizar aplicaciones contribuidas o de terceros.
* Varios ficheros de *settings*, según el entorno. Todos los ficheros heredan de uno que es base. Incluirlos en el control de versiones.
* Modelo *MTV* (*Model* - *Template* - *View*). Es el modelo de Django_ y conviene conocerlo y respetarlo. Los modelos contienen la lógica, las vistas deben ser simples y las plantillas mucho más simples. Un buen ejemplo, es el modelo de usuarios que incluyen en contribuidos. Utilizar Jinja2_ en las plantillas, pero en casos muy concretos. Es mejor tener plantillas mantenibles que HTML bonito.

Para el despliegue, comentó los siguientes puntos:

* Nginx_, gunicorn_ y supervisord_, para mantener vivo al segundo, es una buena combinación para ejecutarlo. Para los estáticos recomienda utilizar Nginx_ o, en casos muy extremos, una *CDN*.
* Fabric_, que permite programar tareas automatizadas que interactúan con los servidores por *SSH*.
* South_, exclusiva para Django_, se integra con el modelo y permite crear los ficheros de migración automáticamente, que luego se pueden modificar.
* Celery_ consiste en un sistema de tareas asíncronas y encolado de trabajos basado en mensajes distribuidos. Necesita una cola de mensajes. Recomienda utilizar Redis_ antes que RabbitMQ_.
* Redis_, para almacenar sesiones activas, cache en general, compatible con memcached_. Ideal para cálculos en real-time, estadísticas, monitoring, throttling, mensajes, índices y filtros.
* Sentry_, donde poder llevar el registro de eventos, agregándolos. Permite monitorizar errores, obtener toda la información para el post-mortem. Usa el ``logger`` de Python_, es muy fácil de usar. Se puede desplegar en instancia o utilizarlo como servicio_.

Para la depuración:

* IPython_, intérprete integrado en ``manage.py shell``.
* ipdb_, para tracear.
* `Django Debug Toolbar`_, muy potente, para optimizar rendimiento de la base de datos vista a vista.

Unit testing y el mito de los 0 bugs
------------------------------------

`Fernando Escolar`_ explicó que testear es comparar la salida de un proceso ante una entrada, con la salida que se esperaba. Si coinciden, el test es correcto y devolverá un OK. Pero si no coinciden, el test deberá devolver un error.

Se presentó la siguiente clasificación:

* *Whitebox*: Se conoce todo el código.
* *Blackbox*: No se conoce nada del código.
* *Visual testing*: Cuando se presenta la información del test de forma clara y visualmente identificable.
* *Greybox*: Se conoce parte del código.

Se pueden identificar los siguientes niveles de test:

* Unitario: Se prueba una sola parte pequeña de la pieza. Se prueba un método o una función.
* Integración: Se prueban todas las piezas juntas.
* Sistema: Se prueba que todo el conjunto funciona.
* Aceptación: Se prueba que cumple todo lo que se esperaba.

Las siguientes características deben encontrarse en todas las pruebas:

* *Fast*: Debe ser rápido sin crear esperas.
* *Isolated*: No puede depender de otros componentes.
* *Repeatable*: Debe ser repetible, en las mismas condiciones deberá dar el mismo resultado, hasta que se cambie el código.
* *Self-Validating*: Debe ser suficientemente simple para que sea correcto.
* *Timely*: Debe ser usado en el momento adecuado.

Fernando_ además, añadió las siguientes:

* Profesional
* Unitario
* Automatizable
* No usar recursos

Estructura de cada uno de los tests:

* *Assume*: Cosas que asumimos, contratos, especificación. Es opcional, según el caso.
* *Arrange*: Preparar el contexto, crear los objectos necesarioes, etc.
* *Act*: Interactuar con el método o función a testear.
* *Assert*: Confirmar el resultado, o los resultados.

Para hacer código testeable, recomendó:

* Desacoplar y sustituir componentes por interfaces para todo.
* Patrones: *Inversion of Control* y *Abstract Factory*.
* *Test doubles*: *Dummies*, *Fakes*, *Stubs*, *Spies* y *Mock*. Consisten en distintas técnicas para suplantar servicios que son necesarios para el test, pero no lo que se está testeando.
* Evitar el uso de estáticos (*hard coded values*) y *singletons*.
* Simplificar los constructores: No utilizar ``new`` dentro del constructor, no asignar algo que no sean atributos, no usar *Initializer*, condicionales ni bucles.
* Testear positivo y negativo.

Y sobre las métricas de codigo, comentó las dos más importantes:

* Cyclomatic Complexity: Es el número de caminos diferentes que el algoritmo puede tomar.
* Code Coverage: La proporción de líneas de código que, en algún momento, se comprueban en tests unitarios.

.. _Fabric: http://fabfile.org
.. _South: http://southaeracode.org
.. _Celery: http://www.celeryproject.org
.. _RabbitMQ: http://www.rabbitmq.com
.. _Redis: http://redis.io
.. _Sentry: http://sentry.readthedocs.org/en/latest/quickstart/
.. _servicio: http://getsentry.com
.. _Nginx: http://nginx.org
.. _gunicorn: http://gunicorn.org
.. _supervisord: http://supervisord.org
.. _virtualenv: http://www.virtualenv.org
.. _virtualenvwrapper: http://virtualenvwrapper.readthedocs.org/en/latest/
.. _`Agile Station`: http://bcndevcon.org/activities/agile-station/
.. _`Agile BCN`: http://barcelona.agile-spain.org/
.. _BcnDevCon: http://bcndevcon.org
.. _`Hackathon for education`: http://bcndevcon.org/hackathon/
.. _RetroBarcelona: http://bcndevcon.org/retrobarcelona/
.. _`David Poblador`: https://twitter.com/davidpoblador
.. _Spotify: http://www.spotify.com
.. _`Fusion IO`: http://www.fusionio.com
.. _`David Arcos`: https://twitter.com/DZPM
.. _Django: http://djangoproject.com
.. _Python: http://python.org
.. _JSON: http://es.wikipedia.org/wiki/JSON
.. _`Fernando Escolar`: https://twitter.com/fernandoescolar
.. _Fernando: `Fernando Escolar`_
.. _TDD: http://es.wikipedia.org/wiki/Desarrollo_guiado_por_pruebas
.. _IPython: http://ipython.org
.. _ipdb: https://pypi.python.org/pypi/ipdb
.. _`Django Debug Toolbar`: https://pypi.python.org/pypi/django-debug-toolbar
.. _Jinja2: http://jinja.pocoo.org/docs/
.. _memcached: http://memcached.org/
