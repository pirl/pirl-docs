---
title: Interfaz de Línea de Comandos
weight: 3
pre: "<b>3. </b>"
chapter: true
---

```
$ Pirl help
NAME:
   Pirl - the go-Pirl command line interface


USAGE:
   Pirl [options] command [command options] [arguments...]

VERSION:
   1.8.2-Hulk

COMMANDOS:
   account           Cuentas de administración
   attach            Iniciar un entorno de JavaScript interactivo (conectarse al nodo)
   bug               abre una ventana para informar de un error en el repositorio de Pirl
   console           Iniciar un entorno de JavaScript interactivo
   copydb            Cree una cadena local desde una carpeta de cadena de datos de destino
   dump              Volcar un bloque específico de almacenamiento
   dumpconfig        Mostrar valores de configuración
   export            Exportar cadena de bloques en un archivo
   export-preimages  Exportar la base de datos de preimagen en una secuencia de RLP
   import            Importar un archivo cadena de bloques
   import-preimages  Importe la base de datos de preimagen desde una secuencia de RLP
   init              Arranca e inicializa un nuevo bloque de génesis.
   js                Ejecutar los archivos JavaScript especificados
   license           Mostrar información de licencia
   makecache         Generar caché de verificación ethash (para pruebas)
   makedag           Generar minería ethash DAG (para pruebas)
   monitor           Monitorear y visualizar las métricas de los nodos.
   removedb          Eliminar cadena de bloques y bases de datos estatales
   version           Imprimir números de versión
   wallet            Gestionar carteras Pirl
   help, h           Muestra una lista de comandos o ayuda para un comando

OPCIONES Pirl:
  --config value                    Archivo de configuración de TOML
  --datadir "/home/ligi/.pirl"      Directorio de datos para las bases de datos y almacén de llaves.
  --keystore                        Directorio para el almacén de claves (por defecto = dentro del directorio de datos)
  --nousb                           Disables monitoring for and managing USB hardware wallets
  --networkid value                 Identificador de red (integer, 1=Frontier, 2=Morden (disused), 3=Ropsten, 4=Rinkeby) (default: 1)
  --testnet                         Red Ropsten: Preconfigurada red de prueba de trabajo
  --rinkeby                         Red de Rinkeby: Red de prueba de autoridad preconfigurada
  --syncmode "fast"                 Modo de sincronización de cadena de bloques ("fast", "full", or "light")
  --gcmode value                    Modo de recolección de basura de cadena de bloques ("full", "archive") (default: "full")
  --ethstats value                  URL de informe de un servicio de estadísticas de eth (nombre de nodo:secret@host:port)
  --identity value                  Nombre de nodo personalizado
  --lightserv value                 Porcentaje máximo de tiempo permitido para atender solicitudes LES (0-90) (default: 0)
  --lightpeers value                Número máximo de compañeros clientes de LES (default: 100)
  --lightkdf                        Reduzca el uso de RAM y CPU de derivación de clave a un costo adicional de la potencia KDF

OPCIONES DE CADENA DE DESARROLLADOR:
  --dev               Red de prueba de autoridad efímera con una cuenta de desarrollador prefinanciada, minería habilitada
  --dev.period value  Período de bloque para usar en modo desarrollador (0 = mía solo si la transacción está pendiente) (default: 0)

ETHASH OPCIONES:
  --ethash.cachedir                     Directorio para almacenar las memorias caché de verificación etash (default = dentro del directorio de datos)
  --ethash.cachesinmem value            Número de cachés Ethash recientes para mantener en la memoria (16MB each) (default: 2)
  --ethash.cachesondisk value           Número de cachés Ethash recientes para mantener en el disco (16MB each) (default: 3)
  --ethash.dagdir "/home/ligi/.ethash"  Directorio para almacenar los DAGs de minería etash. (default = dentro de la carpeta de inicio)
  --ethash.dagsinmem value              Número de DAG de minería de datos recientes para mantener en la memoria (1+GB each) (default: 1)
  --ethash.dagsondisk value             Número de DAG de minería de datos recientes para mantener en el disco. (1+GB each) (default: 2)

OPCIONES DE TRANSACCION DE PISCINA :
  --txpool.nolocals            Desactiva las exenciones de precios para transacciones enviadas localmente
  --txpool.journal value       Diario de disco para transacciones locales para sobrevivir reinicios de nodo (default: "transactions.rlp")
  --txpool.rejournal value     Intervalo de tiempo para regenerar el diario de transacciones local. (default: 1h0m0s)
  --txpool.pricelimit value    Límite mínimo del precio del gas para hacer cumplir la aceptación en la piscina. (default: 1)
  --txpool.pricebump value     Porcentaje de aumento de precios para reemplazar una transacción ya existente (default: 10)
  --txpool.accountslots value  Número mínimo de ranuras de transacciones ejecutables garantizadas por cuenta (default: 16)
  --txpool.globalslots value   Número máximo de ranuras de transacciones ejecutables para todas las cuentas (default: 4096)
  --txpool.accountqueue value  Número máximo de ranuras de transacciones no ejecutables permitidas por cuenta (default: 64)
  --txpool.globalqueue value   Número máximo de ranuras de transacciones no ejecutables para todas las cuentas (default: 1024)
  --txpool.lifetime value      Cantidad máxima de tiempo que la transacción no ejecutable está en cola (default: 3h0m0s)

OPCIONES DE SINTONIZACIÓN DE RENDIMIENTO:
  --cache value            Megabytes de memoria asignados al caché interno. (default: 1024)
  --cache.database value   Porcentaje de asignación de memoria caché para usar en la base de datos (default: 75)
  --cache.gc value         Porcentaje de asignación de memoria caché que se debe utilizar para la trie poda (default: 25)
  --trie-cache-gens value  Número de generaciones de nodo trie para mantener en la memoria(default: 120)

OPCIONES DE CUENTA:
  --unlock value    Lista de cuentas separadas por comas para desbloquear
  --password value  Archivo de contraseña para usar la entrada de contraseña no interactiva

OPCIONES DE CONSOLA API:
  --rpc                  Habilitar el servidor HTTP-RPC
  --rpcaddr value        Interfaz de escucha del servidor HTTP-RPC (default: "localhost")
  --rpcport value        Puerto de escucha del servidor HTTP-RPC (default: 8545)
  --rpcapi value         API ofrecidos a través de la interfaz HTTP-RPC
  --ws                   Habilitar el servidor WS-RPC
  --wsaddr value         Interfaz de escucha del servidor WS-RPC (default: "localhost")
  --wsport value         Puerto de escucha del servidor WS-RPC (default: 8546)
  --wsapi value          API ofrecidos a través de la interfaz WS-RPC
  --wsorigins value      Orígenes desde los cuales aceptar solicitudes de sockets web.
  --ipcdisable           Deshabilitar el servidor IPC-RPC
  --ipcpath              Nombre de archivo para el socket / tubería IPC dentro del directorio de datos (las rutas explícitas lo escapan)
  --rpccorsdomain value  Lista separada por comas de dominios desde los cuales se aceptan solicitudes de origen cruzado (se aplica el navegador)
  --rpcvhosts value      Lista separada por comas de nombres de host virtuales desde los cuales aceptar solicitudes (servidor forzado). Acepta el comodín '*'. (default: "localhost")
  --jspath loadScript    Ruta raíz de JavaScript para loadScript (default: ".")
  --exec value           Ejecutar declaración de JavaScript
  --preload value        Lista separada por comas de archivos JavaScript para precargar en la consola

OPCIONES DE REDES:
  --bootnodes value     URLs de enodo separados por comas para bootstrap de descubrimiento P2P (establezca v4 + v5 en lugar de servidores light)
  --bootnodesv4 value   URLs de enodo separados por comas para el bootstrap de descubrimiento P2P v4 (servidor light, nodos completos)
  --bootnodesv5 value   URLs enode separados por comas para el bootstrap de descubrimiento P2P v5 (servidor light, nodos light)
  --port value          Puerto de escucha de red (default: 30303)
  --maxpeers value      Número máximo de interlocutores de red (red deshabilitada si se establece en 0) (default: 25)
  --maxpendpeers value  Número máximo de intentos de conexión pendientes (se utilizan los valores predeterminados si se establece en 0) (default: 0)
  --nat value           Mecanismo de mapeo de puertos NAT (any|none|upnp|pmp|extip:<IP>) (default: "any")
  --nodiscover          Desactiva el mecanismo de descubrimiento de iguales (adición manual de pares)
  --v5disc              Habilita el mecanismo experimental RLPx V5 (Topic Discovery).
  --netrestrict value   Restringe la comunicación de red a las redes IP dadas (CIDR masks)
  --nodekey value       Archivo de clave de nodo P2P
  --nodekeyhex value    Clave de nodo P2P como hexadecimal (for testing)

OPCIONES MINERAS:
  --mine                    Habilitar la minería
  --minerthreads value      Número de subprocesos de CPU que se utilizarán para la minería (default: 8)
  --etherbase value         Dirección pública para recompensas de minería en bloque (default = primera cuenta creada) (default: "0")
  --targetgaslimit value    El límite de gas objetivo establece el piso de gas objetivo artificial para los bloques a minar (default: 4712388)
  --gasprice "18000000000"  Precio mínimo del gas a aceptar por minar una transacción.
  --extradata value         Bloquear datos extra establecidos por el minero (default = client version)

OPCIONES DE ORÁCULO DE PRECIO DE GAS:
  --gpoblocks value      Número de bloques recientes para verificar los precios del gas. (default: 20)
  --gpopercentile value  El precio de gas sugerido es el percentil dado de un conjunto de precios de gas de transacciones recientes (default: 60)

OPCIONES DE MAQUINA VIRTUAL:
  --vmdebug  Registrar información útil para VM y depuración de contratos.

OPCIONES DE REGISTRO Y DEBUGADO:
  --metrics                 Habilitar la recopilación de métricas y los informes
  --fakepow                 Desactiva la verificación de prueba de trabajo
  --nocompaction            Desactiva la compactación db después de la importación
  --verbosity value         Verbosidad de registro: 0=silent, 1=error, 2=warn, 3=info, 4=debug, 5=detail (default: 3)
  --vmodule value           Verbosidad por módulo: lista separada por comas de <pattern>=<level> (e.g. eth/*=5,p2p=4)
  --backtrace value         Solicitar un seguimiento de pila en una declaración de registro específica (e.g. "block.go:271")
  --debug                   Prefiere los mensajes de registro con la ubicación del sitio de llamada (file and line number)
  --pprof                   Habilitar el servidor HTTP pprof
  --pprofaddr value         Interfaz de escucha del servidor pprof HTTP (default: "127.0.0.1")
  --pprofport value         Puerto de escucha del servidor pprof HTTP (default: 6060)
  --memprofilerate value    Activar el perfil de memoria con la tasa dada (default: 524288)
  --blockprofilerate value  Activar perfil de bloque con la tasa dada (default: 0)
  --cpuprofile value        Escriba el perfil de la CPU en el archivo dado
  --trace value             Escribir seguimiento de ejecución en el archivo dado.

OPCIONES (EXPERIMENTALES)SUSURRO:
  --shh                       Habilitar susurro
  --shh.maxmessagesize value  Tamaño máximo de mensaje aceptado (default: 1048576)
  --shh.pow value             POW mínimo aceptado (default: 0.2)

OPCIONES DEPRECADAS:
  --fast   Habilitar la sincronización rápida a través de descargas de estado (replaced by --syncmode)
  --light  Habilitar el modo de cliente ligero (replaced by --syncmode)

OPCIONES MISC:
  --help, -h  show help


COPYRIGHT:
   Copyright 2013-2017 The go-ethereum Authors
   Copyright 2017-2019 PIRL Sprl

```

---
Autor(s):  

@Fawkes

Contribuyente(s):  

@Dptelecom
