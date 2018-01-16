---
title: "SDN... NFV... ¿WTF?"
author: "Daniel Aresté"
slug: "sdn-nfv-wtf"
date: 2014-07-22T21:20:00

tags: ["Redes", "Virtualización"]
---

¿WTF? Esas serán probablemente las tres consonantes con las que alguien nos responderá si le empezamos a hablar de NFV. O puede que nos contesten “no tomo drogas, gracias“ si nos acercamos a contarle las bondades del SDN. En realidad, ambos grupos de consonantes son siglas relacionadas con una serie de conceptos en auge en el mundo del networking y muy cercanos a la filosofía DevOps, conceptos sobre los cuales queremos arrojar algo de luz con una serie de artículos que empezamos hoy. 

<!--more-->


Pero… ¿esto qué es?
===================

SDN *(Software Defined Networking)* y NFV *(Network Functions Virtualization)* son dos paradigmas que abogan por la automatización y la virtualización de la red, respectivamente. Estableciendo un símil con la ingeniería de sistemas, podríamos decir que SDN es el equivalente a la idea de gestión de la configuración que desemboca en herramientas como Puppet o Chef, mientras que NFV sería la tecnología de hipervisores.

Los conceptos en sí no son novedosos. Lo novedoso es dónde se aplican, ya que están provocando lo que probablemente sea el cambio conceptual más importante de los últimos 20 años en el mundo de las redes.

Divide y vencerás
=================

Dividir problemas complejos en subproblemas más simples y manejables es un método que funciona extraordinariamente bien en ingeniería, y ahora estamos ante otro ejemplo más. Tanto SDN como NFV persiguen dividir funciones.

La definición formal de SDN incide en ”separar la capa de control *(Control Plane)* de la capa de datos *(Data Plane)*”. Eso significa que un equipo de red diseñado bajo el paradigma SDN tiene que pensarse en dos módulos separados e independientes entre sí: por un lado, el hardware o software dedicado a manipular, enrutar o modificar los paquetes de datos que atraviesan el dispositivo; por otro, la interfaz a través de la cual definiremos el comportamiento del mismo.

En realidad no es más que separar el cómo del qué. Pensad un segundo en los motores de base de datos SQL. A través de un lenguaje declarativo (y estándar casi siempre) le decimos al motor de BBDD qué información queremos alterar o recuperar, y dicho motor se ocupa de cómo hacerlo de la forma más óptima posible sin que a nosotros se nos den detalles sobre ese proceso ni nos importe lo más mínimo (excepto si somos DBAs).

El mismo concepto de división se da con NFV. En este caso se persigue separar función y hardware mediante técnicas de virtualización, superando así el paradigma del *appliance*, bajo el cual los fabricantes de soluciones de networking siempre han entregado su producto como una combinación indivisible de hardware y software.

Abrazar el paradigma NFV es, de nuevo, subdividir tareas. Por un lado, la capa de hardware puede pensarse en términos de disponibilidad y sin tener en cuenta la función, y por contra la capa de software permite centrarse en la función con la tranquilidad de saber que la disponibilidad está garantizada.

La estandarización, la clave
============================

¿Tendrán éxito estos nuevos paradigmas, o quedarán en marketing vacío y buenas intenciones? Dependerá del nivel de estandarización que se alcance. Por mucho que hace cincuenta años se empezara a soñar con un mundo interconectado donde la información fluyera de extremo a extremo, no ha sido sino la adopción masiva de miles de estándares abiertos (como Ethernet, Wireless, IP, TCP, UDP o HTTP) los que han hecho posible que millones de dispositivos interoperen dando lugar al Internet que existe hoy.

En el próximo artículo hablaremos más en detalle sobre SDN, sus ventajas y desventajas, y los estándares que están surgiendo a su alrededor. ¡Hasta entonces!
