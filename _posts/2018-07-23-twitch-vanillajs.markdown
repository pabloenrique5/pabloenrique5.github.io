---
layout: post
title:  "Twitch con Vanilla JS"
description: Sustitución de jQuery por Vanilla JS
date: 2018-09-22 20:23:25 +0100
categories: JavaScript, Ajax, jQuery, VanillaJS
img: twitch.jpg
author: Pablo Enrique
---

En este artículo vamos a reproducir un pequeño proyecto de Twitch con VanillaJS. Actualmente está programado con jQuery, así que podremos ver las principales diferencias entre una de las librerías más populares y el JavaScript de toda la vida.

**TWITCH CON JQUERY**

Tenemos el siguiente código jQuery:

```js
var channels = ["freecodecamp", "ESL_SC2", "OgamingSC2", "cretetion", "storbeck", "habathcx", "RobotCaleb", "noobs2ninjas", "brunofin", "comster404"];

function getChannelInfo() {

  channels.forEach(function(channel) {
    function makeURL(type, name) {
      return 'https://wind-bow.hyperdev.space/twitch-api/' + type + '/' + name + '?callback=?';
    };


    $.getJSON(makeURL("streams", channel), function(data) {
      var game,
          status;
      if (data.stream === null) {
        game = "Offline";
        status = "offline";
      } else if (data.stream === undefined) {
        game = "Not found";
        status = "offline";
      } else {
        game = data.stream.game;
        status = "online";
      };

      $.getJSON(makeURL("channels", channel), function(data) {
        var logo = data.logo != null ? data.logo : "https://dummyimage.com/50x50/ecf0e7/5c5457.jpg&text=0x3F",
          name = data.display_name != null ? data.display_name : channel,
          description = status === "online" ? ': ' + data.status : "";

          html = '<div class="row ' + status + '" id="canal"><div class="col-xs-2 col-md-2" id="icon"><img src="' +
          logo + '" class="logo"></div><div class="col-xs-5 col-md-3" id="name"><a href="' +
          data.url + '" target="_blank">' + name + '</a></div><div class="col-xs-5 col-md-7" id="streaming">'+
          game + '<span class="hidden-xs">' + description + '</span></div></div>';

        status === "online" ? $("#display").prepend(html) : $("#display").append(html);
      });
    });
});
};

$(document).ready(function() {
  getChannelInfo();

  $(".selector").click(function() {

    $(".selector").removeClass("active");
    $(this).addClass("active");
    var status = $(this).attr('id');

    if (status === "all") {
      $(".online, .offline").removeClass("hidden");
    } else if (status === "online") {
      $(".online").removeClass("hidden");
      $(".offline").addClass("hidden");
    } else {
      $(".offline").removeClass("hidden");
      $(".online").addClass("hidden");
    }


  });

});
```

Con este código visualizaremos una página con una serie de canales de TwitchTV y si se encuentran online u offline. Es la siguiente:

![No se puede cargar la imagen](/assets/images/twitch1.PNG)

A continuación vamos a ir paso a paso cambiando el código jQuery por el de Vanilla JS. Empecemos.

**Función ready()**

Como se ha podido observar, el código dispone de una función *ready()* que se encargará de realizar ciertas acciones una vez esté cargada la página.

```js
$(document).ready(function() { // Función ready()
  getChannelInfo(); // Ejecuta la función getChannelInfo()

  $(".selector").click(function() { // Obtenemos los tres elementos de la lista

    $(".selector").removeClass("active"); // Eliminamos la clase "active"
    $(this).addClass("active"); // Se la añadimos al elemento pulsado
    var status = $(this).attr('id'); // Obtenemos el id del elemento pulsado

    if (status === "all") { // Si es "all" hacemos visibles "online" y "offline"
      $(".online, .offline").removeClass("hidden");
    } else if (status === "online") { // Si es "online" la hacemos visible y ocultamos "offline"
      $(".online").removeClass("hidden");
      $(".offline").addClass("hidden");
    } else { // Si no es ninguna de las anteriores hacemos visible "offline" y ocultamos "online"
      $(".offline").removeClass("hidden");
      $(".online").addClass("hidden");
    }


  });

});
```

Lo primero que hace una vez cargada la página es ejecutar el método *getChannelInfo()* (que después veremos qué es lo que hace).

A continuación vienen una serie de controladores de eventos. Con la función "click" asociamos un evento a cada uno de los elementos que tengan la clase "selector" y dependiendo del que pulsemos se mostrarán u ocultarán los elementos asociados.

En VanillaJS este código sería el siguiente:

```js
window.addEventListener('DOMContentLoaded', function() { // Cuando la página esté cargada, equivale al "ready" de jQuery

	getChannelInfo();

	var selectors = document.querySelectorAll('.selector'); // Obtenemos los tres elementos de la lista
	selectors.forEach(function(element) { // Por cada elemento
		element.addEventListener('click', function() { // Añadimos evento "click"

			selectors.forEach(function(e) { // Les eliminamos la clase "active"
				e.classList.remove('active');
			});

			this.classList.add('active'); // Añadimos la clase "active" al elemento pulsado

			var status = this.getAttribute('id'); // Almacenamos en status el id del elemento pulsado
			
            // (*1)
			var all = document.querySelectorAll('#canal');
			var online = document.querySelectorAll('.online');
			var offline = document.querySelectorAll('.offline');

			if (status === "all") { // Dependiendo del elemento pulsado añadimos y eliminamos la clase "hidden" que es la encargada de ocultar los elementos
				all.forEach(function(element) {
					element.classList.remove("hidden");
				})
			} else if (status === "online") {
				online.forEach(function(element) {
					element.classList.remove("hidden");
				})
				offline.forEach(function(element) {
					element.classList.add("hidden");
				})
			} else {
				online.forEach(function(element) {
					element.classList.add("hidden");
				})
				offline.forEach(function(element) {
					element.classList.remove("hidden");
				})
			}
		});
	});
});
```

>(*1) Hay que tener en cuenta que en las variables "all", "online" y "offline" almacenamos los canales dependiendo de la clase CSS que tengan asignada. Estas clases se les asignan desde la función getChannelInfo().

Llegado a este punto nos damos cuenta de que a lo que acabamos de ver le falta algo, y es todo el trabajo que realiza la función *getChannelInfo()* antes de ejecutar el código que acabamos de analizar. Vamos a ver qué hace esta función.

**Función getChannelInfo()**

```js
// Array con el nombre de algunos canales
var channels = ["freecodecamp", "ESL_SC2", "OgamingSC2", "cretetion", "storbeck", "habathcx", "RobotCaleb", "noobs2ninjas", "brunofin", "comster404"];

function getChannelInfo() {
  // Se va a ejecutar todo el código que viene a continuación por cada uno de los canales del array
  channels.forEach(function(channel) {
  // (*2)
    function makeURL(type, name) {
      return 'https://wind-bow.hyperdev.space/twitch-api/' + type + '/' + name + '?callback=?';
    };

    // Al realizar esta petición, el servidor nos devuelve una respuesta.
    $.getJSON(makeURL("streams", channel), function(data) {
      var game,
          status;
          // Despendiendo de lo que venga en la respuesta querrá decir que el canal está online u offline. Les damos valor a las variables que acabamos de crear "game" y "status". Las utilizaremos en la siguiente función.
      if (data.stream === null) {
        game = "Offline";
        status = "offline";
      } else if (data.stream === undefined) {
        game = "Not found";
        status = "offline";
      } else {
        game = data.stream.game;
        status = "online";
      };

      $.getJSON(makeURL("channels", channel), function(data) {
        var logo = data.logo != null ? data.logo : "https://dummyimage.com/50x50/ecf0e7/5c5457.jpg&text=0x3F",
          name = data.display_name != null ? data.display_name : channel,
          description = status === "online" ? ': ' + data.status : "";

            // Creamos el elemento html que mostraremos al cliente por cada canal
          html = '<div class="row ' + status + '" id="canal"><div class="col-xs-2 col-md-2" id="icon"><img src="' +
          logo + '" class="logo"></div><div class="col-xs-5 col-md-3" id="name"><a href="' +
          data.url + '" target="_blank">' + name + '</a></div><div class="col-xs-5 col-md-7" id="streaming">'+
          game + '<span class="hidden-xs">' + description + '</span></div></div>';

        //Pongo a los que están online los primeros de la lista y a los offline los últimos
        status === "online" ? $("#display").prepend(html) : $("#display").append(html);
      });
    });
});
};
```
>(*2) Utilizamos la función makeUrl en dos ocasiones:
* En la primera le pasamos "streams" y el canal para que nos diga si el canal está emitiendo en estos momentos o no.
* En la segunda le pasamos "channels" y el canal para que nos devuelva información del canal como el nombre o el logo. 


El equivalente en VanillaJS sería el siguiente:

```js
function getChannelInfo() {
  //Las urls
  	channels.forEach(function(channel) {
	    function makeURL(type, name) {
	    	return 'https://api.twitch.tv/kraken/' + type + '/' + name + '?client_id=c8a3wkkb56yqjhlcui7tcfyjvs65dy6';
	  };

        // En VanillaJS hacemos uso del objeto XMLHttpRequest
	  const xhr = new XMLHttpRequest();
		xhr.open('GET', makeURL("streams", channel)); // Primera llamada con "streams"
		xhr.onreadystatechange = function() {
			if (xhr.status === 200 && xhr.readyState === 4) { // Si la petición ha ido bien
			var data = JSON.parse(this.response); // Recogemos la respuesta
			var game, status;

				if (data.stream === null) {
					game = "Offline";
					status = "offline"
				} else if (data.stream === undefined) {
					game = "Not found";
		        	status = "offline";
				} else {
					game = data.stream.game;
		        	status = "online";
				};


				const xhr = new XMLHttpRequest();
				xhr.open('GET', makeURL("channels", channel)); // Segunda llamada con "channels"
				xhr.onreadystatechange = function() {
				    if (xhr.readyState === 4 && xhr.status === 200) { // Si va todo bien
				    
                        // Formamos el html que se motrará al cliente
						var data = JSON.parse(this.responseText);
						var logo = data.logo != null ? data.logo : "https://dummyimage.com/50x50/ecf0e7/5c5457.jpg&text=0x3F",
				          name = data.display_name != null ? data.display_name : channel,
				          description = status === "online" ? ': ' + data.status : "";

				          var html = document.createElement("div");
				          html.innerHTML = '<div class="row ' + status + '" id="canal"><div class="col-xs-2 col-md-2" id="icon"><img src="' +
				          logo + '" class="logo"></div><div class="col-xs-5 col-md-3" id="name"><a href="' +
				          data.url + '" target="_blank">' + name + '</a></div><div class="col-xs-5 col-md-7" id="streaming">'+
				          game + '<span class="hidden-xs">' + description + '</span></div></div>';

				        var display = document.getElementById("display");
                if (status === "online") {
                  display.prepend(html);
                } else {
                  display.appendChild(html);
                }
					} else {
						console.log("Error 1, " + xhr.StatusText);
					}
				};
				xhr.send();
			} else {
				console.log("Error 2, " + xhr.StatusText);
			}
		};
		xhr.send();
	});
};
```

**[Aprende JavaScript con MentoringJS - Step 7](mentoringjs.com)**