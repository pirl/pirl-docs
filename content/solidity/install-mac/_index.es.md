---
title: Nodo Pirl - Instalando en Mac
weight: 9
pre: "<b>9. </b>"
chapter: true
---
## Construyendo desde la fuente

### Construir Pirl (cliente de línea de comando)

Clone el repositorio a un directorio de su elección:

```shell
git clone https://git.pirl.io/community/pirl
```

Construir `pirl` requiere el compilador Go:

```shell
brew install go
```

Finalmente, construya el programa `Pirl` usando el siguiente comando.
```shell
cd pirl
make pirl
```

Si ve algunos errores relacionados con los archivos de encabezado de la biblioteca del sistema Mac OS, instale XCode Command Line Tools e intente nuevamente.

```shell
xcode-select --install
```

Ahora puede ejecutar `build / bin / Pirl` para iniciar su nodo.



---
Autor(s):  

@Fawkes

Contribuyente(s):  

@Dptelecom
