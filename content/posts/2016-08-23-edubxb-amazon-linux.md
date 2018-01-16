---
title: "Amazon Linux, ¿sí o no?"
author: "Eduardo Bellido Bellido"
slug: "amazon-linux-si-o-no"
date: 2016-08-23T19:55:00

tags: ["Amazon WS", "Cloud", "Infraestructura", "Linux", "Sistemas Operativos", "Opinión"]
---

<img src='/images/AmazonWebservices.png' alt='Amazon Web Services' class='align-left' height='80' width='200'/>

Seguro que todos los que usáis o habéis usado Amazon Web Services (AWS para abreviar) alguna vez habréis probado, o usado de forma productiva [Amazon Linux](https://aws.amazon.com/es/amazon-linux-ami/), la versión de Linux basada en RedHat/CentOS preparada por ellos y "equipada" para funcionar perfectamente en su servicio EC2.

Personalmente, mi predilección en cuanto a distribuciones tiende a las de la familia Debian, como la propia Debian o Ubuntu; es algo personal, quizás romántico, llevo muchos años con ellas y me siento más cómodo, no hay motivos técnicos que me liguen a ellas especialmente. A lo largo de mi carrera he trabajado con muchas distribuciones, y todas tienen cosas buenas y malas, no creo que exista la _silver bullet_ de las distribucciones de Linux, nada más lejos de la realidad. Quede claro que el objetivo de este artículo no es entrar en guerras o discusiones en si es mejor usar Debian, Ubuntu, RedHat o CentOS, el quid de la cuestión aquí es la existencia de Amazon Linux, con sus ventajes e inconvenientes. Así que vamos al lío.

<!--more-->


El principal problema en usar una versión de Linux como la de Amazon es la reproducibilidad, imaginemos que AWS no es nuestro único proveedor, o que no dependemos exclusivamente de proveedores _cloud_ y seguir utilizando nuestro propio _hardware_. Dada esta situación, tendríamos el inconviente (por decirlo suavemente) de no poder usar el mismo <abbr title="Sistema Operativo">SO</abbr> en todos los entornos, esto podría provocar que el comportamiento de nuestro servicio no sea el mismo según desde donde estemos prestando nuestros servicios, algo que podría convertirse en un infierno para diagnosticar, imaginad: parches propios, paquetes distintos, kernels a medida, configuraciones por defecto diferentes...

Otro problema, aunque quizás esto recae más en los respectivos mantenedores de las versiones de Linux disponibles para AWS, es que muchas veces no vienen con todos los paquetes instalados por defecto para funcionar _out of the box_ en EC2. Por pone algún ejemplo, podría ser que el paquete [cloud-init](https://cloudinit.readthedocs.io/) no venga instalado, o el <abbr title="Command line interface">cli</abbr> de AWS, muchas veces necesario para realizar acciones automatizadas. Más que ser un drama, es simplemente un inconveniente fácilmente salvable, pero que requiere trabajo, personalmente, creo que las versiones de Linux disponibles en el [_Marketplace_](https://aws.amazon.com/marketplace) de AWS, deberían venir con una base algo más completa dado el entorno en el que se encuentran.

La parte que a mi más me perturba en realidad, es la "magia" que muchas veces hace Amazon Linux, que no echas a faltar hasta que por algún motivo tienes la necesidad (o el requerimiento) de tener que utilizar otra versión de Linux. Pensaréis, nada que no sea adaptable/reproducible seguramente, por supuesto, pero volvemos a lo mismo, requiere más trabajo, y sobretodo, investigación, tendremos que investigar hasta descubrir que es lo que es necesario configurar para replicar el comportamiento que Amazon Linux tiene por defecto. Por poner un ejemplo, tenemos el paquete [ec2-net-utils](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html#ec2-net-utils), este paquete permite que las ENIs que son añadidas en caliente a una instancia EC2 se configuren automáticamente, sin intervención ninguna, algo que no ocurre por ejemplo si estuviéramos usando Ubuntu 12.04 LTS. Este paquete no está disponible en les repositorios de Ubuntu, con lo que `apt-get` no podrá salvarnos el culo en esta ocasión, pero para estos casos la comunidad está siempre para rescatarnos, y en esta ocasión una simple [búsqueda en GitHub](https://github.com/search?q=ec2+net+ubuntu&ref=searchresults&type=Repositories&utf8=%E2%9C%93) nos dará la solución.

Algo que también nos puede descolocar en algún momento es el [nombre de los discos de las instancias](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/device_naming.html) en función del tipo de virtualización que escojamos a la hora de iniciarlas, si optamos por el tipo _Paravirtual_ (modo en el cual el sistema virtualizado necesita un kernel modificado y unos controladores específicos para poder funcionar, este modo también se llama "virtualización ligera") no habrá problema, en cambio, si optamos por las de tipo <abbr title="Hardware Virtual Machine">HVM</abbr> (este modo podríamos decir que es de virtualización completa, el sistema anfitrión dispone de instrucciones _hardware_ que permiten al sistema virtualizado funcionar como si estuviera directamente sobre el _hardware_), la cosa se complica, en este caso, los dispositivos deberían llamarse `/dev/xvdX`, pero Amazon Linux, siempre pensando en el bien común y para hacernos la vida más fácil, crea enlaces simbólicos del tipo `/dev/sdX`, apuntando a los nombres anteriores. Esto no debería ser un problema, hasta que por algún motivo se empieza a utilizar otra versión de Linux y nuestros scripts, o herramientas de _configuration management_ utilizan los enlaces simbólicos para referirse a los discos, es aquí cuando empiezan las risas.

A pesar de todo esto, el trabajo que hace AWS es realmente bueno, disponemos de un sistema bastante actualizado y listo para usarse, lo que en cierto modo nos puede simplificar el trabajo, todo a cambio del "desconocimiento" (hasta que se descubre) de los detalles de configuración propios de esta versión de Linux.

Y después de todo este rollo, qué opináis... Amazon Linux, ¿sí o no?

