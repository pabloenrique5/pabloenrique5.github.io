---
layout: post
title:  "Instalación de SQL Developer"
description: Instalación de la base de datos de Oracle SQL Developer y desbloqueo del esquema HR para poder practicar
date: 2018-01-30 22:06:25 +0100
categories: Oracle
img: oracle.png
author: Pablo Enrique
---

En este artículo vamos a ver cómo instalar el programa SQL Developer para poder trabajar con bases de datos.

Para asegurar el correcto funcionamiento del SQL Developer tendremos que instalar **Oracle Database 11g Express Edition**, el **JDK** (Java Development Kit) y finalmente el **SQL Developer**.

**Oracle Database 11g Express Edition**

Empezaremos instalando el Oracle Database 11g Express Edition. Podemos acceder a la página oficial de Oracle para descargarlo pinchando [aquí](http://www.oracle.com/technetwork/database/database-technologies/express-edition/downloads/index.html).

Una vez en la página de Oracle, tendremos que aceptar la licencia y seguidamente descargar la opción adecuada dependiendo del sistema operativo que tengamos.

![No se puede cargar la imagen](pabloenrique5.github.io\assets\images\oracle1.png)

Si no tenemos usuario de Oracle nos lo tendremos que crear, ya que es obligatorio para poder descargar contenido de la página oficial. Es completamente gratuito y solo nos llevará un par de minutos.

Se nos descargará un archivo comprimido, lo descomprimimos, accedemos a la carpeta *sqldeveloper* y abrimos el ejecutable **setup.exe**. Una vez se haya cargado, habrá que ir pulsando en los botones  de *Next* que nos aparezcan y aceptando las licencias que nos pidan hasta que nos aparezca una ventana para introducir una contraseña. Esta contraseña la utilizaremos más adelante para poder acceder a las bases de datos de pruebas SYS y SYSTEM. **Muy importante tenerla presente y no olvidarla**. Una vez introducida volvemos a pulsar en *Next* y en la siguiente ventana *Install*. Una vez se haya instalado pulsaremos en *Finish*.

**SQL Developer**

Para instalar el SQL Developer accederemos a la página oficial de Oracle haciendo clic [aquí](http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html).

Tendremos que aceptar la licencia y ya podremos descargar una versión. Para que funcione SQL Developer tendremos que tener instalado el **JDK**, hay una de las opciones que ya trae instalado el JDK en el caso de que no lo tengamos instalado, pero si ya lo tenemos instalado nos descargaremos la versión que viene sin el JDK.

![No se puede cargar la imagen](oracle2.png)

Como en la ocasión anterior tendremos que introducir nuestro usuario y contraseña para iniciar la descarga. Una vez descargado descomprimimos el archivo, accedemos a la carpeta y ejecutamos el archivo *sqldeveloper.exe*.

![No se puede cargar la imagen](site.baseurl/assets/images/oracle3.png)

Una vez con el SQL Developer abierto pulsamos en crear nueva conexión (el + que aparece arriba a la izquierda). En la ventana emergente tendremos que rellenar los campos. Por ejemplo, podemos poner como nombre de conexión y usuario “SYS”. **En la contraseña tendremos que poner la que pusimos al instalarnos Oracle Database 11g Express Edition**. En Rol seleccionaremos SYSDBA y le damos a probar. Veremos que en la parte inferior izquierda nos aparece "correcto".

![No se puede cargar la imagen]({{ "/assets/images/oracle4.png" | absolute_url }})

A continuación, le damos a "Guardar" para que nos almacene esta conexión y le damos a "Conectar".
Ahora tenemos que desbloquear el esquema **HR**. Para ello, escribiremos la siguiente sentencia en el editor y la ejecutaremos pulsando en el botón verde de *Play*:

```
ALTER USER HR ACCOUNT UNLOCK IDENTIFIED BY HR
```

![No se puede cargar la imagen]({{ "assets/images/oracle5.png" | site.baseurl }})

Con esto habremos desbloqueado el esquema HR. En la sentencia anterior le hemos dicho que el usuario HR va a tener la contraseña HR. Ahora le volvemos a dar a establecer una nueva conexión, rellenamos los campos con HR y pulsamos en "Probar":

![No se puede cargar la imagen](oracle6.png)

Nos pondrá "Correcto" abajo a la izquierda, guardamos la conexión y pulsamos en "Conectar".
Con esto ya tenemos el esquema HR para poder practicar.
