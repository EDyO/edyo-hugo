---
title: "Noticias semanales (Ene II y III)"
author: "Ignasi Fosch"
slug: "noticias-semanales-enero-2014-21"
date: 2014-01-19T19:45:00

tags: ["Eventos", "Python", "Chef", "Amazon WS", "DevOps", "Pruebas", "Monitorización", "TDD"]
---

.. image:: /images/Weekly-Newspaper.jpg
   :width: 213px
   :height: 141px
   :alt: La información semanal sobre lo que te interesa
   :align: left
   :class: border

Como la semana pasada no se publicaron noticias, las hemos unido, por lo que en esta entrega, tenemos bastantes noticias: La publicación del manual del administrador de `Debian`_, una nueva librería para gestionar recursos en EC2_ desde Python, una presentación sobre Flapjack_, otra para hacer pruebas sobre navegadores con JavaScript, otra plataforma de monitorización que se integra con Graphite_ y Jenkins_, otra más que permite exponer un directorio con guiones de *bash* como API REST, y la adición de nuevas localizaciones a los servicios de CloudFront_ y `Route 53`_.

<!--more-->


El manual de administrador de Debian disponible
-----------------------------------------------

Aunque es una noticia un poco anterior, tiene una importancia considerable: Se ha publicado el `manual del administrador de Debian`_. Este manual, escrito por dos desarrolladores de Debian, Raphaël Hertzog y Roland Mas, está disponible para `leer en línea`_ o `descargarlo`_, aunque también se puede bajar el fuente y `contribuir`_.

La librería ec2: la guinda del pastel sobre boto
------------------------------------------------

La `librería ec2`_ es un añadido a la librería `boto`_ para facilitar la gestión de instancias en EC2 y de los grupos de seguridad. Su principal aportación es que facilita la interacción con las instancias ofreciendo APIs un poco más sencillas que `boto`_.

Conoce Flapjack un poco más
---------------------------

Aunque ya habíamos hablado de Flapjack_ en las noticias anteriores, se publicó esta `presentación`_ que introduce un poco más las funcionalidades del producto.

DalekJS, una librería para testear sobre todos los navegadores
--------------------------------------------------------------

DalekJS_ es una librería JavaScript que permite ejecutar pruebas de interfaz que permite lanzar y automatizar el navegador, rellenar y enviar formularios, actuar sobre botones y enlaces, obtener capturas de pantalla y ejecutar tests funcionales. Funciona para Windows, Linux y Mac.

Cabot, otra herramienta de monitorización, pero un poco distinta
----------------------------------------------------------------

Cabot_ es otra plataforma de monitorización, pero que suma algunas de las mejores funcionalidades de PagerDuty_, `Server Density`_, Pingdom_ y Nagios_. Una de sus funcionalidades es que se puede integrar con otras herramientas de monitorización, como Graphite_ o statsd_.

Pyjojo, pon tus mejores herramientas accesibles
-----------------------------------------------

Para aquellos que recopilen guiones en *shell* que les permiten hacer un buen lote de tareas sólo con ejecutarlos, le puede parecer interesante utilizar pyjojo_ para ponerlos accesibles como API HTTP.

Nuevas localizaciones para CloudFront y Route 53
------------------------------------------------

Amazon CloudFront_ y `Route 53`_ inauguran nuevas localizaciones en Taipei y Rio de Janeiro.

Webinar sobre la transformación en Adobe con Enterprise Chef
------------------------------------------------------------

Aquellos que estén interesados en la versión *enterprise* de Chef_ podrían tener interés en asistir al webinar_ que se celebrará el próximo día 23 de enero, sobre cómo *Enterprise Chef* ha cambiado la presencia de Adobe en la nube.

.. _webinar: http://pages.getchef.com/adobe_enterprisechef_webinar.html?mkt_tok=3RkMMJWWfF9wsRonuq%2FKZKXonjHpfsX87esrX7Hr08Yy0EZ5VunJEUWy2YQJSNQ%2FcOedCQkZHblFnV4NT62jWqINqKMF
.. _pyjojo: https://github.com/atarola/pyjojo
.. _statsd: https://github.com/etsy/statsd/
.. _Nagios: http://nagios.org
.. _Pingdom: http://pingdom.com
.. _`Server Density`: http://serverdensity.com
.. _PagerDuty: http://pagerduty.com
.. _Cabot: https://github.com/arachnys/cabot
.. _DalekJS: http://dalekjs.com
.. _`presentación`: https://speakerdeck.com/auxesis/finding-signal-in-the-monitoring-noise-with-flapjack
.. _`boto`: https://github.com/boto/boto
.. _`librería ec2`: https://github.com/mattrobenolt/ec2
.. _`Debian`: http://debian.org
.. _EC2: http://aws.amazon.com/es/ec2/
.. _Flapjack: http://flapjack.io/
.. _Graphite: http://graphite.wikidot.com/
.. _Jenkins: http://jenkins-ci.org
.. _CloudFront: http://aws.amazon.com/es/cloudfront/
.. _`Route 53`: http://aws.amazon.com/es/route53/
.. _`manual del administrador de Debian`: http://debian-handbook.info/
.. _`leer en línea`: http://debian-handbook.info/browse/stable/
.. _`descargarlo`: http://debian-handbook.info/get/
.. _`contribuir`: http://debian-handbook.info/get/
.. _Chef: http://www.getchef.com/chef/
