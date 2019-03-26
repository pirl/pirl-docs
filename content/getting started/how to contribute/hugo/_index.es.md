---
title: Hugo
weight: 5
pre: "<b>5. </b>"
disableToc: true
---



¡Hola y Bienvenido!

¡Este manual le mostrará cómo ejecutar el servidor Hugo y Hugo directamente desde su línea de comandos!

Con la ayuda de Hugo, puede crear, ver, mejorar las entradas para la Base de conocimientos y contribuir a la comunidad PIRL.

## Visión general

Esta guía explicará cómo descargar, configurar y ejecutar Hugo y el servidor Hugo:


{{< imagesurlsheaders "cloud/Hugo.JPG" >}}


## Prerrequisitos

Para garantizar el éxito de esta operación, necesitará estos requisitos:

* Conexión a Internet
* [Descargue la última versión del binario de Hugo (> 0.25) para su sistema operativo] (https://github.com/gohugoio/hugo/releases)
* Descargue el repositorio de la documentación de pirl desde aquí: [Pirl-docs] (https://git.pirl.io/community/pirl-docs)
* Navegador web de su elección y algún poder de voluntad.

## ¡Acción!


### 1) Mac iOS
Si es usuario de Mac, instale Hugo con un solo comando fuerte y simple.

Mando:
brew install Hugo

Siga la guía de instalación [here](https://gohugo.io/getting-started/quick-start/)

### 2) sistema operativo Windows
* Si usas Windows como lo hago yo, simplemente descarga la última versión de [Hugo] (https://github.com/gohugoio/hugo/releases) para Windows si aún no lo has hecho.
* Descargue el archivo de [PIRL docs file depository] más reciente (https://git.pirl.io/community/pirl-docs) si aún no lo ha hecho. Descomprima / extraiga estas dos carpetas.
* Luego ve a la carpeta de Hugo y copia todo lo que encontrarás allí.
* Salte a la carpeta de documentos PIRL y pase todos los archivos HUGO allí y vuelva a escribir los archivos si es necesario.
* Luego presione el botón Buscar cerca del botón de inicio principal de Windows en la esquina inferior izquierda (normalmente está aquí :))
* Escribe un CMD en la línea vacía y presiona Enter.
* Ahora puede ver exactamente qué necesito escribir cada vez que quiera ejecutar el servidor Hugo y escribir algún artículo de KnowledgeBase (KB).
* Primero necesito localizar mi destino (en este caso, es un Disco D y algunas carpetas más). Luego me moveré hacia la carpeta de Hugo.

Commands in CMD:

1. C:\Users\YourComputername>D:
2. D:\>cd D:\PIRL\HUGO\pirl-docs-master\pirl-docs-master
3. Dir
4. Hugo.exe
5. Hugo.exe server
6. Para apagar el servidor Hugo presione: CTRL+C




### 3) SO Linux

He creado dos formas posibles para descargar, instalar y ejecutar Hugo. Elige lo que está más bien para ti.

#### a) Instalar por el gestor de paquetes

* Escribe el comando:
```
wget https://github.com/gohugoio/hugo/releases/download/v0.49/hugo_0.49_Linux-32bit.deb
sudo dpkg -i hugo_0.49_Linux-32bit.deb
```

#### b) Alternativamente, instale a través de un script de shell y luego use otro script para un inicio repetitivo cómodo
* instalación de script

```
#!/bin/bash
wget https://github.com/gohugoio/hugo/releases/download/v0.49/hugo_0.49_Linux-64bit.tar.gz
tar -xf hugo_0.49_Linux-64bit.tar.gz
```
* Script de inicio repetitivo

```
#!/bin/bash
cd /path/to/hugo
ls -la
./hugo.sh &
pkill -f hugo.sh
./hugo.sh server
```
********************
## Comprobando en el navegador web

Cuando haya terminado la instalación, inicie el navegador web y escriba:
```
http://localhost:1313
```
* Bienvenido a la Matriz. Ahora puede editar o crear nuevos archivos de índice y ayudarnos a crear otros artículos basados en el conocimiento de estudios.
* Para hacerlo, elija el editor de texto que se adapte a sus necesidades. Prefiero [Atom] (https://atom.io/). Es realmente fácil de usar y también amigable para usar GitLab.

--------

Autor:(s)

_[Mickey Maler](https://twitter.com/MickeyMaler)_

Contribuyente(s):
