---
title: "EditorConfig: Mantén tu código uniforme"
author: "Eduardo Bellido Bellido"
slug: "editorconfig-manten-codigo-uniforme"
date: 2013-11-21T22:25:00

tags: ["Herramientas", "Desarrollo", "Free Software", "Open Source"]
---

`EditorConfig`_ es un proyecto que parte de una idea muy simple, pero que resulta ser de gran utilidad. Básicamente se trata de un fichero con una serie de reglas que definen las normas de estilo que deben ser aplicadas al código. Este fichero es interpretado en el editor con un *plugin* que se encargará de ajustar la configuración para el código en cuestión.

<!--more-->


Esta herramienta nos permite mantener una uniformidad en el código sin tener que estar ajustando manualmente nuestro editor. Existen *plugins* para una gran variedad de editores, algo que, para proyectos *Free Software/Open Source* en los que normalmente tienen contribuidores de todo los rincones del planeta y que no tienen porqué trabajar utilizando el mismo entono. En definitiva, la herramienta permite de una manera cómoda mantener un mismo estilo en el código.

Ejemplos de tipos de reglas podemos definir:

- Tipo de sangrado: tabuladores o espacios
- Tamaño del sangrado
- Carácter utilizado para marcar el fin de línea
- etc.

Es posible también definir distintos estilos para los diferentes lenguajes que se estén utilizando, por ejemplo, en un proyecto web donde se utilice Python, HTML y Javascript, se podría tener estilos totalmente diferentes para cada uno. El formato es bastante sencillo y en el `sitio del proyecto`_ podéis encontrar más información sobre su sintaxis.

En el `wiki del proyecto`_ hay un listado de quién lo utiliza, destacando por ejemplo proyectos de la envergadura de **Drupal** o **jQuery**.

Si estáis interesados en probarlo, tenéis un listado con los `editores soportados`_ en su web, que no son pocos.

.. _`EditorConfig`: http://editorconfig.org
.. _`sitio del proyecto`: http://editorconfig.org/#file-format-details
.. _`wiki del proyecto`:  https://github.com/editorconfig/editorconfig/wiki/Projects-Using-EditorConfig
.. _`editores soportados`:  http://editorconfig.org/#download
