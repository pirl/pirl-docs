---
title: Guía Markdown
weight: 3
pre: "<b>3. </b>"
disableToc: true
---

## Introducción

Para contribuir a la documentación de PIRL, deberá usar el formato ["markdown"] (https://daringfireball.net/projects/markdown/syntax). Markdown es una de las muchas formas de hacer documentación. Probablemente no sea lo mejor y ciertamente no lo peor. Es fácil entrar y permitir un ciclo de documentación coherente.

A continuación, encontrará algunos ejemplos de cómo utilizar markdown, junto con nuestras recomendaciones y mejores prácticas. Por favor, use nuestras recomendaciones al redactar la documentación de PIRL para que se vea bien junto con el resto del contenido. Además, asegúrese de consultar[Guía de Style ]({{< ref "/getting started/how to contribute/style guide" >}})para obtener pautas adicionales sobre el formato del contenido.

## Ejemplo de documento de Markdown

Ejemplo de documento de rebaja

A continuación se muestra un documento de ejemplo utilizando markdown. Este documento será procesado por el software para mostrarlo como se describe.


{{< imagesurlsheaders "cloud/sample.jpg" >}}


## Guía Básica de Markdown

### Titulo principal

El título del documento principal se muestra en la parte superior del documento con la fuente más grande. En markdown, el título se encuentra en la parte superior del documento entre la sección ** `---` ** como se muestra a continuación para este mismo documento.

```
---
title: Markdown Guide
weight: 5
---
```

### Encabezados

Los encabezados suelen tener un tamaño desde H1 (el más grande) a H6 (el más pequeño). Markdown no es diferente. El número que representa el tamaño del encabezado está representado por un ** `#` **. Un solo ** `#` ** es equivalente a ** H1 **, dos ** `##` ** es equivalente a ** H2 **, etc.

```
# Esta es una etiqueta H1
## Esta es una etiqueta H2
### Esta es una etiqueta H3
#### Esta es una etiqueta H4
##### Esta es una etiqueta H5
###### Esta es una etiqueta H6
```

> **CONSEJO DE PIRL :** Las secciones principales de un documento comienzan con ** ## ** o H2

### Énfasis

Para * poner en cursiva * el texto, use un único conjunto de asteriscos a su alrededor. Para marcar el texto como ** en negrita **, use un conjunto de dos asteriscos a su alrededor. Para tachar un texto, use dos tildes ** (~) ** a su alrededor.

```
* Este texto estará en cursiva *
** Este texto estará en negrita **
_ ** ¿Qué pasa con negrita cursiva ** _
~~ ¿Dije algo mal? ~~
<center> Soy un escritor centrado </center>
```

* Este texto estará en cursiva *

** Este texto estará en negrita **

_ ** ¿Qué pasa con negrita cursiva ** _

~~ ¿Dije algo mal? ~~

<center> Soy un escritor centrado </center>

### Citación

Para citar algo, use un corchete derecho> ¡Y haga su cotización!
`` `
> ** Manual para este artículo **: Tienes que leer este artículo de principio a fin y mostrar tu gracia. Después de todo, así es como funciona la literatura, ¿verdad?
(a menos que sea un manual de instrucciones, en cuyo caso nadie las lee)
`` `
> ** Manual para este artículo **: Tienes que leer este artículo de principio a fin y mostrar tu gracia. Después de todo, así es como funciona la literatura, ¿verdad?
(a menos que sea un manual de instrucciones, en cuyo caso nadie las lee)


### Tabla
Si desea crear una tabla simple en el editor de texto Atom, simplemente puede bajar el tiempo de "tabla" y presionar Enter! Si estás escribiendo en el bloc de notas, bueno,
le deseo sinceras condolencias :) Pero al escribir esos símbolos, puede crear filas y columnas individuales.

Aquí tienes dos ejemplos:


```
| Header One     | Header Two     |
| :------------- | :------------- |
| Item One       | Item Two       |
```
| Header One     | Header Two     |
| :------------- | :------------- |
| Item One       | Item Two       |



```
|[Web page](https://pirl.io/)|[White Paper](https://storage.gra1.cloud.ovh.net/v1/AUTH_33a0c4ac73cf4d88a243480c275be8ac/pirl/pirl-whitepaper.pdf)| [Twitter](https://twitter.com/PirlOfficial)  |
|:------------- |:-------------:| -----:|

```
|[Web page](https://pirl.io/)|[White Paper](https://storage.gra1.cloud.ovh.net/v1/AUTH_33a0c4ac73cf4d88a243480c275be8ac/pirl/pirl-whitepaper.pdf)| [Twitter](https://twitter.com/PirlOfficial)  |
|:------------- |:-------------:| -----:|



### Lista

Las listas ordenadas se crean utilizando ** 1. ** para el elemento de búsqueda y luego se incrementan con cada línea subsiguiente. Las listas desordenadas se crean utilizando ** + **.

```
1. primero
2. segundos
3. Tercero

+ Satoshi
+ Vitalik
+ PIRL

1. Esta es la primera
   + Lo primero
2. Este es el segundo
   + Segunda cosa
3. Esto es tercero
   + Tercera cosa
`` `

1. primero
2. segundos
3. Tercero

+ Satoshi
+ Vitalik
+ PIRL

1. Esta es la primera
   + Lo primero
2. Este es el segundo
   + Segunda cosa
3. Esto es tercero
     + Tercera cosa

### Enlaces

Hacer enlaces simplemente implica pegar una URL entre un conjunto de ** () ** paréntesis. También hay un par de opciones extra.

```
Este es un [enlace de ejemplo] (http://example.com/ "Con un título"). Seguirá funcionando si lo único que se incluye es el enlace entre paréntesis.
`` `

Este es un [enlace de ejemplo] (http://example.com/ "Con un título"). Seguirá funcionando si lo único que se incluye es el enlace entre paréntesis.

### Imágenes


Vincular imágenes es como enlaces con un codigo corto {{<imagesurlsheaders "cloud / magic.gif">}}

```
* {{< imagesurlsheaders "cloud/magic.gif" >}}
```

* {{< imagesurlsheaders "cloud/magic.gif" >}}


### Código

Hay dos formas de distinguir el código del texto, una para uso en línea y otra para bloques de código. Para distinguir el código `inline`, coloque un conjunto de marcas de retroceso alrededor de él. Para hacerlo como un bloque de texto, coloque tres marcas de respaldo en la parte superior e inferior.


{{< imagesurlsheaders "cloud/code.jpg" >}}


```
Esto se mostrará como un bloque de código.
Más importante,, darse cuenta de la marca en la parte superior e inferior.
```

---
Autor:

_[PrimateCrypto](https://twitter.com/PrimateCrypto)_


Contribuyente(s):  

@dptelecom
