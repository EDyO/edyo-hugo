---
title: "El fondo de armario de un ingeniero"
author: "Daniel Aresté"
slug: "fondo-armario-ingeniero"
date: 2016-07-04T12:00:00

tags: ["Full Stack Engineer", "Básicos", "Herramientas"]
---

Mi mujer siempre me repite, medio en broma medio en serio, que visto como si cobrara la mitad de lo que cobro. Es un buen resumen de mi sensibilidad hacia el mundo de la moda, y os debería dejar claro que, a pesar del título, este post no va a tratar sobre imagen personal. 

<!--more-->


El concepto 'fondo de armario' se refiere a todas aquellas prendas que resisten el paso del tiempo y las modas, y siguen siendo tan útiles y actuales como el primer día que las compramos. Alguna vez he oído también referirse a este tipo de prendas como 'los básicos'. El fondo de armario del que quiero hablaros, no obstante, no contiene ropa.

No podemos negar que, en el mundo IT, los paradigmas y las herramientas se suceden a velocidad de vértigo. Nos hemos ido del CPD a la nube, y parece que acabaremos en computación serverless; hemos viajado del servidor físico al virtual, siguiendo por containers y  yendo hacia el unikernel; las arquitecturas monolíticas ya no nos gustan y apostamos por los microservicios; hemos dejado de configurar cosas manualmente para automatizar y utilizar control de versiones. 

¿Cuáles son entonces los 'básicos' de un `ingeniero Full Stack`_? ¿Cuáles son los conocimientos, recursos y herramientas que nos funcionan en la actualidad pero que, además, resistirán el paso del tiempo y las modas, y que siempre van a ser transferibles al nuevo paradigma que estará esperándonos a la vuelta de la esquina?

Esta es mi lista, sin ningún orden en particular:

- **Linux**. No se puede negar el éxito de Linux en la parte servidor (o, si queremos ser más precisos en los tiempos que corren, en el lado de los servicios). No parece que esto vaya a cambiar en breve, así que entender sus fundamentos y conocer sus herramientas de línea de comandos más populares parece imprescindible. Yo ya no puedo ni siquiera recordar cuánto tiempo llevo utilizando herramientas como vi, awk, sed, grep, tail o cat. 

- **El protocolo HTTP**. Las APIs se han convertido en algo ubicuo en el presente mundo de recursos distribuidos y con alto grado de abstracción, y HTTP en su sintaxis de facto. Conocer los métodos o verbos HTTP, saber distinguir las partes de una URI, entender los códigos de respuesta HTTP y su significado, o saber cómo usar e interpretar las cabeceras HTTP más habituales, nos garantizan poder interactuar con prácticamente cualquier servicio API existente o futuro.

- **Algorítmica y estructuras de datos**. En un mundo caracterizado por cada vez más altos requerimientos de escalabilidad y donde (de nuevo) los recursos están distribuidos, ciertas bases de algorítmica son imprescindibles. Entender cómo funciona y se construye un B-tree, qué ventajas tiene almacenar información en una Hash List, qué significa que el tiempo de ejecución de un algoritmo es o(log n), o cómo funciona y para qué se usa un algoritmo de consenso; todo ello es clave para entender el funcionamiento y evaluar el rendimiento de cualquier servicio moderno.

- **Programación**. Independientemente del lenguaje, tener la capacidad de transformar una secuencia de acciones concretas en una lista de instrucciones ejecutables es cada vez más imprescindible, no solamente para automatizar y reducir errores manuales, sino para desenvolverse en un mundo donde la interacción con los servicios ya no funciona a golpe de interfaz gráfico o línea de comandos, sino a través de las ya mencionadas APIs.

¿Encontráis algo que falte o sobre? ¿Cuál sería vuestra lista? Sigamos el debate en los comentarios.

.. _`ingeniero Full Stack`: http://www.entredevyops.es/posts/full_stack_engineer.html
