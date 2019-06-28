---
title: Actualización Manual a 1.8.27-damocles
weight: 4
pre: "<b>4. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/Masternodes.png" >}}

## Actualización de Masternode manual a 1.8.27-damocles
Las instrucciones están destinadas a los VPS basados en Redhat o CentOS, pero deberían funcionar en la mayoría de las principales distribuciones de Linux.
Es posible que tenga que ajustar las instrucciones del firewall para que coincidan con el software que se ejecuta en su VPS.
Inicie sesión como root y actualice el sistema, luego instale las dependencias:

## Binario:
(Marlin ahora igual para ambos tipos)
[git.pirl.io tags/1.8.27-damocles](https://git.pirl.io/community/pirl/tags/1.8.27-damocles)  
[marlin-1.8.27-damocles2.0](https://git.pirl.io/community/pirl/uploads/5ae5dee5a3c99f4dba35b630778c1fd1/marlin-1.8.27-damocles2.0)  
[pirl-masternode-premium-1.8.27-damocles](https://git.pirl.io/community/pirl/uploads/11320f624dade87c08d0fabb960cebca/pirl-masternode-premium-1.8.27-damocles)  
[pirl-masternode-content-1.8.27-damocles](https://git.pirl.io/community/pirl/uploads/cd403e61991ce375f5474a8509472572/pirl-masternode-content-1.8.27-damocles)   


## Actualice con el Script de @phatblinkie si no Quiere Hacerlo todo Manual:

[phatblinkie/mn_installer](https://github.com/phatblinkie/mn_installer)



## El Proceso de Actualización:

Detener el servicio pirlnode:

`` `
systemctl stop pirl

```

and  the pirlmarlin service:

```
systemctl stop marlin

```

stop


### Descarga los Binarios de Masternodo Premium:
```
wget https://git.pirl.io/community/pirl/uploads/11320f624dade87c08d0fabb960cebca/pirl-masternode-premium-1.8.27-damocles
wget https://git.pirl.io/community/pirl/uploads/5ae5dee5a3c99f4dba35b630778c1fd1/marlin-1.8.27-damocles2.0

```

### Descargue los Binarios del Nodo de Contenido:

```
wget https://git.pirl.io/community/pirl/uploads/cd403e61991ce375f5474a8509472572/pirl-masternode-content-1.8.27-damocles
wget https://git.pirl.io/community/pirl/uploads/5ae5dee5a3c99f4dba35b630778c1fd1/marlin-1.8.27-damocles2.0

```


Mueve el binario principal a /usr/bin/pirl para masternodos premium: 

```
mv masternode-premium-1.8.27-damocles /usr/bin/pirl

```

Para los nodos de contenido: 
```
mv masternode-content-1.8.27-damocles /usr/bin/pirl

```

Mueve el binario principal a /usr/bin/marlin  para masternodos premium y nodos de contenido:  

```
mv marlin-1.8.27-damocles2.0 /usr/bin/marlin

```

Para conceder el permiso:

```
chmod 0755 /usr/bin/pirl
chmod 0755 /usr/bin/marlin

```


### Ahora Reinicie el Vps.
```
reboot
```


Mira cómo se sincroniza el proceso de masternodo con la cadena de bloques:
```
journalctl -f

```

Una vez que se muestran mensajes como los siguientes, su masternodo ahora está sincronizado y contribuyendo a la red.

```
  ########  masternode sending proof of activity to poseidon for block  3934695  please check poseidon.pirl.io for details  //  marlin-1.8.27-damocles2.0 #########

```

Vigilancia
No recomendamos el acceso activo en el servidor. Sin embargo, si desea verificar el estado, inicie sesión en su servidor y ejecute el siguiente comando:
```
journalctl -f
```

Controle el estado de su masternode consultando la página de detalles de Poseidon Masternode. Un nodo en funcionamiento debería aparecer como sigue, aunque la versión puede ser diferente de la que se muestra en la captura de pantalla a continuación.

{{% notice warning %}}
En caso de que la sincronización no funcione, siga estos pasos para eliminar la base de datos:
{{% /notice %}} 

- Primero exportar los tokens:

```
export MASTERNODE=fzeffz-zefzef-zefze-zefze-zefzef-zefzef <<<---YOUR TOKEN GOES HERE
export TOKEN=zfzefezfzefzecfzegregkgeorgoerbvnijv <<<---YOUR TOKEN GOES HERE


```

ese paso anterior también se puede hacer,
Si tiene este archivo / etc / pirlnode-env,
tu puedes hacer:  
```
. /etc/pirlnode-env && export MASTERNODE TOKEN

```


- Y luego quitar la base de datos:  

```
pirl removedb

```

o el último recurso:  

```
rm -rf /root/.pirl

```



Saludos cordiales,
Equipo Pirl.  

---
Autor(s):


The Pirl Team


Contribuyente(s):


@Dptelecom
