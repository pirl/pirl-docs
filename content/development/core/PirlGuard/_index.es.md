---
title: PirlGuard
weight: 6
pre: "<b>6. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/pirlguard.png"  >}}


## PirlGuard - Solución innovadora contra ataques del 51%.


<iframe width="560" height="315" src="https://www.youtube.com/embed/Q-f01eFYlig" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


El bloque 2,442,442 de pirl es un evento histórico no solo para Pirl sino para la seguridad de la cadena de bloques en general.


Como la mayoría de la comunidad de Pirl es consciente de que el equipo de Pirl durante varios meses ha estado investigando diferentes maneras de asegurar nuestra cadena de bloques contra ASICS y ataques del 51%, abiertamente dentro de nuestra Discord y detrás de escena. Durante este tiempo, Pirl fue víctima de un ataque del 51% junto con muchas otras cadenas de bloque.



{{< imagesurlsheaders "cloud/1.png" >}}




Uno de los factores de amenaza contribuyentes que recientemente ha hecho que casi todos los mecanismos de consenso de PoW sean susceptibles a los ataques del 51% ha sido la disminución de las ganancias mineras que han llevado a cantidades excesivas de poder hash barato.


La mayoría de las fuentes disponibles explican la complejidad de esos ataques y muestran soluciones de PoS y de terceros como una buena medida para protegerse contra tales ataques. Una solución consistiría en deshacer la cadena de bloques, lo que aún perjudicaría a los mineros, inversores y tenedores de Pirl. Si bien un mecanismo de consenso de PoS también es vulnerable a otros tipos de ataques, como el ataque "Nothing-At-Stake".


Después de una investigación y análisis exhaustivos de los métodos de seguridad de blockchain, el equipo de Pirl no vio ninguna de las opciones disponibles actualmente como medidas prevenibles a largo plazo aceptables contra estos tipos de ataques. Esto dejó al equipo con la única opción posible disponible, desarrollar un nuevo protocolo de seguridad.


Para comprender el protocolo PirlGuard, incluido cómo y por qué detrás de Pirl el desarrollo de la solución innovadora, debe comprender cómo funciona un ataque del 51%. Si confía en su conocimiento sobre la anatomía de un ataque del 51%, no dude en pasar a la sección "¿Cómo funciona PirlGuard?" De este artículo.


## Cómo funciona un ataque del 51%


Fuente: [CoinMonks](https://medium.com/coinmonks/what-is-a-51-attack-or-double-spend-attack-aa108db63474)


Autor: [Jimi.S](https://twitter.com/JimiSinnige)


Cuando un propietario de Bitcoin firma una transacción, se coloca en un grupo local de transacciones no confirmadas. Los mineros seleccionan las transacciones de estos grupos para formar un bloque de transacciones. Para agregar este bloque de transacciones a la cadena de bloques,
Necesitan encontrar una solución a un problema matemático muy difícil. Intentan encontrar esta solución usando el poder computacional. Esto se llama hash. 
Mientras más poder computacional tenga un minero, mayores serán sus posibilidades de encontrar una solución antes de que otros mineros encuentren la suya. Cuando un minero encuentra una solución,
se emitirá (junto con su bloque) a los otros mineros y lo verificarán si todas las transacciones dentro del bloque son válidas de acuerdo con el registro de transacciones existente en la cadena de bloques.
Tenga en cuenta que incluso un minero dañado nunca puede crear una transacción para otra persona porque necesitarían la firma digital de esa persona para hacer eso (su clave privada).
Por lo tanto, enviar Bitcoin desde la cuenta de otra persona es simplemente imposible sin tener acceso a la clave privada correspondiente.


## Minería sigilosa - creando una descendencia de la cadena de bloques


Ahora presta atención. Sin embargo, un minero malicioso puede intentar revertir las transacciones existentes. Cuando un minero encuentra una solución, se supone que se transmite a todos los demás mineros para que puedan verificarla después de que el bloque se agregue a la cadena de bloques (los mineros alcanzan el consenso). Sin embargo, un minero corrupto puede crear una descendencia de la cadena de bloques al no transmitir las soluciones de sus bloques al resto de la red. Ahora hay dos versiones de la blockchain.



{{< imagesurlsheaders "cloud/2.png" >}}



Ahora hay dos versiones de la cadena de bloques. La cadena de bloques roja se puede considerar en modo "sigiloso".


Una versión que está siendo seguida por los mineros no corrompidos, y otra vez que está siendo seguida por el minero corrompido. El minero corrompido ahora está trabajando en su propia versión de esa cadena de bloques y no está transmitiendo al resto de la red. El resto de la red no responde a esta cadena, porque después de todo, no se ha emitido. Está aislado al resto de la red. El minero corrupto ahora puede gastar todos sus Bitcoins en la versión de la cadena de bloques, en la que están todos los demás mineros. Digamos que lo gasta en un Lamborghini, por ejemplo. En la cadena de bloques, sus Bitcoins ahora se gastan. Mientras tanto, no incluye estas transacciones en su versión de la cadena de bloques. En su versión aislada de la cadena de bloques, todavía tiene esos Bitcoins.



{{< imagesurlsheaders "cloud/3.png" >}}


Mientras tanto, él todavía está recogiendo bloques y los verifica todos él mismo en su versión aislada de la cadena de bloques. Aquí es donde comienzan todos los problemas ... La cadena de bloques está programada para seguir un modelo de gobierno democrático, también conocido como la mayoría. La cadena de bloques hace esto siempre siguiendo la cadena más larga; después de todo, la mayoría de los mineros agregan bloques a su versión de la cadena de bloques más rápido que el resto de la red (por lo tanto, la cadena más larga = la mayoría). Así es como la cadena de bloques determina qué versión de su cadena es la verdadera y, a su vez, en qué se basan todos los saldos de billeteras. Una carrera ya ha comenzado. Quien tenga más poder de hash agregará bloques más rápido a su versión de la cadena de bloques.



{{< imagesurlsheaders "cloud/4.png" >}}



## Una carrera: Revertir las transacciones existentes mediante la transmisión de una nueva cadena


El minero corrupto ahora intentará agregar bloques a su cadena de bloques aislada más rápido que los otros mineros agregan bloques a la cadena de bloques (verdadera). Tan pronto como el minero corrupto crea una cadena de bloques más larga, de repente transmite esta versión de la cadena de bloques al resto de la red. El resto de la red ahora detectará que esta versión (corrupta) de la cadena de bloques es en realidad más larga que la que estaban trabajando, y el protocolo los obliga a cambiar a esta cadena.



{{< imagesurlsheaders "cloud/5.png" >}}


La cadena de bloques corrupta ahora se considera la cadena de bloques verdadera, y todas las transacciones que no están incluidas en esta cadena se revertirán de inmediato. El atacante ha gastado sus Bitcoins en un Lamborghini antes, pero esta transacción no se incluyó en su cadena de bloques sigilosa, la cadena que ahora tiene el control, por lo que ahora está otra vez en control de esos Bitcoins. Él es capaz de gastarlos de nuevo.



{{< imagesurlsheaders "cloud/6.png" >}}



* Este es un ataque de doble gasto. *

Se le conoce comúnmente como un ataque del 51% porque el minero malicioso requerirá más poder de hash que el resto de la red combinada (por lo tanto, el 51% del poder de hash) para agregar bloques a su versión de la cadena de bloques más rápido, lo que le permitirá construir una cadena más larga.


Ahora que sabemos cómo funciona el ataque, podemos resumirlo en unos pocos momentos clave.


A) The attacker needs to mine his own version of the blockchain in private with hashrate greater than the one on the main network in order to be faster and create a longer chain. This is often a race for getting a chain with 10–20–50 blocks longer.A) El atacante necesita minar su propia versión de la cadena de bloques en privado con hashrate mayor que el de la red principal para ser más rápido y crear una cadena más larga. Esta es a menudo una carrera para obtener una cadena con 10–20–50 bloques más largos.


B) Una vez que esté en posesión de una cadena de bloques más larga, necesita transmitirla a la red. Entonces la red necesita reconocerla como la cadena más larga y aceptarla.


C) Una doble inversión exitosa dejaría huérfanas a las transacciones iniciales haciendo que las monedas estén disponibles en la cartera del atacante una vez más después de la cadena más larga aplicada.


## Cómo funciona PirlGuard?


Para interrumpir la mecánica detrás del ataque del 51% que permite que un atacante tenga éxito, hemos implementado una solución central con un algoritmo de consenso modificado que defenderá nuestra cadena de bloques y muchas otras en el futuro cercano de casi todos los ataques del 51%.


## Sistema PirlGuard
Con el protocolo PirlGuard desplegado, las posibilidades de que un ataque tenga éxito se reducen enormemente. Como sabemos, una vez que el atacante haya creado una cadena más larga mediante la minería privada de una cadena separada, tendrá que transmitirla a la red. Una vez que el atacante abre su nodo, intentará conectar con el resto de los nodos de la red, diciéndoles que están equivocados. Sin embargo, una vez que esto suceda, PirlGuard eliminará a los par y los penalizará al sentenciarlos a explotar X la cantidad de bloqueos de penalización debido a su minería sin par. La cantidad de bloqueos de penalización asignada depende de la cantidad de bloques que el minero malicioso extrajo en privado.Con el protocolo PirlGuard desplegado, las posibilidades de que un ataque tenga éxito se reducen enormemente. Como sabemos, una vez que el atacante haya creado una cadena más larga mediante la minería privada de una cadena separada, tendrá que transmitirla a la red. Una vez que el atacante abre su nodo, intentará conectar con el resto de los nodos de la red, diciéndoles que están equivocados. Sin embargo, una vez que esto suceda, PirlGuard eliminará a los par y los penalizará al sentenciarlos a minar X la cantidad de bloques de penalización debido a su minería sin par. La cantidad de bloques de penalización asignada depende de la cantidad de bloques que el minero malicioso extrajo en privado.



{{< imagesurlsheaders "cloud/7.png" >}}


El protocolo de seguridad PirlGuard disuade en gran medida a los atacantes de intentar ataques maliciosos, lo que da a la red principal un impulso muy necesario en la seguridad. Este nuevo mecanismo de seguridad reduce las posibilidades a aproximadamente 0.03%.


Pero, esta no es la única medida de seguridad que hemos preparado.


## Masternode operaba contratos notariales en múltiples cadenas de bloques y sistemas de monitoreo.


Los masternodes tomarán un nuevo rol en conjunto con sus otras funciones de utilidad. Notizarán la cadena de bloques y se les permitirá actuar en el proceso de penalizar a los malos actores y preservar un consenso honesto sobre la cadena de bloques de Pirl.


En caso de que un atacante aún esté determinado a aplicar una gran cantidad de fondos y recursos para probar suerte (0.03% de probabilidad), y de alguna manera logre imponer una cadena más larga en la red, un sistema de monitoreo huérfano recién iniciado detectará las reorganizaciones de bloques huérfanos Lo que alertará al equipo para tomar las medidas necesarias y contramedidas.


Como medida de seguridad adicional, el contrato de notario se implementará tanto en las cadenas de bloques de Pirl como en las de Ethereum.


## Incrementando la cantidad de confirmaciones requeridas para intercambios.


Una medida adicional que se implementará es un requisito más alto de confirmaciones de bloque en los intercambios para validar los depósitos. Otro paso para hacer que un ataque sea casi imposible y que ni siquiera valga la pena el tiempo de un atacante.


##  Código Abierto


Hasta el momento, Pirl ha contribuido a la cadena de bloques desarrollando la primera red masternode basada en el código Ethash, la primera implementación privada de IPFS que se ejecuta en una red masternode, y actualmente está trabajando en su propia solución de almacenamiento de cadena de bloques cifrada.
El Protocolo de seguridad PirlGuard se agregará a nuestra biblioteca de código abierto junto con el núcleo del proyecto.
En Pirl estamos desarrollando para revolucionar y modernizar la tecnología de cadena de bloques para toda la industria de cadena de bloques. Esto significa que nuestro código estará disponible para que cualquier persona estudie, eduque, pruebe, modifique o aplique a su propia seguridad de red de cadena de bloques contra futuros ataques del 51%.


[Código Abierto:](https://git.pirl.io/community/pirl)
[Sitio web:](https://pirl.io/en)



#Juntos Pirl es fuerte



Suyo,

Equipo de PIRL


---
Autor(s):  

@Fawkes

Contribuyente(s):

@dptelecom
