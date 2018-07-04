---
layout: post
title:  "Modificar el DOM con JavaScript"
description: Explicación y ejemplos para hacer modificaciones en el DOM (Document Object Model)
date: 2018-06-14 19:43:25 +0100
categories: JavaScript
img: javascript.png
author: Pablo Enrique
---

Cualquier desarrollador de *frontend* sabe la importancia que tiene saber modificar el DOM. Antes se necesitaba jQuery para hacer las cosas más sencillas, pero ya no es necesario.

En este artículo voy a explicar una serie de funciones que nos permitirán hacer todas estas cosas:

* Seleccionar elementos HTML
* Añadir o eliminar eventos de escucha
* Añadir o eliminar clases
* Añadir o eliminar elementos HTML

**SELECCIONAR ELEMENTOS HTML**

Seleccionar un elemento HTML es uno de los conceptos más sencillos y uno de los que más cosas nos permiten hacer.
Tan solo necesitaremos dos métodos: ***querySelector*** y ***querySelectorAll***.

**querySelector**

Con *querySelector* podremos seleccionar un elemento HTML. Devuelve el primer elemento del documento que coincida con los selectores que le hemos indicado. Hay que decir que los selectores son **selectores CSS**. La sintaxis es la siguiente:

```js
document.querySelector(selectores);
```

Vamos a aplicar esta función en el siguiente ejemplo:

```html
<div id="primero">ID</div>
<div class="segundo">Mi clase</div>
<p>Mi etiqueta</p>
```

Ahora podemos seleccionar cada uno de los elementos del ejemplo:
* Para seleccionar un elemento por id: `document.querySelector('#primero');`
* Para seleccionar un elemento por clase: `document.querySelector('.segundo');`
* Para seleccionar un elemento por la etiqueta: `document.querySelector('p');`

Para ver la potencia que tiene esta función vamos a ver un ejemplo más complejo:

```js
var elemento = document.querySelector("div.uno input[name='dos']");
```

En este ejemplo se seleccionará el primer elemento `<input name="dos">` que se encuentre dentro de `<div class="uno">`.

**querySelectorAll**

Con *querySelectorAll* obtenemos una ***NodeList*** estática con los elementos que han coincidido con los selectores indicados.

>**¿Qué es una NodeList?**

>Son colecciones de nodos, y aunque no es un Array, es posible iterar sobre ellos utilizando `forEach()`. En algunos casos, la *NodeList* es una colección en vivo, es decir, que los cambios en el DOM se reflejan en la colección. En el caso de *querySelectorAll* se trata de una colección estática, lo que significa que cualquier cambio posterior en el DOM no afecta al contenido de la colección.

La sintaxis de esta función sería la siguiente:
```js
document.querySelectorAll(selectores);
```
A diferencia de *querySelector*, con *querySelectorAll* podemos seleccionar varios selectores separándolos con comas. Por ejemplo:

```html
<div class="miClase">Una Clase</div>
<div class="miClase">Otra Clase</div>
<div class="terceraClase">Tercera Clase</div>
```

Si a este ejemplo le aplicamos la siguiente funcionalidad, seleccionamos los tres contenedores:
```js
var coleccion = document.querySelectorAll('div.miClase, div.terceraClase');
```
Como se ha explicado en el apartado de la *NodeList*, podríamos recorrer nuestra colección con `coleccion.forEach()`.

**AÑADIR O ELIMINAR EVENTOS DE ESCUCHA**

Los eventos de escucha nos permiten realizar acciones con nuestro código. Se dispararán cuando el usuario interactúe con el DOM.

Utilizaremos dos funciones: `addEventListener` y `removeEventListener`.

**Añadir eventos de escucha**

Para añadir un evento de escucha seleccionaremos un elemento HTML con las funciones que hemos visto anteriormente, y después llamaremos a la función `addEventListener`:

```js
var elemento = document.querySelector('#selector');
elemento.addEventListener('evento', callback);
```

En este ejemplo *evento* es el tipo de evento que queremos que se lance, es decir, la acción que debe realizar el usuario para que se active. Hay muchos tipos de evento, [aquí](https://developer.mozilla.org/en-US/docs/Web/Events) dejo un enlace donde podremos ver todos los eventos disponibles.

*Callback* es la llamada a alguna de nuestras funciones donde especificaremos lo que queremos que ocurra cuando se ejecute el evento. Podemos ejecutar el *callback* llamando a otra función:

```js
elemento.addEventListener('click', saludo);
.
.
.
function saludo(){
    alert("¡Hola!, ¿Qué tal?");
}
```

O también podemos añadir la funcionalidad desde *addEventListener*:

```js
elemento.addEventListener('click', function(){
    alert("¡Hola!, ¿Qué tal?");
});
```

**Eliminar eventos de escucha**

Eliminar eventos de escucha es muy parecido a añadirlos:
```js
elemento.removeEventListener('evento', callback);
```
De normal, siempre eliminaremos algún eevento que hayamos añadido previamente como se muestra en el siguiente ejemplo:
```js
elemento.addEventListener('click', saludo);

function saludo(){
    alert("¡Hola!, ¿Qué tal?");
}

elemento.removeEventListener('click', saludo);
```

En este ejemplo que acabamos de ver hay que tener en cuenta que una vez se elimine el evento no se volverá a disparar. Se debería eliminar el evento cuando ya no lo vayamos a utilizar más.

**AÑADIR O ELIMINAR CLASES**

Para añadir o eliminar clases utilizaremos los siguientes métodos: `classList.add()` y `classList.remove()`.

En el siguiente ejemplo, vamos a suponer que tenemos en nuestro CSS una clase que se llama `.claseParaNav` que le dará un estilo a nuestro elemento `nav`. Ahora añadiremos dicha clase al elemento:

```js
var elemento = document.querySelector('nav');
elemento.classList.add('claseParaNav');
```

Y eliminaríamos la clase con:

```js
elemento.classList.remove('claseParaNav');
```

**AÑADIR O ELIMINAR ELEMENTOS HTML**

Para añadir un elemento solo necistaremos utilizar la función `document.create Element('element');`. Pero una vez está creado debemos hacer algo con él.

Teniendo el siguiente HTML:
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header></header>

  <button class="articulo">Artículo</button>

  <ul>
    <li>¡Artículo añadido!</li>
  </ul>

  <script src="script.js"></script>
</body>
</html>
```

Vamos a hacer que cada vez que se pulse el botón se añada un elemento `li` o se elimine en el caso de que ya se esté mostrando. Para ello, nuestro javascript debería ser como el siguiente:

```js
let articulo = document.querySelector('.articulo');
let lista = document.querySelector('ul');

function crearElemento () {
  let li = document.createElement('li'); // Creamos elemento 'li'
  li.innerHTML = '¡Artículo añadido!'; // Le introducimos el contenido que queremos que muestre
  return li;
}

articulo.addEventListener('click', e => {
  if (lista.children.length > 0) { // Si ya hay algún elemento 'li'...
    let elemento = lista.children[0];
    lista.removeChild(elemento); // Lo eliminamos
    articulo.innerHTML = 'Añadir';
  } else { // Sino...
    lista.append(crearElemento()); // Lo añadimos
    articulo.innerHTML = 'Eliminar';
  }
});
```

**[Aprende JavaScript con MentoringJS - Step 7](mentoringjs.com)**