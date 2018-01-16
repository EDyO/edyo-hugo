---
title: "Laboratorio de pruebas"
slug: "laboratorio-pruebas"
date: 2014-07-02T03:14:00

tags: ["OpenStack", "Laboratorio"]
author: "Javier Arellano"
description: ""
---


Vamos a empezar una serie de artículos que en los que vamos a realizar instalaciones y pruebas, para poder empezar necesitaremos crear nuestro laboratorio, en este caso vamos a utilizar un ordenador físico, un pequeño servidor al cual le vamos a instalar un OpenStack_ siguiendo el sistema de Packstack_ de Redhat que permite instalar todos los componentes de OpenStack en una única máquina prácticamente sin dolor. 

<!--more-->


Todo lo iniciamos con una instalación fresca de una CentOS_ 6.5 a la que le actualizamos los paquetes:

.. code-block:: bash

	yum update glibc* python* yum* rpm*
	yum update -y
	
Y reiniciamos la maquina  para tener el sistema fresco con el último kernel.

.. code-block:: bash
	
	reboot

Una vez reiniciado instalamos el repositorio y los paquetes de dependencias de OpenStack. Es muy importante realizar la última actualización ya que las dependencias pueden haber variado y necesitar otros paquetes:

.. code-block:: bash

	yum install -y http://rdo.fedorapeople.org/rdo-release.rpm
	yum install -y openstack-packstack
	yum update -y 

Una vez actualizado todo, realizamos la instalación real:

.. code-block:: bash

	packstack --allinone --provision-demo=n --provision-all-in-one-ovs-bridge=n --os-heat-install=y --os-heat-cfn-install=y --os-neutron-install=y


Los parámetros que le pasamos nos aseguran utilizar el último servicio de redes (y no el obsoleto, seguramente esta opción no es necesaria, pero por si acaso). Y también la instalación del sistema HEAT_, que permite la automatización mediante el sistema HOT de plantillas. Una de las opciones más importantes es el parámetro *--provision-all-in-one-ovs-bridge=n* que le está indicando a la instalación que ya hay una `red externa`_. 

Y después de un largo rato tenemos el siguiente resultado:

.. code-block:: bash

	**** Installation completed successfully ******
	
	Additional information:
	 * A new answerfile was created in: /root/packstack-answers-20140528-194405.txt
	 * Time synchronization installation was skipped. Please note that unsynchronized time on server instances might be problem for some OpenStack components.
	 * Did not create a cinder volume group, one already existed
	 * File /root/keystonerc_admin has been created on OpenStack client host 192.168.0.120. To use the command line tools you need to source the file.
	 * To access the OpenStack Dashboard browse to http://192.168.0.120/dashboard .
	Please, find your login credentials stored in the keystonerc_admin in your home directory.
	 * To use Nagios, browse to http://192.168.0.120/nagios username : nagiosadmin, password : fbf**********608
	 * The installation log file is available at: /var/tmp/packstack/20140528-194405-KZHbZQ/Openstack-setup.log
	 * The generated manifests are available at: /var/tmp/packstack/20140528-194405-KZHbZQ/manifests
 
 
de forma que tenemos las credenciales en el fichero /root/keystonerc_admin, para poder utilizar esta credenciales hay que cargarlas:

.. code-block:: bash

	source /root/keystonerc_admin

en mi caso al tener una red externa se ha de realizar unos cambios en los ficheros, editar o crear el fichero */etc/sysconfig/network-scripts/ifcfg-br-ex* con el siguiente contenido adaptándolo a cada una de nuestras configuraciones:

.. code-block:: bash

	DEVICE=br-ex
	DEVICETYPE=ovs
	TYPE=OVSBridge
	BOOTPROTO=static
	IPADDR=192.168.122.212 # La IP de la máquina
	NETMASK=255.255.255.0  # La red
	GATEWAY=192.168.122.1  # La puerta de enlace
	DNS1=192.168.122.1     # El DNS de la red
	ONBOOT=yes

y cambiar el fichero */etc/sysconfig/network-scripts/ifcfg-eth0* por: 

.. code-block:: bash

	DEVICE=eth0
	HWADDR=42:42:42:42:42:EE  # aquí va la MAC de vuestra tarjeta
	TYPE=OVSPort
	DEVICETYPE=ovs
	OVS_BRIDGE=br-ex
	ONBOOT=yes

Muy importante eliminar la linea *BOOTPROTO*. Y en el fichero */etc/neutron/plugin.ini* se ha de modificar o añadir estas lineas, en el apartado donde el esta el ejemplo de estas directrices:

.. code-block:: bash

	network_vlan_ranges = physnet1
	bridge_mappings = physnet1:br-ex

Y una vez hecho se reincia el servicio de redes

.. code-block:: bash

	service network restart

Para evitar problemas también le cambio las directivas de *selinux* por permisive en el fichero */etc/selinux/config*:

.. code-block:: bash

	SELINUX=permissive 

Y instalar unas utilidades que nos van a ir bien y después reiniciaremos la máquina:

.. code-block:: bash

	yum install mlocate wget acpid git
	reboot



De esta forma ya tenemos un servidor de pruebas OpenStack. En siguientes artículos iremos desgranando OpenStack realizando pruebas con él. 

.. _OpenStack : https://www.openstack.org
.. _Packstack : http://openstack.redhat.com
.. _CentOS : http://www.centos.org
.. _`red externa` : http://openstack.redhat.com/Neutron_with_existing_external_network
.. _HEAT : http://openstack.redhat.com/DeployHeatOnHavana
