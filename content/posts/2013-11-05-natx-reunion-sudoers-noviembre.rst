---
title: "Reunión de Sudoers BCN de Noviembre"
author: "Ignasi Fosch"
slug: "reunion-sudoers-noviembre"
date: 2013-11-06T20:00:00

tags: ["Eventos", "Sudoers BCN", "Ansible"]
---

.. image:: /images/SudoersBCN.png
   :width: 180
   :height: 150
   :alt: sudo make me a sandwich
   :align: left

En la charla de este mes, `Javier Arturo Rodríguez`_ habló sobre Ansible_, otra herramienta para la gestión de configuración. Aunque bien podría compararse en funcionalidad con Puppet_ o Chef_, su diseño y las técnicas utilizadas la convierten en una herramienta muy sencilla, completa e interesante, incluso para sustituir a otras herramientas como Fabric_ o Capistrano_.

<!--more-->


Origen del nombre
-----------------

El término Ansible_ lo utilizó `Ursula K. Le Guin`_ en sus relatos de ciencia ficción, para referirse a un dispositivo de comunicación instantánea y superluminal, y otros autores, como `Orson Scott Card`_ en `Ender's Game`_, lo reaprovecharon. De todos modos, también es el término utilizado para referirse al director de una orquesta. No en vano, Ansible_ funciona desde un nodo central que suele ser la consola del administrador.

El proyecto
-----------

El proyecto es iniciado por `Michael DeHaan`_, actual CTO de la empresa que da soporte. Tiene un diseño basado en KISS_, utiliza SSH_ para conectarse a los clientes, que únicamente necesitan disponer de la versión 2.6 de ``python``. Al utilizar el protocolo SSH_, aprovecha su puerto de conexión y su infraestructura, como la de autenticación, para funcionar. Hay que destacar que para las tareas que requieran privilegios, puede utilizar ``sudo``, pero no es capaz de funcionar con contraseña.

Aunque se trata de *software open source*, existe un modelo de negocio comercial, al que da soporte la empresa AnsibleWorks_, que incluye ciertos componentes de pago.

Instalación
-----------

Instalación se puede realizar de diferentes formas:

* Con paquetes nativos, existen incluso para BSD_.
* Se puede instalar usando ``pip``, como tantos otros módulos de Python_.
* Tambié se puede instalar compilándolo desde el código fuente, que es descargable en un paquete o utilizando GitHub_.

Es conveniente tener los siguientes elementos bien configurados:

* Tener claves SSH_ adecuadas.
* Utilizar ``ssh-agent`` en la estación de trabajo, asociando dichas claves.
* Comprovar el fichero ``~/.ssh/config``, de modo que los accesos que requieran utilizar puertos alternativos estén bien configurados.

Configuración
-------------

La configuración es tan sencilla como disponer de uno o más ficheros de inventario. Estos ficheros tienen un formato muy sencillo: En cada línea se escribirá el nombre de un nodo a gestionar. En caso de que dicho nodo requiera el uso de un puerto distinto al habitual, convendrá indicarlo añadiéndolo al nombre del servidor con un ``:`` delante. En los nombres de los equipos se pueden utilizar ciertas expresiones para indicar, por ejemplo, rangos numéricos, indicando así una serie más grande de nodos en una sola línea.

Además, como si de un fichero INI_ se tratara, se pueden espeficar secciones, encabezadas con un nombre entre corchetes (``[]``) que corresponderán en grupos de servidores. En caso que sea necesario, se puede incluir otra sección para un grupo ya existente que contenga variables específicas para esos grupos.

Pueden disponerse de distintos ficheros, pero sólo uno se puede utilizar al mismo tiempo, debiendo indicar a Ansible_ cuál se desea utilizar con el atributo ``-i``.

Módulos
-------

Los módulos son los que le dan funcionalidad a Ansible_. Estos módulos consisten en código que Ansible_ envía al nodo remoto y lo ejecuta, esperando que devuelva una estructura JSON_ con un conjunto de datos que variarán según el módulo. En cualquier caso, el JSON_ deberá contener un atributo llamado ``changed``, consistente en un valor booleano que indicarà si la ejecución cambió algo o no. La ejecución de un módulo siempre debe ser idempotente, por lo que, si no es necesario, no debería realizar ningún cambio. Existe un comando ``ansible-doc`` que ofrece documentación en consola sobre los módulos y sus opciones.

En los siguientes comandos, se ejecuta el módulo setup en todos los servidores, en uno sólo llamado ``courseware`` o en todos los pertecientes a un grupo llamado ``webservers``: ::

    ansible -vvvv -i production all -m setup
    ansible -vvvv -i production courseware -m setup
    ansible -vvvv -i production webservers -m setup

Hay muchos módulos, algunos muy interesantes, permiten, por ejemplo, acceder a la información que el facter_, de Puppet_, o el ohai_, de Chef_, pueden recopilar del nodo. Esta información se podrá utilizar en la configuración del mismo.

*Playbooks*
-----------

Para evitar la ejecución consecutiva de órdenes, Ansible_ permite crear lo que denomina *Playbooks*. En ellos, se definen qué módulos se aplican y cómo. Pueden contemplarse como una descripción del estado deseado del nodo en cuestión. Esta definición se escribe en una variante de YAML_, conteniendo cuatro secciones específicas:

* ``vars`` donde, si es necesario se crearán las variables necesarias para la ejecución del *playbook*.
* ``hosts`` donde se indicará a qué nodo, o nodos, se debe aplicar.
* ``tasks`` que detallan los módulos con sus respectivas opciones.
* ``handlers`` que, si es necesario, indicarán gestores para ciertas situaciones.

Los *playbooks* se organizan en directorios donde se pueden encontrar también:

* ficheros individuales, que serán copiados tal cuál están al servidor configurado.
* plantillas, escritas en Jinja2_, para generar ficheros cuyo contenido puede variar según ciertos parámetros.
* definiciones de roles, que son otro tipo de agrupaciones de servidores que permiten incluir variables, nodos, tareas, gestores y plantillas específicas.

Los *playbooks*, aunque utilicen YAML_, pueden permitir cierto nivel de control de flujo o seleccciones interesantes. Por ejemplo, se puede aplicar un módulo sobre una lista de elementos sobre la que iterar, los cuales pueden modificar variables o parámetros. La aplicación de un *playbook* específico sobre un único servidor se hará con el comando ``ansible-play -l <nodo> <playbook>``.

Modos
-----

Uno de las principales desventajas que tiene Ansible_ por su diseño es la cantidad de nodos que se pueden gestionar simultáneamente. Especialmente, debido al coste de las sesiones SSH_. Por ello se creó, inicialmente, lo que se denominó modo *Fireball*. Este modo consistía en arrancar un servidor persistente en el cliente que, mediante el uso de una instancia local de 0mq_ y claves propias, iba recibiendo las instrucciones y las iba ejecutando. De todos modos, esto quedó obsoleto y se sustituyó por el modo *Accelerated* que hace algo similar, pero por SSH_ de nuevo y sin 0mq_. También se dispone de un modo llamado *Local* que es el utilizado para configurar con Ansible el mismo nodo en el que se encuentra.

Otra de las desventajas que se pueden producir es el acceso a nodos en ubicaciones con latencias muy altas, o con conectividad muy inestable. Para ello se suele utilizar un `nodo bastión`_, como si de un proxy_ se tratara.

Versión comercial
-----------------

La versión comercial incluye, a parte de las opciones de soporte correspondientes, dos módulos especiales:

* *AWX* que es un interfaz web de gestión que permite ciertos niveles de configuración más fácilmente, como el concepto de organizaciones o proyectos.
* El modo *Callback* que consiste en permitir el envío asíncrono de configuraciones.

Más información
---------------

Durante y posteriormente a la charla, se comentaron ciertas utilidades relacionadas con Ansible_:

* En Rackspace_ utilizan Ansible_ para `gestionar varios miles de servidores de un modo distinto`_.
* Existe una herramienta_ para trabajar con Ansible_ de forma interactiva.

Con mucha probabilidad existan muchas más herramientas.

.. _`Javier Arturo Rodríguez`: https://twitter.com/codehead
.. _Ansible: http://www.ansibleworks.com/
.. _Puppet: http://puppetlabs.com/
.. _Chef: http://www.opscode.com/chef/
.. _Fabric: http://docs.fabfile.org/en/1.8/
.. _Capistrano: http://www.capistranorb.com/
.. _`Ursula K. Le Guin`: http://es.wikipedia.org/wiki/Ursula_K._Le_Guin
.. _`Orson Scott Card`: http://es.wikipedia.org/wiki/Orson_Scott_Card
.. _`Ender's game`: http://es.wikipedia.org/wiki/El_juego_de_Ender
.. _`Michael DeHaan`: http://michaeldehaan.net/
.. _KISS: http://es.wikipedia.org/wiki/Principio_KISS
.. _SSH: http://openssh.org/es/
.. _AnsibleWorks: Ansible_
.. _BSD: http://bsd.org
.. _Python: http://python.org
.. _Github: http://github.com/
.. _INI: http://es.wikipedia.org/wiki/INI_(extensi%C3%B3n_de_archivo)
.. _JSON: http://es.wikipedia.org/wiki/JSON
.. _facter: http://puppetlabs.com/facter
.. _ohai: http://docs.opscode.com/ohai.html
.. _YAML: http://es.wikipedia.org/wiki/YAML
.. _Jinja2: http://jinja.pocoo.org/docs/
.. _0mq: http://zeromq.org/
.. _`nodo bastión`: http://es.wikipedia.org/wiki/Bastion_host
.. _proxy: http://es.wikipedia.org/wiki/Proxy
.. _Rackspace: http://www.rackspace.com/es/
.. _`gestionar varios miles de servidores de un modo distinto`: http://www.slideshare.net/JesseKeating/ansiblefest-rax
.. _herramienta: https://github.com/dominis/ansible-shell
