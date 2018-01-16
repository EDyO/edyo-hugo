---
title: "Comparando Serverless"
author: "Javier Arellano"
slug: "comparando-serverless"
date: 2017-03-16T03:14:00

tags: ["Servesless", "Amazon WS", "Azure"]
---

El líder indiscutible del cloud es AWS, pero tiene un competidor que le sigue de cerca. Bueno, siendo realistas no tan de cerca, pero que se ha acercado mucho en estos últimos tiempos.

Hemos visto el avance de [Lambda](https://aws.amazon.com/es/lambda/details/), y como pasó de ser un anuncio en el re:Invent del 2014, a ocupar varias charlas en el re:Invent del año pasado. Teniendo en cuenta que ahora mismo, tenemos el sistema distribuido entre: el lambda de siempre, en el [snowball](https://aws.amazon.com/es/snowball/details/) y próximamente en  la ejecución lambda de los [nodos edge de cloudfront](https://pages.awscloud.com/lambda-at-edge-preview.html)  y en los productos que usen [AWS Greengrass](https://aws.amazon.com/es/greengrass/),  pero la pregunta es: ¿cual es la herramienta de Azure para combatir Lambda?

<!--more-->


Azure tiene 2 servicios que son denominados serverless [Functions](https://azure.microsoft.com/es-es/services/functions/) y [Logic Apps](https://azure.microsoft.com/es-es/services/logic-apps/)

Funtions es una aproximación más cercana a lambda ya que los dos ejecutan funciones en cambio LogicApps, recuerda más a un workflow de [IFTTT](https://ifttt.com).

El funcionamiento de LogicApps se basa en un entorno visual donde se encadenan conectores con actuadores, por ejemplo: si aparece un fichero nuevo en un SFTP conectarme a [Trello](https://trello.com) añadir una nueva tarjeta, y enviar un mail. Esta orientado a la facilidad de conectividad con distintos servicios.

Funtions es un sistema mucho más similar a Lambda. Soporta: JavaScript, C# y F#, Python, PHP, Bash, Batch y PowerShell. Mientras que Lambda soporta: Java, Node.js, C# y Python oficialmente, aunque de forma no directa se pueden ejecutar múltiples lenguajes como comenta David en el artículo: [Ejecutando shell script en AWS Lambda](http://www.entredevyops.es/posts/shellscript-lambda.html)

Lambda tiene como disparadores los siguientes eventos: S3, DynamoDB, Kinesis Streams, SNS, SES, Cognito, CloudFormation, CloudWatch Log, CloudWatch Events, CodeCommit, Scheduled Events , AWS Config, Amazon Echo, Amazon Lex y Amazon API Gateway

Y Azure tiene los siguientes eventos: Temporizador, petición http, Blob storage, Azure Event Hubs, Azure Storage queue, Azure Service Bus.

Con estos disparadores tanto Azure directamente, como Lambda a través de API Gateway pueden servir páginas desde serverless.

Otro de los puntos a revisar son los recursos usados por Lambda que van desde los 128 MB a los 1.5Gb. De la misma forma que Azure, aunque estos han cambiado el calculo de recursos desde  noviembre pasado, por lo que no se ha de calcular el tamaño de memoria de las ejecuciones sino que son calculadas y cambiadas [automáticamente](https://blogs.msdn.microsoft.com/appserviceteam/2016/11/15/making-azure-functions-more-serverless/).

Uno de los problemas que plantea AWS es que no siempre el menor consumo de RAM es más barato, ya que las peticiones de más RAM se ejecutan en maquinas más rápidas , por lo que si se tiene un proceso que tarda 10 segundos en 128Mb de RAM es un consumo de 1280Mb , en cambio si lo ejecutamos en 320Mb y tarda 2 segundos el consumo es de 640Mb. Más información en [esta página](https://serverless.zone/my-accidental-3-5x-speed-increase-of-aws-lambda-functions-6d95351197f3#.xcf9f6af3)

El precio es un factor que no tenemos que despreciar pero es muy difícil de asegurar ya que los cálculos son complejos de realizar sin saber el consumo de memoria por segundo que vamos a realizar. Los precios extraídos de las páginas web se puede ver que son muy similares.

Azure cuesta €0,000013/GB/s pero dan 400.000 GB/s gratis al mes y aparte del gasto de recursos también se cuenta 0,17€ por millón de ejecuciones (el primer millón al mes gratuito).

La capa gratuita de Lambda comprende un millón de solicitudes gratuitas al mes y 400 000 GB/segundo de tiempo de computación al mes. A partir de ahí, 0,20 USD por cada millón de solicitudes.

Como resumen: sobre papel los entornos son muy similares. La ventaja que AWS puede tener al ser los primeros puede estar siendo recortada con la implantación de las LogicApp (que son visuales), o con el debug remoto en Functions a través de Visual Code.

Espero vuestros comentarios.
