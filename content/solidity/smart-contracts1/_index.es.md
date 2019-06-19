---
title: Contratos Inteligentes I
weight: 5
pre: "<b>5. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/smartcontract.png"  >}}



## Introducción

Contratos inteligentes. Los contratos inteligentes son piezas de código que viven en la cadena de bloques y ejecutan comandos exactamente como se les dijo. Pueden leer otros contratos, tomar decisiones, enviar mensajes y ejecutar otros contratos. Los contratos existirán y se ejecutarán mientras exista toda la red, y solo se detendrán si se quedan sin gas o si se programaron para autodestruirse.

¿Qué puedes hacer con los contratos? Puede hacer casi cualquier cosa realmente, pero para esta guía hagamos algunas cosas simples: obtendrá fondos a través de un crowdfunding que, si tiene éxito, proporcionará una organización democrática y radicalmente transparente que solo obedecerá a sus propios ciudadanos, nunca se alejará de ellos. Su constitución y no puede ser censurado o clausurado. Y todo eso en menos de 300 líneas de código.

Así que vamos a empezar.


## Tu primer ciudadano: El Greeter.

El Greeter es una entidad digital inteligente que vive en la cadena de bloques y puede tener conversaciones con cualquier persona que interactúe con él, según su entrada. Puede que no sea un hablador, pero es un gran oyente. Aquí está su código:

```js
contract mortal {
    /* Define variable owner of the type address*/
    address owner;

    /* this function is executed at initialization and sets the owner of the contract */
    function mortal() { owner = msg.sender; }

    /* Function to recover the funds on the contract */
    function kill() { if (msg.sender == owner) suicide(owner); }
}

contract greeter is mortal {
    /* define variable greeting of the type string */
    string greeting;

    /* this runs when the contract is executed */
    function greeter(string _greeting) public {
        greeting = _greeting;
    }

    /* main function */
    function greet() constant returns (string) {
        return greeting;
    }
}
```

Notarás que hay dos contratos diferentes en este código: _"mortal"_ and _"greeter"_.  Esto se debe a que Solidity (el lenguaje de contrato de alto nivel que estamos usando) tiene * herencia *, lo que significa que un contrato puede heredar las características de otro. Esto es muy útil para simplificar la codificación, ya que los rasgos comunes de los contratos no tienen que reescribirse cada vez, y todos los contratos se pueden escribir en partes más pequeñas y más legibles. Entonces, al simplemente declarar que _greeter es mortal_ heredó todas las características del contrato "mortal" y mantuvo el código de bienvenida simple y fácil de leer.

La característica heredada _ "mortal" _ simplemente significa que el contrato de bienvenida puede ser cancelado por su propietario, para limpiar la cadena de bloques y recuperar los fondos bloqueados cuando el contrato ya no es necesario. Los contratos en Pirl son, por defecto, inmortales y no tienen propietario, lo que significa que una vez implementado, el autor ya no tiene privilegios especiales. Considere esto antes de desplegar.

### Instalando un compilador

Sin embargo, antes de poder implementarlo, necesitará dos cosas: el código compilado y la interfaz binaria de la aplicación, que es una especie de plantilla de referencia que define cómo interactuar con el contrato.

Lo primero que puedes conseguir usando un compilador. Deberías tener un compilador de solidity integrado en tu consola pirl. Para probarlo, use este comando:

    eth.getCompilers()

Si lo tiene instalado, debería mostrar algo como esto:

    ['Solidity' ]

Si, en cambio, el comando devuelve un error, entonces debe instalarlo.

#### Usando un compilador en línea

Si no tiene instalado solC, tenemos un [compilador solidity en línea](https://chriseth.github.io/cpp-Pirl/) disponible. Pero tenga en cuenta que ** si el compilador está comprometido, su contrato no es seguro **. Por este motivo, si desea utilizar el compilador en línea, le recomendamos que [aloje el suyo propio] (https://github.com/chriseth/browser-solidity).

#### Instalar SolC en Ubuntu

Presione control + c para salir de la consola (o escriba _exit_) y volver a la línea de comandos. Abre el terminal y ejecuta estos comandos:

    sudo add-apt-repository ppa:Pirl/Pirl
    sudo apt-get update
    sudo apt-get install solc
    which solc

Tome nota del camino dado por la última línea, lo necesitará pronto.

#### Instalar SolC en Mac OSX

Necesitas [brew] (http://brew.sh) para instalar en tu mac

    brew tap Pirl/Pirl
    brew install solidity
    which solc

Tome nota del camino dado por la última línea, lo necesitará pronto.

#### Instalar SolC en Windows

Necesitas [chocolatey] (http://chocolatey.org) para instalar solc.

    cinst -pre solC-stable

Windows es más complicado que eso, tendrás que esperar un poco más.

Si tiene el compilador SolC Solidity instalado, ahora necesita reformatear eliminando espacios para que quepa en una variable de cadena [(hay algunas herramientas en línea que lo harán)] (http://www.textfixer.com/tools/remove -line-breaks.php):

#### Compilar desde la fuente

    git clone https://github.com/Pirl/cpp-Pirl.git
    mkdir cpp-Pirl/build
    cd cpp-Pirl/build
    cmake -DJSONRPC=OFF -DMINER=OFF -DETHKEY=OFF -DSERPENT=OFF -DGUI=OFF -DTESTS=OFF -DJSCONSOLE=OFF ..
    make -j4
    make install
    which solc

#### Vinculando tu compilador en pirl

Ahora [vuelve a la consola] (../ pirl) y escribe este comando para instalar solC, reemplazando _path / to / solc_ a la ruta que obtuviste en el último comando que hiciste:

    admin.setSolc("path/to/solc")

Ahora escribe de nuevo:

    eth.getCompilers()

Si ahora tiene solC instalado, entonces felicitaciones, puede seguir leyendo. Si no lo hace, vaya a nuestros [foros] (http://forum.Pirl.org) o [subreddit] (http://www.reddit.com/r/Pirl) y regañenos por no hacer el proceso es más fácil.


### Compilando tu contrato


Si tiene el compilador instalado, ahora necesita reformatear su contrato eliminando saltos de línea para que se ajuste a una variable de cadena [(hay algunas herramientas en línea que lo harán)] (http://www.textfixer.com/tools /remove-line-breaks.php):

    var greeterSource = 'contract mortal { address owner; function mortal() { owner = msg.sender; } function kill() { if (msg.sender == owner) suicide(owner); } } contract greeter is mortal { string greeting; function greeter(string _greeting) public { greeting = _greeting; } function greet() constant returns (string) { return greeting; } }'

    var greeterCompiled = web3.eth.compile.solidity(greeterSource)

Ahora has compilado tu código. Ahora necesita prepararlo para la implementación, esto incluye configurar algunas variables, como cuál es su saludo. Edite la primera línea a continuación para algo más interesante que "¡Hola mundo!" Y ejecute estos comandos:

    var _greeting = "Hello World!"
    var greeterContract = web3.eth.contract(greeterCompiled.greeter.info.abiDefinition);

    var greeter = greeterContract.new(_greeting,{from:web3.eth.accounts[0], data: greeterCompiled.greeter.code, gas: 1000000}, function(e, contract){
      if(!e) {

        if(!contract.address) {
          console.log("Contract transaction send: TransactionHash: " + contract.transactionHash + " waiting to be mined...");

        } else {
          console.log("Contract mined! Address: " + contract.address);
          console.log(contract);
        }

      }
    })


### Correr el Greeter

In Para llamar a su bot, simplemente escriba el siguiente comando en su terminal:

    greeter.greet();

Como esta llamada no cambia nada en la cadena de bloques, regresa al instante y sin ningún costo de combustible. Deberías verlo devolver tu saludo:

    'Hello World!'


### Lograr que otras personas interactúen con tu código

Para que otras personas ejecuten su contrato necesitan dos cosas: la dirección donde se encuentra el contrato y la ABI (Interfaz binaria de aplicación), que es una especie de manual de usuario, que describe el nombre de sus funciones y cómo llamarlas. Para que cada uno de ellos ejecute estos comandos:

    greeterCompiled.greeter.info.abiDefinition;
    greeter.address;

Luego, puede crear una instancia de un objeto javascript que se puede usar para solicitar el contrato en cualquier máquina conectada a la red. Reemplace 'ABI' y 'dirección' para crear un objeto de contrato en javascript:

    var greeter = eth.contract(ABI).at(Address);

Este ejemplo en particular puede ser instanciado por cualquier persona simplemente llamando a:

    var greeter2 = eth.contract([{constant:false,inputs:[],name:'kill',outputs:[],type:'function'},{constant:true,inputs:[],name:'greet',outputs:[{name:'',type:'string'}],type:'function'},{inputs:[{name:'_greeting',type:'string'}],type:'constructor'}]).at('greeterAddress');

Reemplace _greeterAddress_ con la dirección de su contrato.


** Sugerencia: si el compilador de solidity no está instalado correctamente en su máquina, puede obtener el ABI del compilador en línea. Para hacerlo, use el código siguiente y reemplaza cuidadosamente _greeterCompiled.greeter.info.abiDefinition_ con el abi de su compilador. **


### Limpiando tu mismo

Debe estar muy emocionado de tener su primer contrato en vivo, pero esta emoción desaparece a veces, cuando los propietarios escriben nuevos contratos, lo que lleva a la desagradable vista de los contratos abandonados en la cadena de bloques. En el futuro, la renta de la cadena de bloques podría implementarse para aumentar la escalabilidad de la cadena de bloques pero, por el momento, sea un buen ciudadano y humanamente elimine los robots abandonados.

A diferencia de la última vez, no haremos una llamada ya que deseamos cambiar algo en la cadena de bloques. Esto requiere que se envíe una transacción a la red y se pague una tarifa por los cambios realizados. El suicidio está subsidiado por la red, por lo que costará mucho menos que una transacción habitual.

    greeter.kill.sendTransaction({from:eth.accounts[0]})

Puede verificar que la escritura se realiza simplemente viendo si esto devuelve 0:

    eth.getCode(greeter.contractAddress)

Tenga en cuenta que cada contrato tiene que implementar su propia cláusula de muerte. En este caso particular, solo la cuenta que creó el contrato puede matarlo.

Si no agrega ninguna cláusula de muerte, podría vivir para siempre (o al menos hasta que se eliminen todos los contratos de la frontera) independientemente de usted y de cualquier frontera terrestre, así que antes de ponerlo en marcha, verifique lo que dicen sus leyes locales al respecto, incluyendo cualquier posible limitación en la exportación de tecnología, restricciones en el habla y tal vez cualquier legislación sobre los derechos civiles de los seres digitales sensibles. Trata a tus robots con humanidad.





## La moneda

¿Qué es una moneda? Las monedas son mucho más interesantes y útiles de lo que parecen, en esencia son solo un token intercambiable, pero pueden llegar a ser mucho más, dependiendo de cómo las uses. Su valor depende de lo que haga con él: se puede usar un token para controlar el acceso (** un ticket de entrada **), se puede usar para los derechos de voto en una organización (** una acción **), se pueden colocar como marcadores de posición para un activo en poder de un tercero (** un certificado de propiedad **) o incluso se puede usar simplemente como un intercambio de valor dentro de una comunidad (** una moneda **).

Puede hacer todas esas cosas creando un servidor centralizado, pero el uso de un contrato de token Pirl viene con algunas funcionalidades gratuitas: por un lado, es un servicio descentralizado y los tokens pueden intercambiarse incluso si el servicio original se desactiva por cualquier motivo. El código puede garantizar que nunca se crearán tokens distintos a los establecidos en el código original. Finalmente, al hacer que cada usuario tenga su propio token, esto elimina los escenarios en los que un solo servidor puede provocar la pérdida de fondos de miles de clientes.

Puede crear su propio token en una cadena de bloques diferente, pero crear en Pirl es más fácil, así que puede enfocar su energía en la innovación que hará que su moneda se destaque, y es más segura, ya que su seguridad es brindada por todos los mineros que están apoyando la red Pirl. Finalmente, al crear su token en Pirl, su moneda será compatible con cualquier otro contrato que se ejecute en Pirl.

### El código

Este es el código para el contrato que estamos construyendo:

    contract token {
        mapping (address => uint) public coinBalanceOf;
        event CoinTransfer(address sender, address receiver, uint amount);

      /* Initializes contract with initial supply tokens to the creator of the contract */
      function token(uint supply) {
            coinBalanceOf[msg.sender] = supply;
        }

      /* Very simple trade function */
        function sendCoin(address receiver, uint amount) returns(bool sufficient) {
            if (coinBalanceOf[msg.sender] < amount) return false;
            coinBalanceOf[msg.sender] -= amount;
            coinBalanceOf[receiver] += amount;
            CoinTransfer(msg.sender, receiver, amount);
            return true;
        }
    }

Si alguna vez programó, no le resultará difícil entender lo que hace: es un contrato que genera 10 mil tokens al creador del contrato, y luego permite que cualquier persona con saldo suficiente se lo envíe a otros. Estos tokens son la unidad mínima comercializable y no se pueden subdividir, pero para los usuarios finales se podrían presentar como 100 unidades subdivisibles por 100 subunidades, por lo que poseer un solo token representaría tener un 0.01% del total. Si su aplicación necesita una divisibilidad atómica más precisa, aumente la cantidad de emisión inicial.

En este ejemplo, declaramos que la variable "coinBalanceOf" es pública, esto creará automáticamente una función que verifica el saldo de cualquier cuenta.

### Compilar e implementar

** Así que vamos a ejecutarlo! **

    var tokenSource = ' contract token { mapping (address => uint) public coinBalanceOf; event CoinTransfer(address sender, address receiver, uint amount); /* Initializes contract with initial supply tokens to the creator of the contract */ function token(uint supply) { coinBalanceOf[msg.sender] = supply; } /* Very simple trade function */ function sendCoin(address receiver, uint amount) returns(bool sufficient) { if (coinBalanceOf[msg.sender] < amount) return false; coinBalanceOf[msg.sender] -= amount; coinBalanceOf[receiver] += amount; CoinTransfer(msg.sender, receiver, amount); return true; } }'

    var tokenCompiled = eth.compile.solidity(tokenSource)

Ahora configuremos el contrato, tal como lo hicimos en la sección anterior. Cambie el "Suministro inicial" a la cantidad de tokens no divisibles que desee crear. Si desea tener unidades divisibles, debe hacer eso en la interfaz del usuario pero mantenerlas representadas en la unidad de cuenta mínima.

    var supply = 10000;
    var tokenContract = web3.eth.contract(tokenCompiled.token.info.abiDefinition);
    var token = tokenContract.new(
      supply,
      {
        from:web3.eth.accounts[0],
        data:tokenCompiled.token.code,
        gas: 1000000
      }, function(e, contract){
        if(!e) {

          if(!contract.address) {
            console.log("Contract transaction send: TransactionHash: " + contract.transactionHash + " waiting to be mined...");

          } else {
            console.log("Contract mined! Address: " + contract.address);
            console.log(contract);
          }

        }
    })


### Consultar saldo viendo las transferencias de monedas

Si todo funcionó correctamente, debería poder verificar su propio saldo con:

    token.coinBalanceOf(eth.accounts[0]) + " tokens"

Debe tener todas las 10 000 fichas que se crearon una vez que se publicó el contrato. Como no hay ninguna otra forma definida de emitir nuevas monedas, estas son todas las que existirán.

Puede configurar un ** Watcher ** para que reaccione cada vez que alguien envíe una moneda utilizando su contrato. Así es como lo haces:

    var event = token.CoinTransfer({}, '', function(error, result){
      if (!error)
        console.log("Coin transfer: " + result.args.amount + " tokens were sent. Balances now are as following: \n Sender:\t" + result.args.sender + " \t" + token.coinBalanceOf.call(result.args.sender) + " tokens \n Receiver:\t" + result.args.receiver + " \t" + token.coinBalanceOf.call(result.args.receiver) + " tokens" )
    });

### Enviando monedas

Ahora, por supuesto, esos tokens no son muy útiles si los acumulas a todos, así que para enviarlos a otra persona, usa este comando:

    token.sendCoin.sendTransaction(eth.accounts[1], 1000, {from: eth.accounts[0]})

Si un amigo ha registrado un nombre en el registrador, puede enviarlo sin saber su dirección, haciendo esto:

    token.sendCoin.sendTransaction(registrar.addr("Alice"), 2000, {from: eth.accounts[0]})


Tenga en cuenta que nuestra primera función ** coinBalanceOf ** simplemente fue llamada directamente en la instancia del contrato y devolvió un valor. Esto fue posible ya que fue una operación de lectura simple que no incurre en ningún cambio de estado y que se ejecuta de forma local y síncrona. Nuestra segunda función ** sendCoin ** necesita una llamada **. SendTransaction () **. Dado que esta función pretende cambiar el estado (operación de escritura), se envía como una transacción a la red para que los mineros la recojan e incluyan en la cadena de bloques canónica. Como resultado, el estado de consenso de todos los nodos participantes reflejará adecuadamente los cambios de estado resultantes de la ejecución de la transacción. La dirección del remitente debe enviarse como parte de la transacción para financiar el combustible necesario para ejecutar la transacción. Ahora, espere un minuto y verifique los saldos de ambas cuentas:

    token.coinBalanceOf.call(eth.accounts[0])/100 + "% of all tokens"
    token.coinBalanceOf.call(eth.accounts[1])/100 + "% of all tokens"
    token.coinBalanceOf.call(registrar.addr("Alice"))/100 + "% of all tokens"


### Sugerencias de mejora

En este momento, esta criptomoneda es bastante limitada, ya que solo habrá 10,000 monedas y todas están controladas por el creador de monedas, pero puedes cambiar eso. Por ejemplo, podría recompensar a los mineros de Pirl creando una transacción que recompensará a quienes encontraron el bloque actual:

    mapping (uint => address) miningReward;
    function claimMiningReward() {
      if (miningReward[block.number] == 0) {
        coinBalanceOf[block.coinbase] += 1;
        miningReward[block.number] = block.coinbase;
      }
    }

Puede modificar esto para cualquier otra cosa: tal vez recompensar a alguien que encuentre una solución para un nuevo rompecabezas, gane un juego de ajedrez, instale un panel solar, siempre que se pueda traducir de alguna manera a un contrato. O tal vez quiera crear un banco central para su país personal, de modo que pueda hacer un seguimiento de las horas trabajadas, los favores adeudados o el control de la propiedad. En ese caso, es posible que desee agregar una función para permitir que el banco congele fondos de manera remota y destruya tokens si es necesario.


### Registre un nombre para su moneda

Los comandos mencionados solo funcionan porque tiene un objeto token javascript instanciado en su máquina local. Si envías tokens a alguien, no podrán adelantarlos porque no tienen el mismo objeto y no sabrán dónde buscar tu contrato o llamar a sus funciones. De hecho, si reinicia su consola, estos objetos se eliminarán y los contratos en los que ha estado trabajando se perderán para siempre. Entonces, ¿cómo se ejemplifica el contrato en una máquina limpia?

Hay dos maneras. Comencemos con lo rápido y sucio, brindando a sus amigos una referencia al ABI de su contrato:

    token = eth.contract([{constant:false,inputs:[{name:'receiver',type:'address'},{name:'amount',type:'uint256'}],name:'sendCoin',outputs:[{name:'sufficient',type:'bool'}],type:'function'},{constant:true,inputs:[{name:'',type:'address'}],name:'coinBalanceOf',outputs:[{name:'',type:'uint256'}],type:'function'},{inputs:[{name:'supply',type:'uint256'}],type:'constructor'},{anonymous:false,inputs:[{indexed:false,name:'sender',type:'address'},{indexed:false,name:'receiver',type:'address'},{indexed:false,name:'amount',type:'uint256'}],name:'CoinTransfer',type:'event'}]).at('0x4a4ce7844735c4b6fc66392b200ab6fe007cfca8')

Simplemente reemplace la dirección al final de su propia dirección de token, entonces cualquier persona que use este fragmento de código podrá usar su contrato de inmediato. Por supuesto, esto funcionará solo para este contrato específico, así que analicemos paso a paso y veamos cómo mejorar este código para poder usarlo en cualquier lugar.

Todas las cuentas están referenciadas en la red por su dirección pública. Pero las direcciones son largas, difíciles de escribir, difíciles de memorizar e inmutables. El último es especialmente importante si desea poder generar cuentas nuevas a su nombre o actualizar el código de su contrato. Para resolver esto, hay un contrato de registro de nombres predeterminado que se utiliza para asociar las direcciones largas con nombres cortos y amigables para los humanos.

Los nombres deben usar solo caracteres alfanuméricos y no pueden contener espacios en blanco. En futuras versiones, el registrador de nombres probablemente implementará un proceso de licitación para evitar la ocupación de nombres, pero por ahora, funciona por orden de llegada: siempre que nadie más haya registrado el nombre, puede reclamarlo.


Primero, si registra un nombre, no necesitará la dirección codificada al final. Seleccione un buen nombre de moneda e intente reservarlo para usted. Primero, seleccione su nombre:

    var tokenName = "MyFirstCoin"

Luego, verifica la disponibilidad de tu nombre:

    registrar.addr(tokenName)

Si esa función devuelve "0x00 ..", puedes reclamarlo:

    registrar.reserve.sendTransaction(tokenName, {from: eth.accounts[0]});


Espere a que se recoja la transacción anterior. Espera hasta treinta segundos y luego prueba:

    registrar.owner(myName)

Si devuelve su dirección, significa que es el propietario de ese nombre y que puede configurar el nombre elegido en cualquier dirección que desee:

    registrar.setAddress.sendTransaction(tokenName, token.address, true,{from: eth.accounts[0]});

_Puedes reemplazar ** token.address ** por ** eth.accounts [0] ** si quieres usarlo como un apodo personal._

Espere un poco para que la transacción se recoja también y pruébela:

    registrar.addr("MyFirstCoin")

Puede enviar una transacción a cualquier persona o cualquier contrato por nombre en lugar de cuenta simplemente escribiendo

    eth.sendTransaction({from: eth.accounts[0], to: registrar.addr("MyFirstCoin"), value: web3.toWei(1, "ether")})

** Consejo: no mezclar registrar.addr por registrar.owner. La primera es a qué dirección se indica ese nombre: cualquiera puede señalar un nombre a cualquier otro lugar, al igual que cualquiera puede reenviar un enlace a google.com, pero solo el propietario del nombre puede cambiar y actualizar el enlace. Puedes configurar ambos para que sean la misma dirección. **

Ahora debería devolver su dirección de token, lo que significa que ahora el código anterior para crear una instancia podría usar un nombre en lugar de una dirección.

    token = eth.contract([{constant:false,inputs:[{name:'receiver',type:'address'},{name:'amount',type:'uint256'}],name:'sendCoin',outputs:[{name:'sufficient',type:'bool'}],type:'function'},{constant:true,inputs:[{name:'',type:'address'}],name:'coinBalanceOf',outputs:[{name:'',type:'uint256'}],type:'function'},{inputs:[{name:'supply',type:'uint256'}],type:'constructor'},{anonymous:false,inputs:[{indexed:false,name:'sender',type:'address'},{indexed:false,name:'receiver',type:'address'},{indexed:false,name:'amount',type:'uint256'}],name:'CoinTransfer',type:'event'}]).at(registrar.addr("MyFirstCoin"))

Esto también significa que el propietario de la moneda puede actualizar la moneda indicando al registrador el nuevo contrato. Por supuesto, esto requeriría que los tenedores de monedas confíen en el propietario establecido en registrar.owner ("MyFirstCoin")

### Aprende más

* [Estándar de la moneda meta] (https://github.com/Pirl/wiki/wiki/Standardized_Contract_APIs) es una propuesta de estandarización de los nombres de funciones para los contratos de monedas y fichas, para permitir que se agreguen automáticamente a otro contrato de Pirl que utiliza el comercio , como intercambios o escrow.

* [Prueba formal] (https://github.com/Pirl/wiki/wiki/Pirl-Natural-Specification-Format#documentation-output) es una forma en la que el desarrollador del contrato podrá afirmar algunas cualidades invariables del contrato. , como la tapa total de la moneda. *Aun no implementado*.



# Multitud financia tu idea

A veces una buena idea requiere muchos fondos y esfuerzo colectivo. Puede solicitar donaciones, pero los donantes prefieren donar a proyectos que tienen más certeza de que obtendrán la tracción y la financiación adecuada. Este es un ejemplo donde un crowdfunding sería ideal: establece un objetivo y una fecha límite para alcanzarlo. Si no cumple con su objetivo, se devuelven las donaciones, lo que reduce el riesgo para los donantes. Dado que el código es abierto y auditable, no hay necesidad de una plataforma de confianza centralizada y, por lo tanto, las únicas tarifas que todos pagarán son solo las tarifas de gas.

En una multitud se suelen otorgar premios. Esto requerirá que obtenga la información de contacto de todos y realice un seguimiento de quién posee qué. Pero como acabas de crear tu propio token, ¿por qué no usarlo para hacer un seguimiento de los premios? Esto permite a los donantes poseer inmediatamente algo después de que donaron. Pueden almacenarlo de manera segura, pero también pueden venderlo o intercambiarlo si se dan cuenta de que ya no quieren el premio. Si su idea es algo físico, todo lo que tiene que hacer después de completar el proyecto es entregar el producto a todas las personas que le envíen un token. Si el proyecto es digital, el token en sí mismo puede usarse inmediatamente para que los usuarios participen u obtengan una entrada en su proyecto.

### El código

La forma en que funciona este contrato de venta público en particular es que establezca una tasa de cambio para su ficha y luego los donantes obtendrán de inmediato una cantidad proporcional de fichas a cambio de su éter. También elegirá una meta de financiamiento y una fecha límite: una vez que finalice la fecha límite, puede hacer ping al contrato y, si se alcanzó la meta, le enviará el éter que le ha sido solicitado, de lo contrario, se remite a los donantes. Los donantes mantienen sus fichas incluso si el proyecto no alcanza su objetivo, como prueba de que ayudaron.


    contract token { mapping (address => uint) public coinBalanceOf; function token() {}  function sendCoin(address receiver, uint amount) returns(bool sufficient) {  } }

    contract Crowdsale {

        address public beneficiary;
        uint public fundingGoal; uint public amountRaised; uint public deadline; uint public price;
        token public tokenReward;   
        Funder[] public funders;
        event FundTransfer(address backer, uint amount, bool isContribution);

        /* data structure to hold information about campaign contributors */
        struct Funder {
            address addr;
            uint amount;
        }

        /*  at initialization, setup the owner */
        function Crowdsale(address _beneficiary, uint _fundingGoal, uint _duration, uint _price, token _reward) {
            beneficiary = _beneficiary;
            fundingGoal = _fundingGoal;
            deadline = now + _duration * 1 minutes;
            price = _price;
            tokenReward = token(_reward);
        }   

        /* The function without name is the default function that is called whenever anyone sends funds to a contract */
        function () {
            uint amount = msg.value;
            funders[funders.length++] = Funder({addr: msg.sender, amount: amount});
            amountRaised += amount;
            tokenReward.sendCoin(msg.sender, amount / price);
            FundTransfer(msg.sender, amount, true);
        }

        modifier afterDeadline() { if (now >= deadline) _ }

        /* checks if the goal or time limit has been reached and ends the campaign */
        function checkGoalReached() afterDeadline {
            if (amountRaised >= fundingGoal){
                beneficiary.send(amountRaised);
                FundTransfer(beneficiary, amountRaised, false);
            } else {
                FundTransfer(0, 11, false);
                for (uint i = 0; i < funders.length; ++i) {
                  funders[i].addr.send(funders[i].amount);  
                  FundTransfer(funders[i].addr, funders[i].amount, false);
                }               
            }
            suicide(beneficiary);
        }
    }

### Establecer los parámetros

Antes de continuar, comencemos por establecer los parámetros de la venta pública:

    var _beneficiary = eth.accounts[1];    // create an account for this
    var _fundingGoal = web3.toWei(100, "ether"); // raises 100 ether
    var _duration = 30;     // number of minutes the campaign will last
    var _price = web3.toWei(0.02, "ether"); // the price of the tokens, in ether
    var _reward = token.address;   // the token contract address.

En Beneficiario ponga la nueva dirección que recibirá los fondos recaudados. El objetivo de financiación es la cantidad de éter que se elevará. La fecha límite se mide en tiempos de bloque que tienen un promedio de 12 segundos, por lo que el valor predeterminado es de aproximadamente 4 semanas. El precio es complicado: solo cambia el número 2 por la cantidad de fichas que recibirán los contribuyentes por cada éter donado. Finalmente, la recompensa debe ser la dirección del contrato de token que creó en la última sección.

En este ejemplo, usted está vendiendo la mitad de todos los tokens que alguna vez existieron, a cambio de 100 éter. Decida esos parámetros con mucho cuidado, ya que jugarán un papel muy importante en la próxima parte de nuestra guía.

### Implementar

Ya conoce el ejercicio: si está utilizando el compilador solC, [elimine los saltos de línea] (http://www.textfixer.com/tools/remove-line-breaks.php) y copie los siguientes comandos en el terminal:


    var crowdsaleCompiled = eth.compile.solidity(' contract token { mapping (address => uint) public coinBalanceOf; function token() {} function sendCoin(address receiver, uint amount) returns(bool sufficient) { } } contract Crowdsale { address public beneficiary; uint public fundingGoal; uint public amountRaised; uint public deadline; uint public price; token public tokenReward; Funder[] public funders; event FundTransfer(address backer, uint amount, bool isContribution); /* data structure to hold information about campaign contributors */ struct Funder { address addr; uint amount; } /* at initialization, setup the owner */ function Crowdsale(address _beneficiary, uint _fundingGoal, uint _duration, uint _price, token _reward) { beneficiary = _beneficiary; fundingGoal = _fundingGoal; deadline = now + _duration * 1 minutes; price = _price; tokenReward = token(_reward); } /* The function without name is the default function that is called whenever anyone sends funds to a contract */ function () { Funder f = funders[++funders.length]; f.addr = msg.sender; f.amount = msg.value; amountRaised += f.amount; tokenReward.sendCoin(msg.sender, f.amount/price); FundTransfer(f.addr, f.amount, true); } modifier afterDeadline() { if (now >= deadline) _ } /* checks if the goal or time limit has been reached and ends the campaign */ function checkGoalReached() afterDeadline { if (amountRaised >= fundingGoal){ beneficiary.send(amountRaised); FundTransfer(beneficiary, amountRaised, false); } else { FundTransfer(0, 11, false); for (uint i = 0; i < funders.length; ++i) { funders[i].addr.send(funders[i].amount); FundTransfer(funders[i].addr, funders[i].amount, false); } } suicide(beneficiary); } }');

    var crowdsaleContract = web3.eth.contract(crowdsaleCompiled.Crowdsale.info.abiDefinition);
    var crowdsale = crowdsaleContract.new(
      _beneficiary,
      _fundingGoal,
      _duration,
      _price,
      _reward,
      {
        from:web3.eth.accounts[0],
        data:crowdsaleCompiled.Crowdsale.code,
        gas: 1000000
      }, function(e, contract){
        if(!e) {

          if(!contract.address) {
            console.log("Contract transaction send: TransactionHash: " + contract.transactionHash + " waiting to be mined...");

          } else {
            console.log("Contract mined! Address: " + contract.address);
            console.log(contract);
          }

        }    })


Espera hasta treinta segundos y verás un mensaje como este:

    Contract mined! address: 0xdaa24d02bad7e9d6a80106db164bad9399a0423e

Si recibió esa alerta, entonces su código debería estar en línea. Siempre puedes volver a verificar haciendo esto:

    eth.getCode(crowdsale.address)

¡Ahora financie su contrato recién creado con los tokens necesarios para que pueda distribuir automáticamente las recompensas a los contribuyentes!

    token.sendCoin.sendTransaction(crowdsale.address, 5000,{from: eth.accounts[0]})

Después de seleccionar la transacción, puede verificar la cantidad de tokens que tiene la dirección de crowdsale y todas las demás variables de esta manera:

    "Current crowdsale must raise " + web3.fromWei(crowdsale.fundingGoal.call(), "ether") + " ether in order to send it to " + crowdsale.beneficiary.call() + "."



### Poner algunos observadores

Desea recibir una alerta cada vez que su crowdsale reciba nuevos fondos, así que pegue este código:

    var event = crowdsale.FundTransfer({}, '', function(error, result){
      if (!error)

        if (result.args.isContribution) {
            console.log("\n New backer! Received " + web3.fromWei(result.args.amount, "ether") + " ether from " + result.args.backer  )

            console.log( "\n The current funding at " +( 100 *  crowdsale.amountRaised.call() / crowdsale.fundingGoal.call()) + "% of its goals. Funders have contributed a total of " + web3.fromWei(crowdsale.amountRaised.call(), "ether") + " ether.");

            var timeleft = Math.floor(Date.now() / 1000)-crowdsale.deadline();
            if (timeleft>3600) {  console.log("Deadline has passed, " + Math.floor(timeleft/3600) + " hours ago")
            } else if (timeleft>0) {  console.log("Deadline has passed, " + Math.floor(timeleft/60) + " minutes ago")
            } else if (timeleft>-3600) {  console.log(Math.floor(-1*timeleft/60) + " minutes until deadline")
            } else {  console.log(Math.floor(-1*timeleft/3600) + " hours until deadline")
            }

        } else {
            console.log("Funds transferred from crowdsale account: " + web3.fromWei(result.args.amount, "ether") + " ether to " + result.args.backer  )
        }

    });




### Registrar el contrato

Ahora estás listo. Ahora cualquiera puede contribuir simplemente enviando ether a la dirección de venta masiva, pero para hacerlo aún más sencillo, registremos un nombre para su venta. Primero, elige un nombre para tu crowdsale:

    var name = "mycrowdsale"

Compruebe si está disponible y regístrese:

    registrar.addr(name)
    registrar.reserve.sendTransaction(name, {from: eth.accounts[0]});

Espere a que se recoja la transacción anterior y luego:

    registrar.setAddress.sendTransaction(name, crowdsale.address, true,{from: eth.accounts[0]});


### Contribuir a la Venta Colectiva

Contribuir a la venta colectiva es muy simple, ni siquiera requiere una instanciación del contrato. Esto se debe a que la venta colectiva responde a depósitos de éter simples, por lo que cualquier persona que envíe éter a la venta colectiva recibirá automáticamente una recompensa.
Cualquiera puede contribuir a él simplemente ejecutando este comando:

    var amount = web3.toWei(5, "ether") // decide how much to contribute

    eth.sendTransaction({from: eth.accounts[0], to: crowdsale.address, value: amount, gas: 1000000})


Alternativamente, si desea que alguien más lo envíe, incluso pueden usar el registrador de nombres para contribuir:

    eth.sendTransaction({from: eth.accounts[0], to: registrar.addr("mycrowdsale"), value: amount, gas: 500000})


Ahora espere un minuto para que se recuperen los bloques y puede verificar si el contrato recibió el éter realizando cualquiera de estos comandos:

    web3.fromWei(crowdsale.amountRaised.call(), "ether") + " ether"
    token.coinBalanceOf.call(eth.accounts[0]) + " tokens"
    token.coinBalanceOf.call(crowdsale.address) + " tokens"


### Recuperar fondos

Una vez que se supera el plazo, alguien tiene que despertar el contrato para que los fondos se envíen al beneficiario o se los devuelvan a los financiadores (si esto falla). Esto sucede porque no existe tal cosa como un bucle activo o temporizador en Pirl, por lo que cualquier transacción futura debe ser activada por alguien.

    crowdsale.checkGoalReached.sendTransaction({from:eth.accounts[0], gas: 2000000})

Puedes consultar tus cuentas con estas líneas de código:

    web3.fromWei(eth.getBalance(eth.accounts[0]), "ether") + " ether"
    web3.fromWei(eth.getBalance(eth.accounts[1]), "ether") + " ether"
    token.coinBalanceOf.call(eth.accounts[0]) + " tokens"
    token.coinBalanceOf.call(eth.accounts[1]) + " tokens"

La instancia de crowdsale está configurada para autodestruirse una vez que ha cumplido su tarea, por lo que si el plazo finaliza y todos obtuvieron sus premios, el contrato ya no existe, como puede ver al ejecutar esto:

    eth.getCode(crowdsale.address)

Por lo tanto, recaudó 100 éteres y distribuyó con éxito su moneda original entre los donantes de la multitud. ¿Qué podrías hacer después con esas cosas?






# Democracia DAO



Hasta ahora, ha creado un token intercambiable y lo ha distribuido con éxito entre todos aquellos que estaban dispuestos a ayudar a recaudar fondos para 100 éteres. Eso es todo muy interesante, pero ¿para qué son exactamente esos tokens? ¿Por qué alguien querría poseerlo o cambiarlo por algo valioso? Si puede convencer a su nuevo token es la próxima gran cantidad de dinero, tal vez otros lo querrán, pero hasta ahora su token no ofrece valor per se. Vamos a cambiar eso al crear su primera organización autónoma descentralizada, o DAO.

Piense en la DAO como la constitución de un país, la rama ejecutiva de un gobierno o tal vez como un administrador robótico de una organización. La DAO recibe el dinero que su organización recauda, ​​lo mantiene seguro y lo utiliza para financiar lo que sus miembros quieran. El robot es incorruptible, nunca defraudará al banco, nunca creará planes secretos, nunca usará el dinero para otra cosa que no sea lo que votaron sus electores. La DAO nunca desaparecerá, nunca huirá y no podrá ser controlada por nadie más que sus propios ciudadanos.

El token que distribuimos usando el crowdsale es el único documento ciudadano que se necesita. Cualquiera que tenga un token puede crear y votar propuestas. De manera similar a ser un accionista en una empresa, el token se puede intercambiar en el mercado abierto y el voto es proporcional a las cantidades de tokens que posee el elector.

Tómese un momento para soñar con las posibilidades revolucionarias que esto permitiría, y ahora puede hacerlo usted mismo, en menos de 100 líneas de código:


### El código




    contract token { mapping (address => uint) public coinBalanceOf;   function token() { }   function sendCoin(address receiver, uint amount) returns(bool sufficient) {  } }


    contract Democracy {

        uint public minimumQuorum;
        uint public debatingPeriod;
        token public voterShare;
        address public founder;
        Proposal[] public proposals;
        uint public numProposals;

        event ProposalAdded(uint proposalID, address recipient, uint amount, bytes32 data, string description);
        event Voted(uint proposalID, int position, address voter);
        event ProposalTallied(uint proposalID, int result, uint quorum, bool active);

        struct Proposal {
            address recipient;
            uint amount;
            bytes32 data;
            string description;
            uint creationDate;
            bool active;
            Vote[] votes;
            mapping (address => bool) voted;
        }

        struct Vote {
            int position;
            address voter;
        }

        function Democracy(token _voterShareAddress, uint _minimumQuorum, uint _debatingPeriod) {
            founder = msg.sender;  
            voterShare = token(_voterShareAddress);
            minimumQuorum = _minimumQuorum || 10;
            debatingPeriod = _debatingPeriod * 1 minutes || 30 days;
        }


        function newProposal(address _recipient, uint _amount, bytes32 _data, string _description) returns (uint proposalID) {
            if (voterShare.coinBalanceOf(msg.sender)>0) {
                proposalID = proposals.length++;
                Proposal p = proposals[proposalID];
                p.recipient = _recipient;
                p.amount = _amount;
                p.data = _data;
                p.description = _description;
                p.creationDate = now;
                p.active = true;
                ProposalAdded(proposalID, _recipient, _amount, _data, _description);
                numProposals = proposalID+1;
            }
        }

        function vote(uint _proposalID, int _position) returns (uint voteID){
            if (voterShare.coinBalanceOf(msg.sender)>0 && (_position >= -1 || _position <= 1 )) {
                Proposal p = proposals[_proposalID];
                if (p.voted[msg.sender] == true) return;
                voteID = p.votes.length++;
                p.votes[voteID] = Vote({position: _position, voter: msg.sender});
                p.voted[msg.sender] = true;
                Voted(_proposalID,  _position, msg.sender);
            }
        }

        function executeProposal(uint _proposalID) returns (int result) {
            Proposal p = proposals[_proposalID];
            /* Check if debating period is over */
            if (now > (p.creationDate + debatingPeriod) && p.active){   
                uint quorum = 0;
                /* tally the votes */
                for (uint i = 0; i <  p.votes.length; ++i) {
                    Vote v = p.votes[i];
                    uint voteWeight = voterShare.coinBalanceOf(v.voter);
                    quorum += voteWeight;
                    result += int(voteWeight) * v.position;
                }
                /* execute result */
                if (quorum > minimumQuorum && result > 0 ) {
                    p.recipient.call.value(p.amount)(p.data);
                    p.active = false;
                } else if (quorum > minimumQuorum && result < 0) {
                    p.active = false;
                }
                ProposalTallied(_proposalID, result, quorum, p.active);
            }
        }
    }





Hay mucho que hacer pero es más simple de lo que parece. Las reglas de su organización son muy simples: cualquier persona con al menos un token puede crear propuestas para enviar fondos desde la cuenta del país. Después de una semana de debate y votos, si ha recibido votos por un total de 100 fichas o más y tiene más aprobaciones que rechazos, se enviarán los fondos. Si el quórum no se ha cumplido o termina en un empate, entonces la votación se mantiene hasta que se resuelva. De lo contrario, la propuesta se bloquea y se mantiene con fines históricos.

Así que recapitulemos lo que esto significa: en las dos últimas secciones, usted creó 10,000 fichas, envió 1,000 de ellas a otra cuenta que controla, 2,000 a una amiga llamada Alice y distribuyó 5,000 de ellas a través de una multitud. Esto significa que ya no controlas más del 50% de los votos en la DAO, y si Alice y las bandas de la comunidad se unen, pueden superar cualquier decisión de gasto en los 100 éteres recaudados hasta el momento. Así es exactamente como debería funcionar una democracia. Si ya no quiere ser parte de su país, lo único que puede hacer es vender sus propios tokens en un intercambio descentralizado y optar por no participar, pero no puede evitar que los demás lo hagan.


### Configura tu organización

Así que abre tu consola y preparémonos para finalmente poner tu país en línea. Primero, establezcamos los parámetros correctos, los seleccionamos con cuidado:

    var _voterShareAddress = token.address;
    var _minimumQuorum = 10; // Minimun amount of voter tokens the proposal needs to pass
    var _debatingPeriod = 60; // debating period, in minutes;

Con estos parámetros predeterminados, cualquier persona con cualquier token puede hacer una propuesta sobre cómo gastar el dinero de la organización. La propuesta tiene 1 hora para ser debatida y se aprobará si tiene al menos votos de al menos el 0,1% del total de fichas y tiene más apoyo que rechazos. Elija esos parámetros con cuidado, ya que no podrá cambiarlos en el futuro.

    var daoCompiled = eth.compile.solidity('contract token { mapping (address => uint) public coinBalanceOf; function token() { } function sendCoin(address receiver, uint amount) returns(bool sufficient) { } } contract Democracy { uint public minimumQuorum; uint public debatingPeriod; token public voterShare; address public founder; Proposal[] public proposals; uint public numProposals; event ProposalAdded(uint proposalID, address recipient, uint amount, bytes32 data, string description); event Voted(uint proposalID, int position, address voter); event ProposalTallied(uint proposalID, int result, uint quorum, bool active); struct Proposal { address recipient; uint amount; bytes32 data; string description; uint creationDate; bool active; Vote[] votes; mapping (address => bool) voted; } struct Vote { int position; address voter; } function Democracy(token _voterShareAddress, uint _minimumQuorum, uint _debatingPeriod) { founder = msg.sender; voterShare = token(_voterShareAddress); minimumQuorum = _minimumQuorum || 10; debatingPeriod = _debatingPeriod * 1 minutes || 30 days; } function newProposal(address _recipient, uint _amount, bytes32 _data, string _description) returns (uint proposalID) { if (voterShare.coinBalanceOf(msg.sender)>0) { proposalID = proposals.length++; Proposal p = proposals[proposalID]; p.recipient = _recipient; p.amount = _amount; p.data = _data; p.description = _description; p.creationDate = now; p.active = true; ProposalAdded(proposalID, _recipient, _amount, _data, _description); numProposals = proposalID+1; } else { return 0; } } function vote(uint _proposalID, int _position) returns (uint voteID){ if (voterShare.coinBalanceOf(msg.sender)>0 && (_position >= -1 || _position <= 1 )) { Proposal p = proposals[_proposalID]; if (p.voted[msg.sender] == true) return; voteID = p.votes.length++; Vote v = p.votes[voteID]; v.position = _position; v.voter = msg.sender; p.voted[msg.sender] = true; Voted(_proposalID, _position, msg.sender); } else { return 0; } } function executeProposal(uint _proposalID) returns (int result) { Proposal p = proposals[_proposalID]; /* Check if debating period is over */ if (now > (p.creationDate + debatingPeriod) && p.active){ uint quorum = 0; /* tally the votes */ for (uint i = 0; i < p.votes.length; ++i) { Vote v = p.votes[i]; uint voteWeight = voterShare.coinBalanceOf(v.voter); quorum += voteWeight; result += int(voteWeight) * v.position; } /* execute result */ if (quorum > minimumQuorum && result > 0 ) { p.recipient.call.value(p.amount)(p.data); p.active = false; } else if (quorum > minimumQuorum && result < 0) { p.active = false; } } ProposalTallied(_proposalID, result, quorum, p.active); } }');

    var democracyContract = web3.eth.contract(daoCompiled.Democracy.info.abiDefinition);

    var democracy = democracyContract.new(
        _voterShareAddress,
        _minimumQuorum,
        _debatingPeriod,
        {
          from:web3.eth.accounts[0],
          data:daoCompiled.Democracy.code,
          gas: 3000000
        }, function(e, contract){
          if(!e) {

            if(!contract.address) {
              console.log("Contract transaction send: TransactionHash: " + contract.transactionHash + " waiting to be mined...");

            } else {
              console.log("Contract mined! Address: " + contract.address);
              console.log(contract);
            }

          }      
        })


Espera un minuto hasta que los mineros lo recojan. Te costará unos 850k de gas. Una vez que se recoja, es hora de crear una instancia y configurarla, apuntándola a la dirección correcta del contrato de token que creó anteriormente.

Si todo funcionó, puedes echar un vistazo a toda la organización ejecutando esta cadena:

    "This organization has " +  democracy.numProposals() + " proposals and uses the token at the address " + democracy.voterShare() ;

Si todo está configurado, su DAO debería devolver un recuento de propuestas de 0 y una dirección marcada como "fundador". Si bien todavía no hay propuestas, el fundador de la DAO puede cambiar la dirección del token a cualquier cosa que desee.

### Registre el nombre de su organización

También registremos un nombre para su contrato para que sea fácilmente accesible (¡no olvide verificar la disponibilidad de su nombre con registrar.addr ("nameYouWant") antes de reservar!)

    var name = "MyPersonalDemocracy"
    registrar.reserve.sendTransaction(name, {from: eth.accounts[0]})
    var democracy = eth.contract(daoCompiled.Democracy.info.abiDefinition).at(democracy.address);
    democracy.setup.sendTransaction(registrar.addr("MyFirstCoin"),{from:eth.accounts[0]})

Espere a que se recojan las transacciones anteriores y luego:

    registrar.setAddress.sendTransaction(name, democracy.address, true,{from: eth.accounts[0]});


### Las democracia de los Bots de vigilancia


    var event = democracy.ProposalAdded({}, '', function(error, result){
      if (!error)
        console.log("New Proposal #"+ result.args.proposalID +"!\n Send " + web3.fromWei(result.args.amount, "ether") + " ether to " + result.args.recipient.substring(2,8) + "... for " + result.args.description  )
    });
    var eventVote = democracy.Voted({}, '', function(error, result){
      if (!error)
        var opinion = "";
        if (result.args.position > 0) {
          opinion = "in favor"
        } else if (result.args.position < 0) {
          opinion = "against"
        } else {
          opinion = "abstaining"
        }

        console.log("Vote on Proposal #"+ result.args.proposalID +"!\n " + result.args.voter + " is " + opinion )
    });
    var eventTally = democracy.ProposalTallied({}, '', function(error, result){
      if (!error)
        var totalCount = "";
        if (result.args.result > 1) {
          totalCount = "passed"
        } else if (result.args.result < 1) {
          totalCount = "rejected"
        } else {
          totalCount = "a tie"
        }
        console.log("Votes counted on Proposal #"+ result.args.proposalID +"!\n With a total of " + Math.abs(result.args.result) + " out of " + result.args.quorum + ", proposal is " + totalCount + ". Proposal is " + (result.args.active? " still on the floor" : "archived") )
    });


### Interactuando con el DAO

Una vez que esté satisfecho con lo que desea, es hora de obtener todo el éter que obtuvo de la financiación colectiva en su nueva organización:

    eth.sendTransaction({from: eth.accounts[1], to: democracy.address, value: web3.toWei(100, "ether")})

¡Esto debería tomar solo un minuto y su país está listo para los negocios! Ahora, como primera prioridad, su organización necesita un buen logotipo, pero a menos que sea un diseñador, no tiene idea de cómo hacerlo. En aras de la discusión, digamos que usted encuentra que su amigo Bob es un gran diseñador que está dispuesto a hacerlo solo por 10 éteres, por lo que desea proponerle un contrato.

    recipient = registrar.addr("bob");
    amount =  web3.toWei(10, "ether");
    shortNote = "Logo Design";

    democracy.newProposal.sendTransaction( recipient, amount, '', shortNote,  {from: eth.accounts[0], gas:1000000})

Después de un minuto, cualquiera puede verificar el destinatario de la propuesta y la cantidad ejecutando estos comandos:

    "This organization has " +  (Number(democracy.numProposals())+1) + " pending proposals";

### Vigila la organización

A diferencia de la mayoría de los gobiernos, el gobierno de su país es completamente transparente y fácilmente programable. Como una pequeña demostración, aquí hay un fragmento de código que repasa todas las propuestas actuales e imprime lo que son y para quién:



    function checkAllProposals() {
        console.log("Country Balance: " + web3.fromWei( eth.getBalance(democracy.address), "ether") );
        for (i = 0; i< (Number(democracy.numProposals())); i++ ) {
            var p = democracy.proposals(i);
            var timeleft = Math.floor(((Math.floor(Date.now() / 1000)) - Number(p[4]) - Number(democracy.debatingPeriod()))/60);  
            console.log("Proposal #" + i + " Send " + web3.fromWei( p[1], "ether") + " ether to address " + p[0].substring(2,6) + " for "+ p[3] + ".\t Deadline:"+ Math.abs(Math.floor(timeleft)) + (timeleft>0?" minutes ago ":" minutes left ") + (p[5]? " Active":" Archived") );
        }
    }

    checkAllProposals();

Un ciudadano preocupado podría escribir fácilmente un bot que haga ping periódicamente en la cadena de bloques y luego publique las nuevas propuestas que se hayan presentado, garantizando una total transparencia.

Ahora, por supuesto, desea que otras personas puedan votar sobre sus propuestas. Puede consultar el tutorial de crowdsale sobre la mejor manera de registrar su aplicación de contrato para que todas las necesidades de los usuarios sean un nombre, pero por ahora, usemos la versión más sencilla. Cualquier persona debería poder crear una copia local de su país en su computadora usando este comando gigante:


    democracy = eth.contract( [{ constant: true, inputs: [{ name: '', type: 'uint256' } ], name: 'proposals', outputs: [{ name: 'recipient', type: 'address' }, { name: 'amount', type: 'uint256' }, { name: 'data', type: 'bytes32' }, { name: 'descriptionHash', type: 'bytes32' }, { name: 'creationDate', type: 'uint256' }, { name: 'numVotes', type: 'uint256' }, { name: 'quorum', type: 'uint256' }, { name: 'active', type: 'bool' } ], type: 'function' }, { constant: false, inputs: [{ name: '_proposalID', type: 'uint256' } ], name: 'executeProposal', outputs: [{ name: 'result', type: 'uint256' } ], type: 'function' }, { constant: true, inputs: [ ], name: 'debatingPeriod', outputs: [{ name: '', type: 'uint256' } ], type: 'function' }, { constant: true, inputs: [ ], name: 'numProposals', outputs: [{ name: '', type: 'uint256' } ], type: 'function' }, { constant: true, inputs: [ ], name: 'founder', outputs: [{ name: '', type: 'address' } ], type: 'function' }, { constant: false, inputs: [{ name: '_proposalID', type: 'uint256' }, { name: '_position', type: 'int256' } ], name: 'vote', outputs: [{ name: 'voteID', type: 'uint256' } ], type: 'function' }, { constant: false, inputs: [{ name: '_voterShareAddress', type: 'address' } ], name: 'setup', outputs: [ ], type: 'function' }, { constant: false, inputs: [{ name: '_recipient', type: 'address' }, { name: '_amount', type: 'uint256' }, { name: '_data', type: 'bytes32' }, { name: '_descriptionHash', type: 'bytes32' } ], name: 'newProposal', outputs: [{ name: 'proposalID', type: 'uint256' } ], type: 'function' }, { constant: true, inputs: [ ], name: 'minimumQuorum', outputs: [{ name: '', type: 'uint256' } ], type: 'function' }, { inputs: [ ], type: 'constructor' } ] ).at(registrar.addr('MyPersonalCountry'))

Entonces cualquier persona que posea alguno de sus tokens puede votar sobre las propuestas haciendo esto:

    var proposalID = 0;
    var position = -1; // +1 for voting yea, -1 for voting nay, 0 abstains but counts as quorum
    democracy.vote.sendTransaction(proposalID, position, {from: eth.accounts[0], gas: 1000000});

    var proposalID = 1;
    var position = 1; // +1 for voting yea, -1 for voting nay, 0 abstains but counts as quorum
    democracy.vote.sendTransaction(proposalID, position, {from: eth.accounts[0], gas: 1000000});


A menos que haya cambiado los parámetros básicos en el código, cualquier propuesta deberá ser debatida durante al menos una semana hasta que pueda ejecutarse. Después de eso, cualquiera, incluso un no ciudadano, puede exigir que se cuenten los votos y que la propuesta se ejecute. Los votos se cuentan y ponderan en ese momento y, si se acepta la propuesta, el éter se envía inmediatamente y la propuesta se archiva. Si los votos terminan en empate o no se ha alcanzado el quórum mínimo, la votación se mantiene abierta hasta que se resuelva el estancamiento. Si se pierde, se archiva y no se puede volver a votar.

    var proposalID = 1;
    democracy.executeProposal.sendTransaction(proposalID, {from: eth.accounts[0], gas: 1000000});


Si la propuesta fue aprobada, entonces deberías ver los éteres de Bob llegando a su dirección:

    web3.fromWei(eth.getBalance(democracy.address), "ether") + " ether";
    web3.fromWei(eth.getBalance(registrar.addr("bob")), "ether") + " ether";


** Inténtelo usted mismo: ** Este es un contrato de democracia muy simple, que podría mejorarse enormemente: actualmente, todas las propuestas tienen el mismo tiempo de debate y se ganan por voto directo y mayoría simple. ¿Puede cambiar eso para que tenga algunas situaciones, dependiendo de la cantidad propuesta, que el debate pueda ser más largo o que requiera una mayoría más amplia? También piense de alguna manera en que los ciudadanos no necesitaban votar sobre cada tema y podrían delegar temporalmente sus votos a un representante especial. Es posible que también hayas notado que agregamos una pequeña descripción para cada propuesta. Esto podría usarse como título para la propuesta o podría ser un hash de un documento más grande que lo describa en detalle.

### ¡Vamos a explorar!

Has llegado al final de este tutorial, pero es solo el comienzo de una gran aventura. Mire hacia atrás y vea cuánto logró: creó un robot vivo y parlante, su propia criptomoneda, recaudó fondos mediante un crowdfunding sin confianza y lo utilizó para impulsar su propia organización democrática personal.

En aras de la simplicidad, solo usamos la organización democrática que creaste para enviar a ether, la moneda nativa de Pirl. Si bien eso podría ser lo suficientemente bueno para algunos, esto es solo arañar la superficie de lo que se puede hacer. En la red de Pirl, los contratos tienen todos los mismos derechos que cualquier usuario normal, lo que significa que su organización podría realizar cualquiera de las transacciones que haya realizado desde sus propias cuentas.


### ¿Qué podría pasar después?

* El contrato de bienvenida que creó al principio podría mejorarse para cobrar al éter por sus servicios y podría canalizar esos fondos a la DAO.

* Los tokens que aún controlas podrían venderse en una bolsa descentralizada o intercambiarse por bienes y servicios para financiar aún más el primer contrato y hacer crecer la organización.

* Su DAO podría poseer su propio nombre en el registrador de nombres, y luego cambiar a donde se está redireccionando para actualizarse si los titulares de token aprobaron.

* La organización podría tener no solo éteres, sino cualquier otro tipo de moneda creada en Pirl, incluidos los activos cuyo valor está ligado al bitcoin o al dólar.

* El DAO podría programarse para permitir una propuesta con múltiples transacciones, algunas programadas para el futuro.
También podría poseer acciones de otras DAO, lo que significa que podría votar en una organización más grande o ser parte de una federación de DAO.

* El Contrato de token se puede reprogramar para que contenga éter o para mantener otros tokens y distribuirlos a los poseedores del token. Esto vincularía el valor del token con el valor de otros activos, por lo que el pago de dividendos podría lograrse simplemente moviendo los fondos a la dirección del token.

Todo esto significa que esta pequeña sociedad que usted creó podría crecer, obtener fondos de terceros, pagar salarios recurrentes, poseer cualquier tipo de cripto-activos e incluso usar crowdsales para financiar sus actividades. Todo con total transparencia, total responsabilidad y completa inmunidad contra cualquier interferencia humana. Mientras viva la red, los contratos ejecutarán exactamente el código para el que fueron creados, sin excepción, para siempre.

Entonces, ¿cuál será su contrato? ¿Será un país, una empresa, un grupo sin fines de lucro? ¿Qué hará tu código?

Eso depende de usted.


---
Autor(s):  

@Fawkes

Contribuyente(s):  

@Dptelecom
