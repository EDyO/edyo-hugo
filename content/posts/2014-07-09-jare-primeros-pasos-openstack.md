---
title: "Primeros pasos con OpenStack"
slug: "primeros-pasos-openstack"
date: 2014-07-09T04:14:00
tags: ["OpenStack", "Laboratorio"]
author: "Javier Arellano"
---

Continuando con nuestro pequeño laboratorio OpenStack necesitamos crear las nuevas redes.

<!--more-->

```bash
source /root/keystonerc_demo
neutron router-create router
neutron net-create private
neutron subnet-create private 10.0.0.0/24 --name private_subnet
neutron router-interface-add router private_subnet
neutron net-create public --router:external=True
neutron subnet-create public 192.168.0.0/24 --name public_subnet --enable_dhcp=False --allocation-pool start=192.168.0.129,end=192.168.0.254 --gateway=192.168.0.1
neutron router-gateway-set router public
```

Una vez ya tenemos redes, una externa (192.168.0.0/24) que pertenece a nuestra red exterior y una interna (10.0.0.0/24) para uso de las instancias de OpenStack. Una vez creadas las redes añadimos los permisos del SSH y del ping a la configuración de seguridad. Los *security groups* son firewalls que actúan sobre el objeto al que hagamos referencia, es decir, tanto se puede aplicar a un puerto como a una máquina.

```bash
source /root/keystonerc_demo
neutron security-group-rule-create --protocol icmp --direction ingress default
neutron security-group-rule-create --protocol tcp --port-range-min 22 --port-range-max 22 --direction ingress default
```

El comando *source* no es necesario si ya se ha ejecutado en la misma sesión. ya que se trata de variables de entorno.

También necesitamos crear las imágenes, las imágenes son los modelos en los que se van a copiar creando instancias del modelo base. En mi caso en vez de crear nuevas imágenes me bajo 2 creadas:

```bash
wget http://download.cirros-cloud.net/0.3.2~pre2/cirros-0.3.2~pre2-x86_64-disk.img
glance image-create --name CirrOS --disk-format qcow2 --container-format bare --is-public true < cirros-0.3.2*

wget http://repos.fedorapeople.org/repos/openstack/guest-images/centos-6.5-20140117.0.x86_64.qcow2
glance image-create --name "CentOS 6.5" --disk-format qcow2 --container-format bare --is-public true < centos-6.5*
```

CirrOS es un minisistema creado para realizar test en sistemas cloud, como OpenStack. CentOS es un sistema similar a RedHat y va a ser el sistema base que voy ha utilizar de momento. 

Y ya estamos preparados para realizar la primera prueba con los comandos. El primero llama al fichero *lab1.yaml* que se trata del listado abajo.

```bash
SUBNET_UUID_PRIVATE=`neutron subnet-list| grep private| awk '{print $2 }'`
NET_UUID_PRIVATE=`neutron net-list| grep private| awk '{print $2 }'`
SUBNET_UUID_PUBLIC=`neutron subnet-list| grep public| awk '{print $2 }'`
NET_UUID_PUBLIC=`neutron net-list| grep public| awk '{print $2 }'`

heat stack-create lab1 --template-file=lab1.yaml --parameters="image=CentOS 6.5;flavor=m1.small;key_name=cloud;public_net_id=$NET_UUID_PUBLIC;private_net_id=$NET_UUID_PRIVATE;private_subnet_id=$SUBNET_UUID_PRIVATE"
```

```yaml
heat_template_version: 2013-05-23

description: >
  HOT template to deploy my first server

parameters:
  key_name:
    type: string
    description: Name of keypair to assign to servers
  image:
    type: string
    description: Name of image to use for servers
  flavor:
    type: string
    description: Flavor to use for servers
  public_net_id:
    type: string
    description: >
      ID of public network for which floating IP addresses will be allocated
  private_net_id:
    type: string
    description: ID of private network into which servers get deployed
  private_subnet_id:
    type: string
    description: ID of private sub network into which servers get deployed

resources:
  server1:
    type: OS::Nova::Server
    properties:
      name: Server1
      image: { get_param: image }
      flavor: { get_param: flavor }
      key_name: { get_param: key_name }
      networks:
        - port: { get_resource: server1_port }

  server1_port:
    type: OS::Neutron::Port
    properties:
      network_id: { get_param: private_net_id }
      security_groups: [grupo_seguridad]
      fixed_ips:
        - subnet_id: { get_param: private_subnet_id }

  server1_floating_ip:
    type: OS::Neutron::FloatingIP
    properties:
      floating_network_id: { get_param: public_net_id }
      port_id: { get_resource: server1_port }

outputs:
  server1_private_ip:
    description: IP address of server1 in private network
    value: { get_attr: [ server1, first_address ] }
  server1_public_ip:
    description: Floating IP address of server1 in public network
    value: { get_attr: [ server1_floating_ip, floating_ip_address ] }
```

Una vez ejecutado el script veremos el progreso de la creación del stack mediante el comando:

```bash
heat stack-list
```
