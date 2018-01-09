---
layout: post
title:  "Crear blog con Jekyll"
description: Crear un blog con Jekyll vía Chocolatey para sistema operativo Windows
date: 2018-01-09 22:52:25 +0100
categories: Jekyll
img: jekyll-poster.png
author: Pablo Enrique
---

Vamos a crear nuestro propio blog para **Windows** utilizando **Jekyll**. Jekyll es un generador de sitios web estáticos, es ideal para crear nuestro blog personal y al estar desarrollado por el cofundador de GitHub, Tom Preston-Werner, está perfectamente sincronizado con GitHub y nos permitirá alojar nuestro blog en GitHub Pages.

Jekyll está escrito en lenguaje **Ruby**, por lo que también tendremos que instalar Ruby en nuestro equipo.

##Instalación de Chocolatey
Empezaremos instalando el gestor de paquetes **Chocolatey**, necesario para crear nuestro blog. Chocolatey es la mejor forma para instalar Jekyll en Windows.

Para ello, abriremos el **símbolo del sistema como administrador** e introduciremos las siguientes líneas:

```
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1’))” && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```

##Instalación de Ruby

Una vez se haya cargado, procedemos a la instalación de Ruby con:

```
choco install ruby -y
```

Una vez ejecutado y completado este comando cerraremos y volveremos a abrir el símbolo del sistema como administrador.

El siguiente paso es descargar las gemas de Ruby. Pinchando en el siguiente enlace descragaremos las gemas más actualizadas:

[Descargar gemas de Ruby](https://rubygems.org/gems/rubygems-update-2.7.4.gem)

Es recomendable almacenar este archico en un directorio raíz. Una vez descargadas, accedemos al directorio donde hemos almacenado el archivo desde el símbolo del sistema con:

```
cd rutaDondeEstaElArchivo
```

Una vez en ese directorio utilizamos el comando `dir` para ver todos los archivos que hay en el directorio y así poder localizar el archivo de las gemas de Ruby que hemos descargado. Cuando lo encontremos ejecutamos el siguiente comando:

```
gem install --local nombreDelArchivoCompleto
```

Con esto se nos instalaría Ruby con la última versión. Podemos comprobar que se ha instalado correctamente y la versión que se nos ha instalado con `update_rubygems`

##Instalación de Jekyll

Ahora instalamos jekyll:

```
gem install jekyll
```

Y para comprobar la versión:

```
jekyll -v
```

Por último, tenemos que instalar el *bundler*:

```
gem install bundler
```

Ahora accedemos por el símbolo del sistema a la ruta donde queremos almacenar nuestro blog:

```
cd rutaDondeAlmacenarBlog
```
Y ejecutamos el comando para crear el blog:

```
jekyll new nombreBlog
```

Una vez creado entramos en nuestro blog con `cd nombreBlog` y creamos nuestro servidor local con el comando:

```
jekyll serve
```

Una vez realizados todos estos pasos, si accedemos al navegador y escribimos **localhost:4000** podremos visualizar nuestro blog.