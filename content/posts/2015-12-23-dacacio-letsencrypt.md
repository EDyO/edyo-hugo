---
title: "Probando Let's Encrypt: certificados SSL para todos!"
author: "David Acacio"
slug: "laboratorio_lets_encrypt"
date: 2015-12-23T16:30:00
tags: ["Laboratorio", "Let's Encrypt"]
---

![Lets Encrypt](/images/c3198b70-ad60-11e5-8736-57bd99ad0ca3.jpg)

El pasado día 03/12/2015 [Let's Encrypt](https://letsencrypt.org/) entró en fase beta pública. La idea con la cual nace este proyecto es la de ofrecer **gratuitamente** certificados X.509 para encriptación TLS a través de procesos automáticos, eliminando los complejos y engorrosos procesos de creación, validación, firma, instalación y renovación de los certificados para la securización de sitios web.

A continuación paso a detallar la prueba que hice.

<!--more-->

Comentar que la prueba la he realizado sobre mi VPS con CentOS 6.7, con Python 2.6 y ejecutando todos los pasos como root.

Para realizar la instalación he seguido los pasos descritos descritos en la web de Let's Encrypt https://letsencrypt.org/howitworks/

Instalamos el cliente descargándolo directamente de Github:

```bash
git clone https://github.com/letsencrypt/letsencrypt
```

A continuación ejecutamos el comando:

```bash
./letsencrypt-auto --help
```

Que te instala de manera directa, si no los tienes, los siguientes paquetes

```bash
Package git-1.7.1-3.el6_4.1.x86_64 already installed and latest version
Package gcc-4.4.7-16.el6.x86_64 already installed and latest version
Package dialog-1.1-9.20080819.1.el6.x86_64 already installed and latest version
Package augeas-libs-1.0.0-10.el6.x86_64 already installed and latest version
Package openssl-devel-1.0.1e-42.el6.x86_64 already installed and latest version
Package libffi-devel-3.0.5-3.2.el6.x86_64 already installed and latest version
Package redhat-rpm-config-9.0.3-44.el6.centos.noarch already installed and latest version
Package ca-certificates-2015.2.4-65.0.1.el6_6.noarch already installed and latest version
```

Llegados a este punto intento solicitar el certificado de mi dominio:

```bash
./letsencrypt-auto certonly --standalone -d acacio.cat
```

Pero en mi caso aparece el siguiente mensaje debido a que utilizo python 2.6

```bash
WARNING: Python 2.6 support is very experimental at present...
if you would like to work on improving it, please ensure you have backups
and then run this script again with the --debug flag!
```

Tal como indica, volvemos a lanzar el comando con dicho flag y nos permite avanzar

```bash
./letsencrypt-auto certonly --debug --standalone -d acacio.cat

Updating letsencrypt and virtual environment dependencies.../root/.local/share/letsencrypt/lib/python2.6/site-packages/cryptography/__init__.py:25: DeprecationWarning: Python 2.6 is no longer supported by the Python core team, please upgrade your Python.
  DeprecationWarning
./root/.local/share/letsencrypt/lib/python2.6/site-packages/cryptography/__init__.py:25: DeprecationWarning: Python 2.6 is no longer supported by the Python core team, please upgrade your Python.
  DeprecationWarning
./root/.local/share/letsencrypt/lib/python2.6/site-packages/cryptography/__init__.py:25: DeprecationWarning: Python 2.6 is no longer supported by the Python core team, please upgrade your Python.
  DeprecationWarning
./root/.local/share/letsencrypt/lib/python2.6/site-packages/cryptography/__init__.py:25: DeprecationWarning: Python 2.6 is no longer supported by the Python core team, please upgrade your Python.
  DeprecationWarning
./root/.local/share/letsencrypt/lib/python2.6/site-packages/cryptography/__init__.py:25: DeprecationWarning: Python 2.6 is no longer supported by the Python core team, please upgrade your Python.
  DeprecationWarning
/root/.local/share/letsencrypt/lib/python2.6/site-packages/cryptography/__init__.py:25: DeprecationWarning: Python 2.6 is no longer supported by the Python core team, please upgrade your Python.
  DeprecationWarning

Running with virtualenv: /root/.local/share/letsencrypt/bin/letsencrypt certonly --debug --standalone -d acacio.cat
/root/.local/share/letsencrypt/lib/python2.6/site-packages/cryptography/__init__.py:25: DeprecationWarning: Python 2.6 is no longer supported by the Python core team, please upgrade your Python.
  DeprecationWarning
Version: 1.1-20080819
Version: 1.1-20080819

IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at
   /etc/letsencrypt/live/acacio.cat/fullchain.pem. Your cert will
   expire on 2016-03-06. To obtain a new version of the certificate in
   the future, simply run Let s Encrypt again.
 - If like Let s Encrypt, please consider supporting our work by:

   Donating to ISRG / Let s Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le
```

Durante la instalación nos aparece una ventana en ncurses que nos solicita una dirección de correo electrónico por si se tienen que ponder en contacto con nosotros.

Al finalizar, tenemos los siguientes ficheros en máquina:

La clave privada para el certificado:

```bash
lrwxrwxrwx 1 root root 37 Dec  7 13:04 privkey.pem -> ../../archive/acacio.cat/privkey.pem
```

Todos los certificados, incluyendo el certificado del servidor:

```bash
lrwxrwxrwx 1 root root 39 Dec  7 13:04 fullchain.pem -> ../../archive/acacio.cat/fullchain.pem
```

Todos los certificados, excluyendo el certificado del servidor:

```bash
lrwxrwxrwx 1 root root 35 Dec  7 13:04 chain.pem -> ../../archive/acacio.cat/chain.pem
```

El certificado del servidor:


```bash
lrwxrwxrwx 1 root root 34 Dec  7 13:04 cert.pem -> ../../archive/acacio.cat/cert.pem
```

En teoría ya tenemos certificados válidos para publicar con nuestro webserver. En mi caso estamos hablando de un nginx, que lo he configurado añadiendo las siguientes lineas:

```nginx
    listen       5.79.75.212:443;
    ssl    on;
    ssl_certificate    /etc/letsencrypt/live/acacio.cat/cert.pem;
    ssl_certificate_key    /etc/letsencrypt/live/acacio.cat/privkey.pem;
    server_name  acacio.cat;
```

Con esta configuración estamos securizando el dominio, pero si hacemos pruebas de acceso nos encontramos que hay clientes que no encuentran el certificado como confiable. Para que esto suceda, necesitamos enviar toda la cadena de certificados, por tal que el cliente sepa validarlo con la CA de IdenTrust. Por tanto, configuramos el servidor para tal efecto:

```nginx
    listen       5.79.75.212:443;
    ssl    on;
    ssl_certificate    /etc/letsencrypt/live/acacio.cat/fullchain.pem;
    ssl_certificate_key    /etc/letsencrypt/live/acacio.cat/privkey.pem;
    server_name  acacio.cat;
```

Y listo! Ya tengo certificado para mi dominio personal https://acacio.cat.
