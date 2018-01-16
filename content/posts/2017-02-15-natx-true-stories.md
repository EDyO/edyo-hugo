---
title: "#TrueStories que no me contó ningún amigo"
author: "Ignasi Fosch"
slug: "true-stories"
date: 2017-02-17T10:35:00

tags: ["Automatización", "Básicos", "Crónica", "Empresa", "Filosofía", "Formación"]
---

<img src='/images/669fab80-f108-11e6-8519-f9af43643c67.jpg' alt='Mitsakes' class='align-left height='200' width='200'/>

Son muchas las citas y reflexiones que se han dicho y escrito sobre los errores y sus consecuencias.
Nadie está exento de equivocarse, pero aprender de esos mismos errores es aquello que permite mejorar y avanzar.

Reflexionar partiendo de errores que se han cometido, por nosotros mismos o otros; Identificar causas, medidas, incluso otros errores cometidos en su resolución, es una tarea difícil y, a veces, dura.
Pero resistirse a hacerlo por <s>el orgullo de algunos</s> cualquier motivo, es un error mucho mayor que cualquier otro.

<!--more-->


## Hace unas semanas...

Por si alguien no lo había oído, desde el 31 de enero hasta el uno de febrero, [GitLab] sufrió una caída de servicio importante debido a la [sucesión encadenada de diferentes errores].
Uno de los más comentados fue que de cinco mecanismos de copia de seguridad de que disponían, ninguno funcionó suficientemente bien.

Aunque ya tenía pensado este post desde hacía un par de meses, este evento me viene que ni al pelo para publicarlo y, además hacer una propuesta.

## Hace unos meses...

Hace unos meses, un viernes tarde, a punto de acabar la jornada, cometí un error al hacer un *pull request* en un proyecto público, de un *script* en el que había estado trabajando.
Los cambios que subí incluían un *commit* que había hecho en local, donde se incluían las credenciales de una cuenta.
Fue mi compañero quien vió las credenciales, revisé la cuenta y vi que sólo podía acceder a un servicio que estábamos probando y únicamente en modo de lectura.
Además las credenciales no eran visibles en el `HEAD`, y pensé que tampoco había mucho problema en arreglarlo tras el fin de semana.

Al día siguiente, me encontré en mi buzón un mensaje de alguien que mencionaba haber encontrado esas claves.
Eso me sorprendió bastante... sinceramente, no creí que nadie mirara las contribuciones a ese nivel en proyectos tan poco relevantes.
Se trataba de un *bot* que su creador usaba para buscar trabajo; detectaba credenciales, y enviaba el mail automáticamente, avisando de los peligros de haber subido las credenciales y dando el contacto del creador y su perfil.
Por supuesto, me apresuré a corregir la historia del repositorio para evitar que el *commit* fuera visible y a cancelar las credenciales.

Por supuesto, no es el único error que he cometido...

## Hace unos años...

Hace unos años, tenía que actualizar el número de serie del registro `SOA` de un dominio que servíamos sobre un [PowerDNS] sobre MySQL.
Así que escribí una sentencia `UPDATE` para cambiarlo, pero olvidé incluir la cláusula `WHERE` apropiada... el resultado fue bastante desastroso, pues había actualizado todos los registros con el mismo contenido.
La resolución fue sencilla: Restaurar de la última copia de seguridad, modificar el registro que había cambiado, y volver a hacer el `UPDATE`, esta vez con el `WHERE` correcto.
Pero además, decidí escribir una función SQL para evitar el error en posteriores situaciones.

## Soluciones peculiares

En otra ocasión, añadiendo usuarios al [LDAP] de un dominio en Samba, un compañero borró la base de datos del dominio de la oficina.
Esta vez, como no se había considerado crítico, no había ningún proceso de copia de seguridad ejecutándose regularmente, y la última copia de seguridad existente era de hacía, creo recordar, seis meses.
Restaurarla habría cancelado unas cuantas cuentas de usuario eliminadas; las de los usuarios que se habían creado en esos meses.

Por suerte, el compañero había volcado a pantalla el contenido de la base de datos y lo pudimos recuperar copiándolo directamente del buffer de la terminal, restaurando las cuentas que faltaban en el *backup*.
Posteriormente, creamos un sistema de copia de seguridad periódico.

## Propuesta

La propuesta es que nos [enviéis](mailto:info@entredevyops.es) <s>vuestras cagadas</s> vuestros errores para que los comentemos, anónimamente, en nuestro podcast.
De este modo, todos nuestros oyentes podrán aprender de los errores de otros.

Créditos de la imagen de cabecera: Creada por [Meredith Atwater] para [opensource.com]

[GitLab]: https://about.gitlab.com/features/
[sucesión encadenada de diferentes errores]: https://about.gitlab.com/2017/02/01/gitlab-dot-com-database-incident/
[PowerDNS]: https://www.powerdns.com/
[LDAP]: https://es.wikipedia.org/wiki/Protocolo_Ligero_de_Acceso_a_Directorios
[Meredith Atwater]: http://twitter.com/meredithatwater
[opensource.com]: https://opensource.com/
