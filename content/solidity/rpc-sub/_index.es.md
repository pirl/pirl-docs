---
title: RPC Subscriptiones
weight: 6
pre: "<b>6. </b>"
chapter: true
---
# Introducción

** _ experimental _ ** soporte para pub / sub usando suscripciones como se define en la especificación JSON-RPC 2.0. Esto permite a los clientes esperar eventos en lugar de sondearlos.

Funciona suscribiéndose a eventos particulares. El nodo devolverá un ID de suscripción. Para cada evento que coincida con la suscripción, se enviará una notificación con datos relevantes junto con el ID de suscripción.

Ejemplo:

    // create subscription
    >> {"id": 1, "method": "eth_subscribe", "params": ["newHeads", {}]}
    << {"jsonrpc":"2.0","id":1,"result":"0xcd0c3e8af590364c09d0fa6a1210faf5"}

    // incoming notifications
    << {"jsonrpc":"2.0","method":"eth_subscription","params":{"subscription":"0xcd0c3e8af590364c09d0fa6a1210faf5","result":{"difficulty":"0xd9263f42a87",<...>, "uncles":[]}}}
    << {"jsonrpc":"2.0","method":"eth_subscription","params":{"subscription":"0xcd0c3e8af590364c09d0fa6a1210faf5","result":{"difficulty":"0xd90b1a7ad02", <...>, "uncles":["0x80aacd1ea4c9da32efd8c2cc9ab38f8f70578fcd46a1a4ed73f82f3e0957f936"]}}}

    // cancel subscription
    >> {"id": 1, "method": "eth_unsubscribe", "params": ["0xcd0c3e8af590364c09d0fa6a1210faf5"]}
    << {"jsonrpc":"2.0","id":1,"result":true}

# Consideraciones
1. Las notificaciones se envían para eventos actuales y no para eventos pasados. Si su caso de uso requiere que no se pierda ninguna notificación, las suscripciones probablemente no sean la mejor opción.
2. Las suscripciones requieren una conexión dúplex completa. Pirl ofrece tales conexiones en forma de websockets (habilitar con --ws) e ipc (habilitado de forma predeterminada).
3. Las suscripciones están acopladas a una conexión. Si la conexión se cierra, todas las suscripciones que se crean a través de esta conexión se eliminan.
4. las notificaciones se almacenan en un búfer interno y se envían desde este búfer al cliente. Si el cliente no puede mantenerse al día y el número de notificaciones en búfer alcanza un límite (actualmente 10k), la conexión se cierra. Tenga en cuenta que la suscripción a algunos eventos puede causar una avalancha de notificaciones, por ejemplo. escuchando todos los registros / bloques cuando el nodo comienza a sincronizarse.

## Crear suscripción
Las suscripciones se crean con una llamada RPC regular con `eth_subscribe` como método y el nombre de la suscripción como primer parámetro. Si tiene éxito, devuelve el ID de suscripción.

### Parámetros
1. nombre de suscripción
2. argumentos opcionales

### Ejemplo

    >> {"id": 1, "method": "eth_subscribe", "params": ["newHeads", {"includeTransactions": true}]}
    << {"id": 1, "jsonrpc": "2.0", "result": "0x9cef478923ff08bf67fde6c64013158d"}

## Cancelar suscripción
Las suscripciones se cancelan con una llamada RPC regular con `eth_unsubscribe` como método y el ID de suscripción como primer parámetro. Devuelve un bool que indica si la suscripción se canceló correctamente.

### Parámetros
1. ID de suscripción

### Ejemplo

    >> {"id": 1, "method": "eth_unsubscribe", "params": ["0x9cef478923ff08bf67fde6c64013158d"]}
    << {"jsonrpc":"2.0","id":1,"result":true}

# Suscripciones soportadas

## newHeads
Se activa una notificación cada vez que se agrega un nuevo encabezado a la cadena, incluidas las reorganizaciones de la cadena. Los usuarios pueden usar el filtro bloom para determinar si el bloque contiene registros que les interesen.

En caso de una reorganización de la cadena, la suscripción emitirá todos los nuevos encabezados para la nueva cadena. Por lo tanto, la suscripción puede emitir múltiples encabezados en la misma altura.

### Ejemplo
```
    >> {"id": 1, "method": "eth_subscribe", "params": ["newHeads"]}
    << {"jsonrpc":"2.0","id":2,"result":"0x9ce59a13059e417087c02d3236a0b1cc"}

    << {
  "jsonrpc": "2.0",
  "method": "eth_subscription",
  "params": {
    "result": {
      "difficulty": "0x15d9223a23aa",
      "extraData": "0xd983010305844765746887676f312e342e328777696e646f7773",
      "gasLimit": "0x47e7c4",
      "gasUsed": "0x38658",
      "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
      "miner": "0xf8b483dba2c3b7176a3da549ad41a48bb3121069",
      "nonce": "0x084149998194cc5f",
      "number": "0x1348c9",
      "parentHash": "0x7736fab79e05dc611604d22470dadad26f56fe494421b5b333de816ce1f25701",
      "receiptRoot": "0x2fab35823ad00c7bb388595cb46652fe7886e00660a01e867824d3dceb1c8d36",
      "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
      "stateRoot": "0xb3346685172db67de536d8765c43c31009d0eb3bd9c501c9be3229203f15f378",
      "timestamp": "0x56ffeff8",
      "transactionsRoot": "0x0167ffa60e3ebc0b080cdb95f7c0087dd6c0e61413140e39d94d3468d7c9689f"
    },
    "subscription": "0x9ce59a13059e417087c02d3236a0b1cc"
  }
}
```

## registros
Devuelve los registros que se incluyen en los nuevos bloques importados y coinciden con los criterios de filtro dados.

En el caso de una reorganización de la cadena, los registros enviados anteriormente que están en la cadena antigua se reenviarán con la propiedad `removido 'establecida en verdadero. Se emiten los registros de las transacciones que terminaron en la nueva cadena. Por lo tanto, una suscripción puede emitir registros para la misma transacción varias veces.

### Parámetros
1. `objeto` con los siguientes campos (opcionales)
     - ** dirección **, ya sea una dirección o una matriz de direcciones. Solo se devuelven los registros que se crean a partir de estas direcciones (opcional)
     - ** temas **, solo registros que coinciden con los temas especificados (opcional)


### Ejemplo
    >> {"id": 1, "method": "eth_subscribe", "params": ["logs", {"address": "0x8320fe7702b96808f7bbc0d4a888ed1468216cfd", "topics": ["0xd78a0cb8bb633d06981248b816e7bd33c2a35a6089241d099fa519e361cab902"]}]}
    << {"jsonrpc":"2.0","id":2,"result":"0x4a8a4c0517381924f9838102c5a4dcb7"}

    << {"jsonrpc":"2.0","method":"eth_subscription","params": {"subscription":"0x4a8a4c0517381924f9838102c5a4dcb7","result":{"address":"0x8320fe7702b96808f7bbc0d4a888ed1468216cfd","blockHash":"0x61cdb2a09ab99abf791d474f20c2ea89bf8de2923a2d42bb49944c8c993cbf04","blockNumber":"0x29e87","data":"0x00000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000003","logIndex":"0x0","topics":["0xd78a0cb8bb633d06981248b816e7bd33c2a35a6089241d099fa519e361cab902"],"transactionHash":"0xe044554a0a55067caafd07f8020ab9f2af60bdfe337e395ecd84b4877a3d1ab4","transactionIndex":"0x0"}}}

## newPendingTransactions
Devuelve el hash para todas las transacciones que se agregan al estado pendiente y se firman con una clave que está disponible en el nodo.

Cuando una transacción que anteriormente era parte de la cadena canónica no es parte de la nueva cadena canónica después de una reogranización, se emite nuevamente.

### Parámetros
ninguna

### Ejemplo
    >> {"id": 1, "method": "eth_subscribe", "params": ["newPendingTransactions"]}
    << {"jsonrpc":"2.0","id":2,"result":"0xc3b33aa549fb9a60e95d21862596617c"}

    << {
            "jsonrpc":"2.0",
            "method":"eth_subscription",
            "params":{
                "subscription":"0xc3b33aa549fb9a60e95d21862596617c",
                "result":"0xd6fdc5cc41a9959e922f30cb772a9aef46f4daea279307bc5f7024edc4ccd7fa"
            }
        }

## sincronizando
Indica cuando el nodo inicia o detiene la sincronización. El resultado puede ser un valor booleano que indica que la sincronización ha comenzado (verdadero), finalizado (falso) o un objeto con varios indicadores de progreso.

### Parámetros
ninguna

### Ejemplo
    >> {"id": 1, "method": "eth_subscribe", "params": ["syncing"]}
    << {"jsonrpc":"2.0","id":2,"result":"0xe2ffeb2703bcf602d42922385829ce96"}

    << {"subscription":"0xe2ffeb2703bcf602d42922385829ce96","result":{"syncing":true,"status":{"startingBlock":674427,"currentBlock":67400,"highestBlock":674432,"pulledStates":0,"knownStates":0}}}}


## Posible suscripción futura:
- cambios de balance
- cambios de cuenta
- Cambios únicos
- Cambios de almacenamiento en los contratos.



---
Autor(s):  

@Fawkes

Contribuyente(s):  

@Dptelecom