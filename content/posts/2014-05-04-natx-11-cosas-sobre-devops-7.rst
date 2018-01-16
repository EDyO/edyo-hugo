---
title: "11 cosas sobre DevOps (7): El valor de DevOps"
author: "Ignasi Fosch"
slug: "11-cosas-necesitas-saber-devops-7"
date: 2014-05-07T01:05:00

tags: ["Agile", "DevOps", "Empresa", "Entrega Contínua", "Integración Contínua"]
---

.. image:: /images/hands.png
   :alt: Valor
   :align: right

En el séptimo punto, `Gene Kim`_ explica el valor intrínseco de DevOps para la organización, expuesto a partir de los beneficios que la adopción de DevOps aporta, recopilados a partir de estudios, experiencias, conversaciones y sus propios libros.

A partir de los puntos en los que DevOps aporta valor, establece, para acabar, una relación primordial, básica y primaria por la que aplicar los principios de DevOps.

<!--more-->


7. ¿Cuál es el valor de DevOps?
-------------------------------

Creo [*]_ que las organizaciones que adoptan DevOps obtienen tres beneficios:

  * Reducción en el tiempo de comercialización, por ejemplo, con tiempos de ciclo más reducidos y ritmos de despliegue más altos.
  * Incremento de la calidad, a partir de mayor disponibilidad, incremento del ritmo de cambios exitosos, reducción de los fallos.
  * Incremento de la efectividad organizacional, basada en el incremento de la inversión del tiempo en las actividades que aporten valor, en lugar del gasto y, por lo tanto, incrementando la cantidad de valor que se ofrece al cliente.

Reducción en el tiempo de comercialización
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

En 2007, en el instituto `IT Process`_, se `realizó`_ un análisis comparando 1.500 organizaciones de IT, concluyendo que las organizaciones IT de alto rendimiento eran, en promedio, de 5 a 7 veces más productivas que el resto de las organizaciones. Realizaron 14 veces más cambios, con la mitad de fallos, de los que 4 veces más fueron resueltos al primer arreglo, y los tiempos de las incidencias de severidad 1 fueron 10 veces más cortos. También tenían 10 veces menos problemas encontrados repetidamente en auditorías, la probabilidad de detectar agujeros en el control interno automatizado era 5 veces menor, y la efectividad en cuanto a las fechas de entrega de los proyectos era 8 veces mejor.

Durante nuestra investigación, el ritmo de despliegue más alto fue 1000 cambios en producción por semana, con un ratio de éxito en los cambios del 99,5%. Nos pareció muy rápido...

Una de las características de las organizaciones de alto rendimiento es que se alejan mucho de la manada. En otras palabras, lo mejor continúa mejorando. Esto ocurre completamente en el área del ritmo de despliegue. Las organizaciones aplicando prácticas DevOps sobrepasan nuestro mejor ejemplo de alto rendimiento en órdenes de magnitud. Recientemente, Accenture realizó un estudio sobre lo que las empresas de Internet están haciendo, en el cual `Amazon`_ destacó al afirmar que despliegan más de 1000 veces al día, con un ratio de éxito del cambio del 99,999%. Podéis ver la `charla`_, o sus `diapositivas`_, que `Jon Jenkins`_ dió en la `Velocity`_ de 2011 sobre el modelo de despliegues y operaciones IT de `Amazon`_.

La capacidad de sostener ratios de despliegue altos, o lo que es lo mismo, tiempos de ciclo rápidos, se traduce en valor de negocio de dos formas: Aumentar la velocidad con la que el negocio puede pasar de una idea a la entrega del valor al cliente, y en cuántos experimentos la organización puede realizar simultáneamente.

No tengo ninguna duda de que si estoy en una organización que puede hacer sólo un despliegue cada nueve meses, y mi competencia puede hacer 10 en un día, tengo una desventaja competitiva estructural muy importante.

Ritmos de despliegue altos también permiten una experimentación rápida y constante. `Scott Cook`_, fundador de `Intuit`_, ha sido uno de los más ardientes defensores de una "cultura de la innovación desenfrenada" en todos los niveles de la organización. `Uno`_ de mis ejemplos favoritos es el siguiente:

  "Cada empleado debería ser capaz de hacer experimentos rápidos y a alta velocidad... `Dan Maurer`_ lleva nuestra división de consumo, incluyendo la operación del sitio de TurboTax. Cuando entró, realizábamos cerca de siete experimentos al año. Al instalar una cultura de innovación desenfrenada, ahora realizan 165 experimentos en la temporada de declaración de impuestos. ¿Resultado de negocio? El ratio de conversión del sitio web ha subido un 50%. ¿Resultado para los empleados? Ellos están encantados, porque ahora sus ideas llegan al mercado."

Para mí, la parte más impactante de la historia de `Scott Cook`_ es que estaban haciendo todos esos experimentos ¡durante el período de declaración de impuestos! La mayoría de las organizaciones congelan sus operaciones en las temporadas de mayor importancia. Pero si se consiguen incrementar los ratios de conversión, y por lo tanto, las ventas, durante esas temporadas, cuando la competencia no puede, eso se convierte en una ventaja auténtica.

Los prerequisitos para hacer esto incluyen ser capaz de hacer muchos cambios pequeños rápidamente, sin interrumpir el servicio a los clientes.

Cantidad de pérdida en IT
~~~~~~~~~~~~~~~~~~~~~~~~~

`Mike Orzen`_ y yo hemos hablado largamente sobre el enorme gasto en el flujo de valor de IT, causado por los largos plazos, pobres transferencias, mala planificación y reelaboración. En `un artículo`_ para `Michael Krigsman`_ estimamos cuánto valor se podía recuperar aplicando principilos como los de DevOps.

Calculamos que si podíamos acortar a la mitad el gasto en IT, y reinvertir ésos dólares de forma que generasen cinco veces lo que se había invertido, podríamos generar 3 billones de dólares por año en valor.

No deja de ser una cantidad asombrosa que estamos dejando que se escape entre nuestros dedos. Es un 4,7% del PIB mundial anual, o más que toda la producción económica de Alemania.

Creo que esto es importante, especialmente cuando pienso en el mundo que mis tres hijos heredarán. El impacto económico potencial, los estándares del nivel de vida y la prosperidad casi hacen de esto un imperativo moral.

Sin embargo, aún hay un coste mucho mayor. Trabajar en muchas organizaciones IT es a menudo desagradecido y frustrante. Mucha gente se siente atrapada en una película de terror que no deja de repetirse y impotente para hacer un cambio en la situación. La dirección abdica su responsabilidad en el correcto funcionamiento de IT, resultando en unas interminables guerras tribales entre los departamentos de desarrollo, operaciones IT, y seguridad informática. Cuando los auditores aparecen las cosas sólo pueden ir a peor.

Todo esto resulta, inequívocamente en un bajo rendimiento crónico. La vida de un profesional en IT es, a menudo, desmoralizante y frustrante, que lleva, normalmente, a los sentimientos de impotencia y estrés, que se acaban filtrando en cada aspecto de la vida. Incluyendo problemas de salud relacionados con el estrés, problemas de relación social o tensiones en el hogar, ser un profesional de IT no es sólo insalubre, sinó que además es insostenible.

Como personas, estamos hechos para contribuir y sentir que realmente marcamos la diferencia. Encima, cuando los profesionales IT piden soporte a sus organizaciones, a menudo son recibidos con un 'no lo entiendes' o, aún peor, con un apenas emmascarado 'no te importa'.

En `IT Revolution Press`_, nuestra misión es mejorar el nivel de vida de los que para 2017, serán 1 millón de trabajadores en IT. Esperamos que `When IT Fails: A Business Novel`_ pueda ayudar a los negocios y sus equipos de IT alcanzar la comprensión compartida del problema, y que `DevOps Cookbook`_ pueda ayudar a la gente a resolver el problema.

.. [*] La primera persona hace referencia al autor del original.

.. _`Gene Kim`: http://itrevolution.com/authors/gene-kim/
.. _`IT Process`: http://www.itpi.org/
.. _`realizó`: http://realgenekim.squarespace.com/visible-ops/
.. _`Jon Jenkins`: https://twitter.com/jonjenk
.. _`Amazon`: http://velocityconf.com/
.. _`charla`: http://www.youtube.com/watch?v=dxk8b9rSKOo
.. _`diapositivas`: http://assets.en.oreilly.com/1/event/60/Velocity%20Culture%20Presentation.pdf
.. _`Velocity`: http://velocityconf.com/
.. _`Scott Cook`: http://en.wikipedia.org/wiki/Scott_Cook
.. _`Intuit`: http://intuit.com
.. _`Uno`: http://network.intuit.com/2011/04/20/leadership-in-the-agile-age/
.. _`Dan Maurer`: http://about.intuit.com/about_intuit/executives/dan_maurer.jsp
.. _`Mike Orzen`: http://www.maorzen.com/
.. _`un artículo`: http://www.zdnet.com/blog/projectfailures/worldwide-cost-of-it-failure-revisited-3-trillion/15424
.. _`Michael Krigsman`: http://mkrigsman.com/
.. _`IT Revolution Press`: http://itrevolution.com/
.. _`When IT Fails: A Business Novel`: http://www.slideshare.net/lschwartz925/itsm-academy-whenitfailswebinar-august2012
.. _`DevOps Cookbook`: http://www.realgenekim.me/devops-cookbook/
.. _`#11cosasdevops`: https://twitter.com/search?q=%2311cosasdevops
