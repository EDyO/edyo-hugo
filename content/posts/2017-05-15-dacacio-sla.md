---
title: "El SLA del Cloud"
author: "David Acacio"
slug: "sla-cloud-aws-azure"
date: 2017-05-17T13:35:00

tags: ["Cloud", "SLA", "AWS", "Azure", "Amazon", "Microsoft"]
---

<img src='/images/743e78a4-370b-11e7-9d3d-e8321c7d49c9.jpg' alt='SLA' class='align-left'/>

A raíz del incidente de [AWS S3 del pasado 28 de Febrero](https://aws.amazon.com/es/message/41926/)  he oído, y no en pocas ocasiones, frases del estilo “pero esto del cloud no se caía, no?”, “hasta el cloud tiene caídas de servicio” y similares. 
Si hablamos con personas que conozcan que es el cloud seguramente tendrán una opinión similar: una de las ventajas de migrar hacia el cloud es que nunca tendrás caídas de servicio. 

Lamentablemente eso no es del todo verdad y las empresas que ofrecen servicios de cloud lo saben.

<!--more-->


Si bien es cierto que con un buen diseño de infraestructura podemos minimizar el riesgo de pérdida de servicio, todo proveedor sabe que existe una posibilidad de indisponibilidad y se indica a nivel contractual con el [SLA](https://en.wikipedia.org/wiki/Service-level_agreement). Para mí, el sla es cuánto se fía nuestro proveedor de su infraestructura y el compromiso que está dispuesto a asumir con sus clientes así como las compensaciones (normalmente económicas).

He querido revisar el SLA ofrecido por los líderes actuales en IaaS, que según gartner son Amazon y Microsoft:

<img src='/images/743c5f88-370b-11e7-9959-272f9beae788.png' alt='SLA' width=80% class='align-center'>

## Amazon

>### EC2
>
>El popular servicio de máquinas virtuales de Amazon ofrece un **[SLA del 99.95%](https://aws.amazon.com/es/ec2/sla/)**. Utilizando una [calculadora online de SLAs](https://uptime.is/) vemos que Amazon puede **dejar de darnos servicio durante 4 horas y 23 minutos al año** sin que tenga ningún tipo de penalización.
>
>
>### RDS
>
>Sobre el servicio de base de datos de AWS ofrece **[el mismo acuerdo de servicio que EC2 (99.95%)](https://aws.amazon.com/es/rds/sla/)**. 
>
>
>### S3
>
>El storage de AWS, que sirve de base para muchos servicios de Amazon, [tal como pudimos verificar con el incidente de Febrero](https://aws.amazon.com/es/message/41926/), tiene un nivel de servicio inferior a EC2 y RDS, cosa que me ha sorprendido. El **[SLA del S3 es del 99.90%](https://aws.amazon.com/es/s3/sla/)**, así que estaríamos hablando de **casi 8 horas y 46 minutos de indisponibilidad al año**. 
>
>
## Azure 

>### Virtual Machines
>
>Por parte de Microsoft vemos que **[garantiza el servicio de máquinas virtuales en un 99,95%](https://azure.microsoft.com/en-us/support/legal/sla/virtual-machines/v1_0/)** similar a EC2.
>
>
>### SQL Database
>
>La base de datos de Microsoft en este caso no coincide con Amazon. El nivel de servicio que nos ofrece **[Azure SQL Database es del 99,90%](https://azure.microsoft.com/en-us/support/legal/sla/sql-database/v1_0/)**.
>
>
>### Storage
>
>El storage de Microsoft vemos que también tiene el **mismo SLA que el storage de S3, un [99,90%](https://azure.microsoft.com/en-us/support/legal/sla/storage/v1_0/)**.
>
>
## Conclusiones

Os hago un pequeño resumen en una tabla:

<img src='/images/7b06ed92-407a-11e7-8478-ec88fce16a49.png' alt='SLA' class='align-center'>

Os recomiendo que dentro de cada página del SLA de cada servicio , echéis un vistazo a la manera de realizar el cálculo de dicho SLA, porque habitualmente se tienen en cuenta varias variables, no únicamente el uptime de los servicios. Si esto es positivo o negativo lo dejo a vuestro criterio.

Como conclusión decir que los niveles de servicio que ofrecen ambos proveedores en sus principales productos son muy parecidos. Aquí la clave es valorar el coste de generar una infraestructura que nos cubra sobre estas posibles indisponibilidades contra el beneficio que obtendríamos teniendo nuestra infraestructura funcionando durante ese periodo. 
