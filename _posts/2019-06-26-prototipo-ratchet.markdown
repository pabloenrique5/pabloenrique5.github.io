---
layout: post
title:  "Prototipo"
description: Prototipo de aplicación administrativa "Tachán"
date: 2019-06-24 18:45:25 +0100
categories: Ratchet
img: prototipo.png
author: Pablo Enrique
---
[Aprende JavaScript con MentoringJS - Step 9](http://mentoringjs.com/)

En este artículo voy a presentar el prototipo de la aplicación que quiero diseñar.

Se trata de una aplicación de gestión de asociaciones u organizaciones, en la que se podrá preparar eventos, crear noticias o encuestas y mantener un registro de todos los colaboradores de la asociación.

El primer usuario en crear la asociación obtendrá automáticamente el rol de administrador, y a partir de ahí se podrán ir dando de alta otros usuarios para la asociación. La principal diferencia entre el administrador y el resto de usuarios es que se habilitará una sección de **gestión de usuarios**. El administrador será el que podrá dar de alta o de baja al resto de usuarios.

**TACHÁN**

En todo momento se mostrará un menú en la parte inferior de cada pantalla desde donde se podrá acceder al perfil del usuario, volver a la pantalla de inicio, configurar las opciones de la app y, en el caso del administrador, gestionar usuarios.

La aplicación mostrará una interfaz muy sencilla y accesible a todas sus diferentes pantallas desde prácticamente cualquier punto de la app.

Mostrará un panel principal donde se verán publicadas noticias, comentarios o fotos que vayan añadiendo los componentes de de la asociación.

![No se puede cargar la imagen](/assets/images/prototipo1.PNG){:height="470px" width="273px"}

Desde el botón de "Nuevo Artículo" podremos añadir nuevos artículos para que los puedan visualizar el resto de componentes de la asociación.

Estos artículos podrán ser, noticias, algún comentario para informar a la asociación, fotos o encuestas para que puedan votar el resto de componentes sobre un tema en concreto o decisión que se deba tomar.

Desde el botón de "Actividades" accederemos a la sección de actividades.

**Actividades**

Desde esta pantalla veremos todas las actividades que todavía siguen vigentes. Cada actividad tendrá una fecha de evento. Una vez venza esa fecha ya no se mostrarán en esta pantalla las actividades y pasarán directamente al histórico.

![No se puede cargar la imagen](/assets/images/prototipo2.PNG)

Cada una de las actividades vigentes tendrán un botón desde el cual podremos ver la vista del detalle de la actividad.

![No se puede cargar la imagen](/assets/images/prototipo3.PNG)

Como se puede apreciar, veremos la descripción del evento asi como la fecha en la que se tiene pensado ejecutar dicho evento. Si todavía no hemos decidido si colaborar en el evento, podremos darle al botón "Colaborar" para ser nuevos colaboradores del evento. 

Desde el botón "Colaborardores" veremos la lista de usuarios que ya están como colaboradores del evento.

Si la actividad ya venció su fecha de evento, aparecerá un botón de "Reutilizar"     que nos permitirá recuperar una actividad que queramos volver a hacer y no tengamos que volver a definirla.

**Perfil**

Desde el botón de "Perfil" del menú inferior accederemos a nuestro perfil personal.

![No se puede cargar la imagen](/assets/images/prototipo4.PNG)

Aquí podremos editar nuestro perfil y ver el ranking mensual de los participantes de la asociación.

Cuanto más interactúe un usuario con la aplicación más puntos ganará. Hay diferentes formas de ganar puntos: accediendo a la aplicación cada día, poniendo comentarios, realizando encuestas, participando en eventos...

Cada mes se pondrá a 0 la puntuaciónde cada usuario.

**Gestión de usuarios**

El administrador de la asociación tendrá la potestad de dar de alta usuarios para la organización o darlos de baja.

![No se puede cargar la imagen](/assets/images/prototipo5.PNG)

El administrador verá en esta pantalla la lista de usuarios que actualmente están en la organización.

Habrá también un buscador en la parte superior donde podremos buscar por nombre y apellidos.

Al dar de alta un usuario se mostrará una ventana donde podremos introducir el nombre de usuario, el password inicial y el rol que va a ocupara en la aplicación. Los roles serán administrador y usuario.

Con la ayuda de **mentoringjs** iré creando poco a poco mi propia app. Estará programada con **ReactJS** e iré publicando cada paso de la construcción de la app [aquí](https://github.com/pabloenrique5/tachan).