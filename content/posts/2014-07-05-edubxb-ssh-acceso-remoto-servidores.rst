---
title: "SSH: Acceso remoto a servidores"
author: "Eduardo Bellido Bellido"
slug: "ssh-acceso-remoto-servidores"
date: 2014-07-05T10:00:00

tags: ["SSH", "Guías", "Herramientas"]
---

Este artículo es el primero de una serie dedicada al protocolo `SSH o Secure Shell`_, un protocolo de acceso remoto a servidores altamente extendido en sistemas UN*X como GNU/Linux o FreeBSD. En los artículos trataremos de explicar el uso básico de este protocolo e iremos profundizando más en las capacidades avanzadas disponibles.

<!--more-->


Existen muchas implementaciones de clientes SSH, como `PuTTY`_ (utilizado principalmente en entornos Windows), `KiTTY`_ (un *fork* del anterior) ambos *Software Libre*, también existen herramientas comerciales como `SecureCRT`_, pero para estos artículos nos centraremos en `OpenSSH`_, el cliente libre por excelencia para sistemas UN*X.

Conectando
==========

Empecemos por el principio, y para el caso, nos conectaremos a un servidor, para hacerlo, usaremos el comando:

.. code:: text

    $ ssh example.com

en el caso que queramos conectar con un usuario distinto al local del equipo en el que nos encontremos, tenemos dos alternativas, mediante el *flag* ``-l``:

.. code:: text

    $ ssh -l usuario example.com

o usando la notación *usuario@servidor*:

.. code:: text

    $ ssh usuario@example.com

el uso de una u otra forma es indiferente.

Si es la primera vez que conectamos al servidor, SSH nos mostrará un mensaje como el siguiente:

.. code:: text

    The authenticity of host '192.168.1.151 (192.168.1.151)' can't be established.
    ECDSA key fingerprint is aa:ef:f9:b9:54:bb:d1:a0:f0:08:4e:a7:b2:68:71:bd.
    Are you sure you want to continue connecting (yes/no)?

advirtiéndonos que no podremos conectar hasta que aceptemos la clave de identificación del servidor, posteriormente esto ya no será necesario.

Usando claves de autenticación
==============================

Yendo un paso más allá en lo que a autenticación se refiere, el protocolo SSH nos brinda la posibilidad de utilizar un juego de claves de autenticación, que mediante un algoritmo de `cifrado asimétrico`_ (dispondremos de una clave privada y de otra pública) podremos autenticarnos de forma fácil y segura, siempre y cuando hayamos habilitado la clave pública en cada una de las máquinas a las que queramos acceder.

Generación de las claves
------------------------

Para generar las claves, el comando a utilizar es ``ssh-keygen`` de la siguiente forma:

.. code:: text

    $ ssh-keygen -t rsa -b 2048 -f .ssh/mi_clave -C "Mi clave SSH"
    Generating public/private rsa key pair.
    Enter passphrase (empty for no passphrase): 
    Enter same passphrase again: 
    Your identification has been saved in mi_clave.
    Your public key has been saved in mi_clave.pub.
    The key fingerprint is:
    d2:d1:8c:eb:22:75:b7:2f:12:07:e9:e1:6b:79:d8:35 Mi clave SSH
    The key's randomart image is:
    +--[ RSA 2048]----+
    |                 |
    |         +       |
    |        o.o      |
    |       .+o       |
    |      ooSo.      |
    |     . ++...E    |
    |    . . .B.. .   |
    |     . .* +.     |
    |       . o ..    |
    +-----------------+

Algunos *flags* son opcionales, como por ejemplo el ``-t`` para indicar el tipo de clave que queremos generar, en este caso hemos elegido RSA_, el ``-b`` para indicar de cuantos bits queremos que sea la clave (en la actualidad el mínimo recomendado para claves RSA es 2048), el *flag* ``-f`` nos permite indicar la ruta destino de las claves y su nombre, que por defecto es ``~/.ssh/id_rsa`` para el tipo RSA (la clave pública tendrá el mismo nombre pero con la extensión *.pub*), y nos queda el *flag* ``-C`` que nos permite añadir un comentario a la clave, que puede sernos útil para identificarla más fácilmente.

En este caso, la clave privada ha sido generada sin contraseña (hemos pulsado la tecla ``intro`` sin introducir ninguna), esto, en cierto modo, puede ser "arriesgado", ya que si por algún motivo alguien se hace con nuestra clave, podrá acceder sin restricciones a todos los servidores en los que hayamos habilitado dicha clave. Es por esto que una buena práctica es **proteger siempre nuestras claves con contraseña**, la cual será solicitada cada vez que accedamos a un servidor al que podamos acceder con clave. Esto también nos permite tener una única contraseña, la de nuestra clave, y no tener que recordar cada una de las claves de los usuarios remotos, en el caso que sean distintas.

Transferencia de las claves a máquinas remotas
----------------------------------------------

Una vez tengamos las claves generadas para poder utilizaras en la autenticación es necesario añadir la clave pública en el servidor remoto, para hacerlo, un procedimiento podría ser el siguiente:

.. code:: text

    $ ssh -l usuario servidor

Ahora, ya dentro del servidor:

.. code:: text

    $ mkdir .ssh
    $ cat >> .ssh/authorized_keys

ahora debemos copiar el contenido del fichero que contiene la clave pública (``~/.ssh/mi_clave.pub``) y pegar el contenido en el terminal, luego, pulsar la combinación de teclas ``Control+D`` para guardar el fichero. Por último, estableceremos los permisos adecuados para aumentar el nivel de seguridad:

.. code:: text

    $ chmod 0700 .ssh
    $ chmod 0600 .ssh/authorized_keys

Un detalle a tener en cuenta es que si el directorio ``.ssh`` tiene unos permisos distintos a los anteriores, el servidor SSH no utilizará nuestras claves y nos solicitará nuestra contraseña hasta que lo hayamos corregido.

Estos pasos pueden ser un tanto "tediosos" de realizar, sobretodo si es necesario crear el directorio y el fichero con las claves autorizadas, y más aún si queremos hacerlo en un número considerable de servidores, por eso, dentro del paquete de herramientas que vienen con el ciente OpenSSH tenemos uno que nos simplificará enormemente esta tarea, el comando ``ssh-copy-id``:

.. code:: text
   
   $ ssh-copy-id -i .ssh/mi_clave.pub 192.168.1.151
   /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
   /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
   user@192.168.1.151's password: 

   Number of key(s) added: 1

   Now try logging into the machine, with:   "ssh '192.168.1.151'"
   and check to make sure that only the key(s) you wanted were added.

la ventaja de este método es que además de ser más rápido, dejará el directorio y el fichero creados con los permisos adecuados.

En el caso que dispongamos de varias claves y no indiquemos una explícitamente con el *flag* ``-i``, todas nuestras claves serán transferidas.

Simplificando la gestión de claves
----------------------------------

Dado que es una buena práctica proteger nuestra clave privada con una contraseña, el hecho de tener que introducirla cada vez que abrimos una sesión SSH no dista mucho de entrar directamente utilizando la contraseña de nuestra cuenta de usuario del servidor al que vayamos a acceder. Comprobémoslo:

.. code:: text

    $ ssh example.com -i .ssh/mi_clave
    Enter passphrase for key '.ssh/mi_clave':

Como no, esto también está solucionado, entrando ahora en juego el *ssh-agent*, que es un demonio que podemos ejecutar en cualquier momento con nuestro usuario (no se trata de un demonio de sistema), y que se encargará de "cachear" nuestras claves privadas para poder usarlas directamente sin necesidad de ir desbloqueándolas mediante contraseña, únicamente cuando hayamos instanciado el demonio y añadido la claves necesitaremos introducir las contraseñas para desbloquearlas, de modo que no será necesario hacerlo cada vez que hagamos una conexión a un servidor.

Procedamos a usar el *ssh-agent*, primero, lo arrancamos:

.. code:: text

    $ ssh-agent
    SSH_AUTH_SOCK=/tmp/ssh-mj8Jg9EEtxCH/agent.9843; export SSH_AUTH_SOCK;
    SSH_AGENT_PID=9844; export SSH_AGENT_PID

añadimos nuestra clave:

.. code:: text

    $ ssh-add .ssh/mi_clave
    Enter passphrase for .ssh/mi_clave:
    Identity added: .ssh/mi_clave (.ssh/mi_clave)
    
opcionalmente podemos comprobar que la clave está añadida correctamente:

.. code:: text

    $ ssh-add -l
    d2:d1:8c:eb:22:75:b7:2f:12:07:e9:e1:6b:79:d8:35 .ssh/mi_clave (RSA)

realizado todo esto, ya podremos acceder fácilmente sin contraseñas a los servidores que queramos.

Cabe comentar que, tanto Mac OS X en la aplicación `Keychain`_, como por ejemplo con el entorno de escritorio GNOME en la aplicación `Contraseñas y claves`_, existe soporte de *ssh-agent*, simplificándonos la gestión de nuestras claves mediante interfaz gráfica, con lo que no necesitaremos del demonio que tiene con el cliente OpenSSH.

Conclusión
==========

Con esto finalizamos esta entrega. Para los que quieran ir un paso por delante y no puedan esperar al siguiente artículo, siempre pueden acudir a la `documentación oficial de OpenSSH`_ o mirar las *man pages* correspondientes.


.. _`SSH o Secure Shell`: https://es.wikipedia.org/wiki/Secure_Shell
.. _OpenSSH: http://www.openssh.com/
.. _PuTTY: http://www.chiark.greenend.org.uk/~sgtatham/putty/
.. _KiTTY: http://www.9bis.net/kitty/
.. _SecureCRT: http://www.vandyke.com/products/securecrt/
.. _SSH: https://es.wikipedia.org/wiki/Secure_Shell
.. _`cifrado asimétrico`: https://es.wikipedia.org/wiki/Criptograf%C3%ADa_asim%C3%A9tric
.. _`documentación oficial de OpenSSH`: http://www.openssh.com/manual.html
.. _RSA: https://es.wikipedia.org/wiki/RSA
.. _Keychain: https://en.wikipedia.org/wiki/Keychain_(Mac_OS)
.. _`Contraseñas y claves`: https://help.gnome.org/users/seahorse/stable/
