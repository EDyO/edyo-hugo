---
title: "Publicación estática"
author: "Ignasi Fosch"
slug: "publicacion-estatica"
date: 2016-07-11T12:00:00

tags: ["Automatización", "Herramientas", "Web"]
---

Muy probablemente, muchos de vosotros ya sabréis lo que es un sitio estático.
Seguramente, también tendréis o trabajaréis con alguno.
Hay muchas suites para hacerlos, y muchas formas de desplegarlos automáticamente.

<!--more-->


Aunque el concepto de sitio estático pueda no ser demasiado conocido, el de un `sistema de gestión de contenidos`_, CMS por sus siglas en inglés, seguro que lo es más.
La mayoría conoceréis softwares como `WordPress`_, `Joomla`_, `Drupal`_, `Plone`_, y muchos otros más.
Estas son aplicaciones que permiten a usuarios no técnicos y con relativamente pocos conocimientos de Internet y Web, crear sites de una forma más o menos sencilla y con bastante buenos resultados.

¡Ojo! Esa última frase tiene una pequeña trampa... Lo explicamos mejor:
Cuando alguien necesita una página, pero no tiene conocimientos de HTML, CSS, JavaScript y otras tecnologías; usar una de estas herramientas suele ser una buena solución.
Pero normalmente, tal perfil, tampoco va a saber instalar, configurar y dejar listo todo lo necesario para usar, por ejemplo, WordPress.
Al menos, no sin tener que aprender un buen montón de cosas por el camino.

Existe la alternativa de que use un SaaS, pero la mayoría de los que hay disponibles, o tienen un precio bastante alto, o no ofrecen la flexibilidad que tiene el hacerlo para cada caso.
Por eso es muy habitual que el interesado acabe o bien aprendiendo a hacerlo por su cuenta, o contratando a alguien que sepa y se lo haga.
Por desgracia, una aventura así no acaba ahí...

Estos programas tienen:
- su código, 
- el de las librerías y pilas tecnológicas que usan, 
- el de todos los temas y plugins que proporcionan,
- el de la base de datos,...

Además, la mayoría de CMS, tiene un panel de administración integrado, con el que los usuarios pueden gestionar el contenido.
Esos paneles están en rutas bastantes conocidas y suelen tener contraseñas puestas por los usuarios.
Su código puede tener agujeros de seguridad que se peudan utilizar para acceder a otros sistemas, o ejecutar código aleatorio.
Eso las convierte en objeto de ataque de seguridad constantemente.

Para evitar que esos ataques tengan éxito, hay que mantenerlos bien actualizados, entre otras gestiones,... Y como normalmente no suelen ser sencillos de actualizar, llevan trabajo. ¡Y eso, con suerte!

Por supuesto, hay casos de uso en los que tiene sentido.
Pero no todos, por ejemplo, un blog personal, de un proyecto, o de una empresa pequeña... muy probablemente, no va a necesitar tantos plugins, temas y funcionalidades.

Además, si se quiere que el sitio cumpla ciertas condiciones de tolerancia a fallos y alta disponibilidad, se requieren unas arquitecturas bastante complejas, que suelen también añadir nuevos software, que necesitará su gestión y actualización.
En definitiva, un bonito escenario para alguien que no tiene conocimientos tecnológicos o los tiene limitados.

Pues bien, aquí es donde entran los sitios estáticos.
Un sitio estático en un servicio web en el que todo contenido, pero en forma de ficheros en lugar de programas ejecutándose.
No hay ningún software más que el servidor web y el sistema operativo, lo que facilita muchísimo la actualización.
Son menos vulnerables a ataques, ya que el software se mantiene actualizado más fácilmente.
Son más rápidos sirviendo que cualquier CMS, pues no necesitan procesar nada, sólo leer el fichero.
Además, su distribución y disponibilidad son mucho más fáciles, ya que son sólo ficheros que se van actualizando al publicar.
El principal inconveniente, como se ha explicado antes, es que hay que escribir HTML y CSS a mano.

Para ello se pueden usar los generadores de sitios estáticos, que no son más que un programa que lee una entrada, consistente en ficheros en formatos como ReST, Markdown, o similares, y crea los ficheros estáticos (HTML, CSS, imágenes, ...).
Muchos de estos generadores, incluso, disponen de plugins y temas, para facilitar el trabajo con ellos, pero todos acaban generando los ficheros.

Si a eso, le sumamos el uso de herramientas como `Travis-CI`_, junto con servicios como `GitHub Pages`_, resulta muy fácil disponer de un sitio web estático sin demasiado trabajo de gestión.
En el `blog de Entre Dev Y Ops`_, utilizamos `Nikola`_; en el `blog de GolangBCN`_, `Hugo`_; y en el `blog de PyBCN`_, usamos `Lektor`_. Todos ellos publican mediante `Travis-CI`_ en `GitHub Pages`_. Los repositorios, son todos públicos, tanto el de `Entre Dev Y Ops`_, el del blog de `GolangBCN`_, o el de `PyBCN`_.

Como este artículo ya se ha extendido un poco, dejamos para próximas entregas los detalles sobre cómo funcionan y cómo se publica con ellos.

.. _`sistema de gestión de contenidos`: https://es.wikipedia.org/wiki/Sistema_de_gesti%C3%B3n_de_contenidos
.. _`WordPress`: https://es.wordpress.org/
.. _`Joomla`: https://www.joomla.org/
.. _`Drupal`: https://www.drupal.org/
.. _`Plone`: https://plone.org/
.. _`Travis-CI`: https://travis-ci.org
.. _`GitHub Pages`: https://pages.github.com/
.. _`blog de Entre Dev Y Ops`: http://entredevyops.es
.. _`Nikola`: http://getnikola.com
.. _`blog de GolangBCN`: http://golangbcn.org
.. _`Hugo`: http://gohugo.io
.. _`blog de PyBCN`: http://pybcn.org
.. _`Lektor`: http://getlektor.com
.. _`Entre Dev Y Ops`: https://github.com/EDyO/blog
.. _`GolangBCN`: https://github.com/GolangBCN/golangbcn.github.io/
.. _`PyBCN`: https://github.com/pybcn/pybcn.github.io
