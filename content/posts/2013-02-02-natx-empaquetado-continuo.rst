---
title: "Empaquetado Contínuo"
author: "Ignasi Fosch"
slug: "empaquetado-continuo"
date: 2013-02-02T16:00:00

tags: ["FOSDEM", "Eventos", "Integración Contínua"]
---

====================
Empaquetado contínuo
====================

Maciej Pasternacki contó_ cómo, con componentes ya existentes y otros que ha creado él, se puede construir una cadena de empaquetamiento contínuo.

<!--more-->


El principal problema al que se enfrenta, es que necesita crear paquetes de instalación para distintos sistemas con todas las dependencias necesarias. Como hacerlo siguiendo las normas de cada distribución y método de empaquetamiento es altamente costoso, se ha creado un proceso utilizando las siguientes herramientas:

* Vendorificator_: Es una herramienta, creada por el mismo Maciej, para tener las dependencias de cada proyecto junto al mismo. Utiliza definiciones de los paquetes que se pueden compartir entre los proyectos.
* MetaRake_: Es una extensión de Rake que permite a éste encontrar módulos que necesitan ser compilados en el mismo repositorio del proyecto en el que está trabajando, compilándolos, incluyéndolos y vinculándolos al proyecto. También está creado por Maciej.
* Evoker_: La última herramienta que Maciej ha incluido, es otro complemento de Rake que permite descargar y gestionar dependencias externas de cada proyecto, parcheándolo o modificándolo como más convenga.
* FPM_: La siguiente herramienta, obra de `Jordan Sissel`_, es una utilidad bastante conocida que permite crear y convertir paquetes entre diferentes formatos y tipos, como por ejemplo, una gema de Ruby en un .deb instalable.
* Freight_: Ésta herramienta, creación de `Richard Crowley`_, sirve para mantener un repositorio de tipo Debian/Ubuntu.

.. _contó: https://fosdem.org/2013/schedule/event/continuous_packaging_pipeline/
.. _Vendorificator: https://github.com/3ofcoins/vendorificator
.. _MetaRake: https://github.com/3ofcoins/metarake
.. _Evoker: https://github.com/3ofcoins/evoker
.. _FPM: https://github.com/jordansissel/fpm
.. _`Jordan Sissel`: http://www.semicomplete.com/
.. _Freight: https://github.com/rcrowley/freight
.. _`Richard Crowley`: http://rcrowley.org/
