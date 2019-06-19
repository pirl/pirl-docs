---
title: APIs Administración
weight: 4
pre: "<b>4. </b>"
chapter: true
---
Además de la interfaz oficial de las API de DApp, ir a pirl
tiene soporte para APIs de gestión adicionales. Similar a las API de DApp, también se proporcionan utilizando
[JSON-RPC] (http://www.jsonrpc.org/specification) y siga exactamente las mismas convenciones. Viene pirl
con un cliente de consola que admite todas las API adicionales que se describen aquí.

## Habilitando las API de gestión

Para ofrecer estas API a través de los puntos finales de Pirl RPC, especifíquelas con la interfaz `- $ {interface}
argumento de la línea de comando (donde `$ {interface}` puede ser `rpc` para el punto final HTTP,` ws` para WebSocket
punto final y `ipc` para el punto final Unix (Unix) o canalización con nombre (Windows)).

Por ejemplo: `Pirl --ipcapi admin, eth, minero --rpcapi eth, web3 --rpc`

* Habilita las API de administrador, DApp oficial y minero a través de la interfaz IPC
* Habilita las API oficiales de DApp y web3 a través de la interfaz HTTP

La interfaz HTTP RPC debe habilitarse explícitamente mediante el indicador `--rpc`.

Tenga en cuenta que ofrecer una API a través de las interfaces HTTP (`rpc`) o WebSocket (` ws`) dará a todos
acceso a las API que pueden acceder a esta interfaz (DApps, pestañas del navegador, etc.). Ten cuidado que APIs
usted habilita De forma predeterminada, Pirl habilita todas las API a través de la interfaz IPC (`ipc`) y solo el` db`, `eth`,
Las API `net` y` web3` sobre las interfaces HTTP y WebSocket.

Para determinar qué API proporciona una interfaz, se puede invocar el método JSON-RPC `modules`. por
Ejemplo sobre una interfaz `ipc` en sistemas unix:

```
echo '{"jsonrpc":"2.0","method":"rpc_modules","params":[],"id":1}' | nc -U $datadir/Pirl.ipc
```

Dará todos los módulos habilitados incluyendo el número de versión:

```
{  
   "id":1,
   "jsonrpc":"2.0",
   "result":{  
      "admin":"1.0",
      "db":"1.0",
      "debug":"1.0",
      "eth":"1.0",
      "miner":"1.0",
      "net":"1.0",
      "personal":"1.0",
      "shh":"1.0",
      "txpool":"1.0",
      "web3":"1.0"
   }
}
```

## Consumiendo las API de administración

Estas API adicionales siguen las mismas convenciones que las API oficiales de DApp. Web3 puede ser
utilizadas para consumir estas API adicionales.


** 2 ejemplos: **

* Console: `miner.start()`

* IPC: `echo '{"jsonrpc":"2.0","method":"miner_start","params":[],"id":1}' | nc -U $datadir/Pirl.ipc`

* HTTP: `curl -X POST --data '{"jsonrpc":"2.0","method":"miner_start","params":[],"id":74}' localhost:8545`

Con el número de HILOS como argumentos:

* Console: `miner.start(4)`

* IPC: `echo '{"jsonrpc":"2.0","method":"miner_start","params":[4],"id":1}' | nc -U $datadir/Pirl.ipc`

* HTTP: `curl -X POST --data '{"jsonrpc":"2.0","method":"miner_start","params":[4],"id":74}' localhost:8545`

## Lista de APIs de gestión

Además de los espacios de nombres API de DApp oficialmente expuestos (`eth`,` shh`, `web3`), Pirl proporciona lo siguiente
espacios de nombres de API de gestión adicionales:

* `admin`: Gestión de nodos Pirl
* `debug`: depuración del nodo Pirl
* `minero`: Minero y DAG
* `personal`: Gestión de cuentas
* `txpool`: inspección del grupo de transacciones

| [admin](#admin)              | [debug](#debug)                                   | [miner](#miner)                     | [personal](#personal)                    | [txpool](#txpool)          |
| :--------------------------- | :-----------------------------------------------  | :---------------------------------- | :--------------------------------------- | :------------------------- |
| [addPeer](#admin_addpeer)    | [backtraceAt](#debug_backtraceAt)                 | [setExtra](#miner_setextra)         | [ecRecover](#personal_ecrecover)         | [content](#txpool_content) |
| [datadir](#datadir)          | [blockProfile](#debug_blockProfile)               | [setGasPrice](#miner_setgasprice)   | [importRawKey](#personal_importrawkey)   | [inspect](#txpool_inspect) |
| [nodeInfo](#admin_nodeinfo)  | [cpuProfile](#debug_cpuProfile)                   | [start](#miner_start)               | [listAccounts](#personal_listaccounts)   | [status](#txpool_status)   |
| [peers](#admin_peers)        | [dumpBlock](#debug_dumpblock)                     | [stop](#miner_stop)                 | [lockAccount](#personal_lockaccount)     |                            |
| [setSolc](#admin_setcolc)    | [gcStats](#debug_gcStats)                         | [Gethashrate](#miner_gethashrate)   | [newAccount](#personal_newaccount)       |                            |
| [startRPC](#admin_startrpc)  | [getBlockRlp](#debug_getblockrlp)                 | [setEtherbase](#miner_setetherbase) | [unlockAccount](#personal_unlockaccount) |                            |
| [startWS](#admin_startws)    | [goTrace](#debug_goTrace)                         |                                     | [sendTransaction](#personal_sendtransaction) |                        |
| [stopRPC](#admin_stoprpc)    | [memStats](#debug_memStats)                       |                                     | [sign](#personal_sign)                   |                            |
| [stopWS](#admin_stopws)      | [seedHash](#debug_seedhash)[sign](#personal_sign)|                                      |                                          |                            |
|                              | [setBlockProfileRate](#debug_setBlockProfileRate) |                                     |                                          |                            |
|                              | [setHead](#debug_sethead)                         |                                     |                                          |                            |
|                              | [stacks](#debug_stacks)                           |                                     |                                          |                            |
|                              | [startCPUProfile](#debug_startCPUProfile)         |                                     |                                          |                            |
|                              | [startGoTrace](#debug_startGoTrace)               |                                     |                                          |                            |
|                              | [stopCPUProfile](#debug_stopCPUProfile)           |                                     |                                          |                            |
|                              | [stopGoTrace](#debug_stopGoTrace)                 |                                     |                                          |                            |
|                              | [traceBlock](#debug_traceblock)                   |                                     |                                          |                            |
|                              | [traceBlockByNumber](#debug_blockbynumber)        |                                     |                                          |                            |
|                              | [traceBlockByHash](#debug_blockbyhash)            |                                     |                                          |                            |
|                              | [traceBlockFromFile](#debug_traceblockfromfile)   |                                     |                                          |                            |
|                              | [traceTransaction](#debug_tracetransaction)       |                                     |                                          |                            |
|                              | [verbosity](#debug_verbosity)                     |                                     |                                          |                            |
|                              | [vmodule](#debug_vmodule)                         |                                     |                                          |                            |
|                              | [writeBlockProfile](#debug_writeBlockProfile)     |                                     |                                          |                            |
|                              | [writeMemProfile](#debug_writeMemProfile)         |                                     |                                          |                            |

## Admin

La API `admin` le da acceso a varios métodos RPC no estándar, que le permitirán tener
un control detallado sobre su instancia de Pirl, que incluye, entre otros, la red de igual y el RPC
gestión de puntos finales.

### admin_addPeer

El método administrativo `addPeer` solicita agregar un nuevo nodo remoto a la lista de estática rastreada
nodos El nodo intentará mantener la conectividad con estos nodos en todo momento, reconectando cada
De vez en cuando si la conexión remota se cae.

El método acepta un solo argumento, el 'enode'
URL del interlocutor remoto para iniciar el seguimiento y devuelve un `BOOL` que indica si el interlocutor fue aceptado
Para el seguimiento o se produjo algún error.

| Client  | Method invocation                              |
|:-------:|------------------------------------------------|
| Go      | `admin.AddPeer(url string) (bool, error)`      |
| Console | `admin.addPeer(url)`                           |
| RPC     | `{"method": "admin_addPeer", "params": [url]}` |

#### Ejemplo

```javascript
> admin.addPeer("enode://a979fb575495b8d6db44f750317d0f4622bf4c2aa3365d6af7c284339968eef29b69ad0dce72a4d8db5ebb4968de0e3bec910127f134779fbcb0cb6d3331163c@52.16.188.185:30303")
true
```

### admin_datadir

La propiedad administrativa `datadir` puede consultarse para la ruta absoluta del nodo Pirl en ejecución
Actualmente se utiliza para almacenar todas sus bases de datos.

| Client  | Method invocation                 |
|:-------:|-----------------------------------|
| Go      | `admin.Datadir() (string, error`) |
| Console | `admin.datadir`                   |
| RPC     | `{"method": "admin_datadir"}`     |

#### Ejemplo

```javascript
> admin.datadir
"/home/karalabe/.pirl"
```

### admin_nodeInfo

La propiedad administrativa `nodeInfo` puede consultarse para obtener toda la información conocida sobre la ejecución
Nodo Pirl en la granularidad de la red. Estos incluyen información general sobre el nodo como un
participante del protocolo de superposición P2P, así como información especializada agregada por cada uno de los protocolos de aplicación en ejecución
(e.g. `eth`, `les`, `shh`, `bzz`).

| Client  | Method invocation                         |
|:-------:|-------------------------------------------|
| Go      | `admin.NodeInfo() (*p2p.NodeInfo, error`) |
| Console | `admin.nodeInfo`                          |
| RPC     | `{"method": "admin_nodeInfo"}`            |

#### Ejemplo

```javascript
> admin.nodeInfo
{
  enode: "enode://44826a5d6a55f88a18298bca4773fca5749cdc3a5c9f308aa7d810e9b31123f3e7c5fba0b1d70aac5308426f47df2a128a6747040a3815cc7dd7167d03be320d@[::]:30303",
  id: "44826a5d6a55f88a18298bca4773fca5749cdc3a5c9f308aa7d810e9b31123f3e7c5fba0b1d70aac5308426f47df2a128a6747040a3815cc7dd7167d03be320d",
  ip: "::",
  listenAddr: "[::]:30303",
  name: "Pirl/v1.5.0-unstable/linux/go1.6",
  ports: {
    discovery: 30303,
    listener: 30303
  },
  protocols: {
    eth: {
      difficulty: 17334254859343145000,
      genesis: "0xd4e56740f876aef8c010b86a40d5f56745a118d0906a34e69aec8c0db1cb8fa3",
      head: "0xb83f73fbe6220c111136aefd27b160bf4a34085c65ba89f24246b3162257c36a",
      network: 1
    }
  }
}
```

### admin_peers

La propiedad administrativa `peers` puede ser consultada para toda la información conocida sobre los conectados
Nodos remotos en la granularidad de la red. Estos incluyen información general sobre los nodos mismos
como participantes del protocolo de superposición P2P, así como información especializada agregada por cada una de las aplicaciones en ejecución
protocolos(e.g. `eth`, `les`, `shh`, `bzz`).

| Client  | Method invocation                        |
|:-------:|------------------------------------------|
| Go      | `admin.Peers() ([]*p2p.PeerInfo, error`) |
| Console | `admin.peers`                            |
| RPC     | `{"method": "admin_peers"}`              |

#### Ejemplo

```javascript
> admin.peers
[{
    caps: ["eth/61", "eth/62", "eth/63"],
    id: "08a6b39263470c78d3e4f58e3c997cd2e7af623afce64656cfc56480babcea7a9138f3d09d7b9879344c2d2e457679e3655d4b56eaff5fd4fd7f147bdb045124",
    name: "Pirl/v1.5.0-unstable/linux/go1.5.1",
    network: {
      localAddress: "192.168.0.104:51068",
      remoteAddress: "71.62.31.72:30303"
    },
    protocols: {
      eth: {
        difficulty: 17334052235346465000,
        head: "5794b768dae6c6ee5366e6ca7662bdff2882576e09609bf778633e470e0e7852",
        version: 63
      }
    }
}, /* ... */ {
    caps: ["eth/61", "eth/62", "eth/63"],
    id: "fcad9f6d3faf89a0908a11ddae9d4be3a1039108263b06c96171eb3b0f3ba85a7095a03bb65198c35a04829032d198759edfca9b63a8b69dc47a205d94fce7cc",
    name: "Pirl/v1.3.5-506c9277/linux/go1.4.2",
    network: {
      localAddress: "192.168.0.104:55968",
      remoteAddress: "121.196.232.205:30303"
    },
    protocols: {
      eth: {
        difficulty: 17335165914080772000,
        head: "5794b768dae6c6ee5366e6ca7662bdff2882576e09609bf778633e470e0e7852",
        version: 63
      }
    }
}]
```

### admin_setSolc

El método administrativo `setSolc` establece la ruta del compilador de Solidity que usará el nodo cuando
invocando el método RPC `eth_compileSolidity`. La ruta del compilador de Solidity por defecto es `/ usr / bin / solc`
si no se configura, solo necesita cambiarlo para usar una ubicación de compilador no estándar.

El método acepta una ruta absoluta al compilador de Solidity para usar (especificando una ruta relativa
dependería de la actual (para el usuario desconocido - directorio de trabajo de Pirl), y devuelve el
cadena de versión reportada por `solc --version`.

| Client  | Method invocation                               |
|:-------:|-------------------------------------------------|
| Go      | `admin.SetSolc(path string) (string, error`)    |
| Console | `admin.setSolc(path)`                           |
| RPC     | `{"method": "admin_setSolc", "params": [path]}` |

#### Ejemplo

```javascript
> admin.setSolc("/usr/bin/solc")
"solc, the solidity compiler commandline interface\nVersion: 0.3.2-0/Release-Linux/g++/Interpreter\n\npath: /usr/bin/solc"
```

### admin_startRPC

El método administrativo `startRPC` inicia un [JSON RPC] basado en HTTP (http://www.jsonrpc.org/specification)
Servidor web API para manejar las solicitudes de los clientes. Todos los parámetros son opcionales:

* `host`: interfaz de red para abrir el socket de escucha (predeterminado en` "localhost" `)
* `port`: puerto de red para abrir el socket de escucha (predeterminado en` 8545`)
* `cors`: [recurso compartido de origen cruzado] (https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) encabezado para usar (predeterminado en` "" ``)
* `apis`: módulos API que se ofrecen a través de esta interfaz (por defecto es` "eth, net, web3" `)

El método devuelve una bandera booleana que especifica si el agente de escucha RPC de HTTP se abrió o no. Tenga en cuenta que solo un punto final de HTTP puede estar activo en cualquier momento.

| Client  | Method invocation                                                                             |
|:-------:|-----------------------------------------------------------------------------------------------|
| Go      | `admin.StartRPC(host *string, port *rpc.HexNumber, cors *string, apis *string) (bool, error)` |
| Console | `admin.startRPC(host, port, cors, apis)`                                                      |
| RPC     | `{"method": "admin_startRPC", "params": [host, port, cors, apis]}`                            |
'*
#### Ejemplo

```javascript
> admin.startRPC("127.0.0.1", 8545)
true
```

### admin_startWS

El método administrativo `startWS` inicia un WebSocket basado en [JSON RPC] (http://www.jsonrpc.org/specification)
Servidor web API para manejar las solicitudes de los clientes. Todos los parámetros son opcionales:

* `host`: interfaz de red para abrir el socket de escucha (predeterminado en` "localhost" `)
* `port`: puerto de red para abrir el socket de escucha (predeterminado en` 8546`)
* `cors`: [recurso compartido de origen cruzado] (https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) encabezado para usar (predeterminado en` "" ``)
* `apis`: módulos API que se ofrecen a través de esta interfaz (por defecto es` "eth, net, web3" `)

El método devuelve una bandera booleana que especifica si el escucha de WebSocket RPC se abrió o no. Tenga en cuenta que solo se permite que un punto final de WebSocket esté activo en cualquier momento.

| Client  | Method invocation                                                                             |
|:-------:|-----------------------------------------------------------------------------------------------|
| Go      | `admin.StartWS(host *string, port *rpc.HexNumber, cors *string, apis *string) (bool, error)` |
| Console | `admin.startWS(host, port, cors, apis)`                                                      |
| RPC     | `{"method": "admin_startWS", "params": [host, port, cors, apis]}`                            |
'*
#### Ejemplo

```javascript
> admin.startWS("127.0.0.1", 8546)
true
```

### admin_stopRPC

El método administrativo `stopRPC` cierra el punto final HTTP RPC actualmente abierto. Como el nodo solo puede tener un único punto final HTTP en ejecución, este método no toma parámetros, devolviendo un valor booleano si el punto final fue cerrado o no.

| Client  | Method invocation               |
|:-------:|---------------------------------|
| Go      | `admin.StopRPC() (bool, error`) |
| Console | `admin.stopRPC()`               |
| RPC     | `{"method": "admin_stopRPC"`    |

#### Ejemplo

```javascript
> admin.stopRPC()
true
```

### admin_stopWS

El método administrativo `stopWS` cierra el punto final de WebSocket RPC actualmente abierto. Como el nodo solo puede tener un único punto final WebSocket en ejecución, este método no toma parámetros, devolviendo un valor booleano si el punto final se cerró o no.

| Client  | Method invocation              |
|:-------:|--------------------------------|
| Go      | `admin.StopWS() (bool, error`) |
| Console | `admin.stopWS()`               |
| RPC     | `{"method": "admin_stopWS"`    |

#### Ejemplo

```javascript
> admin.stopWS()
true
```

## depuración

La API `debug` le da acceso a varios métodos RPC no estándar, que le permitirán inspeccionar,
depurar y establecer ciertos indicadores de depuración durante el tiempo de ejecución.


### debug_backtraceAt

Establece la ubicación de seguimiento de registro. Cuando una ubicación de retroceso
se establece y se emite un mensaje de registro en esa ubicación, la pila
del goroutine que ejecuta la declaración de registro se imprimirá a stderr.

La ubicación se especifica como `<filename>: <line>`.

| Client  | Method invocation                                     |
|:-------:|-------------------------------------------------------|
| Console | `debug.backtraceAt(string)`                           |
| RPC     | `{"method": "debug_backtraceAt", "params": [string]}` |

Ejemplo:

```javascript
> debug.backtraceAt("server.go:443")
```

### debug_blockProfile

Activa el perfil de bloque para la duración dada y escribe
perfil de datos en el disco. Utiliza una tasa de perfil de 1 para la mayoría
información precisa. Si se desea una tasa diferente, ajuste
la tasa y escribir el perfil manualmente utilizando
`debug_writeBlockProfile`.

| Client  | Method invocation                                              |
|:-------:|----------------------------------------------------------------|
| Console | `debug.blockProfile(file, seconds)`                            |
| RPC     | `{"method": "debug_blockProfile", "params": [string, number]}` |

###debug_cpuPerfil

Activa el perfil de CPU para la duración dada y escribe
perfil de datos en el disco.

| Client  | Method invocation                                            |
|:-------:|--------------------------------------------------------------|
| Console | `debug.cpuProfile(file, seconds)`                            |
| RPC     | `{"method": "debug_cpuProfile", "params": [string, number]}` |

### debug_dumpBlock

Recupera el estado que corresponde al número de bloque y devuelve una lista de cuentas (incluida
almacenamiento y codigo).

| Client  | Method invocation                                     |
|:-------:|-------------------------------------------------------|
| Go      | `debug.DumpBlock(number uint64) (state.World, error)` |
| Console | `debug.traceBlockByHash(number, [options])`           |
| RPC     | `{"method": "debug_dumpBlock", "params": [number]}`   |

#### Ejemplo

```javascript
> debug.dumpBlock(10)
{
    fff7ac99c8e4feb60c9750054bdc14ce1857f181: {
      balance: "49358640978154672",
      code: "",
      codeHash: "c5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
      nonce: 2,
      root: "56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
      storage: {}
    },
    fffbca3a38c3c5fcb3adbb8e63c04c3e629aafce: {
      balance: "3460945928",
      code: "",
      codeHash: "c5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
      nonce: 657,
      root: "56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
      storage: {}
    }
  },
  root: "19f4ed94e188dd9c7eb04226bd240fa6b449401a6c656d6d2816a87ccaf206f1"
}
```

### debug_gcStats

Devuelve las estadísticas de GC.

Consulte https://golang.org/pkg/runtime/debug/#GCStats para obtener información sobre
Los campos del objeto devuelto.

| Client  | Method invocation                                 |
|:-------:|---------------------------------------------------|
| Console | `debug.gcStats()`                                 |
| RPC     | `{"method": "debug_gcStats", "params": []}`       |

### debug_getBlockRlp

Recupera y devuelve el bloque codificado RLP por número.

| Client  | Method invocation                                     |
|:-------:|-------------------------------------------------------|
| Go      | `debug.GetBlockRlp(number uint64) (string, error)`    |
| Console | `debug.getBlockRlp(number, [options])`                |
| RPC     | `{"method": "debug_getBlockRlp", "params": [number]}` |



### debug_goTrace

Activa el seguimiento en tiempo de ejecución de Go para la duración dada y escribe
rastrear los datos al disco.

| Client  | Method invocation                                         |
|:-------:|-----------------------------------------------------------|
| Console | `debug.goTrace(file, seconds)`                            |
| RPC     | `{"method": "debug_goTrace", "params": [string, number]}` |

### debug_memStats

Devuelve estadísticas detalladas de la memoria en tiempo de ejecución.

Consulte https://golang.org/pkg/runtime/#MemStats para obtener información sobre
Los campos del objeto devuelto.

| Client  | Method invocation                                 |
|:-------:|---------------------------------------------------|
| Console | `debug.memStats()`                                |
| RPC     | `{"method": "debug_memStats", "params": []}`      |

### debug_seedHash

Obtiene y recupera el hash de semilla del bloque por número

| Client  | Method invocation                                  |
|:-------:|----------------------------------------------------|
| Go      | `debug.SeedHash(number uint64) (string, error)`    |
| Console | `debug.seedHash(number, [options])`                |
| RPC     | `{"method": "debug_seedHash", "params": [number]}` |

### debug_setHead

Establece la cabecera actual de la cadena local por número de bloque. **Nota**, esto es un
Acción destructiva y puede dañar gravemente tu cadena. Usar con precaución *extrema*.

| Client  | Method invocation                                 |
|:-------:|---------------------------------------------------|
| Go      | `debug.SetHead(number uint64)`                    |
| Console | `debug.setHead(number)`                           |
| RPC     | `{"method": "debug_setHead", "params": [number]}` |



### debug_setBlockProfileRate

Establece la velocidad (en muestras / seg) del perfil de bloque goroutine
recopilación de datos. Una tasa distinta de cero permite el perfilado de bloques,
configurándolo a cero detiene el perfil. Datos de perfil recogidos
se puede escribir usando `debug_writeBlockProfile`.

| Client  | Method invocation                                             |
|:-------:|---------------------------------------------------------------|
| Console | `debug.setBlockProfileRate(rate)`                             |
| RPC     | `{"method": "debug_setBlockProfileRate", "params": [number]}` |

### debug_stacks

Devuelve una representación impresa de las pilas de todos los goroutines.
Tenga en cuenta que la envoltura web3 para este método se encarga de la impresión.
y no devuelve la cadena.

| Client  | Method invocation                                 |
|:-------:|---------------------------------------------------|
| Console | `debug.stacks()`                                  |
| RPC     | `{"method": "debug_stacks", "params": []}`        |

###debug_startCPUProfile

Activa el perfil de la CPU de forma indefinida, escribiendo en el archivo dado.

| Client  | Method invocation                                         |
|:-------:|-----------------------------------------------------------|
| Console | `debug.startCPUProfile(file)`                             |
| RPC     | `{"method": "debug_startCPUProfile", "params": [string]}` |

### debug_startGoTrace

Comienza a escribir una traza del tiempo de ejecución de Go en el archivo dado.

| Client  | Method invocation                                      |
|:-------:|--------------------------------------------------------|
| Console | `debug.startGoTrace(file)`                             |
| RPC     | `{"method": "debug_startGoTrace", "params": [string]}` |

### debug_stopCPUProfile

Detiene un perfil de CPU en curso.

| Client  | Method invocation                                  |
|:-------:|----------------------------------------------------|
| Console | `debug.stopCPUProfile()`                           |
| RPC     | `{"method": "debug_stopCPUProfile", "params": []}` |

### debug_stopGoTrace

Deja de escribir la traza del tiempo de ejecución Go.

| Client  | Method invocation                                 |
|:-------:|---------------------------------------------------|
| Console | `debug.startGoTrace(file)`                        |
| RPC     | `{"method": "debug_stopGoTrace", "params": []}`   |

### debug_traceBlock

El método `traceBlock` devolverá un seguimiento de pila completo de todos los códigos de operación invocados de todas las transacciones
que fueron incluidos incluidos en este bloque. ** Nota **, el padre de este bloque debe estar presente o
va a fallar

| Client  | Method invocation                                                        |
|:-------:|--------------------------------------------------------------------------|
| Go      | `debug.TraceBlock(blockRlp []byte, config. *vm.Config) BlockTraceResult` |
| Console | `debug.traceBlock(tblockRlp, [options])`                                 |
| RPC     | `{"method": "debug_traceBlock", "params": [blockRlp, {}]}`               |
'**


#### Ejemplo

```javascript
> debug.traceBlock("0xblock_rlp")
{
  gas: 85301,
  returnValue: "",
  structLogs: [{
      depth: 1,
      error: "",
      gas: 162106,
      gasCost: 3,
      memory: null,
      op: "PUSH1",
      pc: 0,
      stack: [],
      storage: {}
  },
    /* snip */
  {
      depth: 1,
      error: "",
      gas: 100000,
      gasCost: 0,
      memory: ["0000000000000000000000000000000000000000000000000000000000000006", "0000000000000000000000000000000000000000000000000000000000000000", "0000000000000000000000000000000000000000000000000000000000000060"],
      op: "STOP",
      pc: 120,
      stack: ["00000000000000000000000000000000000000000000000000000000d67cbec9"],
      storage: {
        0000000000000000000000000000000000000000000000000000000000000004: "8241fa522772837f0d05511f20caa6da1d5a3209000000000000000400000001",
        0000000000000000000000000000000000000000000000000000000000000006: "0000000000000000000000000000000000000000000000000000000000000001",
        f652222313e28459528d920b65115c16c04f3efc82aaedc97be59f3f377c0d3f: "00000000000000000000000002e816afc1b5c0f39852131959d946eb3b07b5ad"
      }
  }]
```

### debug_traceBlockByNumber

Similar a [debug_traceBlock](# debug_traceBlock), `traceBlockByNumber` acepta un número de bloque y reproducirá el
Bloque que ya está presente en la base de datos.

| Client  | Method invocation                                                              |
|:-------:|--------------------------------------------------------------------------------|
| Go      | `debug.TraceBlockByNumber(number uint64, config. *vm.Config) BlockTraceResult` |
| Console | `debug.traceBlockByNumber(number, [options])`                                  |
| RPC     | `{"method": "debug_traceBlockByNumber", "params": [number, {}]}`               |



### debug_traceBlockByHash

Similar a [debug_traceBlock] (# debug_traceBlock), `traceBlockByHash` acepta un hash de bloque y reproducirá el
Bloque que ya está presente en la base de datos.

| Client  | Method invocation                                                               |
|:-------:|---------------------------------------------------------------------------------|
| Go      | `debug.TraceBlockByHash(hash common.Hash, config. *vm.Config) BlockTraceResult` |
| Console | `debug.traceBlockByHash(hash, [options])`                                       |
| RPC     | `{"method": "debug_traceBlockByHash", "params": [hash {}]}`                     |



### debug_traceBlockFromFile

Similar a [debug_traceBlock] (# debug_traceBlock), `traceBlockFromFile` acepta un archivo que contiene el RLP del bloque.

| Client  | Method invocation                                                                |
|:-------:|----------------------------------------------------------------------------------|
| Go      | `debug.TraceBlockFromFile(fileName string, config. *vm.Config) BlockTraceResult` |
| Console | `debug.traceBlockFromFile(fileName, [options])`                                  |
| RPC     | `{"method": "debug_traceBlockFromFile", "params": [fileName, {}]}`               |



### debug_traceTransaction

El método de depuración `traceTransaction` intentará ejecutar la transacción exactamente de la misma manera
Como fue ejecutado en la red. Repetirá cualquier transacción que haya sido ejecutada antes.
a éste antes de que finalmente intente ejecutar la transacción que corresponde a la dada
picadillo.

Además del hash de la transacción, puede darle un argumento secundario * opcional *, que
Especifica las opciones para esta llamada específica. Las posibles opciones son:

* `disableStorage`:` BOOL`. Al establecer esto en verdadero, se deshabilitará la captura de almacenamiento (predeterminado = falso).
* `disableMemory`:` BOOL`. Al establecer esto en verdadero, se deshabilitará la captura de memoria (predeterminado = falso).
* `disableStack`:` BOOL`. Al establecer esto en verdadero, se deshabilitará la captura de pila (por defecto = falso).
* `tracer`:` STRING`. Al establecer esto, se habilitará el rastreo de transacciones basado en JavaScript, que se describe a continuación. Si se establece, los cuatro argumentos anteriores se ignorarán.
* `timeout`:` STRING`. Anula el tiempo de espera predeterminado de 5 segundos para llamadas de seguimiento basadas en JavaScript. Los valores válidos se describen [aquí] (https://golang.org/pkg/time/#ParseDuration).

| Client  | Method invocation                                                                            |
|:-------:|----------------------------------------------------------------------------------------------|
| Go      | `debug.TraceTransaction(txHash common.Hash, logger *vm.LogConfig) (*ExecutionResurt, error)` |
| Console | `debug.traceTransaction(txHash, [options])`                                                  |
| RPC     | `{"method": "debug_traceTransaction", "params": [txHash, {}]}`                               |

#### Ejemplo

```javascript
> debug.traceTransaction("0x2059dd53ecac9827faad14d364f9e04b1d5fe5b506e3acc886eff7a6f88a696a")
{
  gas: 85301,
  returnValue: "",
  structLogs: [{
      depth: 1,
      error: "",
      gas: 162106,
      gasCost: 3,
      memory: null,
      op: "PUSH1",
      pc: 0,
      stack: [],
      storage: {}
  },
    /* snip */
  {
      depth: 1,
      error: "",
      gas: 100000,
      gasCost: 0,
      memory: ["0000000000000000000000000000000000000000000000000000000000000006", "0000000000000000000000000000000000000000000000000000000000000000", "0000000000000000000000000000000000000000000000000000000000000060"],
      op: "STOP",
      pc: 120,
      stack: ["00000000000000000000000000000000000000000000000000000000d67cbec9"],
      storage: {
        0000000000000000000000000000000000000000000000000000000000000004: "8241fa522772837f0d05511f20caa6da1d5a3209000000000000000400000001",
        0000000000000000000000000000000000000000000000000000000000000006: "0000000000000000000000000000000000000000000000000000000000000001",
        f652222313e28459528d920b65115c16c04f3efc82aaedc97be59f3f377c0d3f: "00000000000000000000000002e816afc1b5c0f39852131959d946eb3b07b5ad"
      }
  }]
```

#### rastreo basado en JavaScript
Especificar la opción `tracer` en el segundo argumento habilita el rastreo basado en JavaScript. En este modo, `tracer` se interpreta como una expresión de JavaScript que se espera que evalúe a un objeto con (al menos) dos métodos, llamados` step` y `resultado`.

`step` es una función que toma dos argumentos, log y db, y se llama para cada paso del EVM, o cuando se produce un error, mientras se rastrea la transacción especificada.

`log` tiene los siguientes campos:

 - `pc`: Número, el contador del programa actual
 - `op`: Object, un objeto OpCode que representa el opcode actual
 - `gas`: Número, la cantidad de gas restante
 - `gasPrice`: Número, el costo en wei de cada unidad de gas
 - `memory`: Objeto, una estructura que representa el espacio de memoria del contrato
 - `stack`: array [big.Int], la pila de ejecución EVM
 - `depth`: la profundidad de ejecución
 - `account`: la dirección de la cuenta que ejecuta la operación actual
 - `err`: si ocurrió un error, información sobre el error

Si `err` no es nulo, todos los demás campos deben ignorarse.

Por eficiencia, el mismo objeto `log` se reutiliza en cada paso de ejecución, actualizado con los valores actuales; asegúrese de copiar los valores que desea conservar más allá de la llamada actual. Por ejemplo, esta función de paso no funcionará:

    function(log) {
      this.logs.append(log);
    }

Pero esta función de paso:

    function(log) {
      this.logs.append({gas: log.gas, pc: log.pc, ...});
    }

`log.op` has the following methods:

 - `isPush()` - returns true iff the opcode is a PUSHn
 - `toString()` - returns the string representation of the opcode
 - `toNumber()` - returns the opcode's number

`log.memory` has the following methods:

 - `slice(start, stop)` - returns the specified segment of memory as a byte slice
 - `length()` - returns the length of the memory

`log.stack` has the following methods:

 - `peek(idx)` - returns the idx-th element from the top of the stack (0 is the topmost element) as a big.Int
 - `length()` - returns the number of elements in the stack

`db` has the following methods:

 - `getBalance(address)` - returns a `big.Int` with the specified account's balance
 - `getNonce(address)` - returns a Number with the specified account's nonce
 - `getCode(address)` - returns a byte slice with the code for the specified account
 - `getState(address, hash)` - returns the state value for the specified account and the specified hash
 - `exists(address)` - returns true if the specified address exists

La segunda función, 'resultado', no toma argumentos, y se espera que devuelva un valor serializable JSON para devolver al llamante RPC.

Si la función de paso lanza una excepción o ejecuta una operación ilegal en cualquier punto, no se llamará en ningún otro paso de VM, y el error se devolverá a la persona que llama.

Tenga en cuenta que varios valores son objetos Golang big.Int, no números de JavaScript o bigints JS. Como tales, tienen la misma interfaz que se describe en los dioses. Su serialización por defecto a JSON es como un número de Javascript; para serializar números grandes con precisión, llame a `.String ()` en ellos. Para mayor comodidad, se proporciona `big.NewInt (x)`, y convertirá una uint en un Go BigInt.

Ejemplo de uso, devuelve el elemento superior de la pila solo en cada código de operación CALL:

    debug.traceTransaction(txhash, {tracer: '{data: [], step: function(log) { if(log.op.toString() == "CALL") this.data.push(log.stack.peek(0)); }, result: function() { return this.data; }}'});

### debug_verbosity

Establece el techo de verbosidad de registro. Registrar mensajes con nivel
Se imprimirá hasta e incluyendo el nivel dado.

La verbosidad de paquetes individuales y archivos fuente.
puede plantearse usando `debug_vmodule`.

| Client  | Method invocation                                 |
|:-------:|---------------------------------------------------|
| Console | `debug.verbosity(level)`                          |
| RPC     | `{"method": "debug_vmodule", "params": [number]}` |

### debug_vmodule

Establece el patrón de verbosidad de registro.

| Client  | Method invocation                                 |
|:-------:|---------------------------------------------------|
| Console | `debug.vmodule(string)`                           |
| RPC     | `{"method": "debug_vmodule", "params": [string]}` |


#### Ejemplo

Si desea ver los mensajes de un paquete de Go en particular (directorio)
y todos los subdirectorios, usar:

```javascript
> debug.vmodule("eth/*=6")
```

Si desea restringir los mensajes a un paquete en particular (por ejemplo, p2p)
pero excluye subdirectorios, usa:

```javascript
> debug.vmodule("p2p=6")
```

Si desea ver los mensajes de registro de un archivo fuente en particular, use

```javascript
> debug.vmodule("server.go=6")
```

Puedes componer estos patrones básicos. Si quieres ver todo
salida de peer.go en un paquete debajo de eth (eth / peer.go,
eth / downloader / peer.go) así como la salida del paquete p2p
en el nivel <= 5, use:

``` javascript
debug.vmodule("eth/*/peer.go=6,p2p=5")
```

### debug_writeBlockProfile

Escribe un perfil de bloqueo goroutine en el archivo dado.

| Client  | Method invocation                                           |
|:-------:|-------------------------------------------------------------|
| Console | `debug.writeBlockProfile(file)`                             |
| RPC     | `{"method": "debug_writeBlockProfile", "params": [string]}` |

### debug_writeMemProfile

Escribe un perfil de asignación al archivo dado.
Tenga en cuenta que la tasa de perfilado no se puede establecer a través de la API,
debe establecerse en la línea de comando usando el `--memprofilerate`
bandera.

| Client  | Method invocation                                           |
|:-------:|-------------------------------------------------------------|
| Console | `debug.writeMemProfile(file string)`                        |
| RPC     | `{"method": "debug_writeBlockProfile", "params": [string]}` |

## Minero

La API `miner` le permite controlar de forma remota la operación de minería del nodo y configurar varios
Configuraciones específicas de minería.

### miner_setExtra

Establece los datos adicionales que un minero puede incluir cuando los bloques de mineros. Esto está limitado a
32 bytes.

| Client  | Method invocation                                  |
|:-------:|----------------------------------------------------|
| Go      | `miner.setExtra(extra string) (bool, error)`       |
| Console | `miner.setExtra(string)`                           |
| RPC     | `{"method": "miner_setExtra", "params": [string]}` |


### minero_setGasPrecio

Establece el precio mínimo aceptado del gas cuando se realizan transacciones mineras. Cualquier transacción que sea
Por debajo de este límite se excluyen del proceso minero.

| Client  | Method invocation                                     |
|:-------:|-------------------------------------------------------|
| Go      | `miner.setGasPrice(number *rpc.HexNumber) bool`       |
| Console | `miner.setGasPrice(number)`                           |
| RPC     | `{"method": "miner_setGasPrice", "params": [number]}` |

###iniciar minero

Inicie el proceso de minería de CPU con el número dado de subprocesos y genere un nuevo DAG
si es necesario.

| Client  | Method invocation                                   |
|:-------:|-----------------------------------------------------|
| Go      | `miner.Start(threads *rpc.HexNumber) (bool, error)` |
| Console | `miner.start(number)`                               |
| RPC     | `{"method": "miner_start", "params": [number]}`     |


### miner_stop

Detenga la operación de minería de la CPU.

| Client  | Method invocation                            |
|:-------:|----------------------------------------------|
| Go      | `miner.Stop() bool`                          |
| Console | `miner.stop()`                               |
| RPC     | `{"method": "miner_stop", "params": []}`     |


### miner_setEtherBase

Establece el etherbase, donde irán las recompensas de minería.

| Client  | Method invocation                                           |
|:-------:|-------------------------------------------------------------|
| Go      | `miner.SetEtherbase(common.Address) bool`                   |
| Console | `miner.setEtherbase(address)`                               |
| RPC     | `{"method": "miner_setEtherbase", "params": [address]}`     |


## Personal

La API personal gestiona las claves privadas en el almacén de claves.

### personal_importRawKey

Importa la clave privada sin cifrar dada (cadena hexadecimal) en el almacén de claves,
cifrarlo con la frase de contraseña.

Devuelve la dirección de la nueva cuenta.

| Client    | Method invocation                                                 |
| :-------: | ----------------------------------------------------------------- |
| Console   | `personal.importRawKey(keydata, passphrase)`                      |
| RPC       | `{"method": "personal_importRawKey", "params": [string, string]}` |

### personal_listcuentas

Devuelve todas las direcciones de cuenta Pirl de todas las claves.
en el almacén de llaves.

| Client    | Method invocation                                   |
| :-------: | --------------------------------------------------- |
| Console   | `personal.listAccounts`                             |
| RPC       | `{"method": "personal_listAccounts", "params": []}` |

#### Ejemplo

```javascript
> personal.listAccounts
["0x5e97870f263700f46aa00d967821199b9bc5a120", "0x3d80b31a78c30fc628f20b2c89d7ddbf6e53cedc"]
```

### personal_lockAccount

Elimina la clave privada con la dirección dada de la memoria.
La cuenta ya no se puede utilizar para enviar transacciones.

| Client    | Method invocation                                        |
| :-------: | -------------------------------------------------------- |
| Console   | `personal.lockAccount(address)`                          |
| RPC       | `{"method": "personal_lockAccount", "params": [string]}` |

###personal_newAccount

Genera una nueva clave privada y la almacena en el directorio del almacén de claves.
El archivo de clave se cifra con la frase de contraseña dada.
Devuelve la dirección de la nueva cuenta.

En la consola Pirl, `newAccount` pedirá una frase de contraseña cuando
no se suministra como el argumento.

| Client    | Method invocation                                       |
| :-------: | ---------------------------------------------------     |
| Console   | `personal.newAccount()`                                 |
| RPC       | `{"method": "personal_newAccount", "params": [string]}` |

#### Ejemplo

```javascript
> personal.newAccount()
Passphrase:
Repeat passphrase:
"0x5e97870f263700f46aa00d967821199b9bc5a120"
```

La frase de contraseña también se puede proporcionar como una cadena.

```javascript
> personal.newAccount("h4ck3r")
"0x3d80b31a78c30fc628f20b2c89d7ddbf6e53cedc"
```

### personal_unlockAccount

Descifra la clave con la dirección dada del almacén de claves.

Tanto la contraseña como la duración del desbloqueo son opcionales cuando se usa la consola de JavaScript.
Si la frase de contraseña no se proporciona como un argumento, la consola solicitará
la contraseña de forma interactiva.

La clave no encriptada se guardará en la memoria hasta que expire la duración del desbloqueo.
Si la duración del desbloqueo por defecto es de 300 segundos. Una duración explícita
de cero segundos desbloquea la llave hasta que Pirl sale.

La cuenta se puede usar con `eth_sign` y` eth_sendTransaction` mientras está desbloqueada.

| Client    | Method invocation                                                          |
| :-------: | -------------------------------------------------------------------------- |
| Console   | `personal.unlockAccount(address, passphrase, duration)`                    |
| RPC       | `{"method": "personal_unlockAccount", "params": [string, string, number]}` |

#### Ejemplo

```javascript
> personal.unlockAccount("0x5e97870f263700f46aa00d967821199b9bc5a120")
Unlock account 0x5e97870f263700f46aa00d967821199b9bc5a120
Passphrase:
true
```

Proporcionando la contraseña y la duración del desbloqueo como argumentos:

```javascript
> personal.unlockAccount("0x5e97870f263700f46aa00d967821199b9bc5a120", "foo", 30)
true
```

Si desea escribir la contraseña y aún anular la duración predeterminada de desbloqueo,
Pase `null` como la frase de contraseña.

```
> personal.unlockAccount("0x5e97870f263700f46aa00d967821199b9bc5a120", null, 30)
Unlock account 0x5e97870f263700f46aa00d967821199b9bc5a120
Passphrase:
true
```

###personal_send Transaction

Valide la frase de contraseña dada y envíe la transacción.

La transacción es el mismo argumento que para `eth_sendTransaction` y contiene la dirección` from`. Si la frase de contraseña se puede utilizar para descifrar la clave privada de `tx.from`, la transacción se verifica, se firma y se envía a la red. La cuenta no se desbloquea globalmente en el nodo y no se puede usar en otras llamadas RPC.

| Client    | Method invocation                                                |
| :-------: | -----------------------------------------------------------------|
| Console   | `personal.sendTransaction(tx, passphrase)`                       |
| RPC       | `{"method": "personal_sendTransaction", "params": [tx, string]}` |

*Note, prior to Pirl 1.5, please use `personal_signAndSendTransaction` as that was the original introductory name and only later renamed to the current final version.*

#### Ejemplo

```javascript
> var tx = {from: "0x391694e7e0b0cce554cb130d723a9d27458f9298", to: "0xafa3f8684e54059998bc3a7b0d2b0da075154d66", value: web3.toWei(1.23, "ether")}
undefined
> personal.sendTransaction(tx, "passphrase")
0x8474441674cdd47b35b875fd1a530b800b51a5264b9975fb21129eeb8c18582f
```

### firma personal

El método de signo calcula una firma específica de Pirl con:
`sign (keccack256 (" \ x19Pirl Signed Message: \ n "+ len (message) + message)))`.

Al agregar un prefijo al mensaje, la firma calculada es reconocible como una firma específica de Pirl. Esto evita el uso indebido cuando un DApp malintencionado puede firmar datos arbitrarios (por ejemplo, una transacción) y usar la firma para hacerse pasar por la víctima.

Ver ecRecover para verificar la firma.

| Client  | Method invocation                                     |
|:-------:|-------------------------------------------------------|   
| Console | `personal.sign(message, account, [password])`                |
| RPC     | `{"method": "personal_sign", "params": [message, account, password]}` |


#### Ejemplo

```javascript
> personal.sign("0xdeadbeaf", "0x9b2055d370f73ec7d8a03e965129118dc8f5bf83", "")
"0xa3f20717a250c2b0b729b7e5becbff67fdaef7e0699da4de7ca5895b02a170a12d887fd3b17bfdce3481f10bea41f45ba9f709d39ce8325427b57afcfc994cee1b"
```

### personal_ecRecover

`ecRecover` devuelve la dirección asociada con la clave privada que se utilizó para calcular la firma en` personal_sign`.

| Client  | Method invocation                                     |
|:-------:|-------------------------------------------------------|   
| Console | `personal.ecRecover(message, signature)`                 |
| RPC     | `{"method": "personal_ecRecover", "params": [message, signature]}` |


#### Ejemplo

```javascript
> personal.sign("0xdeadbeaf", "0x9b2055d370f73ec7d8a03e965129118dc8f5bf83", "")
"0xa3f20717a250c2b0b729b7e5becbff67fdaef7e0699da4de7ca5895b02a170a12d887fd3b17bfdce3481f10bea41f45ba9f709d39ce8325427b57afcfc994cee1b"
> personal.ecRecover("0xdeadbeaf", "0xa3f20717a250c2b0b729b7e5becbff67fdaef7e0699da4de7ca5895b02a170a12d887fd3b17bfdce3481f10bea41f45ba9f709d39ce8325427b57afcfc994cee1b")
"0x9b2055d370f73ec7d8a03e965129118dc8f5bf83"
```


## Txpool

La API `txpool` le da acceso a varios métodos RPC no estándar para inspeccionar el contenido de
grupo de transacciones que contiene todas las transacciones pendientes actualmente así como las que están en cola para
Procesamiento futuro.

### txpool_content

La propiedad de inspección `contenido` se puede consultar para enumerar los detalles exactos de todas las transacciones
actualmente pendiente de inclusión en el (los) siguiente (s) bloque (s), así como los que están siendo programados
Solo para futuras ejecuciones.

El resultado es un objeto con dos campos `pendiente` y` en cola`. Cada uno de estos campos son asociativos.
matrices, en las que cada entrada asigna una dirección de origen a un lote de transacciones programadas. Estos lotes
ellos mismos son mapas que asocian nonces con transacciones reales.

Tenga en cuenta que puede haber varias transacciones asociadas con la misma cuenta y nonce. Esto puede
sucederá si el usuario emite varios canales con diferentes tolerancias de gas (o incluso completamente diferentes
actas).

| Client  | Method invocation                                                       |
|:-------:|-------------------------------------------------------------------------|
| Go      | `txpool.Content() (map[string]map[string]map[string][]*RPCTransaction)` |
| Console | `txpool.content`                                                        |
| RPC     | `{"method": "txpool_content"}`                                          |

#### Ejemplo

```javascript
> txpool.content
{
  pending: {
    0x0216d5032f356960cd3749c31ab34eeff21b3395: {
      806: [{
        blockHash: "0x0000000000000000000000000000000000000000000000000000000000000000",
        blockNumber: null,
        from: "0x0216d5032f356960cd3749c31ab34eeff21b3395",
        gas: "0x5208",
        gasPrice: "0xba43b7400",
        hash: "0xaf953a2d01f55cfe080c0c94150a60105e8ac3d51153058a1f03dd239dd08586",
        input: "0x",
        nonce: "0x326",
        to: "0x7f69a91a3cf4be60020fb58b893b7cbb65376db8",
        transactionIndex: null,
        value: "0x19a99f0cf456000"
      }]
    },
    0x24d407e5a0b506e1cb2fae163100b5de01f5193c: {
      34: [{
        blockHash: "0x0000000000000000000000000000000000000000000000000000000000000000",
        blockNumber: null,
        from: "0x24d407e5a0b506e1cb2fae163100b5de01f5193c",
        gas: "0x44c72",
        gasPrice: "0x4a817c800",
        hash: "0xb5b8b853af32226755a65ba0602f7ed0e8be2211516153b75e9ed640a7d359fe",
        input: "0xb61d27f600000000000000000000000024d407e5a0b506e1cb2fae163100b5de01f5193c00000000000000000000000000000000000000000000000053444835ec580000000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        nonce: "0x22",
        to: "0x7320785200f74861b69c49e4ab32399a71b34f1a",
        transactionIndex: null,
        value: "0x0"
      }]
    }
  },
  queued: {
    0x976a3fc5d6f7d259ebfb4cc2ae75115475e9867c: {
      3: [{
        blockHash: "0x0000000000000000000000000000000000000000000000000000000000000000",
        blockNumber: null,
        from: "0x976a3fc5d6f7d259ebfb4cc2ae75115475e9867c",
        gas: "0x15f90",
        gasPrice: "0x4a817c800",
        hash: "0x57b30c59fc39a50e1cba90e3099286dfa5aaf60294a629240b5bbec6e2e66576",
        input: "0x",
        nonce: "0x3",
        to: "0x346fb27de7e7370008f5da379f74dd49f5f2f80f",
        transactionIndex: null,
        value: "0x1f161421c8e0000"
      }]
    },
    0x9b11bf0459b0c4b2f87f8cebca4cfc26f294b63a: {
      2: [{
        blockHash: "0x0000000000000000000000000000000000000000000000000000000000000000",
        blockNumber: null,
        from: "0x9b11bf0459b0c4b2f87f8cebca4cfc26f294b63a",
        gas: "0x15f90",
        gasPrice: "0xba43b7400",
        hash: "0x3a3c0698552eec2455ed3190eac3996feccc806970a4a056106deaf6ceb1e5e3",
        input: "0x",
        nonce: "0x2",
        to: "0x24a461f25ee6a318bdef7f33de634a67bb67ac9d",
        transactionIndex: null,
        value: "0xebec21ee1da40000"
      }],
      6: [{
        blockHash: "0x0000000000000000000000000000000000000000000000000000000000000000",
        blockNumber: null,
        from: "0x9b11bf0459b0c4b2f87f8cebca4cfc26f294b63a",
        gas: "0x15f90",
        gasPrice: "0x4a817c800",
        hash: "0xbbcd1e45eae3b859203a04be7d6e1d7b03b222ec1d66dfcc8011dd39794b147e",
        input: "0x",
        nonce: "0x6",
        to: "0x6368f3f8c2b42435d6c136757382e4a59436a681",
        transactionIndex: null,
        value: "0xf9a951af55470000"
      }, {
        blockHash: "0x0000000000000000000000000000000000000000000000000000000000000000",
        blockNumber: null,
        from: "0x9b11bf0459b0c4b2f87f8cebca4cfc26f294b63a",
        gas: "0x15f90",
        gasPrice: "0x4a817c800",
        hash: "0x60803251d43f072904dc3a2d6a084701cd35b4985790baaf8a8f76696041b272",
        input: "0x",
        nonce: "0x6",
        to: "0x8db7b4e0ecb095fbd01dffa62010801296a9ac78",
        transactionIndex: null,
        value: "0xebe866f5f0a06000"
      }],
    }
  }
}
```

### txpool_inspect

La propiedad de inspección `inspect` puede consultarse para obtener un resumen textual de todas las transacciones
actualmente pendiente de inclusión en el (los) siguiente (s) bloque (s), así como los que están siendo programados
Solo para futuras ejecuciones. Este es un método específicamente diseñado para que los desarrolladores vean rápidamente
Transacciones en la piscina y encontrar posibles problemas.

El resultado es un objeto con dos campos `pendiente` y` en cola`. Cada uno de estos campos son asociativos.
matrices, en las que cada entrada asigna una dirección de origen a un lote de transacciones programadas. Estos lotes
ellos mismos son mapas que asocian nonces con cadenas de resumen de transacciones.

Tenga en cuenta que puede haber varias transacciones asociadas con la misma cuenta y nonce. Esto puede
sucederá si el usuario emite varios canales con diferentes tolerancias de gas (o incluso completamente diferentes
actas).

| Client  | Method invocation                                              |
|:-------:|----------------------------------------------------------------|
| Go      | `txpool.Inspect() (map[string]map[string]map[string][]string)` |
| Console | `txpool.inspect`                                               |
| RPC     | `{"method": "txpool_inspect"}`                                 |

#### Ejemplo

```javascript
> txpool.inspect
{
  pending: {
    0x26588a9301b0428d95e6fc3a5024fce8bec12d51: {
      31813: ["0x3375ee30428b2a71c428afa5e89e427905f95f7e: 0 wei + 500000 × 20000000000 gas"]
    },
    0x2a65aca4d5fc5b5c859090a6c34d164135398226: {
      563662: ["0x958c1fa64b34db746925c6f8a3dd81128e40355e: 1051546810000000000 wei + 90000 × 20000000000 gas"],
      563663: ["0x77517b1491a0299a44d668473411676f94e97e34: 1051190740000000000 wei + 90000 × 20000000000 gas"],
      563664: ["0x3e2a7fe169c8f8eee251bb00d9fb6d304ce07d3a: 1050828950000000000 wei + 90000 × 20000000000 gas"],
      563665: ["0xaf6c4695da477f8c663ea2d8b768ad82cb6a8522: 1050544770000000000 wei + 90000 × 20000000000 gas"],
      563666: ["0x139b148094c50f4d20b01caf21b85edb711574db: 1048598530000000000 wei + 90000 × 20000000000 gas"],
      563667: ["0x48b3bd66770b0d1eecefce090dafee36257538ae: 1048367260000000000 wei + 90000 × 20000000000 gas"],
      563668: ["0x468569500925d53e06dd0993014ad166fd7dd381: 1048126690000000000 wei + 90000 × 20000000000 gas"],
      563669: ["0x3dcb4c90477a4b8ff7190b79b524773cbe3be661: 1047965690000000000 wei + 90000 × 20000000000 gas"],
      563670: ["0x6dfef5bc94b031407ffe71ae8076ca0fbf190963: 1047859050000000000 wei + 90000 × 20000000000 gas"]
    },
    0x9174e688d7de157c5c0583df424eaab2676ac162: {
      3: ["0xbb9bc244d798123fde783fcc1c72d3bb8c189413: 30000000000000000000 wei + 85000 × 21000000000 gas"]
    },
    0xb18f9d01323e150096650ab989cfecd39d757aec: {
      777: ["0xcd79c72690750f079ae6ab6ccd7e7aedc03c7720: 0 wei + 1000000 × 20000000000 gas"]
    },
    0xb2916c870cf66967b6510b76c07e9d13a5d23514: {
      2: ["0x576f25199d60982a8f31a8dff4da8acb982e6aba: 26000000000000000000 wei + 90000 × 20000000000 gas"]
    },
    0xbc0ca4f217e052753614d6b019948824d0d8688b: {
      0: ["0x2910543af39aba0cd09dbb2d50200b3e800a63d2: 1000000000000000000 wei + 50000 × 1171602790622 gas"]
    },
    0xea674fdde714fd979de3edf0f56aa9716b898ec8: {
      70148: ["0xe39c55ead9f997f7fa20ebe40fb4649943d7db66: 1000767667434026200 wei + 90000 × 20000000000 gas"]
    }
  },
  queued: {
    0x0f6000de1578619320aba5e392706b131fb1de6f: {
      6: ["0x8383534d0bcd0186d326c993031311c0ac0d9b2d: 9000000000000000000 wei + 21000 × 20000000000 gas"]
    },
    0x5b30608c678e1ac464a8994c3b33e5cdf3497112: {
      6: ["0x9773547e27f8303c87089dc42d9288aa2b9d8f06: 50000000000000000000 wei + 90000 × 50000000000 gas"]
    },
    0x976a3fc5d6f7d259ebfb4cc2ae75115475e9867c: {
      3: ["0x346fb27de7e7370008f5da379f74dd49f5f2f80f: 140000000000000000 wei + 90000 × 20000000000 gas"]
    },
    0x9b11bf0459b0c4b2f87f8cebca4cfc26f294b63a: {
      2: ["0x24a461f25ee6a318bdef7f33de634a67bb67ac9d: 17000000000000000000 wei + 90000 × 50000000000 gas"],
      6: ["0x6368f3f8c2b42435d6c136757382e4a59436a681: 17990000000000000000 wei + 90000 × 20000000000 gas", "0x8db7b4e0ecb095fbd01dffa62010801296a9ac78: 16998950000000000000 wei + 90000 × 20000000000 gas"],
      7: ["0x6368f3f8c2b42435d6c136757382e4a59436a681: 17900000000000000000 wei + 90000 × 20000000000 gas"]
    }
  }
}
```

###txpool_status

La propiedad de inspección `status` puede consultarse por el número de transacciones actualmente pendientes para
Inclusión en el (los) siguiente (s) bloque (s), así como los que están siendo programados para su futura ejecución solamente.

El resultado es un objeto con dos campos `pendiente` y` en cola`, cada uno de los cuales es un contador que representa
el número de transacciones en ese estado particular.

| Client  | Method invocation                             |
|:-------:|-----------------------------------------------|
| Go      | `txpool.Status() (map[string]*rpc.HexNumber)` |
| Console | `txpool.status`                               |
| RPC     | `{"method": "txpool_status"}`                 |

#### Ejemplo

```javascript
> txpool.status
{
  pending: 10,
  queued: 7
}
```


---
Autor(s):  

@Fawkes

Contribuyente(s):  

@Dptelecom
