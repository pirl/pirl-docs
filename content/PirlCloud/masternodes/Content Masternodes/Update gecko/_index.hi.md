---
title: मैनुअल अपडेट टु 1.8.27-gecko
weight: 3
pre: "<b>3. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/Masternodes.png" >}}

## मैनुअल मास्टरनोड अपडेट टु to 1.8.27-gecko  
निर्देश Redhat या CentOS आधारित VPS के लिए अभिप्रेत हैं, लेकिन अधिकांश प्रमुख लिनक्स वितरण पर काम करना चाहिए।   
आपको अपने VPS पर चल रहे सॉफ़्टवेयर सॉफ़्टवेयर से मेल खाने के लिए फ़ायरवॉल निर्देशों को समायोजित करने की आवश्यकता हो सकती है।  
रूट के रूप में लॉगिन करें और सिस्टम को अपडेट करें, फिर निर्भरताएं स्थापित करें:

## बाइनरी:   
(मार्लिन अब दोनों प्रकारों के लिए समान है)  
https://storage.googleapis.com/pirl-node/pirl-1.8.27-gecko/marlin/marlin-masternode-gecko1_8_27
https://storage.googleapis.com/pirl-node/pirl-1.8.27-gecko/masternodes/content/pirl-linux-amd64-content
https://storage.googleapis.com/pirl-node/pirl-1.8.27-gecko/masternodes/premium/pirl-linux-amd64-premium  


## अगर आप मैनुअल अपडेट नहीं करना चाहते हैं तो आप @phatblinkie की स्क्रिप्ट का उपयोग कर सकते है:

https://github.com/phatblinkie/mn_installer



## अपडेट करने की प्रक्रिया:

प्रिलनोड सेवा को बंद करे:

```
systemctl stop pirl

```

और प्रिलमार्लिन सेवा को बंद करे:

```
systemctl stop marlin

```




### प्रीमियम मास्टरनोड बायनेरी डाउनलोड करें:
```
wget https://storage.googleapis.com/pirl-node/pirl-1.8.27-gecko/masternodes/premium/pirl-linux-amd64-premium
wget https://storage.googleapis.com/pirl-node/pirl-1.8.27-gecko/marlin/marlin-masternode-gecko1_8_27

```

### कंटेंट मास्टरनोड बायनेरी डाउनलोड करें:

```
wget https://storage.googleapis.com/pirl-node/pirl-1.8.27-gecko/masternodes/content/pirl-linux-amd64-content
wget https://storage.googleapis.com/pirl-node/pirl-1.8.27-gecko/marlin/marlin-masternode-gecko1_8_27

```


प्रीमियम मास्टरनोड्स के लिए मुख्य बाइनरी को /usr/bin/pirl पर ले जाएं:  

```
mv pirl-linux-amd64-premium /usr/bin/pirl

```

कंटेंट मास्टरनोड के लिए:  
```
mv pirl-linux-amd64-content /usr/bin/pirl

```

प्रीमियम मास्टरनोड्स और कंटेंट मास्टरनोड्स के लिए मर्लिन बाइनरी को /usr/bin/marlin पर ले जाएँ:  

```
mv marlin-masternode-gecko1_8_27 /usr/bin/marlin

```

अनुमति देना के लिए :

```
chmod 0755 /usr/bin/pirl
chmod 0755 /usr/bin/marlin

```


### अब vps को रिबूट करें.
```
reboot
```


ब्लॉकचैन के साथ सिंक्रनाइज़ होने वाली मास्टरनोड प्रक्रिया को देखने के लिए:
```
journalctl -f

```

आपका मास्टरनोड सिंक्रनाइज़ हो चुका है और नेटवर्क मे योगदान दे रहा है यदी आपकी स्क्रीन पर इस तरह दिख रहा हैः

```
  ########  masternode sending proof of activity to poseidon for block  3625046  please check poseidon.pirl.io for details  //  marlin version is gecko #########

```

निगरानी (मोनेटरींग)
हम सर्वर पर एैकटीव ऐकसेस को प्रोत्साहित नहीं करते हैं। फिर भी आप स्थिति की जाँच करना चाहते हैं, तो अपने सर्वर में लॉग इन करें और निम्नलिखित आदेश जारी करें:  
```
journalctl -f
```

पोस्याडॉन मास्टरनोड विवरण पृष्ठ की जाँच करके अपने मास्टर्नोड की स्थिति की निगरानी करें। एक नोड निम्नानुसार दिखाई देना चाहिए, हालांकि संस्करण स्क्रीन शॉट में दिखाए गए से भिन्न हो सकता है।

{{% notice warning %}}
अगर सिंक्रनाइज़ेशन नही हो रहा है तो डेटाबेस को निकालने के लिए इन निमनलिखीत का प्रयोग करे:
{{% /notice %}}  

- पहले टोकन का निर्यात करें:

```
export MASTERNODE=fzeffz-zefzef-zefze-zefze-zefzef-zefzef <<<---आपका टोकन यहां आता है
export TOKEN=zfzefezfzefzecfzegregkgeorgoerbvnijv <<<---आपका टोकन यहां आता है


```

यदि आपके पास यह फ़ाइल है  /etc/pirlnode-env, तो ऊपर दिऐ गये कदम निमनलिखीत तरीके से भी किये जा सकता है
```
. /etc/pirlnode-env && export MASTERNODE TOKEN

```


- और फिर डेटाबेस को हटा दें:  

```
pirl removedb

```

या आखिरी रास्ता:  

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
