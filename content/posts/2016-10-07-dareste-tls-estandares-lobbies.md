---
title: "TLS: de estándares y lobbies"
author: "Daniel Aresté"
slug: "tls-estandares-lobbies"
date: 2016-10-07T23:00:00

tags: ["Seguridad", "Estándares"]
---

<img src='/images/b782e002-8ceb-11e6-8121-7860d9049fab.png' alt='TLS' class='align-right' height='100' width='150'/>

El grupo de trabajo de IETF encargado de crear la versión 1.3 de TLS lleva trabajando en él desde abril de 2014. 
Llevan ya [16 borradores], el último de este mismo septiembre, así que la publicación del estándar definitivo 
es cuestión de poco tiempo. Siempre que ciertos lobbies lo permitan, claro.

<!--more-->


TLS (Transport Layer Security) es el sustituto del antiguo SSL, cuyo uso ya no se recomienda por ser considerado inseguro. 
TLS regula el establecimiento de canales seguros en Internet; dicta cómo cliente y servidor se autentican mutuamente, 
cómo intercambian claves y qué algoritmo de cifrado van a usar. El ejemplo más ubicuo lo encontramos en https, que no es más
que http sobre un canal TLS.

Uno de los primeros puntos de [consenso] del grupo de trabajo del TLS 1.3 fue la eliminación de las suites de cifrado 
basadas en RSA. Sin entrar en detalles técnicos, lo que pretende el estándar es priorizar las suites de cifrado 
más modernas y seguras, que ofrecen [Perfect Forward Secrecy] (una característica que permite que, aunque 
un atacante comprometa las claves de una comunicación determinada, no pueda descifrar comunicaciones anteriores).

En este contexto (llegamos por fin a lo que me motivó a escribir esta entrada), el pasado 22 de septiembre 
se envió un interesante email a la lista de distribución del grupo de trabajo de TLS 1.3. 
[Aquí] tenéis el enlace original, y bajo estas líneas una traducción libre de los mejores fragmentos. No tiene desperdicio.

>Asunto: Preocupaciones de la industria respecto a TLS 1.3

>Mi nombre es Andrew Kennedy y trabajo en BITS, la división tecnológica de Financial Services Roundtable 
>(http://www.fsroundtable.org/bits). Mi organización representa aproximadamente 100 de las 150 mayores compañías 
>estadounidenses de servicios financieros incluyendo bancos, seguros, financieras domésticas y gestión de activos.

>(...)

>Soy consciente y apoyo totalmente la gran contribución que este grupo de trabajo ha realizado a favor de la seguridad 
>en Internet en estos últimos años. No obstante, he sabido recientemente de un cambio propuesto que afectaría a muchas 
>de las instituciones que forman parte de mi organización: la discontinuación del intercambio de claves RSA.

>Dicha discontinuación (...) causará problemas significativos en las instituciones financieras, la mayor parte 
>de las cuales utiliza TLS internamente y posee inversiones significativas en tecnologías de descifrado fuera de banda.

>(...) 

>A diferencia de otros sectores, las instituciones financieras se apoyan en el descifrado de tráfico TLS para implementar 
>monitorización de fraude y vigilancia de empleados supervisados. Los productos que soportan esas capacidades tendrán 
>que ser reemplazados o sustancialmente rediseñados con un coste y pérdida de escalabilidad significativos para poder 
>continuar soportando la funcionalidad que las instituciones financieras y sus reguladores requieren.

>El impacto en la supervisión será particularmente severo. A las instituciones financieras se les requiere por ley 
>almacenar las comunicaciones de ciertos empleados (incluyendo brokers/dealers) de forma que se asegure que puede 
>recuperarse y leerse en caso de que se inicie una investigación sobre comportamiento impropio.Las regulaciones que 
>requieren dicha retención de las comunicaciones se enfocaron inicialmente en correo físico y electrónico, pero ahora 
>se extienden a muchas otras formas de comunicación incluyendo mensajería instantánea, redes sociales y aplicaciones 
>colaborativas. Todas esas comunicaciones están protegidos por TLS.

>(...)

>Actualmente, las soluciones que ofrece TLS 1.3 a problemas como fuga de datos, detección de intrusiones, 
>mitigación de ataques de denegación de servicio, detección de malware, y monitorización de empleados regulados parecen 
>ser o bien inmaduras o directamente inexistentes.

>(...)

>Hasta que estos asuntos críticos relacionados con la seguridad corporativa, la supervisión de empleados y la visibilidad 
>de red sean solucionados (...) pido en nombre de nuestros miembros que el grupo de trabajo TLS 1.3 retrase esta decisión 
>hasta que se identifique y se examine una solución viable y escalable, y en última instancia se incluya en el estándar.

>Sinceramente,

>Andrew

Respuesta de [Kenny Patterson], uno de los miembros del grupo de trabajo:

>Asunto: Re: Preocupaciones de la industria respecto a TLS 1.3

>Hola Andrew,

>Mi opinión acerca de tu petición: no.

>Razón: estamos intentando construir un internet más seguro.

>Meta-comentario: 

>Llegas un poco tarde a la fiesta. Metafóricamente hablando, estamos ya vaciando los ceniceros y
>rebuscando entre las latas de cerveza medio vacías.

>Más en detalle, estamos ya en el borrador 15 y el transporte de claves RSA desapareció de las especificaciones 
>hace una docena de borradores. Sabía que en la banca sois un poquito lentos, pero esto se lleva la palma.

>Saludos, 

>Kenny

Dejando de lado el ¡zasca! nivel épico que nuestro amigo de la banca recibe, hay tanta chicha y subtexto en estos dos 
mails que no sé ni por dónde empezar. Lo voy a dejar aquí y sigo en los comentarios.

[16 borradores]: https://tools.ietf.org/html/draft-ietf-tls-tls13-16
[consenso]: https://www.ietf.org/mail-archive/web/tls/current/msg12266.html
[Perfect Forward Secrecy]: https://es.wikipedia.org/wiki/Perfect_forward_secrecy
[Aquí]: https://www.ietf.org/mail-archive/web/tls/current/msg21278.html
[Kenny Patterson]: http://www.isg.rhul.ac.uk/~kp/
