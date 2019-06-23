---
title: Como Crear un Token
weight: 1
pre: "<b>1. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/smartcontract.png"  >}}



## La moneda
Vamos a crear un token digital. Los tokens en el ecosistema de Pirl pueden representar cualquier bien comerciable fungible: monedas, puntos de lealtad, certificados de oro, IOU, elementos del juego, etc. Dado que todos los tokens implementan algunas caracter&iacute;sticas b&aacute;sicas de manera est&aacute;ndar, esto tambi&eacute;n significa que su token ser&aacute; instant&aacute;neo. compatible con la billetera Pirl y cualquier otro cliente o contrato que utilice los mismos est&aacute;ndares.

### TOKEN M&Iacute;NIMO VIABLE
El contrato de token est&aacute;ndar puede ser bastante complejo. Pero en esencia un token muy b&aacute;sico se reduce a esto:

    contract MyToken {
    /* This creates an array with all balances */
    mapping (address => uint256) public balanceOf;

    /* Initializes contract with initial supply tokens to the creator of the contract */
    function MyToken(
        uint256 initialSupply
        ) {
        balanceOf[msg.sender] = initialSupply;              // Give the creator all initial tokens
    }

    /* Send coins */
    function transfer(address _to, uint256 _value) {
        require(balanceOf[msg.sender] >= _value);           // Check if the sender has enough
        require(balanceOf[_to] + _value >= balanceOf[_to]); // Check for overflows
        balanceOf[msg.sender] -= _value;                    // Subtract from the sender
        balanceOf[_to] += _value;                           // Add the same to the recipient
    }
}



### EL C&Oacute;DIGO

Pero si solo desea copiar y pegar un c&oacute;digo m&aacute;s completo, use esto:
solidez del pragma ^ 0.4.16;

    interface tokenRecipient { function receiveApproval(address _from, uint256 _value, address _token, bytes _extraData) public; }
    contract TokenERC20 {
    // Public variables of the token
    string public name;
    string public symbol;
    uint8 public decimals = 18;
    // 18 decimals is the strongly suggested default, avoid changing it
    uint256 public totalSupply;

    // This creates an array with all balances
    mapping (address => uint256) public balanceOf;
    mapping (address => mapping (address => uint256)) public allowance;

    // This generates a public event on the blockchain that will notify clients
    event Transfer(address indexed from, address indexed to, uint256 value);

    // This notifies clients about the amount burnt
    event Burn(address indexed from, uint256 value);

    /**
     * Constructor function
     *
     * Initializes contract with initial supply tokens to the creator of the contract
     */
    function TokenERC20(
        uint256 initialSupply,
        string tokenName,
        string tokenSymbol
    ) public {
        totalSupply = initialSupply * 10 ** uint256(decimals);  // Update total supply with the decimal amount
        balanceOf[msg.sender] = totalSupply;                // Give the creator all initial tokens
        name = tokenName;                                   // Set the name for display purposes
        symbol = tokenSymbol;                               // Set the symbol for display purposes
    }

    /**
     * Internal transfer, only can be called by this contract
     */
    function _transfer(address _from, address _to, uint _value) internal {
        // Prevent transfer to 0x0 address. Use burn() instead
        require(_to != 0x0);
        // Check if the sender has enough
        require(balanceOf[_from] >= _value);
        // Check for overflows
        require(balanceOf[_to] + _value > balanceOf[_to]);
        // Save this for an assertion in the future
        uint previousBalances = balanceOf[_from] + balanceOf[_to];
        // Subtract from the sender
        balanceOf[_from] -= _value;
        // Add the same to the recipient
        balanceOf[_to] += _value;
        Transfer(_from, _to, _value);
        // Asserts are used to use static analysis to find bugs in your code. They should never fail
        assert(balanceOf[_from] + balanceOf[_to] == previousBalances);
    }

    /**
     * Transfer tokens
     *
     * Send `_value` tokens to `_to` from your account
     *
     * @param _to The address of the recipient
     * @param _value the amount to send
     */
    function transfer(address _to, uint256 _value) public {
        _transfer(msg.sender, _to, _value);
    }

    /**
     * Transfer tokens from other address
     *
     * Send `_value` tokens to `_to` on behalf of `_from`
     *
     * @param _from The address of the sender
     * @param _to The address of the recipient
     * @param _value the amount to send
     */
    function transferFrom(address _from, address _to, uint256 _value) public returns (bool success) {
        require(_value <= allowance[_from][msg.sender]);     // Check allowance
        allowance[_from][msg.sender] -= _value;
        _transfer(_from, _to, _value);
        return true;
    }

    /**
     * Set allowance for other address
     *
     * Allows `_spender` to spend no more than `_value` tokens on your behalf
     *
     * @param _spender The address authorized to spend
     * @param _value the max amount they can spend
     */
    function approve(address _spender, uint256 _value) public
        returns (bool success) {
        allowance[msg.sender][_spender] = _value;
        return true;
    }

    /**
     * Set allowance for other address and notify
     *
     * Allows `_spender` to spend no more than `_value` tokens on your behalf, and then ping the contract about it
     *
     * @param _spender The address authorized to spend
     * @param _value the max amount they can spend
     * @param _extraData some extra information to send to the approved contract
     */
    function approveAndCall(address _spender, uint256 _value, bytes _extraData)
        public
        returns (bool success) {
        tokenRecipient spender = tokenRecipient(_spender);
        if (approve(_spender, _value)) {
            spender.receiveApproval(msg.sender, _value, this, _extraData);
            return true;
        }
    }

    /**
     * Destroy tokens
     *
     * Remove `_value` tokens from the system irreversibly
     *
     * @param _value the amount of money to burn
     */
    function burn(uint256 _value) public returns (bool success) {
        require(balanceOf[msg.sender] >= _value);   // Check if the sender has enough
        balanceOf[msg.sender] -= _value;            // Subtract from the sender
        totalSupply -= _value;                      // Updates totalSupply
        Burn(msg.sender, _value);
        return true;
    }

    /**
     * Destroy tokens from other account
     *
     * Remove `_value` tokens from the system irreversibly on behalf of `_from`.
     *
     * @param _from the address of the sender
     * @param _value the amount of money to burn
     */
    function burnFrom(address _from, uint256 _value) public returns (bool success) {
        require(balanceOf[_from] >= _value);                // Check if the targeted balance is enough
        require(_value <= allowance[_from][msg.sender]);    // Check allowance
        balanceOf[_from] -= _value;                         // Subtract from the targeted balance
        allowance[_from][msg.sender] -= _value;             // Subtract from the sender's allowance
        totalSupply -= _value;                              // Update totalSupply
        Burn(_from, _value);
        return true;
    }
}



## ENTENDIENDO EL C&Oacute;DIGO


{{< imagesurlsheaders "cloud/1.jpg" >}}



As&iacute; que vamos a empezar con lo b&aacute;sico. Abra la aplicaci&oacute;n Wallet, vaya a la pesta&ntilde;a Contratos y luego Despliegue Nuevo Contrato. En el campo de texto del c&oacute;digo fuente del contrato de solidaridad, escriba el c&oacute;digo a continuaci&oacute;n:

    contract MyToken {
        /* This creates an array with all balances */
        mapping (address => uint256) public balanceOf;
    }


Una asignaci&oacute;n significa una matriz asociativa, donde se asocian las direcciones con los saldos. Las direcciones est&aacute;n en el formato hexadecimal b&aacute;sico de Pirl, mientras que las balanzas son enteros, que van de 0 a 115 quattuorvigintillion. Si no sabes cu&aacute;nto es un quattuorvigintillion, es mucho m&aacute;s que nada para lo que planeas usar tus tokens. La palabra clave p&uacute;blica significa que esta variable ser&aacute; accesible para cualquiera en la cadena de bloques, lo que significa que todos los saldos son p&uacute;blicos (como deben ser, para que los clientes los muestren).


{{< imagesurlsheaders "cloud/2.jpg" >}}


Si publicara su contrato de inmediato, funcionar&iacute;a pero no ser&iacute;a muy &uacute;til: ser&iacute;a un contrato que podr&iacute;a consultar el saldo de su moneda para cualquier direcci&oacute;n, pero como nunca cre&oacute; una sola moneda, cada una de ellas devolver&iacute;a 0. Entonces, vamos a crear algunos tokens al inicio. Agregue este c&oacute;digo antes del &uacute;ltimo corchete de cierre, justo debajo de la l&iacute;nea de mapeo.

    function MyToken() {
        balanceOf[msg.sender] = 21000000;
    }


Observe que la funci&oacute;n MyToken tiene el mismo nombre que el contrato MyToken. Esto es muy importante y si cambia el nombre de uno, tambi&eacute;n tiene que cambiar el nombre del otro: esta es una funci&oacute;n especial de inicio que se ejecuta solo una vez y solo cuando el contrato se carga por primera vez en la red. Esta funci&oacute;n establecer&aacute; el saldo de msg.sender, el usuario que implement&aacute; el contrato, con un saldo de 21 millones.

La elecci&oacute;n de 21 millones fue bastante arbitraria, y puede cambiarlo a cualquier cosa que desee en el c&oacute;digo, pero hay una mejor manera: en su lugar, proporci&oacute;nelo como un par&aacute;metro para la funci&oacute;n, como esto:

    function MyToken(uint256 initialSupply) public {
        balanceOf[msg.sender] = initialSupply;
    }


Mire la columna derecha al lado del contrato y ver&aacute; una lista desplegable, elija un contrato por escrito. Seleccione el contrato "MyToken" y ver&aacute; que ahora muestra una secci&oacute;n llamada Par&aacute;metros del constructor. Estos son par&aacute;metros modificables para su token, por lo que puede reutilizar el mismo c&oacute;digo y solo cambiar estas variables en el futuro.


{{< imagesurlsheaders "cloud/3.jpg" >}}


Ahora mismo tiene un contrato funcional que cre� saldos de tokens, pero como no hay ninguna funci�n para moverlo, todo lo que hace es permanecer en la misma cuenta. As� que vamos a implementar eso ahora. Escriba el siguiente c�digo antes del �ltimo corchete.

      /* Send coins */
    function transfer(address _to, uint256 _value) {
        /* Add and subtract new balances */
        balanceOf[msg.sender] -= _value;
        balanceOf[_to] += _value;
    }


Esta es una funci�n muy sencilla: tiene un destinatario y un valor como par�metro y cada vez que alguien lo llama, restar� el _valor de su saldo y lo agregar� al _para equilibrar. De inmediato hay un problema obvio: �qu� sucede si la persona desea enviar m�s de lo que posee? Dado que no queremos manejar la deuda en este contrato en particular, simplemente haremos un chequeo r�pido y, si el remitente no tiene fondos suficientes, la ejecuci�n del contrato simplemente se detendr�. Tambi�n es para verificar desbordamientos, para evitar tener un n�mero tan grande que vuelva a ser cero.

Para detener la ejecuci�n de un contrato a mitad de la ejecuci�n, puede devolverlo o lanzarlo. El primero costar� menos combustible, pero puede ser m�s doloroso ya que se mantendr�n los cambios que haya hecho en el contrato hasta el momento. Por otro lado, 'lanzar' cancelar� toda la ejecuci�n del contrato, revertir� cualquier cambio que la transacci�n haya podido realizar y el remitente perder� todo el Pirl que envi� por el gas. Pero como la Cartera puede detectar que se lanzar� un contrato, siempre muestra una alerta, por lo tanto, evita que se gaste ning�n Pirl.

    function transfer(address _to, uint256 _value) {
        /* Check if sender has balance and for overflows */
        require(balanceOf[msg.sender] >= _value && balanceOf[_to] + _value >= balanceOf[_to]);

        /* Add and subtract new balances */
        balanceOf[msg.sender] -= _value;
        balanceOf[_to] += _value;
    }


Ahora todo lo que falta es tener informaci�n b�sica sobre el contrato. En un futuro cercano, esto puede ser manejado por un registro de token, pero por ahora los agregaremos directamente al contrato:

string public name;
string public symbol;
uint8 public decimals;


Y ahora actualizamos la funci�n de constructor para permitir que todas esas variables se configuren al inicio:

        /* Initializes contract with initial supply tokens to the creator of the contract */
    function MyToken(uint256 initialSupply, string tokenName, string tokenSymbol, uint8 decimalUnits) {
        balanceOf[msg.sender] = initialSupply;              // Give the creator all initial tokens
        name = tokenName;                                   // Set the name for display purposes
        symbol = tokenSymbol;                               // Set the symbol for display purposes
        decimals = decimalUnits;                            // Amount of decimals for display purposes
    }


Finalmente, ahora necesitamos algunos eventos llamados "Eventos". Estas son funciones especiales y vac�as a las que llama para ayudar a los clientes como Pirl Wallet a realizar un seguimiento de las actividades que se realizan en el contrato. Los eventos deben comenzar con una letra may�scula. Agregue esta l�nea al comienzo del contrato para declarar el evento:

    event Transfer(address indexed from, address indexed to, uint256 value);


Y luego solo necesita agregar estas dos l�neas dentro de la funci�n "transferir":
         /* Notify anyone listening that this transfer took place */
         Transfer(msg.sender, _to, _value);


Y ahora tu token est� listo!

### �NOTADO LOS COMENTARIOS?

�Cu�les son esos comentarios de @notice y @param, podr�as preguntar? Es Natspec, un est�ndar emergente para una especificaci�n de lenguaje natural, que permite a las billeteras mostrar al usuario una descripci�n en lenguaje natural de lo que el contrato est� por hacer. Aunque actualmente no es compatible con muchas carteras, esto cambiar� en el futuro, por lo que es bueno estar preparado.

# C�MO DESPLEGAR

Si a�n no est� all�, abra la cartera de Pirl, vaya a la pesta�a de contratos y luego haga clic en "desplegar nuevo contrato".
Ahora obtenga la fuente de token desde arriba y p�guela en el "Campo de fuente de solidez". Si el c�digo se compila sin ning�n error, deber�a ver una lista desplegable de "elija un contrato" a la derecha. Cons�guelo y selecciona el contrato "MyToken". En la columna de la derecha, ver� todos los par�metros que necesita para personalizar su propio token. Puedes modificarlos como quieras.


{{< imagesurlsheaders "cloud/4.jpg" >}}

Despl�cese hasta el final de la p�gina y ver� una estimaci�n del costo de c�mputo de ese contrato y puede seleccionar una tarifa por la cantidad que Pirl est� dispuesto a pagar. Se le devolver� cualquier Pirl sobrante que no gaste, por lo que puede dejar la configuraci�n predeterminada si lo desea. Presione "desplegar", ingrese la contrase�a de su cuenta y espere unos segundos para que su transacci�n sea recogida.

{{< imagesurlsheaders "cloud/5.jpg" >}}

Ser� redirigido a la p�gina principal donde podr� ver su transacci�n en espera de confirmaci�n. Haga clic en la cuenta y despu�s de no m�s de un minuto deber�a ver que su cuenta mostrar� que tiene el 100% de las acciones que acaba de crear. Para enviar algunos a unos pocos amigos: seleccione "enviar" y luego elija la moneda que desea enviar (Pirl o su recurso compartido reci�n creado), pegue la direcci�n de su amigo en el campo "a" y presione "enviar".

{{< imagesurlsheaders "cloud/6.jpg" >}}


Si lo env�as a un amigo, a�n no ver�n nada en su billetera. Esto se debe a que la billetera solo rastrea los tokens que conoce, y usted debe agregarlos manualmente. Ahora vaya a la pesta�a "Contratos" y deber�a ver un enlace a su contrato reci�n creado. Haz click en �l para ir a su p�gina. Ya que esta es una p�gina de contrato muy simple, no hay mucho que hacer aqu�, simplemente haga clic en "copiar direcci�n" y pegue la direcci�n del contrato en un editor de texto, lo necesitar� en breve.

Para agregar un token para ver, vaya a la p�gina de contratos y luego haga clic en "Watch Token". Aparecer� una ventana emergente y solo deber� pegar la direcci�n del contrato. El nombre del token, el s�mbolo y el n�mero decimal deben llenarse autom�ticamente, pero si no es as�, puede poner lo que quiera (solo afectar� la forma en que se muestra en su billetera). Una vez que haga esto, autom�ticamente se le mostrar� el saldo que tenga de ese token y podr� enviarlo a cualquier otra persona.


{{< imagesurlsheaders "cloud/7.jpg" >}}


�Y ahora tienes tu propio token criptogr�fico! Los tokens por s� mismos pueden ser �tiles como intercambio de valor en las comunidades locales, formas de realizar un seguimiento de las horas trabajadas u otros programas de lealtad. �Pero podemos hacer que una moneda tenga un valor intr�nseco al hacerla �til?

### Mejora tu token

Puedes implementar todo tu token criptogr�fico sin tocar una l�nea de c�digo, pero la verdadera magia sucede cuando comienzas a personalizarlo. Las siguientes secciones ser�n sugerencias sobre las funciones que puede agregar a su token para que se ajuste a sus necesidades.

### M�S FUNCIONES B�SICAS

Notar� que hay algunas funciones m�s en su contrato de token b�sico, como aprobar, enviar desde y otros. Estas funciones est�n ah� para que su token interact�e con otros contratos: si desea, por ejemplo, vender tokens a un intercambio descentralizado, solo enviarlos a una direcci�n no ser� suficiente, ya que el intercambio no ser� consciente de los tokens nuevos o qui�n los envi�. ellos, porque los contratos no pueden suscribirse a eventos solo para llamadas de funci�n. Por lo tanto, para los contratos, primero debe aprobar una cantidad de tokens que pueden mover de su cuenta y luego hacerles un ping para informarles que deben hacer lo suyo, o hacer las dos acciones en una, con approveAndCall.

Debido a que muchas de estas funciones tienen que reimplementar la transferencia de tokens, tiene sentido cambiarlas a una funci�n interna, que solo puede ser llamada por el propio contrato:

    /* Internal transfer, can only be called by this contract */
     function _transfer(address _from, address _to, uint _value) internal {
        require (_to != 0x0);                               // Prevent transfer to 0x0 address. Use burn() instead
        require (balanceOf[_from] >= _value);                // Check if the sender has enough
        require (balanceOf[_to] + _value > balanceOf[_to]); // Check for overflows
        require(!frozenAccount[_from]);                     // Check if sender is frozen
        require(!frozenAccount[_to]);                       // Check if recipient is frozen
        balanceOf[_from] -= _value;                         // Subtract from the sender
        balanceOf[_to] += _value;                           // Add the same to the recipient
        Transfer(_from, _to, _value);
    }


Ahora todas sus funciones que resultan en la transferencia de monedas, pueden hacer sus propios cheques y luego transferir la llamada con los par�metros correctos. Tenga en cuenta que esta funci�n mover� las monedas de cualquier cuenta a cualquier otra, sin requerir el permiso de nadie para hacerlo: es por eso que es una funci�n interna, solo llamada por el contrato: si agrega cualquier funci�n llam�ndola, aseg�rese de que verifique correctamente si el la persona que llama debe tener permiso para mover esos.

### ADMINISTRADOR CENTRALIZADO

Todos los dapps est�n completamente descentralizados por defecto, pero eso no significa que no puedan tener alg�n tipo de administrador central, si as� lo desean. Tal vez desee la posibilidad de acu�ar m�s monedas, tal vez quiera prohibir que algunas personas usen su moneda. Puedes agregar cualquiera de esas caracter�sticas, pero el problema es que solo puedes agregarlas al principio, por lo que todos los poseedores del token siempre conocer�n exactamente las reglas del juego antes de que decidan poseer una.

Para que eso suceda, necesitas un controlador central de moneda. Esta podr�a ser una cuenta simple, pero tambi�n podr�a ser un contrato y, por lo tanto, la decisi�n de crear m�s tokens depender� del contrato: si es una organizaci�n democr�tica la que est� en condiciones de votar, o tal vez sea solo una forma de limitar la Poder del propietario del token.

Para ello aprenderemos una propiedad muy �til de los contratos: la herencia. La herencia permite que un contrato adquiera propiedades de un contrato principal, sin tener que redefinirlas todas. Esto hace que el c�digo sea m�s limpio y m�s f�cil de reutilizar. Agregue este c�digo a la primera l�nea de su c�digo, antes del contrato MyToken {.
���contrato de propiedad
��������direccion propietario publico;

        function owned() {
            owner = msg.sender;
        }

        modifier onlyOwner {
            require(msg.sender == owner);
            _;
        }

        function transferOwnership(address newOwner) onlyOwner {
            owner = newOwner;
        }
    }


Esto crea un contrato muy b�sico que no hace nada, excepto definir algunas funciones gen�ricas sobre un contrato que puede ser "propiedad". Ahora el siguiente paso es agregar el texto que pertenece a su contrato:
��� el contrato MyToken es propiedad
�������� / * El resto del contrato como de costumbre * /


Esto significa que todas las funciones dentro de MyToken ahora pueden acceder al propietario variable y al modificador onlyOwner. El contrato tambi�n obtiene una funci�n para transferir la propiedad. Dado que puede ser interesante establecer el propietario del contrato al inicio, tambi�n puede agregar esto a la funci�n de constructor:

      function MyToken(
        uint256 initialSupply,
        string tokenName,
        uint8 decimalUnits,
        string tokenSymbol,
        address centralMinter
        ) {
        if(centralMinter != 0 ) owner = centralMinter;
    }


### MENTA CENTRAL
Supongamos que quieres que cambie la cantidad de monedas en circulaci�n. Este es el caso cuando sus tokens realmente representan un activo fuera de la cadena de bloques (como certificados de oro o monedas del gobierno) y desea que el inventario virtual refleje el real. Este tambi�n podr�a ser el caso cuando los tenedores de divisas esperan cierto control del precio del token y desean emitir o eliminar tokens de la circulaci�n.

Primero, necesitamos agregar una variable para almacenar el totalSupply y asignarlo a nuestra funci�n de constructor.
��� contrato MyToken {
�������� uint256 public totalSupply;

        function MyToken(...) {
            totalSupply = initialSupply;
            ...
        }
        ...
    }


Ahora agreguemos una nueva funci�n finalmente que permitir� al propietario crear nuevos tokens:

    function mintToken(address target, uint256 mintedAmount) onlyOwner {
        balanceOf[target] += mintedAmount;
        totalSupply += mintedAmount;
        Transfer(0, owner, mintedAmount);
        Transfer(owner, target, mintedAmount);
    }


Observe el modificador onlyOwner al final del nombre de la funci�n. Esto significa que esta funci�n se reescribir� en la compilaci�n para heredar el c�digo del modificador onlyOwner que hab�amos definido anteriormente. El c�digo de esta funci�n se insertar� donde haya un subrayado en la funci�n modificadora, lo que significa que la cuenta que se establece como el propietario solo puede llamar a esta funci�n en particular. Simplemente agregue esto a un contrato con un modificador de propietario y podr� crear m�s monedas.

### CONGELAMIENTO DE ACTIVOS

Dependiendo de su caso de uso, es posible que tenga que tener algunos obst�culos regulatorios sobre qui�n puede y qui�n no puede usar sus fichas. Para que eso suceda, puede agregar un par�metro que permita al propietario del contrato congelar o descongelar activos.
Agregue esta variable y funcione en cualquier lugar dentro del contrato. Puede ubicarlos en cualquier lugar, pero para una buena pr�ctica, le recomendamos que coloque los mapeos con los otros mapeos y los eventos con los otros eventos.
���mapeo (address => bool) public frozenAccount;
����evento FrozenFunds (direcci�n de destino, bool frozen);

    function freezeAccount(address target, bool freeze) onlyOwner {
        frozenAccount[target] = freeze;
        FrozenFunds(target, freeze);
    }


Con este c�digo, todas las cuentas se descongelan de forma predeterminada, pero el propietario puede establecer cualquiera de ellas en el estado de congelaci�n llamando a la cuenta de Freeze. Desafortunadamente, la congelaci�n no tiene un efecto pr�ctico porque no hemos agregado nada a la funci�n de transferencia. Estamos cambiando eso ahora:

    function transfer(address _to, uint256 _value) {
        require(!frozenAccount[msg.sender]);


Ahora, cualquier cuenta que est� congelada seguir� teniendo sus fondos intactos, pero no podr� moverlos. Todas las cuentas se descongelan de forma predeterminada hasta que las congele, pero puede revertir f�cilmente ese comportamiento en una lista blanca donde debe aprobar manualmente cada cuenta. Simplemente cambie el nombre de frozenAccount por la cuenta aprobada y cambie la �ltima l�nea a:
       require(approvedAccount[msg.sender]);


### VENTA Y COMPRA AUTOM�TICA

Hasta ahora, ha confiado en la utilidad y la confianza para valorar su token. Pero si lo desea, puede hacer que el valor del token sea respaldado por Pirl (u otros tokens) creando un fondo que los venda y compre autom�ticamente al valor de mercado.
Primero, fijemos el precio para comprar y vender:
��� uint256 public sellPrice;
���� uint256 public buyPrice;

    function setPrices(uint256 newSellPrice, uint256 newBuyPrice) onlyOwner {
        sellPrice = newSellPrice;
        buyPrice = newBuyPrice;
    }


Esto es aceptable para un precio que no cambia muy a menudo, ya que cada nuevo cambio de precio requerir� que usted ejecute una transacci�n y gaste un poco de Pirl. Si desea tener un precio flotante constante, le recomendamos que investigue fuentes de datos est�ndar.
El siguiente paso es hacer las funciones de compra y venta:

    function buy() payable returns (uint amount){
        amount = msg.value / buyPrice;                    // calculates the amount
        require(balanceOf[this] >= amount);               // checks if it has enough to sell
        balanceOf[msg.sender] += amount;                  // adds the amount to buyer's balance
        balanceOf[this] -= amount;                        // subtracts amount from seller's balance
        Transfer(this, msg.sender, amount);               // execute an event reflecting the change
        return amount;                                    // ends function and returns
    }

    function sell(uint amount) returns (uint revenue){
        require(balanceOf[msg.sender] >= amount);         // checks if the sender has enough to sell
        balanceOf[this] += amount;                        // adds the amount to owner's balance
        balanceOf[msg.sender] -= amount;                  // subtracts the amount from seller's balance
        revenue = amount * sellPrice;
        msg.sender.transfer(revenue);                     // sends Pirl to the seller: it's important to do this last to prevent recursion attacks
        Transfer(msg.sender, this, amount);               // executes an event reflecting on the change
        return revenue;                                   // ends function and returns
    }


Tenga en cuenta que esto no crear� nuevos tokens sino que cambiar� el saldo que posee el contrato. El contrato puede tener sus propios tokens y Pirl y el propietario del contrato, mientras que puede establecer precios o, en algunos casos, crear nuevos tokens (si corresponde) no puede tocar los tokens del banco o Pirl. La �nica forma en que este contrato puede mover fondos es mediante la venta y la compra.

Nota Los "precios" de compra y venta no se establecen en Pirl, pero s� en la moneda m�nima del sistema (equivalente al centavo en el euro y el d�lar, o el Satoshi en Bitcoin). One Pirl es 1000000000000000000 wei. As� que cuando establezca los precios para su token en Pirl, agregue 18 ceros al final.

Al crear el contrato, env�ele Pirl suficiente para que pueda volver a comprar todas las fichas en el mercado, de lo contrario, su contrato ser� insolvente y sus usuarios no podr�n vender sus fichas.

Los ejemplos anteriores, por supuesto, describen un contrato con un solo comprador y vendedor central, un contrato mucho m�s interesante permitir�a un mercado donde cualquier persona puede ofrecer precios diferentes, o tal vez cargar�a los precios directamente de una fuente externa.

### RECARGA AUTOM�TICA

Cada vez que realice una transacci�n en Pirl, deber� pagar una tarifa al minero del bloque que calcular� el resultado de su contrato inteligente. Si bien esto podr�a cambiar en el futuro, por el momento, las tarifas solo se pueden pagar en Pirl y, por lo tanto, todos los usuarios de sus tokens lo necesitan. Las fichas en cuentas con un saldo menor que la tarifa se atascan hasta que el propietario pueda pagar la tarifa necesaria. Pero en algunos casos de uso, es posible que no desee que sus usuarios piensen en Pirl, blockchain o en c�mo obtener Pirl, por lo que un posible enfoque har�a que su moneda recargue autom�ticamente el saldo del usuario tan pronto como detecte que el saldo es peligrosamente bajo.


Para hacer eso, primero debe crear una variable que contendr� la cantidad de umbral y una funci�n para cambiarla.

���uint minBalanceForAccounts;

    function setMinBalance(uint minimumBalanceInFinney) onlyOwner {
         minBalanceForAccounts = minimumBalanceInFinney * 1 finney;
    }


Luego, agregue esta l�nea a la funci�n de transferencia para que el remitente sea reembolsado:
��� / * Enviar monedas * /
���� transferencia de funciones (direcci�n _to, uint256 _valor) {
�������� ...
�������� if (msg.sender.balance <minBalanceForAccounts)
������������ sell ((minBalanceForAccounts - msg.sender.balance) / sellPrice);
���� }


Tambi�n puede cambiarlo para que el remitente pague la tarifa al destinatario:

     /* Send coins */
     function transfer(address _to, uint256 _value) {
        ...
        if(_to.balance<minBalanceForAccounts)
            _to.send(sell((minBalanceForAccounts - _to.balance) / sellPrice));
    }


Esto asegurar� que ninguna cuenta que reciba el token tenga menos del Pirl necesario para pagar las tarifas.

### PRUEBA DE TRABAJO

Hay algunas maneras de vincular su suministro de moneda a una f�rmula matem�tica. Una de las formas m�s simples ser�a convertirla en una "miner�a combinada" con Pirl, lo que significa que cualquier persona que encuentre un bloqueo en Pirl tambi�n recibir� una recompensa de su moneda, dado que cualquiera llama a la funci�n de recompensa en ese bloque. Puede hacerlo utilizando la palabra clave especial coinbase que se refiere al minero que encuentra el bloque.

    function giveBlockReward() {
        balanceOf[block.coinbase] += 1;
    }


Tambi�n es posible agregar una f�rmula matem�tica, de modo que cualquier persona que pueda hacer matem�ticas pueda ganar una recompensa. En este siguiente ejemplo, tiene que calcular la ra�z c�bica del desaf�o actual para obtener un punto y el derecho de establecer el siguiente desaf�o:
��� uint currentChallenge = 1; // �Puedes averiguar la ra�z c�bica de este n�mero?

    function rewardMathGeniuses(uint answerToCurrentReward, uint nextChallenge) {
        require(answerToCurrentReward**3 == currentChallenge); // If answer is wrong do not continue
        balanceOf[msg.sender] += 1;         // Reward the player
        currentChallenge = nextChallenge;   // Set the next challenge
    }


Por supuesto, si bien el c�lculo de las ra�ces c�bicas puede ser dif�cil para alguien, es muy f�cil con una calculadora, por lo que este juego podr�a romperse f�cilmente con una computadora. Adem�s, dado que el �ltimo ganador puede elegir el pr�ximo desaf�o, podr�an elegir a otros que saben y por lo tanto no ser�an un juego muy justo para otros jugadores. Hay tareas que son f�ciles para los humanos pero dif�ciles para las computadoras, pero generalmente son muy dif�ciles de codificar en scripts simples como estos. En cambio, un sistema m�s justo deber�a ser uno que sea muy dif�cil de hacer para una computadora, pero que no sea muy dif�cil de verificar para una computadora. Un gran candidato ser�a crear un desaf�o de hash en el que el retador tenga que generar hashes a partir de m�ltiples n�meros hasta que encuentre uno que sea m�s bajo que una dificultad dada.


Este proceso fue propuesto por primera vez por Adam Back en 1997 como Hashcash y luego implementado en Bitcoin por Satoshi Nakamoto como Prueba de trabajo en 2008.


Si le gusta el Hashing como una forma de emisi�n aleatoria de monedas, a�n puede crear su propia moneda basada en Pirl que tenga una prueba de emisi�n de trabajo:
���bytes32 public currentChallenge; // La moneda comienza con un desaf�o.
����uint public timeOfLastProof; // Variable para realizar un seguimiento de cu�ndo se dieron las recompensas
����dificultad p�blica uint = 10 ** 32; // La dificultad comienza razonablemente baja

    function proofOfWork(uint nonce){
        bytes8 n = bytes8(sha3(nonce, currentChallenge));    // Generate a random hash based on input
        require(n >= bytes8(difficulty));                   // Check if it's under the difficulty

        uint timeSinceLastProof = (now - timeOfLastProof);  // Calculate time since last reward was given
        require(timeSinceLastProof >=  5 seconds);         // Rewards cannot be given too quickly
        balanceOf[msg.sender] += timeSinceLastProof / 60 seconds;  // The reward to the winner grows by the minute

        difficulty = difficulty * 10 minutes / timeSinceLastProof + 1;  // Adjusts the difficulty

        timeOfLastProof = now;                              // Reset the counter
        currentChallenge = sha3(nonce, currentChallenge, block.blockhash(block.number - 1));  // Save a hash that will be used as the next proof
    }


Tambi�n cambie la funci�n Constructor (la que tiene el mismo nombre que el contrato, que se llama en la primera carga) para agregar esta l�nea, para que el ajuste de dificultad no se vuelva loco:
���timeOfLastProof = ahora;


Una vez que el contrato est� en l�nea, seleccione la funci�n "Prueba de trabajo", agregue su n�mero favorito en el campo de nonce e intente ejecutarlo. Si la ventana de confirmaci�n muestra una advertencia roja que dice "No se pueden ejecutar los datos", retroceda y elija otro n�mero hasta que encuentre uno que permita que la transacci�n avance: este proceso es aleatorio. Si encuentra una, se le otorgar� 1 token por cada minuto que haya pasado desde la �ltima recompensa, y luego la dificultad del desaf�o se ajustar� hacia arriba o hacia abajo para alcanzar un promedio de 10 minutos por recompensa.

Este proceso de tratar de encontrar el n�mero que le dar� una recompensa es lo que se llama extracci�n: si la dificultad aumenta, puede ser muy dif�cil encontrar un n�mero de la suerte, pero siempre ser� f�cil verificar que haya encontrado uno.

### Moneda mejorada

## CODIGO MONEDA COMPLETA
Si agrega todas las opciones avanzadas, as� es como deber�a verse el c�digo final:

    pragma solidity ^0.4.16;

    contract owned {
    address public owner;

    function owned() public {
        owner = msg.sender;
    }

    modifier onlyOwner {
        require(msg.sender == owner);
        _;
    }

    function transferOwnership(address newOwner) onlyOwner public {
        owner = newOwner;
    }
}

    interface tokenRecipient { function receiveApproval(address _from, uint256 _value, address _token, bytes _extraData) public; }

    contract TokenERC20 {
    // Public variables of the token
    string public name;
    string public symbol;
    uint8 public decimals = 18;
    // 18 decimals is the strongly suggested default, avoid changing it
    uint256 public totalSupply;

    // This creates an array with all balances
    mapping (address => uint256) public balanceOf;
    mapping (address => mapping (address => uint256)) public allowance;

    // This generates a public event on the blockchain that will notify clients
    event Transfer(address indexed from, address indexed to, uint256 value);

    // This notifies clients about the amount burnt
    event Burn(address indexed from, uint256 value);

    /**
     * Constrctor function
     *
     * Initializes contract with initial supply tokens to the creator of the contract
     */
    function TokenERC20(
        uint256 initialSupply,
        string tokenName,
        string tokenSymbol
    ) public {
        totalSupply = initialSupply * 10 ** uint256(decimals);  // Update total supply with the decimal amount
        balanceOf[msg.sender] = totalSupply;                // Give the creator all initial tokens
        name = tokenName;                                   // Set the name for display purposes
        symbol = tokenSymbol;                               // Set the symbol for display purposes
    }

    /**
     * Internal transfer, only can be called by this contract
     */
    function _transfer(address _from, address _to, uint _value) internal {
        // Prevent transfer to 0x0 address. Use burn() instead
        require(_to != 0x0);
        // Check if the sender has enough
        require(balanceOf[_from] >= _value);
        // Check for overflows
        require(balanceOf[_to] + _value > balanceOf[_to]);
        // Save this for an assertion in the future
        uint previousBalances = balanceOf[_from] + balanceOf[_to];
        // Subtract from the sender
        balanceOf[_from] -= _value;
        // Add the same to the recipient
        balanceOf[_to] += _value;
        Transfer(_from, _to, _value);
        // Asserts are used to use static analysis to find bugs in your code. They should never fail
        assert(balanceOf[_from] + balanceOf[_to] == previousBalances);
    }

    /**
     * Transfer tokens
     *
     * Send `_value` tokens to `_to` from your account
     *
     * @param _to The address of the recipient
     * @param _value the amount to send
     */
    function transfer(address _to, uint256 _value) public {
        _transfer(msg.sender, _to, _value);
    }

    /**
     * Transfer tokens from other address
     *
     * Send `_value` tokens to `_to` in behalf of `_from`
     *
     * @param _from The address of the sender
     * @param _to The address of the recipient
     * @param _value the amount to send
     */
    function transferFrom(address _from, address _to, uint256 _value) public returns (bool success) {
        require(_value <= allowance[_from][msg.sender]);     // Check allowance
        allowance[_from][msg.sender] -= _value;
        _transfer(_from, _to, _value);
        return true;
    }

    /**
     * Set allowance for other address
     *
     * Allows `_spender` to spend no more than `_value` tokens in your behalf
     *
     * @param _spender The address authorized to spend
     * @param _value the max amount they can spend
     */
    function approve(address _spender, uint256 _value) public
        returns (bool success) {
        allowance[msg.sender][_spender] = _value;
        return true;
    }

    /**
     * Set allowance for other address and notify
     *
     * Allows `_spender` to spend no more than `_value` tokens in your behalf, and then ping the contract about it
     *
     * @param _spender The address authorized to spend
     * @param _value the max amount they can spend
     * @param _extraData some extra information to send to the approved contract
     */
    function approveAndCall(address _spender, uint256 _value, bytes _extraData)
        public
        returns (bool success) {
        tokenRecipient spender = tokenRecipient(_spender);
        if (approve(_spender, _value)) {
            spender.receiveApproval(msg.sender, _value, this, _extraData);
            return true;
        }
    }

    /**
     * Destroy tokens
     *
     * Remove `_value` tokens from the system irreversibly
     *
     * @param _value the amount of money to burn
     */
    function burn(uint256 _value) public returns (bool success) {
        require(balanceOf[msg.sender] >= _value);   // Check if the sender has enough
        balanceOf[msg.sender] -= _value;            // Subtract from the sender
        totalSupply -= _value;                      // Updates totalSupply
        Burn(msg.sender, _value);
        return true;
    }

    /**
     * Destroy tokens from other account
     *
     * Remove `_value` tokens from the system irreversibly on behalf of `_from`.
     *
     * @param _from the address of the sender
     * @param _value the amount of money to burn
     */
    function burnFrom(address _from, uint256 _value) public returns (bool success) {
        require(balanceOf[_from] >= _value);                // Check if the targeted balance is enough
        require(_value <= allowance[_from][msg.sender]);    // Check allowance
        balanceOf[_from] -= _value;                         // Subtract from the targeted balance
        allowance[_from][msg.sender] -= _value;             // Subtract from the sender's allowance
        totalSupply -= _value;                              // Update totalSupply
        Burn(_from, _value);
        return true;
    }
}

/******************************************/
/*       TOKEN AVANZADO COMIENZA AQU�      */
/******************************************/

    contract MyAdvancedToken is owned, TokenERC20 {

    uint256 public sellPrice;
    uint256 public buyPrice;

    mapping (address => bool) public frozenAccount;

    /* This generates a public event on the blockchain that will notify clients */
    event FrozenFunds(address target, bool frozen);

    /* Initializes contract with initial supply tokens to the creator of the contract */
    function MyAdvancedToken(
        uint256 initialSupply,
        string tokenName,
        string tokenSymbol
    ) TokenERC20(initialSupply, tokenName, tokenSymbol) public {}

    /* Internal transfer, only can be called by this contract */
    function _transfer(address _from, address _to, uint _value) internal {
        require (_to != 0x0);                               // Prevent transfer to 0x0 address. Use burn() instead
        require (balanceOf[_from] >= _value);               // Check if the sender has enough
        require (balanceOf[_to] + _value > balanceOf[_to]); // Check for overflows
        require(!frozenAccount[_from]);                     // Check if sender is frozen
        require(!frozenAccount[_to]);                       // Check if recipient is frozen
        balanceOf[_from] -= _value;                         // Subtract from the sender
        balanceOf[_to] += _value;                           // Add the same to the recipient
        Transfer(_from, _to, _value);
    }

    /// @notice Create `mintedAmount` tokens and send it to `target`
    /// @param target Address to receive the tokens
    /// @param mintedAmount the amount of tokens it will receive
    function mintToken(address target, uint256 mintedAmount) onlyOwner public {
        balanceOf[target] += mintedAmount;
        totalSupply += mintedAmount;
        Transfer(0, this, mintedAmount);
        Transfer(this, target, mintedAmount);
    }

    /// @notice `freeze? Prevent | Allow` `target` from sending & receiving tokens
    /// @param target Address to be frozen
    /// @param freeze either to freeze it or not
    function freezeAccount(address target, bool freeze) onlyOwner public {
        frozenAccount[target] = freeze;
        FrozenFunds(target, freeze);
    }

    /// @notice Allow users to buy tokens for `newBuyPrice` Pirl and sell tokens for `newSellPrice` Pirl
    /// @param newSellPrice Price the users can sell to the contract
    /// @param newBuyPrice Price users can buy from the contract
    function setPrices(uint256 newSellPrice, uint256 newBuyPrice) onlyOwner public {
        sellPrice = newSellPrice;
        buyPrice = newBuyPrice;
    }

    /// @notice Buy tokens from contract by sending Pirl
    function buy() payable public {
        uint amount = msg.value / buyPrice;               // calculates the amount
        _transfer(this, msg.sender, amount);              // makes the transfers
    }

    /// @notice Sell `amount` tokens to contract
    /// @param amount amount of tokens to be sold
    function sell(uint256 amount) public {
        require(this.balance >= amount * sellPrice);      // checks if the contract has enough Pirl to buy
        _transfer(msg.sender, this, amount);              // makes the transfers
        msg.sender.transfer(amount * sellPrice);          // sends Pirl to the seller. It's important to do this last to avoid recursion attacks
    }
}



## DESPLIEGUE

Despl�cese hacia abajo y ver� un costo estimado para la implementaci�n. Si lo desea, puede cambiar el control deslizante para establecer una tarifa m�s peque�a, pero si el precio est� muy por debajo de la tasa promedio del mercado, su transacci�n podr�a tardar m�s en recuperarse. Haga clic en Implementar y escriba su contrase�a. Despu�s de unos segundos, ser� redirigido al tablero de mandos y en �ltimas transacciones ver� una l�nea que dice "creando contrato". Espere unos segundos para que alguien elija su transacci�n y luego ver� un rect�ngulo azul lento que representa cu�ntos otros nodos han visto su transacci�n y los han confirmado. Cuantas m�s confirmaciones tenga, m�s seguridad tendr� de que su c�digo ha sido implementado.

Haga clic en el enlace que dice la p�gina de administraci�n y se le llevar� al panel de control del banco central m�s sencillo del mundo, donde puede hacer lo que quiera con su moneda reci�n creada.

En el lado izquierdo, debajo de Leer desde el contrato, tiene todas las opciones y funciones que puede usar para leer la informaci�n del contrato, de forma gratuita. Si su token tiene un propietario, mostrar� su direcci�n aqu�. Copie esa direcci�n y p�guela en el Saldo de y le mostrar� el saldo de cualquier cuenta (el saldo tambi�n se muestra autom�ticamente en cualquier p�gina de la cuenta que tenga tokens).
En el lado derecho, debajo de Escribir en contrato, ver� todas las funciones que puede usar para alterar o cambiar la cadena de bloques de cualquier manera. Estos costar�n gas. Si cre� un contrato que le permite acu�ar nuevas monedas, debe tener una funci�n llamada "Mint Token". Selecci�nalo

Seleccione la direcci�n donde se crear�n esas nuevas monedas y luego la cantidad (si tiene decimales establecidos en 2, agregue 2 ceros despu�s de la cantidad para crear la cantidad correcta). En Ejecutar desde seleccione la cuenta que se estableci� como propietario, deje la cantidad de Pirl en cero y luego presione ejecutar.

Despu�s de algunas confirmaciones, el saldo del destinatario se actualizar� para reflejar la nueva cantidad. Pero es posible que la billetera del destinatario no se muestre autom�ticamente: para estar al tanto de tokens personalizados, la billetera debe agregarlos manualmente a una lista de vigilancia. Copie su direcci�n de token (en la p�gina de administraci�n, presione copiar direcci�n) y env�ela a su destinatario. Si a�n no lo han hecho, deben ir a la pesta�a de contratos, presionar Watch Token y luego agregar la direcci�n all�. El usuario final puede personalizar el nombre, los s�mbolos y las cantidades decimales que se muestran, especialmente si tienen otros tokens con un nombre similar (o el mismo). El icono principal no es modificable y los usuarios deben prestarles atenci�n al enviar y recibir tokens para asegurarse de que est�n tratando con el trato real y no con un token de imitaci�n.

### Usando tu moneda

Una vez que haya implementado sus tokens, se agregar�n a su lista de tokens vistos, y el saldo total se mostrar� en su cuenta. Para enviar tokens, simplemente vaya a la pesta�a Enviar y seleccione una cuenta que contenga tokens. Los tokens que tiene la cuenta aparecer�n justo debajo de Pirl. Selecci�nalos y luego escribe la cantidad de tokens que deseas enviar.
Si desea agregar el token de otra persona, simplemente vaya a la pesta�a Contratos y haga clic en Ver token. Por ejemplo, para agregar el token de Pirl Vortex a su lista de vigilancia, solo agregue la direcci�n 0x0489A975393A1cD0330740040141D702C35180cb


{{< imagesurlsheaders "cloud/9.jpg" >}}




### �Ahora que?

Acaba de aprender c�mo puede usar Pirl para emitir un token, que puede representar lo que quiera. �Pero qu� puedes hacer con los tokens? Puede usar, por ejemplo, los tokens para representar una participaci�n en una empresa o puede usar un comit� central para votar cu�ndo emitir nuevas monedas para controlar la inflaci�n. Tambi�n puede usarlos para recaudar dinero para una causa, a trav�s de una venta colectiva. �Qu� vas a construir a continuaci�n?



---
Autor(s):  

@Fawkes

Contribuyente(s):  


@Dptelecom
