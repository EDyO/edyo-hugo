---
title: "Habilitar la autenticación en dos pasos para SSH con Google Authenticator"
author: "David Acacio "
slug: "ssh-2FA"
date: 2016-11-23T00:25:00

tags: ["SSH", "2FA", "Google Authenticator"]
---

<img src='/images/4c54eb54-9466-11e6-8a7b-4aa4459dc02f.png' alt='Ssh Google Authenticator' class='align-right' height='150' width='150'/>

Tal como comenté en mi [pasado artículo en este mismo blog](http://www.entredevyops.es/posts/fail2ban-ssh.html) hace poco detecté que alguna mala persona estaba intentando acceder a mi servidor privado mediante fuerza bruta por SSH. En el artículo de hoy vamos a explicar cómo activar el 2FA (doble factor de autenticación) para acceso SSH con [Google Authenticator](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2). 

<!--more-->


La demostración la vamos a realizar sobre una máquina virtual en mi PC basada en Ubuntu Server 16.04.01.

Lo primero que vamos a necesitar es la instalación del paquete que habilite en el PAM (el sistema que gestiona la autentificación de la máquina) el módulo de Google Authenticator:

```Bash
root@ubuntu:~# sudo apt-get install -y libpam-google-authenticator
```

Y posteriormente añadir la siguiente línea en el fichero /etc/pam.d/sshd para que se habilite dicho módulo en el servicio SSH:
```bash
auth required pam_google_authenticator.so
```

Y el fichero /etc/ssh/sshd_config modificar el siguiente parámetro de 'no' a 'yes'
```bash
ChallengeResponseAuthentication yes
```

Y realizar un reinicio del servicio de SSH:
```bash
root@ubuntu:~# sudo service sshd restart
```

A partir de ahora cualquier acceso SSH requerirá de código de verificación.

Perfecto, ahora que ya tenemos nuestro sistema para que el SSH solicite la doble autentificación, el siguiente paso es configurar los usuarios que van a necesitar acceder. Para configurarlo necesitamos tener a mano el dispositivo el cual tengamos instalado el Google Authenticator, mi caso mi teléfono móvil Android.

Cambiamos al usuario en el que queremos activar la doble autenticación (en este caso mitch) y ejecutamos el siguiente comando:

```bash
mitch@ubuntu:~$ google-authenticator

Do you want authentication tokens to be time-based (y/n) y
https://www.google.com/chart?chs=200x200&chld=M|0&cht=qr&chl=otpauth://totp/mitch@ubuntu%3Fsecret%3D3HXRVMUFOOTJP3OL
```
<img src='/images/1c056f0e-9458-11e6-83d3-4092efbe9dfc.jpg' class='align-center' height='400' width='400'/>

```bash 
Your new secret key is: 3HXRVMUFOOTJP3OL
Your verification code is 561744
Your emergency scratch codes are:
  54523107
  83743686
  46350483
  10209811
  51273874

Do you want me to update your "/home/mitch/.google_authenticator" file (y/n) y

Do you want to disallow multiple uses of the same authentication
token? This restricts you to one login about every 30s, but it increases
your chances to notice or even prevent man-in-the-middle attacks (y/n) y

By default, tokens are good for 30 seconds and in order to compensate for
possible time-skew between the client and the server, we allow an extra
token before and after the current time. If you experience problems with poor
time synchronization, you can increase the window from its default
size of 1:30min to about 4min. Do you want to do so (y/n) y

If the computer that you are logging into isn't hardened against brute-force
login attempts, you can enable rate-limiting for the authentication module.
By default, this limits attackers to no more than 3 login attempts every 30s.
Do you want to enable rate-limiting (y/n) y
```
En este punto tenemos que escanear el código de barras (o introducir los códigos facilitados) y nos aparecerá una nueva entrada en nuestra aplicación móvil:

<img src='/images/cdccac0a-a9fe-11e6-9cd4-09cdf981ec34.png' class='align-center' height='300' width='200'/>

Como podéis observar aparece una entrada para mitch@ubuntu, que es la correspondiente a mi máquina. La otra entrada que aparece es la relativa a mi servicio de Dropbox.

Llegados a este punto ya estamos en disposición de probar si funciona. Abrimos un nuevo terminal y ejecutamos SSH contra nuestro servidor e introducimos usuario y password:

```bash
login as: mitch
Using keyboard-interactive authentication.
Password:
Using keyboard-interactive authentication.
Verification code:
```

Después de solicitarme el password me aparece una nueva línea que me solicita el código de verificación, que es el que tendremos que consultar en nuestra aplicación. Una vez introducido podremos acceder al sistema sin problema. 

Por último un pequeño consejo: si queréis activar el 2FA de manera gradual en el sistema podéis añadir la opción nullok cuando configuréis el PAM en el fichero /etc/pam.d/sshd (recordad reiniciar el sshd al realizar la modificación).
```bash
auth required pam_google_authenticator.so nullok
```
De esta manera solo activará la configuración a aquellos usuarios que hayan ejecutado el proceso de configuración.

Espero que os sea útil y podéis hacerme llegar vuestras dudas/opiniones a través los comentarios del post.
