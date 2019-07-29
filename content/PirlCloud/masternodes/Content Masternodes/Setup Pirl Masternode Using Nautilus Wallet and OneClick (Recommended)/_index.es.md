---
title: Configuración del Contenido de Masternodo
weight: 1
pre: "<b>1. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/Masternodes.png" >}}

- [Visión general](#Visión general)
- [Prerrequisitos](#Prerrequisitos)
- [Verificación de Identidad Monedero Poseidon](#Verificación de Identidad Monedero Poseidon)
- [Contrato de Ejecución de Nautilus](#Contrato de Ejecución de Nautilus)
- [Crear / Lanzar servidor CentOS Linux](#Crear / Lanzar servidor CentOS Linux)
- [Crear Masternodo en Poseidon](#Crear Masternodo en Poseidon)
- [Configuración de Masternodo con un Clic](#Configuración de Masternodo con un Clic)
- [Vigilancia](#Vigilancia)

## Visión general

Ejecutar un masternode PIRL requiere el uso de un Virtual
Servidor privado (VPS) con una dirección IP pública estática asignada directamente a una interfaz.

> *NAT (traducción de direcciones) no es compatible.*

¡Y solo tienen pirl ejecutándose en el servidor, no hay otros nodos o cualquier causa que cause conflicto!

Una vez que tenga los fondos en su lugar,
envía una pequeña transacción 1 PIRL a su billetera Poseidon (su cuenta vendrá con una billetera) para demostrar que controla la billetera Nautilus con el capital de 10K PIRL para Content MN.
Utiliza el txid de la transacción 1 PIRL como parte de la configuración de masternode, junto con su dirección de Nautilus.
Cuando se agrega el masternode,
regresa a su billetera Nautilus y agrega la dirección del contrato de masternode en la pestaña "contratos".
Con la dirección del contrato masternode en su lugar,
se ejecuta la función de registro de nodo.
En este punto, puede utilizar la funcionalidad de un clic de Poseidon que configurará automáticamente su servidor y lo mantendrá actualizado.

Esta guía utiliza la función de configuración de un clic en masternode.
Esta característica de Poseidon configura automáticamente su servidor linux CentOS 7 para ser un Ptern Masternode.
Las actualizaciones se aplicarán automáticamente.
Todo lo que tiene que hacer es monitorear su servidor para asegurarse de que permanezca operativo.
Esto es tan simple como reiniciar el servidor, si se desconecta.

## Prerrequisitos

* ** Un VPS con un mínimo de 4 GB de RAM en el SO total (se recomienda más), suficiente almacenamiento para ejecutar el masternode (Mínimo de 20 GB, 60 GB + recomendado) y una dirección IP pública estática asignada directamente a una interfaz. NAT (traducción de direcciones) no es compatible. **
 - Los requisitos MÍNIMOS oficiales son: 4 GB de RAM, espacio de 20 GB, transferencia de 3 TB, IPv4 pública. Una vez que ordene su VPS, recibirá sus credenciales de raíz. El camino más fácil para avanzar es utilizar este VPS solo para su Pirl Masternode y darle a Poseidon sus credenciales de raíz para que pueda administrar y actualizar su VPS.
* ** Una cuenta de Poseidon en [https://poseidon.pirl.io](https://poseidon.pirl.io) **
 - Navegue hasta https://poseidon.pirl.io y regístrese para obtener una cuenta. Tenga en cuenta que iniciará sesión con su nombre de usuario y no con el correo electrónico.
* ** Cartera Nautilus **
 - Nautilus es la billetera de escritorio oficial de Pirl. Lo necesitará para agregar y ejecutar el "Registro de nodo" del contrato inteligente necesario para ejecutar el Ptern masternode. Puede usar la billetera de escritorio para crear su billetera Pirl [Descargas Nautilus] ({{<ref "/Downloads">}}) o puede usar la billetera web en: https://wallet.pirl.io/.
 - Sea cual sea el método que elija para crear su billetera, asegúrese siempre de guardar su archivo UTC,
 - la contraseña necesaria para descifrar el archivo UTC, así como su clave privada.
 - Puede usar su archivo UTC creado por Nautilus y su contraseña para extraer su clave privada.
 - Puede usar su clave privada en lugar del archivo UTC + Contraseña para acceder a su billetera y retirar sus fondos en caso de una emergencia.
* ** 10,001 Pirl disponibles en su billetera para Content MN **
 - No hay forma de evitarlo, de alguna manera necesitarás diez mil PIRL en una billetera.
 - Y 1 o 0,5 para que el gas interactúe con el contrato.
 - Puedes explotar Pirl utilizando uno de los grupos oficiales disponibles aquí: https://pirl.io/en/pools/.
 - También puedes comprar Pirl en uno de los intercambios de Pirl. Recomiendo https://www.stex.com como un intercambio seguro y confiable.

## Verificación de Identidad Monedero Poseidon

El primer paso en el proceso de configuración de masternode es enviar una transacción desde su billetera Nautilus (también puede usar la billetera web aquí si es necesario) a su billetera Poseidon ubicada aquí: https://poseidon.pirl.io/dashboard/accounting/ billetera/.
Esto es como enviar a Pirl a cualquier otra billetera, excepto que en este caso es su billetera única de Poseidon.
Lo que esto hace es demostrar a Poseidon que usted controla su billetera Nautilus.
No envíe más de 1 o .5 pirl a esta dirección para su verificación, esta no es la dirección a la que enviará los 10k pirls. eso viene despues

Vaya a https://poseidon.pirl.io/ y pegue la dirección de su billetera Nautilus en la parte superior.
Esto mostrará todas las transacciones dentro y fuera de su billetera Nautilus.
La última transacción saliente mostrará que está ingresando en la dirección de su billetera Poseidon.
A la izquierda de la página, se mostrará el txid (es decir, hash de transacción).
O en la billetera nautilus, haga clic una vez en la transacción enviada y verá este Tx-id:
Tome y guarde este txid y cópielo porque lo necesitará más adelante.

** MUY IMPORTANTE: Hay 2 hashes para cada transacción.
Existe el hash de transacción (txid) y el hash de bloque.
Debe usar el hash de transacción (txid) para que funcione el proceso de configuración de masternode.
Hay una manera muy fácil de saber cuál es el txid.
El txid está en el lado izquierdo de la lista general de transacciones de su billetera.
Una vez que haga clic en el txid en sí, verá el hash de bloque mostrado.
o no usar el hash de bloque.
Use el txid en el lado más a la izquierda de su lista de transacciones de billetera en Poseidon **

![](https://cdn-images-1.medium.com/max/1600/0*1LTQiVdFomhRei6u.png)
![](https://cdn-images-1.medium.com/max/1600/0*bVaXgKomLeN0mEYQ.png)

En la billetera de nautilus, haga clic una vez en la transacción enviada y ve este Tx-id:

{{< imagesurlsheaders "cloud/txnautilus.png" >}}

## Contrato de Ejecución de Nautilus

Ahora que tenemos la parte más difícil del camino, sigamos con Nautilus y agregando el contrato de Pirl Masternode.

** Abra Nautilus ** y navegue a la pestaña ** Contrato ** ubicada en la esquina superior derecha.

![](https://cdn-images-1.medium.com/max/1600/0*OW_7W9P_u0k7ZdmZ.png)

Una vez allí, haga clic en el botón **Ver contrato**.

![](https://cdn-images-1.medium.com/max/1600/0*wZbZlfAdjrUuhr53.png)

Hay dos contratos 1 para cada tipo de nodo,
El JSON es para todos los Masternodes el mismo.

** Contenido MN: ** Para ** Dirección del contrato ** rellene `0x6c042141C302C354509d2bff30EEFDEF24dE1047`.
El nombre del contrato ** Nombre del contrato ** para esto es contenido
aunque puede ser lo que quieras.
Y, por último, el campo ** Interfaz JSON ** debe rellenarse con:

```
[{"constant":false,"inputs":[],"name":"nodeRegistration","outputs":[{"name":"paid","type":"bool"}],"payable":true,"stateMutability":"payable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeAddress","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"moderators","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"nodes","outputs":[{"name":"pirlAddress","type":"address"},{"name":"nodeStake","type":"uint256"},{"name":"nodeHash","type":"bytes20"},{"name":"stakeLocked","type":"bool"},{"name":"nodeEnabled","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNodeRegistration","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeCost","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getStakeLockedStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeCount","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"_admin","type":"address"}],"name":"setAdmin","outputs":[{"name":"set","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"owner","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNode","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeRegistrationEnabled","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNode","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[],"name":"withdrawStake","outputs":[{"name":"withdrawn","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"","type":"uint256"}],"name":"nodeAddresses","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeEnabledStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeStake","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNodeRegistration","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeHash","outputs":[{"name":"","type":"bytes20"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeFee","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"admin","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"inputs":[],"payable":false,"stateMutability":"nonpayable","type":"constructor"},{"payable":true,"stateMutability":"payable","type":"fallback"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeRegistered","type":"bool"},{"indexed":false,"name":"_dateRegistered","type":"uint256"}],"name":"MasterNodeRegistered","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeDisabled","type":"bool"},{"indexed":false,"name":"_dateDisabled","type":"uint256"}],"name":"MasterNodeDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeEnabled","type":"bool"},{"indexed":false,"name":"_dateEnabled","type":"uint256"}],"name":"MasterNodeEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodePaid","type":"bool"},{"indexed":false,"name":"_datePaid","type":"uint256"}],"name":"MasterNodeRewarded","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_stakeWithdrawn","type":"bool"},{"indexed":false,"name":"_dateWithdrawn","type":"uint256"}],"name":"StakeWithdrawn","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateEnabled","type":"uint256"},{"indexed":true,"name":"_registrationEnabled","type":"bool"}],"name":"MasterNodeRegistrationEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateDisabled","type":"uint256"},{"indexed":true,"name":"_registrationDisabled","type":"bool"}],"name":"MasterNodeRegistrationDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_admin","type":"address"},{"indexed":true,"name":"_adminSet","type":"bool"}],"name":"SetAdmin","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_newOwner","type":"address"},{"indexed":true,"name":"_ownerChanged","type":"bool"}],"name":"TransferOwnership","type":"event"}]
```

Seleccione el nuevo contrato de dirección de Masternode y verá las funciones disponibles para él como un menú desplegable en el lado derecho debajo del encabezado **Escribir en el contrato**.
Bajo las funciones disponibles, seleccione ** Registro de nodo ** y seleccione la billetera que contiene su 10,000 Pirl for Content MN.
Debajo de eso, complete ** 10,000 Pirl ** para Content MN para enviar la participación al contrato.

{{< imagesurlsheaders "cloud/10k.png" >}}

Una vez que presione ** ejecutar **, ingrese su ** contraseña UTC **y asegúrese de proporcionar ** al menos 121,000 gasolina** para la transacción.

Este es un buen momento para tomar un poco de café o té y dejar que todo se sincronice. 3-5 minutos deben hacer el truco.

## Crear / Lanzar servidor CentOS Linux

Verifique que el servidor cumpla con las especificaciones apropiadas como se indica en el [Tutorial de configuración de Pirl Masternode](https://pirl.io/blog/1-pirl-masternode-setup-tutorial)

El servidor debe ejecutar la distribución CentOS 7 de Linux si planea usar la configuración **Masternode de un solo clic**.

> **Note** Registro de la dirección IP pública estática del servidor, así como la contraseña de root.
> Recomendamos iniciar sesión en ese servidor una vez para asegurar que las credenciales de `root` funcionen.
> No es necesario realizar ninguna otra acción en el servidor después de eso.
> De hecho, es preferible que no haga ningún otro ajuste, en absoluto.

## Crear Masternodo en Poseidon

Inicie sesión en Poseidon y navegue hasta la página que agrega un masternode ubicado aquí:
https://poseidon.pirl.io/dashboard/masternodes/  
and hit the:  

{{< imagesurlsheaders "cloud/redcrossadd.jpg" >}}

entonces obtienes esta bonita pantalla emergente:


{{< imagesurlsheaders "cloud/Create_content_Masternode_Record_in_Poseidon.png" >}}

El nombre puede ser lo que quieras.
La identificación de Masternode Wallet es la dirección de su billetera Nautilus, la que contiene 10,000 Pirl en la actualidad.
Y recuerda,
El campo de validación de hash de Tx necesita el txid (¡no el hash de bloque, ver más arriba!) de la transacción que envía a su billetera Poseidon.

** En la parte inferior de la captura de pantalla anterior, deberás seleccionar que el MN sea Contenido (apuesta de 10 K) **

Presione ** Guardar cambios ** y luego verá la siguiente pantalla.

{{< imagesurlsheaders "cloud/one_click_setup.PNG" >}}

## Configuración de Masternodo con un Clic

Asegúrese de que conoce la dirección IP estática pública y las credenciales `root` antes de continuar.

{{< imagesurlsheaders "cloud/one_click_setup.PNG" >}}

Vamos y completamos todos los campos.
ssh por defecto es puerto: 22
Presione ** Guardar cambios ** y luego verá la siguiente pantalla.

{{< imagesurlsheaders "cloud/Done.PNG" >}}

Después de volver a la pantalla **My Masternodes**, observe que el campo **Managed by Poseidon** de masternode está configurado en `True`

{{< imagesurlsheaders "cloud/managed.jpg" >}}

Espere 30 minutos para que se complete el proceso. Puede hacer clic en el botón **detalles** para monitorear el estado.

Mira cómo se sincroniza el proceso de masternode con la cadena de bloques:

```
journalctl -f
```

Una vez que se muestran mensajes como los siguientes, su masternode ahora está sincronizado y contribuyendo a la red.

{{< imagesurlsheaders "cloud/vps.jpg" >}}

## Vigilancia

No recomendamos el acceso activo en el servidor. Sin embargo, si desea verificar el estado, inicie sesión en su servidor y ejecute el siguiente comando:

```
journalctl -f
```

su masternode está contribuyendo a la red si se ve así:

{{< imagesurlsheaders "cloud/vps.jpg" >}}

Controle el estado de su masternode consultando la página Detalles de Poseidon Masternode haciendo clic en la 🔍.
Un nodo en funcionamiento debe aparecer como sigue:

{{< imagesurlsheaders "cloud/detailsmn.png" >}}

---
Autor(s):

Equipo de Pirl

Contribuyente(s):

@Dptelecom
