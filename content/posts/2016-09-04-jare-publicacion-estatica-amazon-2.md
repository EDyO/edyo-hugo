---
title: "Páginas estáticas en Amazon - 2"
author: "Javier Arellano"
slug: "paginas-estaticas-amazon-2"
date: 2016-09-04T12:00:00
tags: ["Amazon WS", "Automatización", "Herramientas", "Web"]
---

Continuamos con el curso de páginas estáticas de Amazon, pero esta vez vamos a
subir las páginas a Amazon. Elegimos un sistema de generación de contenido
estático. En la siguiente [página](https://staticsitegenerators.net) hay un
listado muy extenso de este tipo de software.

<!--more-->

Para ello usaremos un sistema de generación de páginas  que se llama Nikola. El sistema no es importante, se puede hacer con muchos, para instalar  el que vamos a usar en este caso se ha de visitar su [página web](https://www.getnikola.com/) es un programa realizado en python por lo que los ejemplos que pongo en este artículo han sido probados en Mac y en Linux, y funcionan correctamente en los dos sistemas. Aunque este no intenta ser un manual de nikola, ya que la parte interesante es entender como funcionan los usuarios y los permisos en Amazon.

Siguiendo el manual creamos un proyecto nuevo:

```bash
# nikola init --demo nikola
Creating Nikola Site
====================

This is Nikola v7.3.0.  We will now ask you a few easy questions about your new site.
If you do not want to answer and want to go with the defaults instead, simply restart with the `-q` parameter.
--- Questions about the site ---
Site title [My Nikola Site]:
Site author [Nikola Tesla]:
Site author`s e-mail [n.tesla@example.com]:
Site description [This is a demo site for Nikola.]:
Site URL [http://getnikola.com/]: http://blog.dondever.es
--- Questions about languages and locales ---
We will now ask you to provide the list of languages you want to use.
Please list all the desired languages, comma-separated, using ISO 639-1 codes.  The first language will be used as the default.
Type '?' (a question mark, sans quotes) to list available languages.
Language(s) to use [en]: es

Please choose the correct time zone for your blog. Nikola uses the tz database.
You can find your time zone here:
http://en.wikipedia.org/wiki/List_of_tz_database_time_zones

Time zone [Europe/Madrid]:
    Current time in Europe/Madrid: 19:14:21
Use this time zone? [Y/n] y
--- Questions about comments ---
You can configure comments now.  Type '?' (a question mark, sans quotes) to list available comment systems.  If you do not want any comments, just leave the field blank.
Comment system:

That`s it, Nikola is now configured.  Make sure to edit conf.py to your liking.
If you are looking for themes and addons, check out http://themes.getnikola.com/ and http://plugins.getnikola.com/.
Have fun!
[2016-09-04T17:14:23Z] INFO: init: A new site with example data has been created at nikola.
[2016-09-04T17:14:23Z] INFO: init: See README.txt in that folder for more information.
```

entramos en el directorio y ejecutamos el comando de generar contenido que genera todos los ficheros en el subdirectorio output

```bash
# nikola build
Scanning posts....done!
.  render_archive:output/2012/index.html
.  render_archive:output/archive.html
.  copy_assets:output/assets/css/bootstrap-theme.css
.  copy_assets:output/assets/css/bootstrap-theme.css.map
[...]
.  create_bundles:output/assets/js/all.js
.  sitemap:output/sitemap.xml
.  sitemap:output/sitemapindex.xml
.  robots_file:output/robots.txt
```

Si lo queremos ver en local podemos ejecutar :

```bash
# nikola serve
[2016-09-04T17:18:02Z] INFO: serve: Serving HTTP on 0.0.0.0 port 8000...
```

Podremos ver una página de muestra en un navegador apuntando a la dirección: http://127.0.0.1:8000

Esta pagina generada es una página de ejemplo que la podemos usar tal como está para nuestro propósito

Ahora crearemos un *bucket* que alojará de este proyecto, se llamará blog.dondever.es  y lo crearemos tal como se comentó en [la anterior parte de este artículo](http://www.entredevyops.es/posts/paginas-estaticas-amazon-1.html), recordad que se ha de permitir que sea un *Static website hosting* , los permisos, el registro en route53, etc.

Ahora crearemos el usuario para copiar los ficheros en AWS en la sección IAM apartado *Users* y botón *Create user*. 

Crearemos un usuario llamado "deploy", una vez creado nos muestra por pantalla  el *Access Key ID* y el *Secret Access Key*  es muy importante guardar los datos por que no hay forma de volver a  recuperarlos, por lo que se tendría que volver a recrear en el caso de perdida. 

```bash
Access Key ID: AKIAJBFNFTW2YXEYZWBA
Secret Access Key: gu7TAatrFc18TqxUfEu+f61TStm1yvtHQRUCdJt
```

Por defecto los usuarios no tienen password, sino que se usa la pareja de claves como identificador y autenticador. Una vez se crea el password el usuario podrá acceder a la consola si tiene los permisos adecuados. un usuario recién creado no tiene permisos, sino que necesita que explícitamente le añadamos los permisos para cada uno de los servicios que queramos que el usuario pueda gestionar. 

Ahora que tenemos las credenciales del usuario falta añadirle permisos para que pueda subir ficheros al *bucket*, esto lo hacemos en las propiedades del usuario, pestaña *permissions*, *inline policies* y como no hay ninguna vamos a "click here" en la siguiente pantalla elegimos *custom policies* en *policy name* ponemos algun nombre descriptivo, por ejemplo "politica_deploy_blog" y en el cuerpo copiamos el texto:

```bash
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:ListObjects"
            ],
            "Resource": "arn:aws:s3:::blog.dondever.es/*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": "arn:aws:s3:::blog.dondever.es"
        }
    ]
}
```

Teniendo en cuenta que se ha de cambiar el *bucket* por el que estéis usando.

Ahora lo único que falta es copiar los ficheros desde nuestro directorio al *bucket*, para ello tenemos que instalar el [CLI de amazon](https://aws.amazon.com/es/cli/), ejecutando:

```bash
sudo pip install awscli
```

una vez instalado podemos ejecutar:

```bash
$ export AWS_ACCESS_KEY_ID=AKIAJBFNFTW2YXEYZWBA
$ export AWS_SECRET_ACCESS_KEY=gu7TAatrFc18TqxUfEu+f61TStm1yvtHQRUCdJt
$ export AWS_DEFAULT_REGION=eu-west-1
```

De esta forma ya tiene la información de las credenciales de usuario y la región donde actuar, y podemos ejecutar la subida de los datos:

```bash
$ aws s3 sync output/  s3://blog.dondever.es
upload: output/2012/index.html to s3://blog.dondever.es/2012/index.html
upload: output/archive.html to s3://blog.dondever.es/archive.html
upload: output/assets/css/bootstrap-theme.css.map to s3://blog.dondever.es/assets/css/bootstrap-theme.css.map
upload: output/assets/css/code.css to s3://blog.dondever.es/assets/css/code.css
[...]
upload: output/favicon.ico to s3://blog.dondever.es/favicon.ico
upload: output/stories/a-study-in-scarlet.txt to s3://blog.dondever.es/stories/a-study-in-scarlet.txt
upload: output/stories/a-study-in-scarlet.html to s3://blog.dondever.es/stories/a-study-in-scarlet.html
```

Y ya tenemos el blog funcionando correctamente en Amazon. Próximamente añadiremos un poco más de automatización a poder subir páginas a AWS.
