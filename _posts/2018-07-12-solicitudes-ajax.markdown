---
layout: post
title:  "Solicitudes Ajax y objeto XMLHttpRequest"
description: Cómo realizar solicitudes Ajax
date: 2018-07-22 19:02:25 +0100
categories: JavaScript, Ajax
img: http.jpg
author: Pablo Enrique
---

Para realizar llamadas **Ajax** vamos a apoyarnos en el objeto **XMLHttpRequest**. Podremos obtener información de una URL sin tener que recargar la página. Para instanciar el objeto XMLHttpRequest haremos lo siguiente:

```js
var request = new XMLHttpRequest();
```
Hacer una solicitud **Ajax** requiere dos llamadas a funciones: *open()* y *send()*.

Con *open()* definimos el tipo de solicitud (get, post, put, etc.) y con el método *send()* ejecutamos la solicitud.

```js
request.open('GET', 'https://ruta', true);
request.send();
```

Añadiendo `true` al final del método *open()* indicamos que la llamada debe ser asíncrona. Si por el contrario añadimos `false` el método *send()* no se ejecutará hasta recibir la respuesta completa.

Si quisiéramos añadir cabeceras solo tendríamos que añadir:

```js
request.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
```

Vamos a preguntar al servidor por la capital de un país, país que le pasaremos nosotros en la URI. Si la solicitud se ejecuta correctamente mostrará un *alert* indicando la capital del país, sino mostrará un mensaje de error:

```js
var xhr = new XMLHttpRequest();
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
xhr.open('GET', 'servicio/capital?pais=Portugal');
xhr.onload = function() {
    if (xhr.status === 200) {
        alert("La capital es " + xhr.responseText);
    } else {
        alert("La solicitud ha fallado");
    }
};
xhr.send();
```

**[Aprende JavaScript con MentoringJS - Step 7](http://mentoringjs.com/)**