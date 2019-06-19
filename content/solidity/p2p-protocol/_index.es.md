---
title: P2P Protocolo
weight: 7
pre: "<b>7. </b>"
chapter: true
---
El paquete peer to peer le permite agregar redes peer to peer rápida y fácilmente a cualquier tipo de aplicación. El paquete p2p se configura en una estructura modular y extender el p2p con sus propios subprotocolo adicionales es fácil y sencillo.

Iniciar el servicio p2p solo requiere que configures un `p2p.Server {}` con algunas configuraciones:

```go
import "github.com/pirl/pirl/crypto"
import "github.com/pirl/pirl/p2p"

nodekey, _ := crypto.GenerateKey()
srv := p2p.Server{
	MaxPeers:   10,
	PrivateKey: nodekey,
	Name:       "my node name",
	ListenAddr: ":30300",
	Protocols:  []p2p.Protocol{},
}
srv.Start()
```

Si quisiéramos ampliar las capacidades de nuestro servidor p2p tendríamos que pasarle un subprotocolo adicional en la matriz `Protocol: [] p2p.Protocol {}`.

Un subprotocolo adicional que tiene la capacidad de responder al mensaje "foo" con "barra" requiere que configures un `p2p.Protocol {}`:

```go
func MyProtocol() p2p.Protocol {
	return p2p.Protocol{ // 1.
		Name:    "MyProtocol",                                                    // 2.
		Version: 1,                                                               // 3.
		Length:  1,                                                               // 4.
		Run:     func(peer *p2p.Peer, ws p2p.MsgReadWriter) error { return nil }, // 5.
	}
}
```

1. Un objeto de sub-protocolo en el paquete p2p se llama `Protocolo {}`. Cada vez que un par se conecte con la capacidad de manejar este tipo de protocolo lo utilizará;
2. El nombre de su protocolo para identificar el protocolo en la red;
3. La versión del protocolo.
4. La cantidad de mensajes en los que se basa este protocolo. Debido a que el p2p es ampliable y, por lo tanto, tiene la capacidad de enviar una cantidad arbitraria de mensajes (con un tipo, que veremos más adelante), el controlador p2p necesita saber cuánto espacio debe reservar para su protocolo, para garantizar el consenso. puede ser alcanzado entre los pares haciendo una negociación sobre los identificadores de mensaje. Nuestro protocolo soporta solo uno; `mensaje` (como verás más adelante).
5. El manejador principal de tu protocolo. Hemos dejado esto intencionalmente en blanco por ahora. La variable `peer` es el peer conectado a ti y te proporciona información básica sobre el peer. La variable `ws` que es un lector y un escritor le permite comunicarse con el par. Si un par nos está enviando un mensaje, el `MsgReadWriter` lo manejará y viceversa.

Permite completar los espacios en blanco y crear un compañero algo útil al permitirle comunicarse con otro compañero:

```go
const messageId = 0   // 1.
type Message string   // 2.

func msgHandler(peer *p2p.Peer, ws p2p.MsgReadWriter) error {
    for {
        msg, err := ws.ReadMsg()   // 3.
        if err != nil {            // 4.
            return err // if reading fails return err which will disconnect the peer.
        }

        var myMessage [1]Message
        err = msg.Decode(&myMessage) // 5.
        if err != nil {
            // handle decode error
            continue
        }
        
        switch myMessage[0] {
        case "foo":
            err := p2p.SendItems(ws, messageId, "bar")  // 6.
            if err != nil {
                return err // return (and disconnect) error if writing fails.
            }
         default:
             fmt.Println("recv:", myMessage)
         }
    }

    return nil
}
```

1. El único mensaje que conocemos;
2. Una cadena escrita que decodificamos en;
3. `ReadMsg` espera en la línea hasta que recibe un mensaje, un error o EOF.
4. En caso de error durante la lectura, es mejor devolver ese error y dejar que el servidor p2p lo maneje. Esto generalmente resulta en una desconexión del par.
5. `msg` contiene dos campos y un método de decodificación:
     * `Code` contiene el id del mensaje,` Code == messageId` (es decir, 0)
     * `Carga útil` el contenido del mensaje.
     * `Decode (<ptr>)` es un método auxiliar para: tomar `msg.Payload` y decodifica el resto del mensaje en la interfaz dada. Si falla, devolverá un error.
6. Si el mensaje que desciframos fue `foo`, responda con un` NewMessage` utilizando el identificador de mensaje `messageId` y responda con el mensaje` bar`. El mensaje `bar` se manejaría en el caso` default` en el mismo interruptor.

Ahora, si amarráramos todo esto, tendríamos un servidor p2p en funcionamiento con un subprotocolo de paso de mensajes.

```go
package main

import (
	"fmt"
	"os"

	import "github.com/pirl/pirl/crypto"
    import "github.com/pirl/pirl/p2p"
)

const messageId = 0

type Message string

func MyProtocol() p2p.Protocol {
	return p2p.Protocol{
		Name:    "MyProtocol",
		Version: 1,
		Length:  1,
		Run:     msgHandler,
	}
}

func main() {
	nodekey, _ := crypto.GenerateKey()
	srv := p2p.Server{
		MaxPeers:   10,
		PrivateKey: nodekey,
		Name:       "my node name",
		ListenAddr: ":30300",
		Protocols:  []p2p.Protocol{MyProtocol()},
	}

	if err := srv.Start(); err != nil {
		fmt.Println(err)
		os.Exit(1)
	}

	select {}
}

func msgHandler(peer *p2p.Peer, ws p2p.MsgReadWriter) error {
	for {
		msg, err := ws.ReadMsg()
		if err != nil {
			return err
		}

		var myMessage Message
		err = msg.Decode(&myMessage)
		if err != nil {
			// handle decode error
			continue
		}

		switch myMessage {
		case "foo":
			err := p2p.SendItems(ws, messageId, "bar"))
			if err != nil {
				return err
			}
		default:
			fmt.Println("recv:", myMessage)
		}
	}

	return nil
}
```


---
Autor(s):  

@Fawkes

Contribuyente(s):  

@Dptelecom
   