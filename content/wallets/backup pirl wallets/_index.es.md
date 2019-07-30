---
title: Cómo Hacer Copias de Seguridad de Billetera Pirl
weight: 2
pre: "<b>2. </b>"
chapter: true
---
{{< imagesurlsheaders "images_headers/wallet.png"  >}}

## Visión general

Esta es una guía de las mejores prácticas para hacer copias de seguridad de sus billeteras Pirl y para mantener su Pirl segura y protegida.

## Introducción

Entonces, acabas de recoger un paquete de Pirl, estás en esto por mucho tiempo y vas a mantener estas monedas por mucho tiempo. ¿Cómo puede asegurarse de no perder el acceso a través de incendios / robos / choques?
Es importante hacer una copia de seguridad de sus billeteras Pirl para asegurarse de que cualquier falla no resulte en la pérdida de su Pirl. Esta guía le guiará a través de las mejores prácticas para copias de seguridad y abordará tres plataformas / opciones para hacerlo.

## Importante entender: ¿Qué * es * una billetera?

En su esencia, la parte de la billetera que le da acceso a sus fondos y le permite gastar sus monedas, son sus claves privadas. Su Pirl se almacena en la cadena de bloques, y las claves privadas son las que desbloquean sus fondos y les permiten ser enviados. Estas claves privadas se pueden ver en varias formas diferentes, siendo la forma * raw * una cadena de 64 caracteres hexadecimales que se parece a algo como:
`` `c6cbd7d76bc5baca530c875663711b947efa6a86a900a9e8645ce32e5821484e``

La importancia de sus claves privadas es doble. Le brindan acceso a sus fondos, pero también le darán a cualquier persona con acceso clave a sus fondos. Por ese motivo, es IMPERATIVO que tome medidas para proteger estas claves privadas y mantenerlas en una copia de seguridad.
La siguiente sección detalla los métodos comunes para almacenar estas claves privadas y las mejores prácticas para cada una.

## Tipos de carteras y buenas prácticas

Para que una transacción sea aprobada, siempre debe estar firmada con su clave privada. Sin embargo, para funciones adicionales, como proteger la clave con una contraseña, existen varios formatos para almacenar su clave privada.

Los tipos de billetera más utilizados son los siguientes:

  * ** Clave privada (sin cifrar) **
  * ** Archivo de almacén de claves (UTC / JSON). **
  * ** Carteras de hardware (por ejemplo, Ledger / Trezor) **

### Clave privada (sin cifrar)

Esta es la versión de texto sin cifrar de su clave privada. No requiere tu contraseña.
Si alguien más tiene esta clave, puede acceder a su billetera sin una contraseña.
Esto hace que este método de almacenamiento sea el más simple y el más volátil.

#### Guardar su clave privada como un archivo de Paper Wallet o Keystore

Por lo general, se recomienda usar una versión encriptada, sin embargo, debe imprimir una billetera de papel y guardar esta clave en algún lugar fuera de línea.

Hay una función útil en https://wallet.pirl.io que le permite exportar la información de su billetera como un archivo de almacén de claves (JSON / UTC), o imprimir una billetera de papel.

Simplemente haga clic en la pestaña "Ver información de cartera"

{{< imagesurlsheaders "cloud/main_pirl_wallet_page_view_wallet_highlight.png" >}}

Ingrese los detalles de su billetera en cualquier formato que tenga

{{< imagesurlsheaders "cloud/view_wallet_details_landing_page.png" >}}

Los detalles de su billetera se presentarán como una clave pública / privada, con la opción de generar un archivo de almacén de claves (JSON / UTC) o imprimir una billetera de papel.

{{< imagesurlsheaders "cloud/view_wallet_details.png" >}}

La billetera de papel se verá así.

{{< imagesurlsheaders "cloud/paper_wallet_example.png" >}}

Debe imprimir la billetera de papel dos veces y almacenarla en dos ubicaciones seguras. Trátalo como si fuera efectivo.
También debe descargar el archivo de almacén de claves y guardarlo en un medio externo, como una unidad USB o una unidad de disco duro. Es recomendable tener una copia de seguridad en varias ubicaciones físicas en caso de que ocurra lo peor.
Siempre recuerde la regla de oro de las copias de seguridad: "Dos copias de seguridad es una, y una es ninguna".

### Archivo de almacén de claves (UTC / JSON)

Esta es la versión recomendada para guardar, y también es el formato en el que la Cartera Pirl Nautilus (de escritorio) almacena su billetera.
Dado que el formato del almacén de claves coincide con el utilizado por la billetera web en https://wallet.pirl.io, puede importar fácilmente en cualquier dirección.

Este archivo está cifrado por la contraseña que eligió al crear el archivo.

Debe guardar el archivo de almacén de claves en un medio externo, como una unidad USB o una unidad de disco duro. Es recomendable tener una copia de seguridad en varias ubicaciones físicas en caso de que ocurra lo peor.

#### Copia de seguridad de su billetera Nautilus

Para hacer una copia de seguridad de su Nautilus Wallet, haga clic en ** Archivo **> ** Copia de seguridad **> ** Cuentas **

{{< imagesurlsheaders "cloud/nautilus_backup.png" >}}

Esto abrirá la carpeta appdata que contiene sus archivos de cartera.
{{< imagesurlsheaders "cloud/nautilus_backup_folder.png" >}}

###Carteras de hardware

El soporte de la cartera de hardware para Pirl está disponible en los dispositivos Ledger y Trezor.
Estos dispositivos presentan una forma segura de almacenar y acceder a sus fondos, con las claves privadas almacenadas en un área protegida del dispositivo que evita que se transfieran fuera del dispositivo en formato de texto simple.
Este método significa que incluso si su computadora está comprometida, debería poder firmar transacciones de manera segura.
Al igual que con toda la tecnología, existen medios avanzados para atacar estos dispositivos que potencialmente pueden exponer sus fondos, pero esto está más allá del alcance de este artículo y no es algo que el usuario promedio necesite para preocuparse.

Sin embargo, una precaución de seguridad particular que debe tomarse es comprar solo estos dispositivos a través de tiendas propias o confiables, y asegurarse de que el dispositivo no se haya abierto o alterado de otro modo cuando lo reciba.

## Resumen

En resumen, las acciones más importantes para asegurar su Pirl:

 * Utilice una billetera de hardware si es posible, siendo la siguiente mejor opción el almacén de claves protegido por contraseña (UTC / JSON).Utilice una billetera de hardware si es posible, siendo la siguiente mejor opción el almacén de claves protegido por contraseña (UTC / JSON).

 * Use la billetera web pirl para guardar una billetera de papel e imprimirla dos veces, manteniéndola en dos ubicaciones seguras.

 * Independientemente del formato de billetera que utilice, realice múltiples copias de seguridad en varias ubicaciones.
 * Nunca exponga sus claves privadas a terceros (que no sean de confianza), ya que esto les dará acceso total a sus fondos.

---
Autor(s):

Bigchrome

Contributor(s):
