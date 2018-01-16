---
title: "Laboratorio de sslh: Un puerto para dominarlos a todos"
slug: "laboratorio-sslh"
date: 2014-08-27T19:55:00
tags: ["Laboratorio", "sslh"]
author: "David Acacio"
---

En muchas redes corporativas me estoy encontrado que una manera que tienen los administradores de controlar la actividad de sus usuarios es bloquear el acceso de los clientes a ciertos puertos mediante reglas de firewall (por ejemplo denegar toda conexión al puerto 22 o solo permitir conexiones al puerto 80 o 443). Medida para nada afectiva, ya que no garantiza que el usuario no se conecte al servicio no deseado, sino que no se conecte al puerto por defecto de dicho servicio. Para saltarse esta restricción es tan sencillo como configurar el servicio en uno de los puertos permitidos.

Si bien es cierto que puede ser bastante molesto, ya que obliga a modificar configuraciones, puede suponer un problema si ya tenemos un servicio activo en el puerto requerido. Esto me motivó a buscar la manera de, a través de un único puerto de un servidor, se pudiera acceder a diversos servicios.

<!--more-->

Después de unas búsquedas localicé diversas opciones, pero casi todas ellas
implicaban complejas configuraciones de iptables, cosa poco práctica.
Finalmente encontré la respuesta a todas mis oraciones:
[sslh](https://github.com/yrutschle/sslh).

sslh es un programa desarrollado en [C](http://es.wikipedia.org/wiki/C_(lenguaje_de_programaci%C3%B3n)) por [Yves
Rütschlé](http://www.rutschle.net/). La manera de funcionar es "simple": se queda escuchando en un puerto y cuando recibe una conexión va probando los diversos servicios que tiene configurados hasta dar con el adecuado. Actualmente soporta de manera nativa los siguientes: ssh, openvpn, tinc, xmpp, http, ssl y tls. También es posible especificar otros protocolos en el fichero de configuración mediante expresiones regulares.


Podéis localizar la última versión del programa en [el repositorio de
Github](https://github.com/yrutschle/sslh).

A continuación os vamos a detallar, paso a paso, como realizar la instalación
de esta herramienta. En el ejemplo hemos utilizado una
[CentOS](https://www.centos.org) 6.5.

Primero instalaremos las dependencias de librerías y el compilador gcc:

```bash
yum install -y libconfig libconfig-devel gcc git
```

Bajamos la última versión del código fuente de github (p.e. en la carpeta opt):

```bash
mkdir /opt/sslh
cd /opt/sslh
git init
git pull https://github.com/yrutschle/sslh
```

Y realizamos la compilación:

```bash
make install
```

Ahora copiaremos el script de arranque al init.d para poder realizar un arranque automático del servicio en runlevel 3:

```bash
cp scripts/etc.rc.d.init.d.sslh.centos /etc/rc.d/init.d/sslh
ln -s /usr/local/sbin/sslh /usr/sbin/sslh-select
chkconfig --add sslh
chkconfig --level 3 sslh on
```

Y por último pondremos el fichero de configuración:

```bash
cp basic.cfg /etc/sslh.cfg
```

Dentro de dicho fichero modificaremos los parámetros que necesitemos, en este caso los siguientes:

* Sección listen: indicaremos una sola línea con la IP/HOST de nuestro interfaz de red y el puerto al cual queremos que el servicio esté escuchando:

```bash
listen:
(
    { host: "192.168.10.224"; port: "8081"; }
);
```

* Sección protocols: indicaremos una línea por cada servicio que queramos ofrecer y actualizaremos los campos host y port para cada uno de ellos, poniendo localhost si es un servicio local o la ip/hostname del servidor destino si es un servicio externo. En el caso que nos ocupa lo ofrecerá nuestro servidor, por tanto lo dejaremos tal cual lo muestra el ejemplo:

```bash
protocols:
(
    { name: "ssh"; service: "ssh"; host: "localhost"; port: "22"; probe: "builtin"; },
    { name: "openvpn"; host: "localhost"; port: "1194"; probe: "builtin"; },
    { name: "xmpp"; host: "localhost"; port: "5222"; probe: "builtin"; },
    { name: "http"; host: "localhost"; port: "80"; probe: "builtin"; },
    { name: "ssl"; host: "localhost"; port: "443"; probe: "builtin"; },
    { name: "anyprot"; host: "localhost"; port: "443"; probe: "builtin"; }
);
```

Tan solo queda arrancar el servicio:

```bash
/etc/init.d/sslh start
```

Para probar si el servicio funciona podemos realizar una conexión desde otra máquina a cualquiera de los servicios definidos al puerto 8081 (tal como hemos configurado). En nuestro ejemplo realizaremos una conexión ssh de prueba desde otra máquina:

```bash
ssh -p 8081 root@192.168.10.224
```

Y si habéis seguido todos los pasos correctamente os habréis podido conectar sin problemas.

**NOTA:** Verificad que no existe ningún servicio (p.e. iptables, etc...) que esté bloqueando el acceso.
