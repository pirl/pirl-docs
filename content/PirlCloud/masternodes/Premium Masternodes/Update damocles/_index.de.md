---
title: Manuelles Update auf 1.8.27-damocles
weight: 3
pre: "<b>3. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/Masternodes.png" >}}

## Manuelles Masternode Update auf 1.8.27-damocles

Die Anweisungen sind für RedHat oder CentOS-basierte VPS gedacht, sollten jedoch auf den meisten wichtigen Linux Distributionen funktionieren.
Möglicherweise müssen die Firewall-Anweisungen angepasst werden, um sie an die auf deinem VPS ausgeführte Software anzupassen.
Melden dich als `root` an und aktualisiere das System. Installiere dann die Abhängigkeiten:

## Binärdateien:

(marlin ist nun gleich für beide Node Typen)  
[git.pirl.io tags/1.8.27-damocles](https://git.pirl.io/community/pirl/tags/1.8.27-damocles)  
[marlin-1.8.27-damocles2.0](https://git.pirl.io/community/pirl/uploads/5ae5dee5a3c99f4dba35b630778c1fd1/marlin-1.8.27-damocles2.0)  
[pirl-masternode-premium-1.8.27-damocles](https://git.pirl.io/community/pirl/uploads/11320f624dade87c08d0fabb960cebca/pirl-masternode-premium-1.8.27-damocles)  
[pirl-masternode-content-1.8.27-damocles](https://git.pirl.io/community/pirl/uploads/cd403e61991ce375f5474a8509472572/pirl-masternode-content-1.8.27-damocles)

## Update mit dem Skript von @phatblinkie wenn du nicht alles von Hand machen möchtest:

[phatblinkie/mn_installer](https://github.com/phatblinkie/mn_installer)

## Der Update Prozess:

Stoppe den Pirl Node Service:

```
systemctl stop pirl
```

Und stoppe den Pirl Marlin Node Service:

```
systemctl stop marlin
```

Download die letzten Premium Masternode Binaries:

```
wget https://git.pirl.io/community/pirl/uploads/11320f624dade87c08d0fabb960cebca/pirl-masternode-premium-1.8.27-damocles
wget https://git.pirl.io/community/pirl/uploads/5ae5dee5a3c99f4dba35b630778c1fd1/marlin-1.8.27-damocles2.0
```

Download die letzten Content Masternode Binaries:

```
wget https://git.pirl.io/community/pirl/uploads/cd403e61991ce375f5474a8509472572/pirl-masternode-content-1.8.27-damocles
wget https://git.pirl.io/community/pirl/uploads/5ae5dee5a3c99f4dba35b630778c1fd1/marlin-1.8.27-damocles2.0
```

Verschiebe die Hauptbinärdatei nach /usr/bin/pirl für Premium Masternodes:  

```
mv masternode-premium-1.8.27-damocles /usr/bin/pirl
```

Für Content Nodes:

```
mv masternode-content-1.8.27-damocles /usr/bin/pirl
```

Verschiebe die marlin Datei nach /usr/bin/marlin für Premium and Content Masternodes:  

```
mv marlin-1.8.27-damocles2.0 /usr/bin/marlin
```

Setze die richtigen Berechtigungen:

```
chmod 0755 /usr/bin/pirl
chmod 0755 /usr/bin/marlin
```

Starte nun den VPS neu

```
reboot
```

Schaue dem Masternode Prozess beim synchornisieren mit der Blockchain zu:

```
journalctl -f
```

Sobald Nachrichten wie die folgenden angezeigt werden, ist die Masternode jetzt synchronisiert und trägt zum Netzwerk bei.

```
  ########  masternode sending proof of activity to poseidon for block  3934695  please check poseidon.pirl.io for details  //  marlin-1.8.27-damocles2.0 #########
```

## Monitoring

Wir empfehlen keinen aktiven Zugriff auf den Server. Wenn du jedoch den Status überprüfen möchtest, melden dich an deinem Server an und gebe den folgenden Befehl ein:

```
journalctl -f
```

Überwache den Status deiner Masternode, indem du die Poseidon Seite mit den Masternode Details aufrufst. Eine funktionierende Node sollte wie folgt aussehen, es ist möglich das die Version von der in der Abbildung unten gezeigten Version abweicht.

{{< imagesurlsheaders "cloud/detailsmn.png" >}}

{{% notice warning %}}
Falls die Synchronisation nicht funktioniert, gehe die Schritte unten durch um die Datenbank zu entfernen:
{{% /notice %}}  

- Als erstes exportiere die Token:

```
export MASTERNODE=fzeffz-zefzef-zefze-zefze-zefzef-zefzef <<<---DEIN TOKEN STEHT HIER
export TOKEN=zfzefezfzefzecfzegregkgeorgoerbvnijv <<<---DEIN TOKEN STEHT HIER

```

Der Schritrt oben kann auch wie folgt ausgeführt werden,
wenn du diese Datei hast /etc/pirlnode-env,
kannst du einfach:  

```
. /etc/pirlnode-env && export MASTERNODE TOKEN
```

- Und dann lösche die Datenbank  

```
pirl removedb
```

oder die letzte Möglichkeit:  

```
rm -rf /root/.pirl
```

Kind regards,  
PirlTeam.  

---
Author(s):

The Pirl Team

Contributor(s):

@Dptelecom
@packetflow
