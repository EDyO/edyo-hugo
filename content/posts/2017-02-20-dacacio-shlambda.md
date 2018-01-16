---
title: "Ejecutando shell script en AWS Lambda"
author: "David Acacio"
slug: "shellscript-lambda"
date: 2017-02-20T23:25:00

tags: ["AWS", "Lambda", "Shell script"]
---

<img src='/images/da5bb104-f243-11e6-96e0-f7d9341c64a3.png' alt='AWS Lambda' class='align-right' height='200' width='200'/>

Llevo un tiempo dándole vueltas a migrar de mi servidor virtual privado hacia el cloud, en concreto hacia AWS, pero uno de los motivos que más me echan para atrás es todos los scripts, la mayor parte en shell script, que tengo programados para ejecutarse diariamente en mi servidor y que realizan tareas de lo más útiles. De todos ellos destacaría el que tengo para que cada día me "recolecte" el libro electrónico gratuito que publica [Packtpub](https://www.packtpub.com). Pues bien, parece que este impedimento ha llegado a su fin, ya que utilizando un pequeño truco se pueden ejecutar shell scripts en Lambda.

A continuación, os explico cómo he migrado mis shell scripts a Lambda.

<!--more-->


Si habéis trabajado un poco con Lambda ya sabréis que los lenguajes que admite son C#, Java 8, Edge Node y Python, pero en ningún caso permite la ejecución de shell script. Entonces, ¿cómo vamos a ejecutar nuestros scripts?

Pues es bien sencillo, si no conocéis cómo funciona [AWS Lambda](https://aws.amazon.com/es/lambda/) os diré que se basa en tecnología de contenedores, esto significa que el proceso cree que está corriendo en un servidor Linux de manera totalmente aislada, por tanto nada nos impide hacer llamadas al sistema operativo y ejecutar comandos como ls, cd, cp, etc... y como alguno de vosotros ya habrá deducido tampoco nos impide ejecutar ficheros .sh.

La última parte que nos quedaría es ver cómo realizamos la subida de dichos ficheros, ya que no existe ningún mecanismo estándar de transferencia (ftp, sftp, etc...). Subiremos los ficheros junto los ficheros que contenga el código de la aplicación.

Os voy a relatar cómo he realizado la instalación del script que cada día se conecta a Packtpub y "compra" el libro gratuito. El código lo podéis localizar en [este repositorio de Github](https://github.com/dacacioa/packtpub_lambda) (importante: tendríais que adaptar el fichero .sh con vuestras credenciales de Packtpub, es decir, con vuestro email y contraseña)

Dejadme que os cuente, a modo de guía paso a paso, cómo ejecutar scripts de manera planificada, emulando lo que haríamos editando el crontab de nuestro servidor Linux.

* Lo primero que haremos será descargar los ficheros del [repositorio de Github](https://github.com/dacacioa/packtpub_lambda) que básicamente son:

  1.- El fichero .py que se encagará de ejecutar la llamada a sistema lanzado un shell para cargar el fichero .sh
```
  from __future__ import print_function

  import commands

  def lambda_handler(event, context):
      if commands.getstatusoutput('sh ./packtpub.sh')[0] == 0 :
          return "Ok, enjoy your free book"
```

  2.- El fichero .sh que ejecutará un curl en el contenedor donde se ejecute el código. Dicho curl ya está preparada para hacer login con las credenciales que indiquemos (email y contraseña), buscará el enlace del libro gratuito y simulará un click sobre dicho enalce.

  ```
  rm /tmp/user.cookie; curl -b /tmp/user.cookie https://www.packtpub.com$(curl -L -k -d 'email=your%40email.com&password=yourpassword&op=Login&form_build_id=form-29b891c23331f6a85f502eef8b133303&form_id=packt_user_login_form' -b /tmp/user.cookie -c /tmp/user.cookie 'https://www.packtpub.com/packt/offers/free-learning' | grep -i 'freelearning-claim' | awk '{print $2}' | cut -d'"' -f2)
  ```

  Es importante adaptar el fichero .sh con las credenciales correctas para que todo funcione. Una vez hecho esto generaremos un .zip que contenga los dos ficheros, el .py y el .sh.

* Nos conectaremos al panel de control de AWS y accederemos a la sección de Lambda:

<img src='/images/00270f48-efa9-11e6-9475-840f0de06438.png' alt='AWS Lambda' class='align-center' />

* Pulsamos el botón "Get Started Now" y aparecerá una pantalla para seleccionar plantilla. seleccionamos "Blank Function":

<img src='/images/46ea81d0-efa9-11e6-9521-182ee85c93f2.png' alt='AWS Lambda Function' class='align-center' />

* En la pantalla de configuración de Triggers hacemos click sobre el recuadro con el contorno discontinuo y seleccionamos el trigger "CloudWatch Events - Schedule":

<img src='/images/57ca4c10-efa9-11e6-8a7d-ae37e800d8a0.png' alt='CloudWatch Events' class='align-center' />

* En el apartado de configuración seleccionamos que solo se ejecute una vez al día:
  * En el apartado "Rule Name" indicamos una vez al día.
  * La descripción la dejamos por defecto.
  * Confirmamos que la expresión de planificación es rate(1 day)
  * Por último, seleccionamos la casilla de "Enable trigger" para activar la regla.

<img src='/images/c5ac3126-efa9-11e6-9fb5-a3ff77b2da98.png' alt='Lambda Definition' class='align-center' />

* En la siguiente pantalla configuraremos el entorno de ejecución de nuestra función:
  * En el campo nombre insertaremos un nombre identificativo de la función.
  * La descripción que creamos apropiada.
  * Y en el campo "Runtime" seleccionaremos Python 2.7.
  * Como "Code entry type" indicamos "Upload a .ZIP file" y subiremos el fichero .zip generado en el primer punto.

<img src='/images/d0e6f754-efb5-11e6-9973-0c1428dde6ef.png' alt='AWS Lambda Code' class='align-center' />

 * En el apartado de "Lambda Function Handler" indicaremos lo siguiente:
  * Insertaremos en el campo "Handler" el nombre del fichero .py más el nombre de la función que se tendrá que ejecutar. Si hemos seguido el procedimiento sin modificar ningún nombre de fichero tendríamos que indicar packtpub.lambda_handler .
  * "Role": Seleccionamos "Choose a existing role".
  * "Existing Role": "service-role/lamda_crontab_rol".
 * En el apartado "Advenced settings" modificaremos el timeout a 5 segundos, ya que en ocasiones Packtpub tarda algo en responder y el timeout por defecto de 3 segundos se queda algo corto. Una vez hecha esta modificación podemos pulsar el botón de "Next".

<img src='/images/080ed6c0-efb6-11e6-8695-9a9baa8e20dd.png' alt='AWS Lambda Code 2' class='align-center' />

 * Si todo ha funcionado correctamente tendríamos que ver una pantalla similar a esta:

 <img src='/images/2c5b6ac0-efb6-11e6-8eee-6185ae5d5457.png' alt='AWS Lambda Final' class='align-center' />

 * Pulsaremos el botón de "Test" para ver que funciona correctamente:
  * Seleccionamos "Scheduled Event"
  * Y pulsamos "Save and Test"

  <img src='/images/f2be5f80-f24d-11e6-899a-db037f1c581b.png' alt='AWS Test Event' width=80% class='align-center' />

 * Nos tendría que aparecer una pantalla similar a la que pongo a continuación con el mensaje "Ok, enjoy your free book". Importante: Packtpub limita a un libro al día, por tanto, por muchas veces que lo ejecutemos sólo tendremos disponible en nuestra cuenta de Packtpub una copia del libro).

 <img src='/images/95b7f822-f24e-11e6-873a-11c441259996.png' alt='AWS Lambda TEst Ok' width=80% class='align-center' />

¡Enhorabuena! Ya tenéis funcionando en Lambda una tarea programada que se ejecuta cada día y lanza un shell script para "recolectar" de manera automática los libros gratuitos de Packtpub. Y por cierto, todo a coste 0, ya que el consumo de ejecutar estos procesos es tan bajo que lo cubre la capa gratuita de AWS.

Espero que os sea útil y lo extrapoléis a otros escenarios.
