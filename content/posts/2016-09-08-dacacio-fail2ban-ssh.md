---
title: "Usando Fail2Ban para securizar SSH"
author: "David Acacio Albareda"
slug: "fail2ban-ssh"
date: 2016-09-08T15:30:00

tags: ["Fail2Ban", "SSH"]
---

<img src='/images/796bbae0-6fd7-11e6-91dc-feb4e6aa9afa.jpg' alt='Fail2Ban' class='align-left' height='80' width='200'/>

Hace poco realizando tareas de mantenimiento en mi servidor personal vi varios mensajes en los logs que no me gustaron nada: *Failed password for root from 121.18.238.22 port 40618 ssh2*.

Claramente mi servidor estaba bajo un ataque para conseguir acceso SSH.

<!--more-->

# Introducción

En principio fue algo que no me preocupó, por lo que vi en los mensajes estaban intentando acceder con el usuario root y tenía el login deshabilitado, por tanto todo intento sería en vano. Pero igualmente es algo que no se tenía que tomar a la ligera, e igual que tenía ese servicio bajo ataque podría suceder con cualquier otro, sin olvidar que depende del origen del ataque podrían llegar a saturar el SSH y perder la gestión de mi máquina.

Para "protegerme" de esta situación me planteé dos opciones: 

1. Acudir a mi proveedor de servicios y contratar algún sistema de [IDS](https://es.wikipedia.org/wiki/Sistema_de_detecci%C3%B3n_de_intrusos) con el coste que ello supone.
2. Montarme alguna solución en el propio servidor para controlar estas situaciones.

Ya que se trataba de mi servidor personal, y no contiene ninguna información o servicio que considere crítico, me decanté por esta segunda opción, pero mi recomendación para entornos productivos es que os vayáis a la primera y siempre podéis complementarla con alguna otra solución.

Básicamente lo que quería era bloquear el tráfico de ciertas IPs a ciertos servicios y puertos. Esto lo podría hacer activando el firewall en el servidor, pero el problema es que este tipo de ataques no siempre provienen del mismo origen. Normalmente se suele utilizar diversos orígenes para evitar ser bloqueados, por tanto, necesitaba algún tipo de producto que, sin realizar análisis del tráfico que podría realizar un IDS, me permitiera ir bloqueando dinámicamente los accesos. La solución: [Fail2Ban].

[Fail2Ban] es un software open source programado en [Python](https://www.python.org/) que escanea ficheros de log y detecta patrones que pueden ser identificados como "malvados" (p.e. intentos consecutivos de login como usuario root por ssh ;-) ) y bloquea las IPs mediante el firewall interno del servidor. También lo podemos configurar para realizar alguna otra acción como, por ejemplo, enviar un email. De base ya viene preconfigurado para soportar varios servidores (apache, ssh, nginx, etc...) pero también podemos configurar uno específico.

#Instalación

A continuación os paso a explicar el proceso de instalación y una pequeña introducción a la configuración para proteger el servicio SSH. El taller lo iré realizando en una máquina virtual CentOS 6.8 pero la iré complementando con salidas y configuraciones de mi máquina pública para que se pueda ver el resultado en un entorno "real". Todos los comandos tienen que ser realizados con el usuario root.

[Fail2Ban] no se encuentra disponible en los repositorios base CentOS y será necesario que configuremos los repositorios de EPEL con el siguiente comando:

```Bash
[root@localhost ~]# rpm -Uvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
Recuperando http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
advertencia:/var/tmp/rpm-tmp.bkyK0z: CabeceraV3 RSA/SHA256 Signature, ID de clave 0608b895: NOKEY
Preparando...               ########################################### [100%]
   1:epel-release           ########################################### [100%]
```

Ahora ya podemos ejecutar la instalación con yum

```Bash
[root@localhost ~]# yum install fail2ban -y
Complementos cargados:fastestmirror
Configurando el proceso de instalación
Loading mirror speeds from cached hostfile
epel/metalink                                                                                                                                                                                                      |  21 kB     00:00
 * base: centos.cadt.com
 * epel: epel.besthosting.ua
 * extras: centos.cadt.com
 * updates: centos.cadt.com
epel                                                                                                                                                                                                               | 4.3 kB     00:00
epel/primary_db                                                                                                                                                                                                    | 5.0 MB     00:12
Resolviendo dependencias
--> Ejecutando prueba de transacción
---> Package fail2ban.noarch 0:0.9.3-1.el6.1 will be instalado
--> Procesando dependencias: python-inotify para el paquete: fail2ban-0.9.3-1.el6.1.noarch
--> Procesando dependencias: ipset para el paquete: fail2ban-0.9.3-1.el6.1.noarch
--> Procesando dependencias: gamin-python para el paquete: fail2ban-0.9.3-1.el6.1.noarch
--> Procesando dependencias: ed para el paquete: fail2ban-0.9.3-1.el6.1.noarch
--> Ejecutando prueba de transacción
---> Package ed.i686 0:1.1-3.3.el6 will be instalado
---> Package gamin-python.i686 0:0.1.10-9.el6 will be instalado
---> Package ipset.i686 0:6.11-4.el6 will be instalado
--> Procesando dependencias: libmnl.so.0(LIBMNL_1.0) para el paquete: ipset-6.11-4.el6.i686
--> Procesando dependencias: libmnl.so.0 para el paquete: ipset-6.11-4.el6.i686
---> Package python-inotify.noarch 0:0.9.1-1.el6 will be instalado
--> Ejecutando prueba de transacción
---> Package libmnl.i686 0:1.0.2-3.el6 will be instalado
--> Resolución de dependencias finalizada

Dependencias resueltas

==========================================================================================================================================================================================================================================
 Paquete                                                      Arquitectura                                         Versión                                                       Repositorio                                        Tamaño
==========================================================================================================================================================================================================================================
Instalando:
 fail2ban                                                     noarch                                               0.9.3-1.el6.1                                                 epel                                               419 k
Instalando para las dependencias:
 ed                                                           i686                                                 1.1-3.3.el6                                                   base                                                70 k
 gamin-python                                                 i686                                                 0.1.10-9.el6                                                  base                                                33 k
 ipset                                                        i686                                                 6.11-4.el6                                                    base                                                63 k
 libmnl                                                       i686                                                 1.0.2-3.el6                                                   base                                                22 k
 python-inotify                                               noarch                                               0.9.1-1.el6                                                   epel                                                50 k

Resumen de la transacción
==========================================================================================================================================================================================================================================
Instalar       6 Paquete(s)

Tamaño total de la descarga: 656 k
Tamaño instalado: 2.0 M
Descargando paquetes:
(1/6): ed-1.1-3.3.el6.i686.rpm                                                                                                                                                                                     |  70 kB     00:00
(2/6): fail2ban-0.9.3-1.el6.1.noarch.rpm                                                                                                                                                                           | 419 kB     00:01
(3/6): gamin-python-0.1.10-9.el6.i686.rpm                                                                                                                                                                          |  33 kB     00:00
(4/6): ipset-6.11-4.el6.i686.rpm                                                                                                                                                                                   |  63 kB     00:00
(5/6): libmnl-1.0.2-3.el6.i686.rpm                                                                                                                                                                                 |  22 kB     00:00
(6/6): python-inotify-0.9.1-1.el6.noarch.rpm                                                                                                                                                                       |  50 kB     00:00
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                                                     154 kB/s | 656 kB     00:04
advertencia:rpmts_HdrFromFdno: CabeceraV3 RSA/SHA1 Signature, ID de clave c105b9de: NOKEY
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
Importing GPG key 0xC105B9DE:
 Userid : CentOS-6 Key (CentOS 6 Official Signing Key) <centos-6-key@centos.org>
 Package: centos-release-6-8.el6.centos.12.3.i686 (@anaconda-CentOS-201605211917.i386/6.8)
 From   : /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
warning: rpmts_HdrFromFdno: Header V3 RSA/SHA256 Signature, key ID 0608b895: NOKEY
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6
Importing GPG key 0x0608B895:
 Userid : EPEL (6) <epel@fedoraproject.org>
 Package: epel-release-6-8.noarch (installed)
 From   : /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6
Ejecutando el rpm_check_debug
Ejecutando prueba de transacción
La prueba de transacción ha sido exitosa
Ejecutando transacción
Advertencia: Las bases de datos (RPMDB) han sido modificadas por un elemento ajeno a yum.
  Instalando    : python-inotify-0.9.1-1.el6.noarch                                                                                                                                                                                   1/6
  Instalando    : ed-1.1-3.3.el6.i686                                                                                                                                                                                                 2/6
  Instalando    : gamin-python-0.1.10-9.el6.i686                                                                                                                                                                                      3/6
  Instalando    : libmnl-1.0.2-3.el6.i686                                                                                                                                                                                             4/6
  Instalando    : ipset-6.11-4.el6.i686                                                                                                                                                                                               5/6
  Instalando    : fail2ban-0.9.3-1.el6.1.noarch                                                                                                                                                                                       6/6
  Verifying     : libmnl-1.0.2-3.el6.i686                                                                                                                                                                                             1/6
  Verifying     : fail2ban-0.9.3-1.el6.1.noarch                                                                                                                                                                                       2/6
  Verifying     : gamin-python-0.1.10-9.el6.i686                                                                                                                                                                                      3/6
  Verifying     : ipset-6.11-4.el6.i686                                                                                                                                                                                               4/6
  Verifying     : python-inotify-0.9.1-1.el6.noarch                                                                                                                                                                                   5/6
  Verifying     : ed-1.1-3.3.el6.i686                                                                                                                                                                                                 6/6

Instalado:
  fail2ban.noarch 0:0.9.3-1.el6.1

Dependencia(s) instalada(s):
  ed.i686 0:1.1-3.3.el6                   gamin-python.i686 0:0.1.10-9.el6                   ipset.i686 0:6.11-4.el6                   libmnl.i686 0:1.0.2-3.el6                   python-inotify.noarch 0:0.9.1-1.el6

¡Listo!
```
El programa se compone de dos partes importantes:
* La parte de servidor (daemon), que estará vigilando los diferentes ficheros de log en busca de patrones y creando los bloqueos necesarios.
* La parte cliente, que servirá para interactuar con el servidor y hacer consultas (p.e. número de bloqueos) o incluso aplicar configuraciones "en caliente".

La estructura de directorios y ficheros que genera la instalación es la siguiente:

```Bash
[root@localhost /]# ls -lrt /etc/fail2ban/
total 60
-rw-r--r--. 1 root root   290 ago  1  2015 paths-osx.conf
-rw-r--r--. 1 root root  1174 ago  1  2015 paths-freebsd.conf
-rw-r--r--. 1 root root   743 ago  1  2015 paths-fedora.conf
-rw-r--r--. 1 root root   642 ago  1  2015 paths-debian.conf
-rw-r--r--. 1 root root  1939 ago  1  2015 paths-common.conf
-rw-r--r--. 1 root root 18558 oct 17  2015 jail.conf
-rw-r--r--. 1 root root  2313 oct 17  2015 fail2ban.conf
drwxr-xr-x. 2 root root  4096 oct 17  2015 jail.d
drwxr-xr-x. 2 root root  4096 oct 17  2015 fail2ban.d
drwxr-xr-x. 3 root root  4096 sep  5 15:13 filter.d
drwxr-xr-x. 2 root root  4096 sep  5 15:13 action.d
```

Ahora ha llegado el momento de configurar una prisión (jail en [Fail2Ban]) que básicamente consiste en definir un servicio a monitorizar y unas acciones a realizar. Como he dicho nos interesa controlar el SSH, para esto crearemos el fichero jail.local en la misma ruta:

```Bash
touch /etc/fail2ban/jail.local
```

Y pondremos el siguiente contenido:

```Bash
[DEFAULT]
# Tiempo que bloqueramos la IP: 3600 segundos (1 hora)
bantime = 3600

# La acción que de bloqueo será a traves del firewall interno (iptables)
banaction = iptables-multiport

[sshd] #activamos el jail para el demonio de ssh
enabled = true
```
Arrancamos el demonio:

```Bash
[root@localhost /]# /etc/init.d/fail2ban start
Iniciando fail2ban:                                        [  OK  ]
``` 
Consultamos, a través del cliente, que jails tenemos activos:

```Bash
[root@localhost /]# fail2ban-client status
Status
|- Number of jail:      1
`- Jail list:   sshd
```
Y podemos consultar en detalle el estado de ese jail:

```Bash
[root@localhost /]# fail2ban-client status sshd
Status for the jail: sshd
|- Filter
|  |- Currently failed: 0
|  |- Total failed:     0
|  `- File list:        /var/log/secure
`- Actions
   |- Currently banned: 0
   |- Total banned:     0
   `- Banned IP list:
```

En este caso nos indica que no ha localizado ningún fallo de autentificación, que monitoriza el fichero /var/log/secure (donde deja las trazas por defecto el demonio sshd) y que no ha realizado ninguna acción.

A continuación os voy a dejar la salida del mismo comando pero de mi servidor público que lleva unos 15 días funcionando para que comparéis los resultados:

```Bash
Status for the jail: sshd
|- Filter
|  |- Currently failed: 0
|  |- Total failed:     6445
|  `- File list:        /var/log/secure
`- Actions
   |- Currently banned: 0
   |- Total banned:     562
   `- Banned IP list:
```
Podéis ver que ha localizado 6445 fallos y ha bloqueado un total de 562 IPs. Actualmente no tiene ninguna IP bloqueada (se estarán cansado ;-) ).

#A tener en cuenta

* Para evitar posibles bloqueos no deseados (por ejemplo el de nuestra IP de acceso) podemos definir un rango de exclusión para que se ignoren los orígenes de dichas IPs con el parámetro *ignoreip*
* Mi recomendación es definir tiempos de bloqueo bajos para que, en caso de accidente, podamos recuperar el acceso a nuestro servidor. He comprobado que una hora es suficientemente disuasorio.
* Podéis ver los jails disponibles listando el contenido del fichero */etc/fail2ban/jail.conf* y hacer lo mismo que hemos hecho para el sshd.
* Recordad tener activado los servicios de *iptables* y *fail2ban*.
* Os dejo un ejemplo de configuración para el servidor web [nginx](https://www.nginx.com/resources/wiki/) dando servicio a diferentes dominios y con diferentes ficheros de log:
```Bash
[nginx-botsearch]

enabled = true
port     = http,https
logpath = /var/log/nginx/error.log
        /var/log/nginx/*/error.log
maxretry = 2
```

Espero que os sea útil y espero vuestro feedback.
 
[Fail2Ban]: http://www.fail2ban.org
