---
title: Cómo Restablecer los Datos de la Cadena de Bloques
weight: 3
pre: "<b>3. </b>"
chapter: true
---
{{< imagesurlsheaders "images_headers/wallet.png"  >}}

## Introducción

Esta guía cubre el restablecimiento de los datos de la cadena de bloques, es decir, la eliminación y la nueva sincronización de la cartera Pindl Nautilus chaindata.
La situación más probable que requiere esto es que su billetera Pirl esté bloqueada o no se sincronice.
Si este es el caso, siga la siguiente guía para resolver el problema.

## Nota IMPORTANTE

{{% notice warning %}}

Antes de intentar este proceso, debe hacer una copia de seguridad de los datos de su almacén de claves / Billetera PIRL. Una guía sobre cómo hacer esto está disponible aquí: [Cómo hacer una copia de seguridad de las carteras Pirl]({{< ref "/wallets/backup pirl wallets" >}})

{{% /notice %}}

## Eliminando los datos de la cadena de bloques

Después de asegurarse de haber realizado una copia de seguridad de los datos de su almacén de claves / Billetera de forma segura, el resto del proceso es sencillo y es el siguiente:

 * **Cierre la Billetera de Pirl Nautilus**
 * **Localizar y eliminar la cadena de datos Pirl**
 * **Reabrir la cadena de datos Pirl**

### Ubicando los datos

En Windows, estos datos se encuentran en:

`C:\Users\*YourUsername*\AppData\Roaming\Pirl\pirl`

On Linux, it's located at:

`~/.pirl`

On MacOS X, it's located at:

`~/Library/Pirl`

## Resumen

Los datos de su cadena de bloques ahora deberían restablecerse, lo que generalmente resolverá la mayoría de los problemas relacionados con la billetera.
Cuando vuelva a abrir la billetera, tenga en cuenta que tendrá que descargar los datos de la cadena de bloques de nuevo, lo que puede llevar algún tiempo.

---
Author(s):

@dptelecom

Contributor(s):

@packetflow