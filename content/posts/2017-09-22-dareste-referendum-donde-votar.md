---
title: "Referendum 1-O: ¿Dónde votar?"
author: "Daniel Aresté"
slug: "referendum-votar"
date: 2017-09-22T22:00:00
tags: ["Seguridad", "JavaScript"]

---

<img src='/images/30765928-56c56350-9ff2-11e7-85a8-cc8fad0d7947.jpg' alt='yes-no' class='align-left height='200' width='200'/>

No, no nos hemos vuelto locos, en Edyo seguimos hablando de tecnología. Sabemos también que últimamente no publicamos más que podcasts; a pesar de ello, mantenemos el blog para cosas que se cuentan mejor escritas que narradas. Hoy os traemos un análisis técnico que no puede ser más de actualidad: la web de consulta del censo para el referendum del 1-O. Os prometo que vale la pena.

<!--more-->


Hace apenas un par de días que ha empezado a circular, sobre todo por redes sociales y de mensajería, la URL para que los ciudadanos consulten el colegio electoral que tienen asignado en el referendum del día 1 de Octubre:

[https://onvotar.garantiespelreferendum.com/on-votar/index.html]

En la página encontraréis un formulario donde, introduciendo DNI, fecha de nacimiento y código postal, podemos consultar la mesa electoral que nos corresponde. Hay ciertas cosas que no puedo evitar en esta vida: pedir tiramisú de postre si lo veo en la carta, llevar la contraria, y esnifar tráfico de red cuando hago submit en un formulario.

En este caso, un primer vistazo nos indica que las cosas parecen estar haciéndose bien: la web dispone de un certificado SSL emitido por Comodo, y SSLlabs le otorga la máxima nota (grado A) en todos sus tests:

[https://www.ssllabs.com/ssltest/analyze.html?d=onvotar.garantiespelreferendum.com]

¡Bien por los admins! Podemos estar tranquilos, los datos personales que mandemos van a circular por un canal seguro. No obstante, sigo queriendo ver dónde y cómo se mandan mis datos al hacer click en el botón de buscar. Preparo el escenario: abro las [Chrome Developer Tools], relleno mis datos, pulso el botón de buscar. Bien, la web me responde con los datos del colegio electoral donde siempre me toca ir. No obstante, al echarle un ojo al tráfico http capturado llegan las primeras sorpresas...

## ¿Dónde están mis datos?

Estoy muy acostumbrado a ver un `POST` como forma estándar de subir datos hacia un servidor. En este caso, no obstante, no veo aparecer más que un solitario `GET` en mi pantalla al hacer submit del formulario... No es tan habitual, pero subir información a través de una petición `GET` incorporando los datos en variables en la propia URL, o quizás en cookies, también es una práctica común. Echémosle un ojo a esa petición:


```
Request URL:https://onvotar.garantiespelreferendum.com/db/c3/a1.db
Request Method:GET
Status Code:200
Remote Address:104.18.36.145:443
Referrer Policy:no-referrer-when-downgrade
Origin:null
User-Agent:Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36
```

Un momento. ¿Y mis datos? No están en la URL. No hay ninguna cookie en la petición. No hay ninguna cabecera http fuera de lo normal. Y además, esa URI tan extraña.... `/db/c3/a1.db`. Pruebo a cargarla y obtengo lo siguiente:

```
1febc7fc1f60ae314b424303ea516a290f305a36c0bab4f3dbc98d810f2ee162e59878057968a22bbaa69a9dc066414f1506a8d10dfa1d73130b3ee2f4bf9037c7ab8642528c9b0c5c157b4ea0dd9bbb1815c5b2bd4519852e59c4bac040599db36127f0f52530b7f45455f9d4fa55798a9918a65391c49a0181c677da360346da22e7b0c33b05bfcbb55a4ee75820fe1f9fbdd532b40ccac4c6ba85d610679b66bad2a43fbb2a418eec58c4772a42113b3fa25052c2435c5c4a5ffe8bcaf2896d220eaa4c446f19c62b26ccefd3
e4d353eeb673c351f84276fb8c159381ff641775b9e0a17925245f39bedd33661212588b3ca926ee31a49859055f901382279a24c291076660b3e80e65de8ec66e948bc64b5120ae09dd56f955302e1323ef8afdd29143269f2b7c3a8e6c02ebc70d0c9d949092ca19246d5cba3b0c69c314bf7d7a4222326fd7b78c8768e029e4e5ef1175ed5dd457ce3fc88840f9ce941eeb2bd28521ac5eb8be1be9faf1b40ee3f2f81683be3c3a93f1b806aaa5ff7761b873a725ff470a67983d3d827bbbdfcb228c4ec505b4347945c39ab9
2fd03efea47e19d24331a4b6b0ffa9988efda433d5ad5a31c10d2b0b849ee2013e7be6ccb75336147a600c7f542b702289d843d683156797e32e360a5e96f499c0350ba3de76fbe91694463381b9ff1fbf4820ab215b03da5cf604b5523530c9d21ca7f84e150e8ad3cd08d06f05c6cf81c9e87ee49ee60d709496a1ca35a5a742992cb9736bcbf64295a0103b44c3cb7ea0e923a0a1bd3540abb6a0ec78bf56f94967b2ec92ab8000bec75d4dddcb12f0651d062693c068714cd449e45692eb3ef3821db6c1302ff5e57d572d1d
...
```
Decenas de líneas con strings de lo que parece ser hexadecimal, y de ancho fijo (412 caracteres exactamente). Sr. Puigdemont, definitivamente ha captado usted mi atención.

## El referendum serverless

Ya lo dijo Mahoma: si mis datos no viajan al servidor, tiene que ser el 'servidor' el que viaja hacia mis datos. Efectivamente, parece que estamos ante un caso de contenido estático en servidor y proceso de datos en local. ¿Alguien ha dicho Javascript?

¡Bingo! En `index.html` tenemos a la madre del cordero:

```
<script type="text/javascript" src="../js/bundleV9.js"></script>
<script type="text/javascript">
function calcula() {
  document.querySelector("#stepLoad").style.display="inline"
  var dni = document.querySelector("#dni").value
  dni = dni.replace(/ /g,'').replace(/-/g,'').replace(/\./g,'');
  var dn_dia = document.querySelector("#dn_dia").value
  var dn_mes = document.querySelector("#dn_mes").value
  var dn_any = document.querySelector("#dn_any").value
  var cp = document.querySelector("#cp").value
  if (dn_dia.length == 1)
     dn_dia = "0"+ dn_dia
  if (dn_mes.length == 1)
     dn_mes = "0"+ dn_mes
  if (dn_any.length == 2)
     dn_any = "19" + dn_any
  onvoto.calcular(dni.slice(-6),dn_any+dn_mes+dn_dia,cp, function(i) {
    document.querySelector("#stepLoad").style.display="none"
    if (( typeof i === 'string' ) && ( i == 'not-found' ))  {
        document.querySelector("#response").innerHTML = "No s'ha trobat cap registre corresponent a les dades introduïdes."
    } else {
       document.querySelector("#stepOne").style.display="none";
       document.querySelector("#response").innerHTML = i[0] + "\n" + i[1] + "\n" + i[2] + "\n\n"
                                                     + "Districte:" + i[3] + "\n" + "Secció:" + i[4] + "\n"
                                                     + 'Mesa: ' + i[5];
    }
   })
}
</script>
```
Esencialmente, esta pieza de código recoge nuestros datos (DNI, fecha de nacimiento y código postal), los normaliza (reescribe la fecha en formato AAAAMMDD, por ejemplo) y los pasa a la función `onvoto.calcular`. Esta función devuelve la información de la mesa electoral lista para mostrar o, en su defecto, el string 'not-found' que aparentemente indicaría que no se han encontrado coincidencias.

Nuestro siguiente paso debe ser analizar lo que ocurre en `onvoto.calcular`, cuyo código podremos encontrar en el fichero `/js/bundleV9.js`.

## Los ficheros del censo

Nuestra misteriosa función empieza en la línea 69058 del mencionado fichero, y enseguida empezamos a entender de qué va todo esto (puntos suspensivos indican partes no relevantes omitidas):

```
var calcular = function (d, dn, cp, cb){
    ...
    var key = dni + data_naixement + codi_postal;
    var firstSha256 = hash(bucleHash(key,BUCLE));
    var secondSha256 = hash(firstSha256);
    var dir = secondSha256.substring(0,DIRSHA);
    var file = secondSha256.substring(DIRSHA,DIRSHA+FILESHA);
    var url = window.location.href.replace('/index.html','/');
    ...
    url += '../db/' +dir + "/" + file + FILEEXTENSION;

    request( url, function (error, response, body) {
    ...
```

La función toma nuestros datos y los concatena en la variable `key`. A partir de ese valor, crea dos hashes SHA256 (si seguís las funciones a las que se llaman, veréis que el primero se calcula realizando un bucle de hashes de ¡1714 iteraciones! - guiño guiño) y los almacena en `firstSha256` y `secondSha256` en formato hexadecimal. Y aquí empezamos a entender ciertas cosas: las siguientes líneas construyen la misteriosa URI `/db/xy/zw.db` a partir de los cuatro primeros caracteres de `secondSha256` (dos para la carpeta y dos para el nombre del fichero). Una vez construida la URI, la función `request` se encarga de hacer la petición http correspondiente para descargarla.

Resumiendo lo anterior, estamos ante una especie de database sharding: a partir de nuestro dni, fecha de nacimiento y código postal se construye una URI única a través de la cual se descarga un fichero que supuestamente contiene la información que solicitamos.

Aquí se me activa de inmediato mi sentido arácnido. Ese fichero debe contener no solo mis datos censales sino los de muchas otras personas. El hecho de que haya decenas de líneas hace pensar en un registro/censo por línea, y por otro lado el hecho de truncar el mapeo a cuatro caracteres hexadecimales hace inevitable que se produzcan colisiones.

De hecho, unos cálculos rápidos nos revelan que efectivamente estamos en el caso de un registro censal por línea. Cuatro caracteres hexadecimales nos ofrecen 16^4 combinaciones, o ficheros existentes. Empíricamente he observado unos 70 registros por fichero de media, así que podemos estimar un total de
algo más de 4.5 millones de registros (que bien podría ser el número de catalanes en edad de votar en Catalunya).

De hecho, no es difícil construir un script que recorra el espacio muestral que va de `/db/00/00.db` a `/db/ff/ff.db` y descargar los cuatro millones y medio de registros en no demasiado tiempo. Esto debería ponernos inmediatamente en alerta: ¿acabamos de descargar datos del censo de todos los catalanes en edad de voto? ¿Qué datos contienen exactamente esos ficheros y en qué formato? ¿Va la Guardia Civil a llamar a mi puerta en breve?

Para responder a las preguntas anteriores, sigamos investigando qué es lo que la función `onvoto.calcular` hace con ese fichero una vez descargado.

## Gracias, criptografía

El cuerpo de la función `request` es el siguiente:

```
      var found = false;
      if (error){
        console.log("Error: " + error);
        return;
      }
      var info = body.split("\n");
      info.forEach(function(line){
        if (line.substring(0,60) == secondSha256.substring(4)){
          var info = decrypt(line.substring(60),firstSha256).split('#');
          found = true;
          cb(info);
        }
      })
      if (!found) {
        cb("not-found");
      }
```

La función es básicamente un bucle donde se analiza cada línea del fichero. Si los 60 primeros caracteres hexadecimales coinciden con los 60 últimos caracteres de `secondSha256` (recordad que son 64 en total y los 4 primeros se usaban para construir la URI), aplicamos la función `decrypt` al resto de la línea, y el resultado lo devolvemos por callback en forma de array. Si no hay coincidencia, pasamos a la siguiente línea, y si se acaban las líneas contestamos con un 'not-found'.

Por lo que parece, cada línea de registro no es más que un mapa clave - valor: la clave es un hash de nuestros datos personales, y el valor sería una cadena encriptada con los datos censales. Si seguimos la implementación de la función `decrypt`, veremos que la cadena está cifrada con criptografía de clave simétrica, concretamente `aes-256-cbc`. Cifrado de grado militar.

¿Y cuál es la clave? Pues lo vemos en los parámetros de la llamada: `firstSha256`. Recordemos que esta cadena es el resultado de aplicar sha256 1714 veces recursivamente a la cadena dni+fechanacimiento+codigopostal, algo realmente imposible de revertir. Nuestros datos personales están en los ficheros, pero en forma de hashes irreversibles.

## Datos censales

Prestad de nuevo atención a la línea donde desencriptamos:

```
var info = decrypt(line.substring(60),firstSha256).split('#');
```

Y refresquemos ahora la sección que recoge esos datos y los pinta en el html original:

```
document.querySelector("#response").innerHTML = i[0] + "\n" + i[1] + "\n" + i[2] + "\n\n"
                                              + "Districte:" + i[3] + "\n" + "Secció:" + i[4] + "\n"
                                              + 'Mesa: ' + i[5];
```

La cadena desencriptada contiene varios campos (al menos seis, numerados del cero al cinco), donde la almohadilla actúa de separador. Se puede comprobar fácilmente que los campos, en orden, son los siguientes: nombre del colegio electoral, dirección, población, distrito, sección y mesa. Aún así, quise echarle un vistazo al string original. Descargué el fichero js original, añadí un `console.log` para que me mostrara la cadena desencriptada, hice unas llamadas en local y...

... otra sorpresa. Hay un séptimo campo que no se muestra en el html de resultado. Esto es lo que me muestra mi consola javascript de Chrome:

```
0:"ESCOLA PUBLICA xxxxxxxxx"
1:"[Direccion postal]"
2:"[Poblacion]"
3:"1"
4:"1"
5:"0A"
6:"cb6e1fbbb81e69d9d213e80bebaf946fe3b2520a2c9eb4a0f4cbb72de1a5d0a530556d98d91ee63ac6ddca456388856f7bf01s03"
length:7
```

El campo número 6 es una cadena hexadecimal de 105 caracteres. No se repite en el resto del fichero. He intentado infructuosamente desencriptarla usando la misma clave simétrica que desencripta los campos anteriores, pero no muestra nada con sentido. Y aquí me rindo, amigos lectores; si habéis llegado hasta aquí os animo a que continuéis la investigación y desveléis qué puede significar este séptimo campo.

## Conclusiones

El diseño de la web del referendum es francamente ingenioso, y merece mi más sincero aplauso. El creador ha logrado una arquitectura con contenido estático que no depende de backends para funcionar, ya que traslada toda la lógica al lado cliente con javascript. A la vez, ha logrado almacenar datos sensibles de una forma criptográficamente segura y sin penalizar eficiencia gracias a una ingeniosa técnica de sharding. La arquitectura claramente responde a la necesidad de replicar la web de una forma rápida y funcional ante las más que previsibles órdenes judiciales de bloqueo de hostings que irán llegando.

Y por último, si por casualidad eres uno de los diseñadores y este post ha llegado a ti, por favor cuéntanos: ¿Qué leches es el campo número seis?

[https://onvotar.garantiespelreferendum.com/on-votar/index.html]: https://onvotar.garantiespelreferendum.com/on-votar/index.html
[https://www.ssllabs.com/ssltest/analyze.html?d=onvotar.garantiespelreferendum.com]: https://www.ssllabs.com/ssltest/analyze.html?d=onvotar.garantiespelreferendum.com
[Chrome Developer Tools]: https://developer.chrome.com/devtools
