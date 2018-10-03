---
layout: post
title:  "Debuggear JavaScript"
description: Breve explicación de algunas herramientas para depurar codigo JS
date: 2018-01-14 18:45:25 +0100
categories: JavaScript
img: debugging-js.jpeg
author: Pablo Enrique
---
[Cómo aprender JavaScript - Debugging](http://mentoringjs.com/)

Llamamos debuggear a la acción de analizar nuestro código para localizar errores que impiden la correcta funcionalidad del programa.

Una de las formas más sencillas de realizar alguna prueba para comprobar si la información que estamos pasando o recibiendo es correcta es utilizando "alert". Esto mostrará una ventana emergente en el navegador con la información que le hayamos pasado y un botón "Ok" para cerrarla:

`alert("Esto es un alert");`

También podemos utilizarlo simplemente por si queremos saber si hasta donde hemos colocado el "alert" llega correctamente el flujo de nuestro código.

Cuando se interprete esta línea de código, aparecerá una ventana emergente con la información se le ha puesto en el interior de los paréntesis.
Una particularidad que hay que tener en cuenta, es dónde ponemos los *alert*. Hay que tener cuidado de ponerlos en lugares donde no se vaya a ejecutar muchas veces el mismo trozo de código porque estará saltando continuamente y puede ser un estorbo.

Una forma más avanzada de debuggear es con **Chrome Development Tools**. Tenemos varias formas de abrir esta herramienta:

- Pulsando las teclas Ctrl + Shift + i
- En el navegador, accediendo a Opciones -> Más herramientas -> Herramientas para desarrolladores
- Haciendo click derecho sobre la página -> Inspeccionar

Una vez abierta la ventana para desarrolladores podremos colocarla donde queramos accediendo a la ventana de Opciones (tres puntos) y en *Dock side* podremos seleccionar la zona de la pantalla donde queremos colocar esta ventana.

Si se ha producido algún error, lo veremos en la pestaña de *Source*, donde se mostrará el *html* que estamos *debuggeando*. Cuando localicemos el error, podremos ponernos encima de la "x" que aparecerá en la línea del error para ver por qué ha fallado.

También podremos ver el error en la pestaña de **Console** y además podremos ejecutar algunos comandos básicos de JavaScript.
En la consola, siempre que utilicemos **$_** haremos referencia a la última expresión evaluada. Por ejemplo:

`['Pablo', 'Javier']`

Ahora mismo *$_* tiene el valor del array de nombres, pero si hacemos:

`$_.length`

El valor de *$_* ahora pasaría a ser 2.

Hay otras muchas más funciones que se pueden utilizar para sacarle más rendimiento en [este enlace](https://developers.google.com/web/tools/chrome-devtools/console/command-line-reference?utm_source=dcc&utm_medium=redirect&utm_campaign=2016q3).

También podemos introducir datos directamente en la consola si en la página que estamos debuggeando introducimos "console.log("Texto que queremos mostrar")"

Para código complejo, lo más adecuado es utilizar *breakpoints* llamando a **debugger;**.
Se abrirá una ventana y podremos seguir el flujo del programa línea a línea viendo en todo momento los valores con los que se está trabajando.

Este es solo un breve resumen de lo que podemos encontrar en [este enlace](http://juliepagano.com/blog/2014/05/18/javascript-debugging-for-beginners/) al blog de **Julie Pagano**.