---
title: JSON RPC API
weight: 2
pre: "<b>2. </b>"
chapter: true
---

**Contents**

- [JSON RPC API](#json-rpc-api)
  - [JavaScript API](#javascript-api)
  - [JSON-RPC Endpoint](#json-rpc-endpoint)
    - [Go](#go)
  - [JSON-RPC support](#json-rpc-support)
  - [HEX value encoding](#hex-value-encoding)
  - [The default block parameter](#the-default-block-parameter)
  - [Curl Examples Explained](#curl-examples-explained)
  - [JSON-RPC methods](#json-rpc-methods)
  - [JSON RPC API Reference](#json-rpc-api-reference)
      - [web3_clientVersion](#web3_clientversion)
        - [Parameters](#parameters)
        - [Returns](#returns)
        - [Example](#example)
      - [web3_sha3](#web3_sha3)
        - [Parameters](#parameters-1)
        - [Returns](#returns-1)
        - [Example](#example-1)
      - [net_version](#net_version)
        - [Parameters](#parameters-2)
        - [Returns](#returns-2)
        - [Example](#example-2)
      - [net_listening](#net_listening)
        - [Parameters](#parameters-3)
        - [Returns](#returns-3)
        - [Example](#example-3)
      - [net_peerCount](#net_peercount)
        - [Parameters](#parameters-4)
        - [Returns](#returns-4)
        - [Example](#example-4)
      - [eth_protocolVersion](#eth_protocolversion)
        - [Parameters](#parameters-5)
        - [Returns](#returns-5)
        - [Example](#example-5)
      - [eth_syncing](#eth_syncing)
        - [Parameters](#parameters-6)
        - [Returns](#returns-6)
        - [Example](#example-6)
      - [eth_coinbase](#eth_coinbase)
        - [Parameters](#parameters-7)
        - [Returns](#returns-7)
        - [Example](#example-7)
      - [eth_mining](#eth_mining)
        - [Parameters](#parameters-8)
        - [Returns](#returns-8)
        - [Example](#example-8)
      - [eth_hashrate](#eth_hashrate)
        - [Parameters](#parameters-9)
        - [Returns](#returns-9)
        - [Example](#example-9)
      - [eth_gasPrice](#eth_gasprice)
        - [Parameters](#parameters-10)
        - [Returns](#returns-10)
        - [Example](#example-10)
      - [eth_accounts](#eth_accounts)
        - [Parameters](#parameters-11)
        - [Returns](#returns-11)
        - [Example](#example-11)
      - [eth_blockNumber](#eth_blocknumber)
        - [Parameters](#parameters-12)
        - [Returns](#returns-12)
        - [Example](#example-12)
      - [eth_getBalance](#eth_getbalance)
        - [Parameters](#parameters-13)
        - [Returns](#returns-13)
        - [Example](#example-13)
      - [eth_getStorageAt](#eth_getstorageat)
        - [Parameters](#parameters-14)
        - [Returns](#returns-14)
        - [Example](#example-14)
      - [eth_getTransactionCount](#eth_gettransactioncount)
        - [Parameters](#parameters-15)
        - [Returns](#returns-15)
        - [Example](#example-15)
      - [eth_getBlockTransactionCountByHash](#eth_getblocktransactioncountbyhash)
        - [Parameters](#parameters-16)
        - [Returns](#returns-16)
        - [Example](#example-16)
      - [eth_getBlockTransactionCountByNumber](#eth_getblocktransactioncountbynumber)
        - [Parameters](#parameters-17)
        - [Returns](#returns-17)
        - [Example](#example-17)
      - [eth_getUncleCountByBlockHash](#eth_getunclecountbyblockhash)
        - [Parameters](#parameters-18)
        - [Returns](#returns-18)
        - [Example](#example-18)
      - [eth_getUncleCountByBlockNumber](#eth_getunclecountbyblocknumber)
        - [Parameters](#parameters-19)
        - [Returns](#returns-19)
        - [Example](#example-19)
      - [eth_getCode](#eth_getcode)
        - [Parameters](#parameters-20)
        - [Returns](#returns-20)
        - [Example](#example-20)
      - [eth_sign](#eth_sign)
        - [Parameters](#parameters-21)
        - [Returns](#returns-21)
        - [Example](#example-21)
      - [eth_sendTransaction](#eth_sendtransaction)
        - [Parameters](#parameters-22)
        - [Returns](#returns-22)
        - [Example](#example-22)
      - [eth_sendRawTransaction](#eth_sendrawtransaction)
        - [Parameters](#parameters-23)
        - [Returns](#returns-23)
        - [Example](#example-23)
      - [eth_call](#eth_call)
        - [Parameters](#parameters-24)
        - [Returns](#returns-24)
        - [Example](#example-24)
      - [eth_estimateGas](#eth_estimategas)
        - [Parameters](#parameters-25)
        - [Returns](#returns-25)
        - [Example](#example-25)
      - [eth_getBlockByHash](#eth_getblockbyhash)
        - [Parameters](#parameters-26)
        - [Returns](#returns-26)
        - [Example](#example-26)
      - [eth_getBlockByNumber](#eth_getblockbynumber)
        - [Parameters](#parameters-27)
        - [Returns](#returns-27)
        - [Example](#example-27)
      - [eth_getTransactionByHash](#eth_gettransactionbyhash)
        - [Parameters](#parameters-28)
        - [Returns](#returns-28)
        - [Example](#example-28)
      - [eth_getTransactionByBlockHashAndIndex](#eth_gettransactionbyblockhashandindex)
        - [Parameters](#parameters-29)
        - [Returns](#returns-29)
        - [Example](#example-29)
      - [eth_getTransactionByBlockNumberAndIndex](#eth_gettransactionbyblocknumberandindex)
        - [Parameters](#parameters-30)
        - [Returns](#returns-30)
        - [Example](#example-30)
      - [eth_getTransactionReceipt](#eth_gettransactionreceipt)
        - [Parameters](#parameters-31)
        - [Returns](#returns-31)
        - [Example](#example-31)
      - [eth_getUncleByBlockHashAndIndex](#eth_getunclebyblockhashandindex)
        - [Parameters](#parameters-32)
        - [Returns](#returns-32)
        - [Example](#example-32)
      - [eth_getUncleByBlockNumberAndIndex](#eth_getunclebyblocknumberandindex)
        - [Parameters](#parameters-33)
        - [Returns](#returns-33)
        - [Example](#example-33)
      - [eth_getCompilers (DEPRECATED)](#eth_getcompilers-deprecated)
        - [Parameters](#parameters-34)
        - [Returns](#returns-34)
        - [Example](#example-34)
      - [eth_compileSolidity (DEPRECATED)](#eth_compilesolidity-deprecated)
        - [Parameters](#parameters-35)
        - [Returns](#returns-35)
        - [Example](#example-35)
      - [eth_compileLLL (DEPRECATED)](#eth_compilelll-deprecated)
        - [Parameters](#parameters-36)
        - [Returns](#returns-36)
        - [Example](#example-36)
      - [eth_compileSerpent (DEPRECATED)](#eth_compileserpent-deprecated)
        - [Parameters](#parameters-37)
        - [Returns](#returns-37)
        - [Example](#example-37)
      - [eth_newFilter](#eth_newfilter)
        - [A note on specifying topic filters:](#a-note-on-specifying-topic-filters)
        - [Parameters](#parameters-38)
        - [Returns](#returns-38)
        - [Example](#example-38)
      - [eth_newBlockFilter](#eth_newblockfilter)
        - [Parameters](#parameters-39)
        - [Returns](#returns-39)
        - [Example](#example-39)
      - [eth_newPendingTransactionFilter](#eth_newpendingtransactionfilter)
        - [Parameters](#parameters-40)
        - [Returns](#returns-40)
        - [Example](#example-40)
      - [eth_uninstallFilter](#eth_uninstallfilter)
        - [Parameters](#parameters-41)
        - [Returns](#returns-41)
        - [Example](#example-41)
      - [eth_getFilterChanges](#eth_getfilterchanges)
        - [Parameters](#parameters-42)
        - [Returns](#returns-42)
        - [Example](#example-42)
      - [eth_getFilterLogs](#eth_getfilterlogs)
        - [Parameters](#parameters-43)
        - [Returns](#returns-43)
        - [Example](#example-43)
      - [eth_getLogs](#eth_getlogs)
        - [Parameters](#parameters-44)
        - [Returns](#returns-44)
        - [Example](#example-44)
      - [eth_getWork](#eth_getwork)
        - [Parameters](#parameters-45)
        - [Returns](#returns-45)
        - [Example](#example-45)
      - [eth_submitWork](#eth_submitwork)
        - [Parameters](#parameters-46)
        - [Returns](#returns-46)
        - [Example](#example-46)
      - [eth_submitHashrate](#eth_submithashrate)
        - [Parameters](#parameters-47)
        - [Returns](#returns-47)
        - [Example](#example-47)
      - [eth_getProof](#eth_getproof)
        - [getProof-Parameters](#getproof-parameters)
        - [getProof-Returns](#getproof-returns)
        - [getProof-Example](#getproof-example)
      - [db_putString](#db_putstring)
        - [Parameters](#parameters-48)
        - [Returns](#returns-48)
        - [Example](#example-48)
      - [db_getString](#db_getstring)
        - [Parameters](#parameters-49)
        - [Returns](#returns-49)
        - [Example](#example-49)
      - [db_putHex](#db_puthex)
        - [Parameters](#parameters-50)
        - [Returns](#returns-50)
        - [Example](#example-50)
      - [db_getHex](#db_gethex)
        - [Parameters](#parameters-51)
        - [Returns](#returns-51)
        - [Example](#example-51)
      - [shh_version](#shh_version)
        - [Parameters](#parameters-52)
        - [Returns](#returns-52)
        - [Example](#example-52)
      - [shh_post](#shh_post)
        - [Parameters](#parameters-53)
        - [Returns](#returns-53)
        - [Example](#example-53)
      - [shh_newIdentity](#shh_newidentity)
        - [Parameters](#parameters-54)
        - [Returns](#returns-54)
        - [Example](#example-54)
      - [shh_hasIdentity](#shh_hasidentity)
        - [Parameters](#parameters-55)
        - [Returns](#returns-55)
        - [Example](#example-55)
      - [shh_newGroup](#shh_newgroup)
        - [Parameters](#parameters-56)
        - [Returns](#returns-56)
        - [Example](#example-56)
      - [shh_addToGroup](#shh_addtogroup)
        - [Parameters](#parameters-57)
        - [Returns](#returns-57)
        - [Example](#example-57)
      - [shh_newFilter](#shh_newfilter)
        - [Parameters](#parameters-58)
        - [Returns](#returns-58)
        - [Example](#example-58)
      - [shh_uninstallFilter](#shh_uninstallfilter)
        - [Parameters](#parameters-59)
        - [Returns](#returns-59)
        - [Example](#example-59)
      - [shh_getFilterChanges](#shh_getfilterchanges)
        - [Parameters](#parameters-60)
        - [Returns](#returns-60)
        - [Example](#example-60)
      - [shh_getMessages](#shh_getmessages)
        - [Parameters](#parameters-61)
        - [Returns](#returns-61)
        - [Example](#example-61)



# JSON RPC API

[JSON] (http://json.org/) es un formato ligero de intercambio de datos. Puede representar números, cadenas, secuencias ordenadas de valores y colecciones de pares de nombre / valor.

[JSON-RPC] (http://www.jsonrpc.org/specification) es un protocolo de llamada a procedimiento remoto (RPC) liviano y sin estado. Principalmente, esta especificación define varias estructuras de datos y las reglas en torno a su procesamiento. Es agnóstico en cuanto al transporte, ya que los conceptos se pueden usar dentro del mismo proceso, a través de sockets, a través de HTTP o en muchos entornos de paso de mensajes. Utiliza JSON ([RFC 4627] (http://www.ietf.org/rfc/rfc4627.txt)) como formato de datos.


## JavaScript API

Para hablar con un nodo Pirl desde una aplicación JavaScript, use la biblioteca [web3.js] (https://github.com/Pirl/web3.js), que brinda una interfaz conveniente para los métodos RPC.


## JSON-RPC Endpoint

Default JSON-RPC endpoints:

| Client | URL |
|-------|:------------:|
| Go |http://localhost:8545 | 



### Go

Puede iniciar HTTP JSON-RPC con el indicador `--rpc`
```bash
pirl--rpc
```

cambie el puerto predeterminado (8545) y la dirección del listado (localhost) con:

```bash
pirl--rpc --rpcaddr <ip> --rpcport <portnumber>
```

Si accede al RPC desde un navegador, CORS deberá habilitarse con el conjunto de dominios apropiado. De lo contrario, las llamadas de JavaScript están limitadas por la política del mismo origen y las solicitudes fallarán:

```bash
pirl--rpc --rpccorsdomain "http://localhost:3000"
```


## HEX value encoding

At present there are two key datatypes that are passed over JSON: unformatted byte arrays and quantities. Both are passed with a hex encoding, however with different requirements to formatting:

Al codificar ** CANTIDADES ** (enteros, números): codificar como hexadecimal, prefijo con "0x", la representación más compacta (excepción leve: cero debe representarse como "0x0"). Ejemplos:
- 0x41 (65 en decimal)
- 0x400 (1024 en decimal)
- INCORRECTO: 0x (siempre debe tener al menos un dígito - el cero es "0x0")
- INCORRECTO: 0x0400 (no se permiten ceros iniciales)
- MAL: ff (debe tener el prefijo 0x)

Al codificar ** DATOS UNFORMATT ** (matrices de bytes, direcciones de cuentas, hashes, matrices de bytes): codifique como hexadecimal, prefijo con "0x", dos dígitos hexadecimales por byte. Ejemplos:
- 0x41 (tamaño 1, "A")
- 0x004200 (tamaño 3, "\ 0B \ 0")
- 0x (tamaño 0, "")
- INCORRECTO: 0xf0f0f (debe ser un número par de dígitos)
- INCORRECTO: 004200 (debe tener el prefijo 0x)


## El parámetro de bloque por defecto

Los siguientes métodos tienen un parámetro de bloque predeterminado adicional:

- [eth_getBalance](#eth_getbalance)
- [eth_getCode](#eth_getcode)
- [eth_getTransactionCount](#eth_gettransactioncount)
- [eth_getStorageAt](#eth_getstorageat)
- [eth_call](#eth_call)

Cuando se realizan solicitudes que actúan sobre el estado de Pirl, el último parámetro de bloque predeterminado determina la altura del bloque.

Las siguientes opciones son posibles para el parámetro defaultBlock:

- `HEX String` - un número de bloque entero
- `String "firstest"para el bloque first / génesis
- `String "latest"` - para el último bloque extraído
- `String "pending"` - para el estado / transacciones pendientes

## Ejemplos de bucle explicados

Las siguientes opciones de bucle pueden devolver una respuesta cuando el nodo se queja sobre el tipo de contenido, esto se debe a que la opción --data establece el tipo de contenido en application / x-www-form-urlencoded. Si su nodo se queja, establezca manualmente el encabezado colocando -H "Tipo de contenido: aplicación / json" al comienzo de la llamada.

Los ejemplos tampoco incluyen la combinación de URL / IP y puerto, que debe ser el último argumento dado a curl e.x. 127.0.0.1:8545

## JSON-RPC metodos

* [web3_clientVersion](#web3_clientversion)
* [web3_sha3](#web3_sha3)
* [net_version](#net_version)
* [net_peerCount](#net_peercount)
* [net_listening](#net_listening)
* [eth_protocolVersion](#eth_protocolversion)
* [eth_syncing](#eth_syncing)
* [eth_coinbase](#eth_coinbase)
* [eth_mining](#eth_mining)
* [eth_hashrate](#eth_hashrate)
* [eth_gasPrice](#eth_gasprice)
* [eth_accounts](#eth_accounts)
* [eth_blockNumber](#eth_blocknumber)
* [eth_getBalance](#eth_getbalance)
* [eth_getStorageAt](#eth_getstorageat)
* [eth_getTransactionCount](#eth_gettransactioncount)
* [eth_getBlockTransactionCountByHash](#eth_getblocktransactioncountbyhash)
* [eth_getBlockTransactionCountByNumber](#eth_getblocktransactioncountbynumber)
* [eth_getUncleCountByBlockHash](#eth_getunclecountbyblockhash)
* [eth_getUncleCountByBlockNumber](#eth_getunclecountbyblocknumber)
* [eth_getCode](#eth_getcode)
* [eth_sign](#eth_sign)
* [eth_sendTransaction](#eth_sendtransaction)
* [eth_sendRawTransaction](#eth_sendrawtransaction)
* [eth_call](#eth_call)
* [eth_estimateGas](#eth_estimategas)
* [eth_getBlockByHash](#eth_getblockbyhash)
* [eth_getBlockByNumber](#eth_getblockbynumber)
* [eth_getTransactionByHash](#eth_gettransactionbyhash)
* [eth_getTransactionByBlockHashAndIndex](#eth_gettransactionbyblockhashandindex)
* [eth_getTransactionByBlockNumberAndIndex](#eth_gettransactionbyblocknumberandindex)
* [eth_getTransactionReceipt](#eth_gettransactionreceipt)
* [eth_getUncleByBlockHashAndIndex](#eth_getunclebyblockhashandindex)
* [eth_getUncleByBlockNumberAndIndex](#eth_getunclebyblocknumberandindex)
* [eth_getCompilers](#eth_getcompilers)
* [eth_compileLLL](#eth_compilelll)
* [eth_compileSolidity](#eth_compilesolidity)
* [eth_compileSerpent](#eth_compileserpent)
* [eth_newFilter](#eth_newfilter)
* [eth_newBlockFilter](#eth_newblockfilter)
* [eth_newPendingTransactionFilter](#eth_newpendingtransactionfilter)
* [eth_uninstallFilter](#eth_uninstallfilter)
* [eth_getFilterChanges](#eth_getfilterchanges)
* [eth_getFilterLogs](#eth_getfilterlogs)
* [eth_getLogs](#eth_getlogs)
* [eth_getWork](#eth_getwork)
* [eth_submitWork](#eth_submitwork)
* [eth_submitHashrate](#eth_submithashrate)
* [eth_getProof](#eth_getproof)
* [db_putString](#db_putstring)
* [db_getString](#db_getstring)
* [db_putHex](#db_puthex)
* [db_getHex](#db_gethex) 
* [shh_post](#shh_post)
* [shh_version](#shh_version)
* [shh_newIdentity](#shh_newidentity)
* [shh_hasIdentity](#shh_hasidentity)
* [shh_newGroup](#shh_newgroup)
* [shh_addToGroup](#shh_addtogroup)
* [shh_newFilter](#shh_newfilter)
* [shh_uninstallFilter](#shh_uninstallfilter)
* [shh_getFilterChanges](#shh_getfilterchanges)
* [shh_getMessages](#shh_getmessages)

## JSON RPC API Referencia

***

#### web3_clientVersion

Devuelve la versión actual del cliente.

##### Parámetros
ninguna

##### Devoluciones

`String` - La versión actual del cliente.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":67}'

// Result
{
  "id":67,
  "jsonrpc":"2.0",
  "result": "Mist/v0.9.3/darwin/go1.4.1"
}
```

***

#### web3_sha3

Devuelve Keccak-256 (* no * el SHA3-256 estandarizado) de los dados.

##### Parámetros

1. 'DATOS' - los datos para convertir en un hash SHA3.

```js
params: [
  "0x68656c6c6f20776f726c64"
]
```

##### Devoluciones

`DATA` - El resultado SHA3 de la cadena dada.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"web3_sha3","params":["0x68656c6c6f20776f726c64"],"id":64}'

// Result
{
  "id":64,
  "jsonrpc": "2.0",
  "result": "0x47173285a8d7341e5e972fc677286384f802f8ef42a5ec5f03bbfa254cb01fad"
}
```

***

#### net_version

Devuelve el ID de red actual.

##### Parámetros
ninguno

##### Devoluciones

`String` - El identificador de red actual.
- `" 1 "`: 2 Mainnet


##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"net_version","params":[],"id":67}'

// Result
{
  "id":67,
  "jsonrpc": "2.0",
  "result": "3"
}
```

***

#### net_listening

Devuelve `true` si el cliente está escuchando activamente las conexiones de red.

##### Parámetros
ninguno

##### Devoluciones

`Boolean` -` true` cuando se escucha, de lo contrario, `false`.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"net_listening","params":[],"id":67}'

// Result
{
  "id":67,
  "jsonrpc":"2.0",
  "result":true
}
```

***

#### net_peerCount

Devuelve el número de pares conectados actualmente al cliente.

##### Parámetros
ninguna

##### Devoluciones

`CANTIDAD` - entero del número de pares conectados.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":74}'

// Result
{
  "id":74,
  "jsonrpc": "2.0",
  "result": "0x2" // 2
}
```

***

#### eth_protocolVersion

Devuelve la versión actual del protocolo Pirl.

##### Parámetros
ninguno

##### Devoluciones

`String` - La versión actual del protocolo Pirl.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_protocolVersion","params":[],"id":67}'

// Result
{
  "id":67,
  "jsonrpc": "2.0",
  "result": "54"
}
```

***

#### eth_syncing

Devuelve un objeto con datos sobre el estado de sincronización o `false '.


##### Parámetros
ninguno

##### Devoluciones

`Object | Boolean`, un objeto con datos de estado de sincronización o` FALSE`, cuando no se está sincronizando:
   - `startingBlock`:` QUANTITY` - El bloque en el que comenzó la importación (solo se restablecerá una vez que la sincronización haya llegado a su cabeza)
   - `currentBlock`:` QUANTITY` - El bloque actual, igual que eth_blockNumber
   - `highestBlock`:` QUANTITY` - El bloque más alto estimado

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_syncing","params":[],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": {
    startingBlock: '0x384',
    currentBlock: '0x386',
    highestBlock: '0x454'
  }
}
// Or when not syncing
{
  "id":1,
  "jsonrpc": "2.0",
  "result": false
}
```

***

#### eth_coinbase

Devuelve la dirección de coinbase del cliente.


##### Parámetros
ninguno

##### Devoluciones

`DATOS`, 20 bytes - la dirección de coinbase actual.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_coinbase","params":[],"id":64}'

// Result
{
  "id":64,
  "jsonrpc": "2.0",
  "result": "0xc94770007dda54cF92009BFF0dE90c06F603a09f"
}
```

***

#### eth_mining

Devuelve `true` si el cliente está minando activamente nuevos bloques.

##### Parámetros
ninguno

##### Devoluciones

`Boolean` - devuelve` true` de que el cliente está minando, de lo contrario `false`.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_mining","params":[],"id":71}'

// Result
{
  "id":71,
  "jsonrpc": "2.0",
  "result": true
}

```

***

#### eth_hashrate

Devuelve el número de hashes por segundo con el que se está minando el nodo.

##### Parámetros
ninguno

##### Devoluciones

`CANTIDAD` - número de hashes por segundo.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_hashrate","params":[],"id":71}'

// Result
{
  "id":71,
  "jsonrpc": "2.0",
  "result": "0x38a"
}

```

***

#### eth_gasPrice

Devuelve el precio actual por gas en wei.

##### Parámetros
ninguno

##### Devoluciones

`CANTIDAD` - entero del precio actual del gas en wei.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_gasPrice","params":[],"id":73}'

// Result
{
  "id":73,
  "jsonrpc": "2.0",
  "result": "0x09184e72a000" // 10000000000000
}
```

***

#### eth_accounts

Devuelve una lista de direcciones propiedad del cliente.


##### Parámetros
ninguno

##### Devoluciones

`Array of DATA`, 20 Bytes - direcciones propiedad del cliente.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_accounts","params":[],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": ["0xc94770007dda54cF92009BFF0dE90c06F603a09f"]
}
```

***

#### eth_blockNumber

Devuelve el número del bloque más reciente.

##### Parámetros
ninguno

##### Devoluciones

`CANTIDAD` - número entero del número de bloque actual en el que se encuentra el cliente.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'

// Result
{
  "id":83,
  "jsonrpc": "2.0",
  "result": "0xc94" // 1207
}
```

***

#### eth_getBalance

Devuelve el saldo de la cuenta de la dirección dada.

##### Parámetros

1. `DATA`, 20 Bytes - dirección para verificar el saldo.
2. `QUANTITY | TAG` - número de bloque entero, o la cadena` "latest" `,` "firstiest" `o` "pending" `, consulte el [parámetro predeterminado del bloque] (# the-default-block-parameters)

```js
params: [
   '0xc94770007dda54cF92009BFF0dE90c06F603a09f',
   'latest'
]
```

##### Devoluciones

`QUANTITY` - entero del balance actual en wei.


##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBalance","params":["0xc94770007dda54cF92009BFF0dE90c06F603a09f", "latest"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x0234c8a3397aab58" // 158972490234375000
}
```

***

#### eth_getStorageAt

Devuelve el valor de una posición de almacenamiento en una dirección dada.

##### Parámetros

1. `DATA`, 20 Bytes - dirección del almacenamiento.
2. `QUANTITY` - entero de la posición en el almacenamiento.
3. `QUANTITY | TAG` - número de bloque entero, o la cadena` "latest" `,` "firstiest" `o` "pending" `, consulte el [parámetro predeterminado del bloque] (# the-default-block-parameters)

##### Devoluciones

`DATA` - el valor en esta posición de almacenamiento.

##### Ejemplo
Calcular la posición correcta depende del almacenamiento a recuperar. Considere el siguiente contrato implementado en `0x295a70b2de5e3953354a6a8344e616ed314d7251` por la dirección` 0x391694e7e0b0cce554cb130d723a9d27458f9298.

```
contract Storage {
    uint pos0;
    mapping(address => uint) pos1;
    
    function Storage() {
        pos0 = 1234;
        pos1[msg.sender] = 5678;
    }
}
```

Recuperar el valor de pos0 es sencillo:

```js
curl -X POST --data '{"jsonrpc":"2.0", "method": "eth_getStorageAt", "params": ["0x295a70b2de5e3953354a6a8344e616ed314d7251", "0x0", "latest"], "id": 1}' localhost:8545

{"jsonrpc":"2.0","id":1,"result":"0x00000000000000000000000000000000000000000000000000000000000004d2"}
```

Recuperar un elemento del mapa es más difícil. La posición de un elemento en el mapa se calcula con:
```js
keccack(LeftPad32(key, 0), LeftPad32(map position, 0))
```

Esto significa que para recuperar el almacenamiento en pos1 ["0x391694e7e0b0cce554cb130d723a9d27458f9298"] necesitamos calcular la posición con:
```js
keccak(decodeHex("000000000000000000000000391694e7e0b0cce554cb130d723a9d27458f9298" + "0000000000000000000000000000000000000000000000000000000000000001"))
```
La consola pirl que viene con la biblioteca web3 se puede usar para hacer el cálculo:
```js
> var key = "000000000000000000000000391694e7e0b0cce554cb130d723a9d27458f9298" + "0000000000000000000000000000000000000000000000000000000000000001"
undefined
> web3.sha3(key, {"encoding": "hex"})
"0x6661e9d6d8b923d5bbaab1b96e1dd51ff6ea2a93520fdc9eb75d059238b8c5e9"
```
Ahora para buscar el almacenamiento:
```js
curl -X POST --data '{"jsonrpc":"2.0", "method": "eth_getStorageAt", "params": ["0x295a70b2de5e3953354a6a8344e616ed314d7251", "0x6661e9d6d8b923d5bbaab1b96e1dd51ff6ea2a93520fdc9eb75d059238b8c5e9", "latest"], "id": 1}' localhost:8545

{"jsonrpc":"2.0","id":1,"result":"0x000000000000000000000000000000000000000000000000000000000000162e"}

```

***

#### eth_getTransactionCount

Devuelve el número de transacciones * enviadas * desde una dirección.


##### Parámetros

1. 'DATOS', 20 bytes - dirección.
2. `QUANTITY | TAG` - número de bloque entero, o la cadena` "latest" `,` "firstiest" `o` "pending" `, consulte el [parámetro predeterminado del bloque] (# the-default-block-parameters)

```js
params: [
   '0xc94770007dda54cF92009BFF0dE90c06F603a09f',
   'latest' // state at the latest block
]
```

##### Devoluciones

`QUANTITY` - el número entero de transacciones enviadas desde esta dirección.


##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getTransactionCount","params":["0xc94770007dda54cF92009BFF0dE90c06F603a09f","latest"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x1" // 1
}
```

***

#### eth_getBlockTransactionCountByHash

Devuelve el número de transacciones en un bloque de un bloque que coincide con el hash de bloque dado.


##### Parámetros

1. `DATA`, 32 Bytes - hash de un bloque.

```js
params: [
   '0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238'
]
```

##### Devoluciones

`QUANTITY` - entero del número de transacciones en este bloque.


##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBlockTransactionCountByHash","params":["0xc94770007dda54cF92009BFF0dE90c06F603a09f"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xc" // 11
}
```

***

#### eth_getBlockTransactionCountByNumber
>>
Devuelve el número de transacciones en un bloque que coincide con el número de bloque dado.


##### Parámetros

1. `QUANTITY | TAG` - número entero de un número de bloque, o la cadena` "earliest" `,` "latest" o `" pending "`, como en el [parámetro de bloque predeterminado] (# the-default-block -parámetro).

```js
params: [
   '0xe8', // 232
]
```

##### Devoluciones

`CANTIDAD` - entero del número de transacciones en este bloque.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBlockTransactionCountByNumber","params":["0xe8"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xa" // 10
}
```

***

#### eth_getUncleCountByBlockHash

Devuelve el número de tíos en un bloque de un bloque que coincide con el hash de bloque dado.


##### Parámetros

1. `DATA`, 32 Bytes - hash de un bloque.

```js
params: [
   '0xc94770007dda54cF92009BFF0dE90c06F603a09f'
]
```

##### Devoluciones

`CANTIDAD` - entero del número de tíos en este bloque.


##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getUncleCountByBlockHash","params":["0xc94770007dda54cF92009BFF0dE90c06F603a09f"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xc" // 1
}
```

***

#### eth_getUncleCountByBlockNumber

Devuelve el número de tíos en un bloque de un bloque que coincide con el número de bloque dado.


##### Parámetros

1. `QUANTITY | TAG` - número entero de un número de bloque, o la cadena" más reciente "," más antigua "o" pendiente ", consulte el [parámetro de bloque predeterminado] (# el parámetro de bloque predeterminado).

```js
params: [
   '0xe8', // 232
]
```

##### Devoluciones

`CANTIDAD` - entero del número de tíos en este bloque.


##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getUncleCountByBlockNumber","params":["0xe8"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x1" // 1
}
```

***

#### eth_getCode

Devuelve el código a una dirección dada.


##### Parámetros

1. 'DATOS', 20 bytes - dirección.
2. `QUANTITY | TAG` - número de bloque entero, o la cadena` "latest" `,` "firstiest" `o` "pending" `, consulte el [parámetro predeterminado del bloque] (# the-default-block-parameters) .

```js
params: [
   '0xa94f5374fce5edbc8e2a8697c15331677e6ebf0b',
   '0x2'  // 2
]
```

##### Devoluciones

'DATA' - el código de la dirección dada.


##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getCode","params":["0xa94f5374fce5edbc8e2a8697c15331677e6ebf0b", "0x2"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x600160008035811a818181146012578301005b601b6001356025565b8060005260206000f25b600060078202905091905056"
}
```

***

#### eth_sign

El método de signo calcula una firma específica de Pirl con: `signo (keccak256 (" \ x19Pirl Signed Message: \ n "+ len (message) + message)))`.

Al agregar un prefijo al mensaje, la firma calculada es reconocible como una firma específica de Pirl. Esto evita el uso indebido cuando un DApp malintencionado puede firmar datos arbitrarios (por ejemplo, una transacción) y usar la firma para hacerse pasar por la víctima.

** Nota ** la dirección para firmar debe estar desbloqueada.

##### Parámetros
cuenta, mensaje

1. 'DATA', 20 bytes - dirección.
2. `DATA`, N Bytes - mensaje para firmar.

##### Devoluciones

'DATA': Firma

##### Ejemplo

```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_sign","params":["0x9b2055d370f73ec7d8a03e965129118dc8f5bf83", "0xdeadbeaf"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xa3f20717a250c2b0b729b7e5becbff67fdaef7e0699da4de7ca5895b02a170a12d887fd3b17bfdce3481f10bea41f45ba9f709d39ce8325427b57afcfc994cee1b"
}
```

Se puede encontrar un ejemplo de cómo utilizar Solidar Ececover para verificar la firma calculada con `eth_sign` (aquí) (https://gist.github.com/bas-vk/d46d83da2b2b4721efb0907aecdb7ebd). El contrato se implementa en el testnet Ropsten y Rinkeby.

***

#### eth_sendTransaction

Crea una nueva transacción de llamada de mensaje o una creación de contrato, si el campo de datos contiene código.

##### Parámetros

1. `Object` - El objeto de transacción
  - `from`:` DATA`, 20 Bytes - La dirección desde la que se envía la transacción.
  - `to`:` DATA`, 20 Bytes - (opcional al crear un nuevo contrato) La dirección a la que se dirige la transacción.
  - `gas`:` QUANTITY` - (opcional, predeterminado: 90000) Número entero del gas provisto para la ejecución de la transacción. Se devolverá el gas no utilizado.
  - `gasPrice`:` QUANTITY` - (opcional, predeterminado: A determinar) Integer del gasPrice utilizado para cada gas pagado
  - `value`:` QUANTITY` - (opcional) Número entero del valor enviado con esta transacción
  - `data`:` DATA` - El código compilado de un contrato O el hash de la firma del método invocado y los parámetros codificados.
  - `nonce`:` QUANTITY` - (opcional) Entero de un nonce. Esto permite sobrescribir sus propias transacciones pendientes que utilizan el mismo nonce.

```js
params: [{
  "from": "0xb60e8dd61c5d32be8058bb8eb970870f07233155",
  "to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
  "gas": "0x76c0", // 30400
  "gasPrice": "0x9184e72a000", // 10000000000000
  "value": "0x9184e72a", // 2441406250
  "data": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"
}]
```

##### Devoluciones

`DATOS`, 32 bytes: el hash de transacción o el hash cero si la transacción aún no está disponible.

Use [eth_getTransactionReceipt] (# eth_gettransactionreceipt) para obtener la dirección del contrato, después de que se realizó la extracción de la transacción, cuando creó un contrato.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_sendTransaction","params":[{see above}],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331"
}
```

***

#### eth_sendRawTransaction

Crea una nueva transacción de llamada de mensaje o una creación de contrato para transacciones firmadas.

##### Parámetros

1. 'DATA', Los datos de la transacción firmada.

```js
params: ["0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"]
```

##### Devoluciones

`DATA`, 32 bytes: el hash de transacción o el hash cero si la transacción aún no está disponible.

Use [eth_getTransactionReceipt] (# eth_gettransactionreceipt) para obtener la dirección del contrato, después de que se realizó la extracción de la transacción, cuando creó un contrato.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_sendRawTransaction","params":[{see above}],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331"
}
```

***

#### eth_call

Ejecuta una nueva llamada de mensaje inmediatamente sin crear una transacción en la cadena de bloques.


##### Parámetros

1. `Object` - El objeto de llamada de transacción
  - `from`:` DATA`, 20 Bytes - (opcional) La dirección desde la que se envía la transacción.
  - `to`:` DATA`, 20 Bytes - La dirección a la que se dirige la transacción.
  - `gas`:` QUANTITY` - (opcional) Número entero del gas provisto para la ejecución de la transacción. eth_call consume gas cero, pero este parámetro puede ser necesario para algunas ejecuciones.
  - `gasPrice`:` QUANTITY` - (opcional) Número entero del gasPrice utilizado para cada gas pagado
  - `value`:` QUANTITY` - (opcional) Número entero del valor enviado con esta transacción
  - `data`:` DATA` - (opcional) Hash de la firma del método y los parámetros codificados.
2. `QUANTITY | TAG` - número de bloque entero, o la cadena` "latest" `,` "firstiest" `o` "pending" `, consulte el [parámetro predeterminado del bloque] (# the-default-block-parameters)

##### Devoluciones

'DATA' - el valor de retorno del contrato ejecutado.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_call","params":[{see above}],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x"
}
```

***

#### eth_estimateGas

Genera y devuelve una estimación de cuánto gas es necesario para permitir que la transacción se complete. La transacción no se añadirá a la cadena de bloques. Tenga en cuenta que la estimación puede ser significativamente mayor que la cantidad de gas realmente utilizada por la transacción, por una variedad de razones que incluyen la mecánica de EVM y el rendimiento del nodo.

##### Parámetros

Vea los parámetros [eth_call] (# eth_call), espere que todas las propiedades sean opcionales. Si no se especifica un límite de gas, pirl utiliza el límite de gas de bloque del bloque pendiente como un límite superior. Como resultado, la estimación devuelta podría no ser suficiente para ejecutar la llamada / transacción cuando la cantidad de gas es mayor que el límite de gas de bloque pendiente.

##### Devoluciones

`QUANTITY` - la cantidad de gas utilizada.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_estimateGas","params":[{see above}],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x5208" // 21000
}
```

***

#### eth_getBlockByHash

Devuelve información sobre un bloque por hash.


##### Parámetros

1. 'DATA', 32 Bytes - Hash de un bloque.
2. `Boolean` - Si` true` devuelve los objetos de transacción completos, si `false 'solo los hashes de las transacciones.

```js
params: [
   '0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331',
   true
]
```

##### Devoluciones

`Object` - Un objeto de bloque, o` null` cuando no se encontró ningún bloque:

  - `number`:` QUANTITY` - el número de bloque. `null` cuando su bloque pendiente.
  - `hash`:` DATA`, 32 Bytes - hash del bloque. `null` cuando su bloque pendiente.
  - `parentHash`:` DATA`, 32 Bytes - hash del bloque principal.
  - `nonce`:` DATA`, 8 Bytes - hash de la prueba de trabajo generada. `null` cuando su bloque pendiente.
  - `sha3Uncles`:` DATA`, 32 Bytes - SHA3 de los datos de los tíos en el bloque.
  - `logsBloom`:` DATA`, 256 Bytes - el filtro de floración para los registros del bloque. `null` cuando su bloque pendiente.
  - `transactionRoot`:` DATA`, 32 Bytes - la raíz del trie de transacción del bloque.
  - `stateRoot`:` DATA`, 32 Bytes - la raíz de la prueba de estado final del bloque.
  - `receiptsRoot`:` DATA`, 32 Bytes - la raíz de los recibos trie del bloque.
  - `miner`:` DATA`, 20 Bytes - la dirección del beneficiario a quien se le entregaron las recompensas de la minería.
  - `dificultad`:` CANTIDAD` - entero de la dificultad para este bloque.
  - `totalDifficulty`:` QUANTITY` - entero de la dificultad total de la cadena hasta este bloque.
  - `extraData`:` DATA` - el campo "datos extra" de este bloque.
  - `size`:` QUANTITY` - integra el tamaño de este bloque en bytes.
  - `gasLimit`:` QUANTITY` - el gas máximo permitido en este bloque.
  - `gasUsed`:` QUANTITY` - el total de gas utilizado por todas las transacciones en este bloque.
  - `timestamp`:` QUANTITY` - la marca de tiempo de Unix para cuando se compaginó el bloque.
  - `transaction`:` Array` - Array de objetos de transacción, o hashes de transacción de 32 bytes, según el último parámetro dado.
  - `tíos`:` Array` - Array of tío hashes.


##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBlockByHash","params":["0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331", true],"id":1}'

// Result
{
"id":1,
"jsonrpc":"2.0",
"result": {
    "number": "0x1b4", // 436
    "hash": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331",
    "parentHash": "0x9646252be9520f6e71339a8df9c55e4d7619deeb018d2a3f2d21fc165dde5eb5",
    "nonce": "0xe04d296d2460cfb8472af2c5fd05b5a214109c25688d3704aed5484f9a7792f2",
    "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
    "logsBloom": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331",
    "transactionsRoot": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
    "stateRoot": "0xd5855eb08b3387c0af375e9cdb6acfc05eb8f519e419b874b6ff2ffda7ed1dff",
    "miner": "0x4e65fda2159562a496f9f3522f89122a3088497a",
    "difficulty": "0x027f07", // 163591
    "totalDifficulty":  "0x027f07", // 163591
    "extraData": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "size":  "0x027f07", // 163591
    "gasLimit": "0x9f759", // 653145
    "gasUsed": "0x9f759", // 653145
    "timestamp": "0x54e34e8e" // 1424182926
    "transactions": [{...},{ ... }] 
    "uncles": ["0x1606e5...", "0xd5145a9..."]
  }
}
```

***

#### eth_getBlockByNumber

Devuelve información sobre un bloque por número de bloque.

##### Parámetros

1. `QUANTITY | TAG` - número entero de un número de bloque, o la cadena` "earliest" `,` "latest" o `" pending "`, como en el [parámetro de bloque predeterminado] (# the-default-block -parámetro).
2. `Boolean` - Si` true` devuelve los objetos de transacción completos, si `false 'solo los hashes de las transacciones.

```js
params: [
   '0x1b4', // 436
   true
]
```

##### Devoluciones

Ver [eth_getBlockByHash] (# eth_getblockbyhash)

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["0x1b4", true],"id":1}'
```

Resultado vea [eth_getBlockByHash] (# eth_getblockbyhash)

***

#### eth_getTransactionByHash

Devuelve la información sobre una transacción solicitada por el hash de transacción.


##### Parámetros

1. `DATA`, 32 Bytes - hash de una transacción

```js
params: [
   "0x88df016429689c079f3b2f6ad39fa052532c56795b733da78a91ebe6a713944b"
]
```

##### Devoluciones

`Object` - Un objeto de transacción, o` null` cuando no se encontró ninguna transacción:

  - `blockHash`:` DATA`, 32 Bytes - hash del bloque donde estaba esta transacción. `null` cuando está pendiente.
  - `blockNumber`:` QUANTITY` - número de bloque donde estaba esta transacción. `null` cuando está pendiente.
  - `from`:` DATA`, 20 Bytes - dirección del remitente.
  - `gas`:` QUANTITY` - gas proporcionado por el remitente.
  - `gasPrice`:` CANTIDAD` - precio del gas provisto por el remitente en Wei.
  - `hash`:` DATA`, 32 Bytes - hash de la transacción.
  - `input`:` DATA` - los datos enviados junto con la transacción.
  - `nonce`:` QUANTITY` - el número de transacciones realizadas por el remitente antes de esta.
  - `to`:` DATA`, 20 Bytes - dirección del receptor. `null` cuando es una transacción de creación de contrato.
  - `transactionIndex`:` QUANTITY` - entero de la posición del índice de la transacción en el bloque. `null` cuando está pendiente.
  - `value`:` QUANTITY` - valor transferido en Wei.
  - `v`:` QUANTITY` - ID de recuperación de ECDSA
  - `r`:` DATA`, 32 Bytes - Firma ECDSA r
  - `s`:` DATA`, 32 Bytes - firma ECDSA s

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getTransactionByHash","params":["0x88df016429689c079f3b2f6ad39fa052532c56795b733da78a91ebe6a713944b"],"id":1}'

// Result
{
  "jsonrpc":"2.0",
  "id":1,
  "result":{
    "blockHash":"0x1d59ff54b1eb26b013ce3cb5fc9dab3705b415a67127a003c3e61eb445bb8df2",
    "blockNumber":"0x5daf3b", // 6139707
    "from":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",
    "gas":"0xc350", // 50000
    "gasPrice":"0x4a817c800", // 20000000000
    "hash":"0x88df016429689c079f3b2f6ad39fa052532c56795b733da78a91ebe6a713944b",
    "input":"0x68656c6c6f21",
    "nonce":"0x15", // 21
    "to":"0xf02c1c8e6114b1dbe8937a39260b5b0a374432bb",
    "transactionIndex":"0x41", // 65
    "value":"0xf3dbb76162000", // 4290000000000000
    "v":"0x25", // 37
    "r":"0x1b5e176d927f8e9ab405058b2d2457392da3e20f328b16ddabcebc33eaac5fea",
    "s":"0x4ba69724e8f69de52f0125ad8b3c5c2cef33019bac3249e2c0a2192766d1721c"
  }
}
```

***

#### eth_getTransactionByBlockHashAndIndex

Devuelve información sobre una transacción por hash de bloque y posición de índice de transacción.


##### Parámetros

1. `DATA`, 32 Bytes - hash de un bloque.
2. `CANTIDAD` - entero de la posición del índice de transacción.

```js
params: [
   '0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331',
   '0x0' // 0
]
```

##### Devoluciones

Consulte [eth_getTransactionByHash] (# eth_gettransactionbyhash)

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getTransactionByBlockHashAndIndex","params":["0xc6ef2fc5426d6ad6fd9e2a26abeab0aa2411b7ab17f30a99d3cb96aed1d1055b", "0x0"],"id":1}'
```

Resultado vea [eth_getTransactionByHash] (# eth_gettransactionbyhash)

***

#### eth_getTransactionByBlockNumberAndIndex

Devuelve información sobre una transacción por número de bloque y posición de índice de transacción.


##### Parámetros

1. `QUANTITY | TAG` - un número de bloque, o la cadena` "firstiest" `,` "latest" `o` "pending" `, como en el [parámetro predeterminado del bloque] (# the-default-block-parameters ).
2. `QUANTITY` - la posición del índice de transacción.

```js
params: [
   '0x29c', // 668
   '0x0' // 0
]
```

##### Devoluciones

Consulte [eth_getTransactionByHash] (# eth_gettransactionbyhash)

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getTransactionByBlockNumberAndIndex","params":["0x29c", "0x0"],"id":1}'
```

Resultado vea [eth_getTransactionByHash] (# eth_gettransactionbyhash)

***

#### eth_getTransactionReceipt

Devuelve el recibo de una transacción mediante hash de transacción.

** Nota ** Que el recibo no está disponible para transacciones pendientes.


##### Parámetros

1. `DATA`, 32 Bytes - hash de una transacción

```js
params: [
   '0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238'
]
```

##### Devoluciones

`Object` - Un objeto de recibo de transacción, o` null` cuando no se encontró un recibo:

  - `transactionHash`: `DATA`, 32 Bytes - hash de la transacción.
  - `transactionIndex`:` QUANTITY` - entero de la posición del índice de la transacción en el bloque.
  - `blockHash`:` DATA`, 32 Bytes - hash del bloque donde estaba esta transacción.
  - `blockNumber`:` QUANTITY` - número de bloque donde estaba esta transacción.
  - `from`:` DATA`, 20 Bytes - dirección del remitente.
  - `to`:` DATA`, 20 Bytes - dirección del receptor. nulo cuando se trata de una transacción de creación de contrato.
  - `cumulativeGasUsed`: `QUANTITY` - La cantidad total de gas utilizada cuando esta transacción se ejecutó en el bloque.
  - `gasUsed`: `QUANTITY` - La cantidad de gas utilizada solo por esta transacción específica.
  - `contractAddress`: `DATA`, 20 Bytes - La dirección del contrato creado, si la transacción fue una creación de contrato, de lo contrario,` null`.
  - `logs`:` Array` - Array de objetos de registro, que esta transacción generó.
  - `logsBloom`:` DATA`, 256 Bytes - Filtro Bloom para clientes livianos para recuperar rápidamente los registros relacionados.
  
También devuelve _either_:

  - `root`:` DATA` 32 bytes de stateroot posterior a la transacción (antes de Bizancio)
  - `status`:` CANTIDAD` ya sea `1` (éxito) o` 0` (falla)


##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getTransactionReceipt","params":["0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"],"id":1}'

// Result
{
"id":1,
"jsonrpc":"2.0",
"result": {
     transactionHash: '0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238',
     transactionIndex:  '0x1', // 1
     blockNumber: '0xb', // 11
     blockHash: '0xc6ef2fc5426d6ad6fd9e2a26abeab0aa2411b7ab17f30a99d3cb96aed1d1055b',
     cumulativeGasUsed: '0x33bc', // 13244
     gasUsed: '0x4dc', // 1244
     contractAddress: '0xb60e8dd61c5d32be8058bb8eb970870f07233155', // or null, if none was created
     logs: [{
         // logs as returned by getFilterLogs, etc.
     }, ...],
     logsBloom: "0x00...0", // 256 byte bloom filter
     status: '0x1'
  }
}
```

***

#### eth_getUncleByBlockHashAndIndex

Devuelve información sobre un tío de un bloque por posición de índice hash y tío.


##### Parámetros


1. `DATA`, 32 Bytes - hash un bloque.
2. `CANTIDAD` - la posición del índice del tío.

```js
params: [
   '0xc6ef2fc5426d6ad6fd9e2a26abeab0aa2411b7ab17f30a99d3cb96aed1d1055b',
   '0x0' // 0
]
```

##### Devoluciones

Ver [eth_getBlockByHash] (# eth_getblockbyhash)

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getUncleByBlockHashAndIndex","params":["0xc6ef2fc5426d6ad6fd9e2a26abeab0aa2411b7ab17f30a99d3cb96aed1d1055b", "0x0"],"id":1}'
```

Resultado vea [eth_getBlockByHash] (# eth_getblockbyhash)

** Nota **: Un tío no contiene transacciones individuales.

***

#### eth_getUncleByBlockNumberAndIndex

Devuelve información sobre un tío de un bloque por número y posición de índice de tío.


##### Parámetros

1. `QUANTITY | TAG` - un número de bloque, o la cadena` "firstiest" `,` "latest" `o` "pending" `, como en el [parámetro predeterminado del bloque] (# the-default-block-parameters ).
2. `QUANTITY` - la posición del índice del tío.

```js
params: [
   '0x29c', // 668
   '0x0' // 0
]
```

##### Devoluciones

Ver [eth_getBlockByHash] (# eth_getblockbyhash)

** Nota **: Un tío no contiene transacciones individuales.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getUncleByBlockNumberAndIndex","params":["0x29c", "0x0"],"id":1}'
```

Resultado vea [eth_getBlockByHash] (# eth_getblockbyhash)

***

#### eth_getCompilers (DEPRECATED)

Devuelve una lista de compiladores disponibles en el cliente.

##### Parámetros
ninguna

##### Devoluciones

`Array` - Array de compiladores disponibles.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getCompilers","params":[],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": ["solidity", "lll", "serpent"]
}
```

***

#### eth_compileSolidity (DEPRECATED)

Devuelve el código de solidez compilado.

##### Parámetros

1. `String` - El código fuente.

```js
params: [
   "contract test { function multiply(uint a) returns(uint d) {   return a * 7;   } }",
]
```

##### Devoluciones

'DATOS' - El código fuente compilado.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_compileSolidity","params":["contract test { function multiply(uint a) returns(uint d) {   return a * 7;   } }"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": {
      "code": "0x605880600c6000396000f3006000357c010000000000000000000000000000000000000000000000000000000090048063c6888fa114602e57005b603d6004803590602001506047565b8060005260206000f35b60006007820290506053565b91905056",
      "info": {
        "source": "contract test {\n   function multiply(uint a) constant returns(uint d) {\n       return a * 7;\n   }\n}\n",
        "language": "Solidity",
        "languageVersion": "0",
        "compilerVersion": "0.9.19",
        "abiDefinition": [
          {
            "constant": true,
            "inputs": [
              {
                "name": "a",
                "type": "uint256"
              }
            ],
            "name": "multiply",
            "outputs": [
              {
                "name": "d",
                "type": "uint256"
              }
            ],
            "type": "function"
          }
        ],
        "userDoc": {
          "methods": {}
        },
        "developerDoc": {
          "methods": {}
        }
      }

}
```

***

#### eth_compileLLL (DEPRECATED)

Devuelve el código LLL compilado.

##### Parámetros

1. `String` - El código fuente.

```js
params: [
   "(returnlll (suicide (caller)))",
]
```

##### Devoluciones

'DATOS' - El código fuente compilado.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_compileLLL","params":["(returnlll (suicide (caller)))"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x603880600c6000396000f3006001600060e060020a600035048063c6888fa114601857005b6021600435602b565b8060005260206000f35b600081600702905091905056" // the compiled source code
}
```

***

#### eth_compileSerpent (DEPRECATED)

Devuelve el código de serpiente compilado.

##### Parámetros

1. `String` - El código fuente.

```js
params: [
   "/* some serpent */",
]
```

##### Devoluciones

'DATOS' - El código fuente compilado.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_compileSerpent","params":["/* some serpent */"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x603880600c6000396000f3006001600060e060020a600035048063c6888fa114601857005b6021600435602b565b8060005260206000f35b600081600702905091905056" // the compiled source code
}
```

***

#### eth_newFilter

Crea un objeto de filtro, basado en las opciones de filtro, para notificar cuándo cambia el estado (registros).
Para verificar si el estado ha cambiado, llame a [eth_getFilterChanges] (# eth_getfilterchanges).

##### Una nota sobre la especificación de filtros de temas:
Los temas dependen del orden. Una transacción con un registro con temas [A, B] coincidirá con los siguientes filtros de temas:
* `[]` "cualquier cosa"
* `[A]` "A en la primera posición (y nada después)"
* `[null, B]` "cualquier cosa en la primera posición Y B en la segunda posición (y cualquier cosa después)"
* `[A, B]` "A en la primera posición Y B en la segunda posición (y cualquier cosa después)"
* `[[A, B], [A, B]]` "(A O B) en la primera posición Y (A O B) en la segunda posición (y cualquier cosa después)"

##### Parámetros

1. `Objeto` - Las opciones de filtro:
  - `fromBlock`:` QUANTITY | TAG` - (opcional, predeterminado: `" latest "`) Número de bloque entero, o `" latest "` para el último bloque extraído o `" pendiente "`, `" firstiest "` para Transacciones aún no minadas.
  - `toBlock`:` QUANTITY | TAG` - (opcional, predeterminado: `" latest "`) Número de bloque entero, o `" latest "` para el último bloque extraído o `" pendiente "`, `" firstiest "` para Transacciones aún no minadas.
  - `address`:` DATA | Array`, 20 Bytes - (opcional) Dirección de contrato o una lista de direcciones desde donde se deben originar los registros.
  - `topics`:` Array of DATA`, - (opcional) Array of 32 Bytes `DATA` topics. Los temas dependen del orden. Cada tema también puede ser una matriz de DATOS con "o" opciones.

```js
params: [{
  "fromBlock": "0x1",
  "toBlock": "0x2",
  "address": "0x8888f1f195afa192cfee860698584c030f4c9db1",
  "topics": ["0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b", null, ["0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b", "0x0000000000000000000000000aff3454fce5edbc8cca8697c15331677e6ebccc"]]
}]
```

##### Devoluciones

`CANTIDAD` - Un ID de filtro.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_newFilter","params":[{"topics":["0x0000000000000000000000000000000000000000000000000000000012341234"]}],"id":73}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x1" // 1
}
```

***

#### eth_newBlockFilter

Crea un filtro en el nodo, para notificar cuando llega un nuevo bloque.
Para verificar si el estado ha cambiado, llame a [eth_getFilterChanges] (# eth_getfilterchanges).

##### Parámetros
Ninguno

##### Devoluciones

`CANTIDAD` - Un ID de filtro.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_newBlockFilter","params":[],"id":73}'

// Result
{
  "id":1,
  "jsonrpc":  "2.0",
  "result": "0x1" // 1
}
```

***

#### eth_newPendingTransactionFilter

Crea un filtro en el nodo, para notificar cuando llegan nuevas transacciones pendientes.
Para verificar si el estado ha cambiado, llame a [eth_getFilterChanges] (# eth_getfilterchanges).

##### Parámetros
Ninguno

##### Devoluciones

`QUANTITY` - Un ID de filtro.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_newPendingTransactionFilter","params":[],"id":73}'

// Result
{
  "id":1,
  "jsonrpc":  "2.0",
  "result": "0x1" // 1
}
```

***

#### eth_uninstallFilter

Desinstala un filtro con el id dado. Siempre debe llamarse cuando ya no se necesita reloj.
Además, los filtros agotan el tiempo de espera cuando no se solicitan con [eth_getFilterChanges] (# eth_getfilterchanges) durante un período de tiempo.


##### Parámetros

1. `QUANTITY` - El id del filtro.

```js
params: [
  "0xb" // 11
]
```

##### Devoluciones

`Boolean` -` true` si el filtro se desinstaló con éxito, de lo contrario, `false`.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_uninstallFilter","params":["0xb"],"id":73}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": true
}
```

***

#### eth_getFilterChanges

Polling method for a filter, which returns an array of logs which occurred since last poll.


##### Parameters

1. `QUANTITY` - the filter id.

```js
params: [
  "0x16" // 22
]
```

##### Devoluciones

`Array` - Array de objetos de registro, o un array vacío si nada ha cambiado desde la última encuesta.

- Para los filtros creados con `eth_newBlockFilter`, el retorno son hashes de bloque (` DATA`, 32 Bytes), p. Ej. `[" 0x3454645634534 ... "]`.
- Para los filtros creados con `eth_newPendingTransactionFilter` la devolución son hashes de transacción (`DATA`, 32 Bytes), por ejemplo. `[" 0x6345343454645 ... "]`.
- Para los filtros creados con los registros `eth_newFilter` son objetos con los siguientes parámetros:

  - `remove`:` TAG` - `true` cuando se eliminó el registro, debido a una reorganización de la cadena. `false` si es un registro válido.
  - `logIndex`:` QUANTITY` - entero de la posición del índice de registro en el bloque. `null` cuando su log pendiente.
  - `transactionIndex`:` QUANTITY` - se creó un entero del registro de posición del índice de transacciones. `null` cuando su log pendiente.
  - `transactionHash`:` DATA`, 32 Bytes - hash de las transacciones desde las que se creó este registro. `null` cuando su log pendiente.
  - `blockHash`:` DATA`, 32 Bytes - hash del bloque donde estaba este registro. `null` cuando está pendiente. `null` cuando su log pendiente.
  - `blockNumber`:` QUANTITY` - el número de bloque donde estaba este registro. `null` cuando está pendiente. `null` cuando su log pendiente.
  - `address`:` DATA`, 20 Bytes - dirección desde la cual se originó este registro.
  - `data`:` DATA` - contiene los argumentos no indexados del registro.
  - `topics`:` Array of DATA` - Array de 0 a 4 32 Bytes `DATA` de los argumentos de registro indexados. (En * solidez *: el primer tema es el * hash * de la firma del evento (por ejemplo, `Depósito (dirección, bytes32, uint256)`), excepto que declaró el evento con el especificador `anónimo`.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getFilterChanges","params":["0x16"],"id":73}'

// Result
{
  "id":1,
  "jsonrpc":"2.0",
  "result": [{
    "logIndex": "0x1", // 1
    "blockNumber":"0x1b4", // 436
    "blockHash": "0x8216c5785ac562ff41e2dcfdf5785ac562ff41e2dcfdf829c5a142f1fccd7d",
    "transactionHash":  "0xdf829c5a142f1fccd7d8216c5785ac562ff41e2dcfdf5785ac562ff41e2dcf",
    "transactionIndex": "0x0", // 0
    "address": "0x16c5785ac562ff41e2dcfdf829c5a142f1fccd7d",
    "data":"0x0000000000000000000000000000000000000000000000000000000000000000",
    "topics": ["0x59ebeb90bc63057b6515673c3ecf9438e5058bca0f92585014eced636878c9a5"]
    },{
      ...
    }]
}
```

***

#### eth_getFilterLogs

Devuelve una matriz de todos los registros que coinciden con el filtro con el ID dado.


##### Parámetros

1. `QUANTITY` - El id del filtro.

```js
params: [
  "0x16" // 22
]
```

##### Devoluciones

Consulte [eth_getFilterChanges] (# eth_getfilterchanges)

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getFilterLogs","params":["0x16"],"id":74}'
```

Resultado vea [eth_getFilterChanges] (# eth_getfilterchanges)

***

#### eth_getLogs

Devuelve una matriz de todos los registros que coinciden con un objeto de filtro determinado.

##### Parámetros

1. `Objeto` - Las opciones de filtro:
  - `fromBlock`:` QUANTITY | TAG` - (opcional, predeterminado: `" latest "`) Número de bloque entero, o `" latest "` para el último bloque extraído o `" pendiente "`, `" firstiest "` para Transacciones aún no minadas.
  - `toBlock`:` QUANTITY | TAG` - (opcional, predeterminado: `" latest "`) Número de bloque entero, o `" latest "` para el último bloque extraído o `" pendiente "`, `" firstiest "` para Transacciones aún no minadas.
  - `address`:` DATA | Array`, 20 Bytes - (opcional) Dirección de contrato o una lista de direcciones desde donde se deben originar los registros.
  - `topics`:` Array of DATA`, - (opcional) Array of 32 Bytes `DATA` topics. Los temas dependen del orden. Cada tema también puede ser una matriz de DATOS con "o" opciones.
  - `blockhash`:` DATA`, 32 bytes - (opcional) Con la adición de EIP-234 (pirl> = v1.8.13 o Parity> = v2.1.0), `blockHash` es una nueva opción de filtro que restringe los registros regresó al bloque único con el hash `blockHash` de 32 bytes. Usar `blockHash` es equivalente a` fromBlock` = `toBlock` = el número de bloque con hash` blockHash`. Si `blockHash` está presente en los criterios de filtro, entonces no se permiten` fromBlock` ni `toBlock`.

```js
params: [{
  "topics": ["0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b"]
}]
```

##### Devoluciones

Consulte [eth_getFilterChanges] (# eth_getfilterchanges)

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getLogs","params":[{"topics":["0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b"]}],"id":74}'
```

Resultado vea [eth_getFilterChanges] (# eth_getfilterchanges)

***

#### eth_getWork

Devuelve el hash del bloque actual, el seedHash y la condición de límite que se debe cumplir ("objetivo").

##### Parámetros
ninguna

##### Devoluciones

`Array` - Array con las siguientes propiedades:
   1. `DATA`, 32 Bytes - encabezado de bloque actual pow-hash
   2. `DATA`, 32 Bytes - el hash de semilla utilizado para el DAG.
   3. `DATA`, 32 Bytes - la condición de contorno (" objetivo "), 2 ^ 256 / dificultad.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getWork","params":[],"id":73}'

// Result
{
  "id":1,
  "jsonrpc":"2.0",
  "result": [
      "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
      "0x5EED00000000000000000000000000005EED0000000000000000000000000000",
      "0xd1ff1c01710000000000000000000000d1ff1c01710000000000000000000000"
    ]
}
```

***

#### eth_submitWork

Se utiliza para enviar una solución de prueba de trabajo.


##### Parámetros

1. `DATA`, 8 Bytes - El nonce encontrado (64 bits)
2. `DATA`, 32 bytes: el hash de poder del encabezado (256 bits)
3. 'DATA', 32 bytes - El compendio de la mezcla (256 bits)

```js
params: [
  "0x0000000000000001",
  "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
  "0xD1FE5700000000000000000000000000D1FE5700000000000000000000000000"
]
```

##### Devoluciones

`Boolean` - devuelve` true` si la solución proporcionada es válida, de lo contrario `false`.


##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0", "method":"eth_submitWork", "params":["0x0000000000000001", "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef", "0xD1GE5700000000000000000000000000D1GE5700000000000000000000000000"],"id":73}'

// Result
{
  "id":73,
  "jsonrpc":"2.0",
  "result": true
}
```

***

#### eth_submitHashrate

Usado para enviar hashrate minero.


##### Parámetros

1. `Hashrate`, una representación de cadena hexadecimal (32 bytes) de la tasa de hash
2. `ID`, String - Un ID aleatorio hexadecimal (32 bytes) que identifica al cliente

```js
params: [
  "0x0000000000000000000000000000000000000000000000000000000000500000",
  "0x59daa26581d0acd1fce254fb7e85952f4c09d0915afd33d3886cd914bc7d283c"
]
```

##### Devoluciones

`Boolean` - devuelve` true` si el envío se realizó correctamente y `false 'de lo contrario.


##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0", "method":"eth_submitHashrate", "params":["0x0000000000000000000000000000000000000000000000000000000000500000", "0x59daa26581d0acd1fce254fb7e85952f4c09d0915afd33d3886cd914bc7d283c"],"id":73}'

// Result
{
  "id":73,
  "jsonrpc":"2.0",
  "result": true
}
```

***

#### eth_getProof

Devuelve los valores de cuenta y almacenamiento de la cuenta especificada, incluida la prueba de Merkle.

##### getProof-Parameters

1. `DATA`, 20 bytes - dirección de la cuenta o contrato
2. `ARRAY`, 32 Bytes - matriz de claves de almacenamiento que se deben probar e incluir. Ver eth_getStorageAt
3. `QUANTITY | TAG` - número de bloque entero, o la cadena" más reciente "o" más antigua ", consulte el parámetro de bloque predeterminado


```
params: ["0x1234567890123456789012345678901234567890",["0x0000000000000000000000000000000000000000000000000000000000000000","0x0000000000000000000000000000000000000000000000000000000000000001"],"latest"]
```

##### getProof-Returns

Devoluciones
`Objeto` - Un objeto de cuenta:

`balance`:` QUANTITY` - el saldo de la cuenta. Ver eth_getBalance

`codeHash`:` DATA`, 32 Bytes - hash del código de la cuenta. Para una cuenta simple sin código, devolverá "0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470"

`nonce`:` QUANTITY`, - nonce de la cuenta. Ver eth_getTransactionCount

`storageHash`:` DATA`, 32 Bytes - SHA3 de StorageRoot. Todo el almacenamiento entregará un MerkleProof a partir de este rootHash.

`accountProof`:` ARRAY` - Array de MerkleTree-Nodes rlp-serialized, comenzando con stateRoot-Node, siguiendo la ruta de SHA3 (dirección) como clave.

`storageProof`:` ARRAY` - Arreglo de entradas de almacenamiento según lo solicitado. Cada entrada es un objeto con estas propiedades:

`clave`:` QUANTITY` - la clave de almacenamiento solicitada
`value`:` QUANTITY` - el valor de almacenamiento
`proof`:` ARRAY` - Array de MerkleTree-Nodes rlp-serialized, comenzando con el storageHash-Node, siguiendo la ruta del SHA3 (clave) como ruta.

##### getProof-Example
```
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getProof","params":["0x1234567890123456789012345678901234567890",["0x0000000000000000000000000000000000000000000000000000000000000000","0x0000000000000000000000000000000000000000000000000000000000000001"],"latest"],"id":1}' -H "Content-type:application/json" http://localhost:8545

// Result
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "address": "0x1234567890123456789012345678901234567890",
    "accountProof": [
      "0xf90211a090dcaf88c40c7bbc95a912cbdde67c175767b31173df9ee4b0d733bfdd511c43a0babe369f6b12092f49181ae04ca173fb68d1a5456f18d20fa32cba73954052bda0473ecf8a7e36a829e75039a3b055e51b8332cbf03324ab4af2066bbd6fbf0021a0bbda34753d7aa6c38e603f360244e8f59611921d9e1f128372fec0d586d4f9e0a04e44caecff45c9891f74f6a2156735886eedf6f1a733628ebc802ec79d844648a0a5f3f2f7542148c973977c8a1e154c4300fec92f755f7846f1b734d3ab1d90e7a0e823850f50bf72baae9d1733a36a444ab65d0a6faaba404f0583ce0ca4dad92da0f7a00cbe7d4b30b11faea3ae61b7f1f2b315b61d9f6bd68bfe587ad0eeceb721a07117ef9fc932f1a88e908eaead8565c19b5645dc9e5b1b6e841c5edbdfd71681a069eb2de283f32c11f859d7bcf93da23990d3e662935ed4d6b39ce3673ec84472a0203d26456312bbc4da5cd293b75b840fc5045e493d6f904d180823ec22bfed8ea09287b5c21f2254af4e64fca76acc5cd87399c7f1ede818db4326c98ce2dc2208a06fc2d754e304c48ce6a517753c62b1a9c1d5925b89707486d7fc08919e0a94eca07b1c54f15e299bd58bdfef9741538c7828b5d7d11a489f9c20d052b3471df475a051f9dd3739a927c89e357580a4c97b40234aa01ed3d5e0390dc982a7975880a0a089d613f26159af43616fd9455bb461f4869bfede26f2130835ed067a8b967bfb80",
      "0xf90211a0395d87a95873cd98c21cf1df9421af03f7247880a2554e20738eec2c7507a494a0bcf6546339a1e7e14eb8fb572a968d217d2a0d1f3bc4257b22ef5333e9e4433ca012ae12498af8b2752c99efce07f3feef8ec910493be749acd63822c3558e6671a0dbf51303afdc36fc0c2d68a9bb05dab4f4917e7531e4a37ab0a153472d1b86e2a0ae90b50f067d9a2244e3d975233c0a0558c39ee152969f6678790abf773a9621a01d65cd682cc1be7c5e38d8da5c942e0a73eeaef10f387340a40a106699d494c3a06163b53d956c55544390c13634ea9aa75309f4fd866f312586942daf0f60fb37a058a52c1e858b1382a8893eb9c1f111f266eb9e21e6137aff0dddea243a567000a037b4b100761e02de63ea5f1fcfcf43e81a372dafb4419d126342136d329b7a7ba032472415864b08f808ba4374092003c8d7c40a9f7f9fe9cc8291f62538e1cc14a074e238ff5ec96b810364515551344100138916594d6af966170ff326a092fab0a0d31ac4eef14a79845200a496662e92186ca8b55e29ed0f9f59dbc6b521b116fea090607784fe738458b63c1942bba7c0321ae77e18df4961b2bc66727ea996464ea078f757653c1b63f72aff3dcc3f2a2e4c8cb4a9d36d1117c742833c84e20de994a0f78407de07f4b4cb4f899dfb95eedeb4049aeb5fc1635d65cf2f2f4dfd25d1d7a0862037513ba9d45354dd3e36264aceb2b862ac79d2050f14c95657e43a51b85c80",
      "0xf90171a04ad705ea7bf04339fa36b124fa221379bd5a38ffe9a6112cb2d94be3a437b879a08e45b5f72e8149c01efcb71429841d6a8879d4bbe27335604a5bff8dfdf85dcea00313d9b2f7c03733d6549ea3b810e5262ed844ea12f70993d87d3e0f04e3979ea0b59e3cdd6750fa8b15164612a5cb6567cdfb386d4e0137fccee5f35ab55d0efda0fe6db56e42f2057a071c980a778d9a0b61038f269dd74a0e90155b3f40f14364a08538587f2378a0849f9608942cf481da4120c360f8391bbcc225d811823c6432a026eac94e755534e16f9552e73025d6d9c30d1d7682a4cb5bd7741ddabfd48c50a041557da9a74ca68da793e743e81e2029b2835e1cc16e9e25bd0c1e89d4ccad6980a041dda0a40a21ade3a20fcd1a4abb2a42b74e9a32b02424ff8db4ea708a5e0fb9a09aaf8326a51f613607a8685f57458329b41e938bb761131a5747e066b81a0a16808080a022e6cef138e16d2272ef58434ddf49260dc1de1f8ad6dfca3da5d2a92aaaadc58080",
      "0xf851808080a009833150c367df138f1538689984b8a84fc55692d3d41fe4d1e5720ff5483a6980808080808080808080a0a319c1c415b271afc0adcb664e67738d103ac168e0bc0b7bd2da7966165cb9518080"
    ],
    "balance": "0x0",
    "codeHash": "0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
    "nonce": "0x0",
    "storageHash": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
    "storageProof": [
      {
        "key": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "value": "0x0",
        "proof": []
      },
      {
        "key": "0x0000000000000000000000000000000000000000000000000000000000000001",
        "value": "0x0",
        "proof": []
      }
    ]
  }
}
```

***

#### db_putString

Almacena una cadena en la base de datos local.

** Nota ** esta función está obsoleta y se eliminará en el futuro.

##### Parámetros

1. `String` - Nombre de la base de datos.
2. `String` - Nombre de clave.
3. 'String' - Cadena para almacenar.

```js
params: [
  "testDB",
  "myKey",
  "myString"
]
```

##### Devoluciones

`Boolean` - devuelve` true` si el valor fue almacenado, de lo contrario `false`.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"db_putString","params":["testDB","myKey","myString"],"id":73}'

// Result
{
  "id":1,
  "jsonrpc":"2.0",
  "result": true
}
```

***

#### db_getString

Devuelve la cadena de la base de datos local.

** Nota ** esta función está obsoleta y se eliminará en el futuro.

##### Parámetros

1. `String` - Nombre de la base de datos.
2. `String` - Nombre de clave.

```js
params: [
  "testDB",
  "myKey",
]
```

##### Devoluciones

`String` - La cadena previamente almacenada.


##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"db_getString","params":["testDB","myKey"],"id":73}'

// Result
{
  "id":1,
  "jsonrpc":"2.0",
  "result": "myString"
}
```

***

#### db_putHex

Almacena datos binarios en la base de datos local.

** Nota ** esta función está obsoleta y se eliminará en el futuro.


##### Parámetros

1. `String` - Nombre de la base de datos.
2. `String` - Nombre de clave.
3. 'DATA' - Los datos a almacenar.

```js
params: [
  "testDB",
  "myKey",
  "0x68656c6c6f20776f726c64"
]
```

##### Devoluciones

`Boolean` - devuelve` true` si el valor fue almacenado, de lo contrario `false`.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"db_putHex","params":["testDB","myKey","0x68656c6c6f20776f726c64"],"id":73}'

// Result
{
  "id":1,
  "jsonrpc":"2.0",
  "result": true
}
```

***

#### db_getHex

Devuelve datos binarios de la base de datos local.

** Nota ** esta función está obsoleta y se eliminará en el futuro.


##### Parámetros

1. `String` - Nombre de la base de datos.
2. `String` - Nombre de clave.

```js
params: [
  "testDB",
  "myKey",
]
```

##### Devoluciones

`DATA` - Los datos previamente almacenados.


##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"db_getHex","params":["testDB","myKey"],"id":73}'

// Result
{
  "id":1,
  "jsonrpc":"2.0",
  "result": "0x68656c6c6f20776f726c64"
}
```

***

#### shh_version

Devuelve la versión actual del protocolo de susurro.

##### Parámetros
ninguno

##### Devoluciones

`String` - La versión actual del protocolo de susurro

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"shh_version","params":[],"id":67}'

// Result
{
  "id":67,
  "jsonrpc": "2.0",
  "result": "2"
}
```

***

#### shh_post

Envía un mensaje de susurro.

##### Parámetros

1. `Object` - El objeto de la publicación de susurro:
   - `from`:` DATA`, 60 Bytes - (opcional) La identidad del remitente.
   - `to`:` DATA`, 60 Bytes - (opcional) La identidad del receptor. Cuando el susurro presente cifrará el mensaje de modo que solo el receptor pueda descifrarlo.
   - `topics`:` Array of DATA` - Array of `DATA`, para que el receptor identifique los mensajes.
   - `payload`:` DATA` - La carga útil del mensaje.
   - `priority`:` QUANTITY` - El entero de la prioridad en un rango de ... (?).
   - `ttl`:` QUANTITY` - entero del tiempo para vivir en segundos.

```js
params: [{
  from: "0x04f96a5e25610293e42a73908e93ccc8c4d4dc0edcfa9fa872f50cb214e08ebf61a03e245533f97284d442460f2998cd41858798ddfd4d661997d3940272b717b1",
  to: "0x3e245533f97284d442460f2998cd41858798ddf04f96a5e25610293e42a73908e93ccc8c4d4dc0edcfa9fa872f50cb214e08ebf61a0d4d661997d3940272b717b1",
  topics: ["0x776869737065722d636861742d636c69656e74", "0x4d5a695276454c39425154466b61693532"],
  payload: "0x7b2274797065223a226d6",
  priority: "0x64",
  ttl: "0x64",
}]
```

##### Devoluciones

`Boolean` - devuelve` true` si el mensaje fue enviado, de lo contrario, `false`.


##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"shh_post","params":[{"from":"0xc931d93e97ab07fe42d923478ba2465f2..","topics": ["0x68656c6c6f20776f726c64"],"payload":"0x68656c6c6f20776f726c64","ttl":0x64,"priority":0x64}],"id":73}'

// Result
{
  "id":1,
  "jsonrpc":"2.0",
  "result": true
}
```

***

#### shh_newIdentity

Crea nueva identidad de susurro en el cliente.

##### Parámetros
ninguna

##### Devoluciones

`DATA`, 60 Bytes - la dirección de la nueva identidad.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"shh_newIdentity","params":[],"id":73}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xc931d93e97ab07fe42d923478ba2465f283f440fd6cabea4dd7a2c807108f651b7135d1d6ca9007d5b68aa497e4619ac10aa3b27726e1863c1fd9b570d99bbaf"
}
```

***

#### shh_hasIdentity

Comprueba si el cliente mantiene las claves privadas para una identidad determinada.


##### Parámetros

1. `DATA`, 60 Bytes - La dirección de identidad a verificar.

```js
params: [
  "0x04f96a5e25610293e42a73908e93ccc8c4d4dc0edcfa9fa872f50cb214e08ebf61a03e245533f97284d442460f2998cd41858798ddfd4d661997d3940272b717b1"
]
```

##### Devoluciones

`Boolean` - devuelve` true` si el cliente tiene la clave privada para esa identidad, de lo contrario `false`.


##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"shh_hasIdentity","params":["0x04f96a5e25610293e42a73908e93ccc8c4d4dc0edcfa9fa872f50cb214e08ebf61a03e245533f97284d442460f2998cd41858798ddfd4d661997d3940272b717b1"],"id":73}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": true
}
```

***

#### shh_newGroup

Crea un nuevo grupo.

##### Parámetros
ninguna

##### Devoluciones

'DATA', 60 bytes - la dirección del nuevo grupo.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"shh_newGroup","params":[],"id":73}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xc65f283f440fd6cabea4dd7a2c807108f651b7135d1d6ca90931d93e97ab07fe42d923478ba2407d5b68aa497e4619ac10aa3b27726e1863c1fd9b570d99bbaf"
}
```

***

#### shh_addToGroup

Añade una identidad de susurro al grupo.

##### Parámetros

1. `DATA`, 60 Bytes - La dirección de identidad para agregar a un grupo.

```js
params: [
  "0x04f96a5e25610293e42a73908e93ccc8c4d4dc0edcfa9fa872f50cb214e08ebf61a03e245533f97284d442460f2998cd41858798ddfd4d661997d3940272b717b1"
]
```

##### Devoluciones

`Boolean` - devuelve` true` si la identidad se agregó exitosamente al grupo, de lo contrario `false`.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"shh_addToGroup","params":["0x04f96a5e25610293e42a73908e93ccc8c4d4dc0edcfa9fa872f50cb214e08ebf61a03e245533f97284d442460f2998cd41858798ddfd4d661997d3940272b717b1"],"id":73}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": true
}
```

***

#### shh_newFilter

Crea un filtro para notificar, cuando el cliente recibe un mensaje susurrante que coincide con las opciones de filtro.


##### Parámetros

1. `Objeto` - Las opciones de filtro:
   - `to`:` DATA`, 60 Bytes - (opcional) Identidad del receptor. * Cuando esté presente, intentará descifrar cualquier mensaje entrante si el cliente tiene la clave privada de esta identidad. *
   - `topics`:` Array of DATA` - Array of `DATA` que los temas del mensaje entrante deben coincidir. Puedes usar las siguientes combinaciones:
     - `[A, B] = A && B`
     - `[A, [B, C]] = A && (B || C)`
     - `[null, A, B] = CUALQUIER COSA && A && B`` null` funciona como un comodín

```js
params: [{
   "topics": ['0x12341234bf4b564f'],
   "to": "0x04f96a5e25610293e42a73908e93ccc8c4d4dc0edcfa9fa872f50cb214e08ebf61a03e245533f97284d442460f2998cd41858798ddfd4d661997d3940272b717b1"
}]
```

##### Devoluciones

`QUANTITY` - El filtro de nueva creación.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"shh_newFilter","params":[{"topics": ['0x12341234bf4b564f'],"to": "0x2341234bf4b2341234bf4b564f..."}],"id":73}'

// Result
{
  "id":1,
  "jsonrpc":"2.0",
  "result": "0x7" // 7
}
```

***

#### shh_uninstallFilter

Desinstala un filtro con el id dado. Siempre debe llamarse cuando ya no se necesita reloj.
Los filtros adicionales se agotan cuando no se solicitan con [shh_getFilterChanges] (# shh_getfilterchanges) durante un período de tiempo.


##### Parámetros

1. `QUANTITY` - El id del filtro.

```js
params: [
  "0x7" // 7
]
```

##### Devoluciones

`Boolean` -` true` si el filtro se desinstaló con éxito, de lo contrario, `false`.

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"shh_uninstallFilter","params":["0x7"],"id":73}'

// Result
{
  "id":1,
  "jsonrpc":"2.0",
  "result": true
}
```

***

#### shh_getFilterChanges

Método de sondeo para filtros de susurro. Devuelve nuevos mensajes desde la última llamada de este método.

** Nota ** al llamar al método [shh_getMessages] (# shh_getmessages), se restablecerá el búfer para este método, para que no reciba mensajes duplicados.


##### Parámetros

1. `QUANTITY` - El id del filtro.

```js
params: [
  "0x7" // 7
]
```

##### Devoluciones

`Array` - Arreglo de mensajes recibidos desde la última encuesta:

   - `hash`:` DATA`, 32 Bytes (?) - El hash del mensaje.
   - `from`:` DATA`, 60 Bytes - El remitente del mensaje, si se especificó un remitente.
   - `to`:` DATA`, 60 Bytes - El receptor del mensaje, si se especificó un receptor.
   - `expiry`:` QUANTITY` - Entero del tiempo en segundos cuando este mensaje debe expirar (?).
   - `ttl`:` QUANTITY` - Número entero del tiempo que el mensaje debe flotar en el sistema en segundos (?).
   - `send`:` QUANTITY` - Entero de la marca de tiempo de Unix cuando se envió el mensaje.
   - `topics`:` Array of DATA` - Array of `DATA` que contiene el mensaje.
   - `payload`:` DATA` - La carga útil del mensaje.
   - `workProved`:` QUANTITY` - El número entero del trabajo requerido por este mensaje antes de ser enviado (?).

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"shh_getFilterChanges","params":["0x7"],"id":73}'

// Result
{
  "id":1,
  "jsonrpc":"2.0",
  "result": [{
    "hash": "0x33eb2da77bf3527e28f8bf493650b1879b08c4f2a362beae4ba2f71bafcd91f9",
    "from": "0x3ec052fc33..",
    "to": "0x87gdf76g8d7fgdfg...",
    "expiry": "0x54caa50a", // 1422566666
    "sent": "0x54ca9ea2", // 1422565026
    "ttl": "0x64", // 100
    "topics": ["0x6578616d"],
    "payload": "0x7b2274797065223a226d657373616765222c2263686...",
    "workProved": "0x0"
    }]
}
```

***

#### shh_getMessages

Recibe todos los mensajes que coinciden con un filtro. A diferencia de `shh_getFilterChanges`, esto devuelve todos los mensajes.

##### Parámetros

1. `QUANTITY` - El id del filtro.

```js
params: [
  "0x7" // 7
]
```

##### Devoluciones

Consulte [shh_getFilterChanges] (# shh_getfilterchanges)

##### Ejemplo
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"shh_getMessages","params":["0x7"],"id":73}'
```

Result see [shh_getFilterChanges](#shh_getfilterchanges)



---
Autor(s):  

@Fawkes

Contribuyente(s):  

@Dptelecom
