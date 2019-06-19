---
title: Nodo Pirl - Instalando en Win.
weight: 8
pre: "<b>8. </b>"
chapter: true
---
# Binarios

## Descargar binarios estables

Todas las versiones de Geth están creadas y disponibles para su descarga en https://git.pirl.io/community/pirl/tags.

La página de descarga proporciona un instalador, así como un archivo zip. El instalador pone geth en tu
PATH automáticamente. El archivo zip contiene el comando .exe y se puede usar sin instalar.

1. Descargar archivo zip
1. Extrae geth.exe de zip
1. Abra un símbolo del sistema
1. chdir <ruta a geth.exe>
1. abrir geth.exe

# Fuente

## Compilando pirl-node con herramientas de chocolatey.

El gestor de paquetes de Chocolatey proporciona una manera fácil de obtener
las herramientas de construcción necesarias instaladas. Si aún no tienes chocolatey,
siga las instrucciones en https://chocolatey.org para instalarlo primero.

Luego abre un indicador de comando del Administrador e instala las herramientas de compilación
necesitamos:

```text
C:\Windows\system32> choco install git
C:\Windows\system32> choco install golang
C:\Windows\system32> choco install mingw
``` 

Instalar estos paquetes configurará la variable de entorno `Path`.
Abra un nuevo símbolo del sistema para obtener el nuevo `Path`. Los siguientes pasos no
necesitan privilegios de administrador.

Asegúrese de que la versión de Go instalada es 1.7 (o cualquier versión posterior).

Primero, crearemos y configuraremos un diseño de directorio para el espacio de trabajo,
luego clonar la fuente.

*** OBS *** Si, durante los siguientes comandos, aparece el siguiente mensaje:
```
 WARNING: The data being saved is truncated to 1024 characters.
```
Entonces eso significa que el comando `setx` fallará, y el proceso truncará el` Path` / `GOPATH`. Si esto sucede, es mejor abortar e intentar hacer un poco más de espacio en `Path` antes de volver a intentarlo.

```text
C:\Users\xxx> set "GOPATH=%USERPROFILE%"
C:\Users\xxx> set "Path=%USERPROFILE%\bin;%Path%"
C:\Users\xxx> setx GOPATH "%GOPATH%"
C:\Users\xxx> setx Path "%Path%"
C:\Users\xxx> mkdir src\github.com\pirl
C:\Users\xxx> git clone https://git.pirl.io/community/pirl src\git.pirl.io\community\pirl
C:\Users\xxx> cd src\github.com\pirl\pirl
C:\Users\xxx> go get -u -v golang.org/x/net/context
```

Finalmente, el comando para compilar el nodo pirl es:

```text
C:\Users\xxx\src\git.pirl.io\community\pirl> go install -v ./cmd/...
```




---
Autor(s):  

@Fawkes

Contribuyente(s):  

@Dptelecom