---
title: मास्टरनोड स्टेक को पुनः प्राप्त करें
weight: 2
pre: "<b>2. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/Masternodes.png" >}}

## अवलोकन

आप किसी भी समय केवल दो मास्टरनोड कॉन्ट्रैक्ट चला के अपने 10,000 प्रिल अपने वैलेट में वापस प्राप्त कर सकते हैं।

## मास्टरनोड को निष्क्रिय करना और स्टेक को पुनः प्राप्त करना

**नॉटिलस खोलें** और ऊपरी दाएं कोने पर स्थित **कॉन्ट्रैक्ट** टैब पर जाएं।

आपको बाईं तरफ मे मास्टरनोड कॉन्ट्रैक्ट दिखेगा। इसका एड्रेस होगा `0x6c042141C302C354509d2bff30EEFDEF24dE1047`. इस एड्रेस का चयन करें।

> **नोट** यदि आपके पास **वॉच कॉन्ट्रैक्ट** सेक्शन में कोई कॉन्ट्रैक्ट नहीं दिख रहा है, तो आप इसे अगले सेक्शन में बताए अनुसार जोड़ सकते हैं।

दाईं ओर, कॉन्ट्रैक्ट फ़ंक्शन मेनू दिखायी देगा।

**डिसेबल नोड** फ़ंक्शन का चयन करें, फिर कॉन्ट्रैक्ट से संबंधित वैलेट चुने और फिर **एकझिक्युट** करें

<div align="center"><div style="width:55%;">{{< imagesurlsheaders "cloud/disable-node.png" >}}</div></div>

अगली स्क्रीन पर, पुष्टि करें कि आपके पास लेन-देन के लिए पर्याप्त **गैस** है, अपना **UTC फ़ाइल पासवर्ड** दर्ज करें और फिर **ट्रांसेक्शन भेजें**.

<div align="center"><div style="width:55%;">{{< imagesurlsheaders "cloud/disable-node2.png" >}}</div></div>

अगला चरण से पहले 30-60 सेकंड इंतज़ार करे।

**विथड्रा स्टेक** फंक्शन को चुने फिर कॉन्ट्रैक्ट से जुड़े वॉलेट चुने और **एकझिक्युट** हिट करें।

<div align="center"><div style="width:55%;">{{< imagesurlsheaders "cloud/withdraw-stake.png" >}}</div></div>

अगली स्क्रीन पर, पुष्टि करें कि आपके पास लेन-देन के लिए पर्याप्त **गैस** है, अपना **UTC फ़ाइल पासवर्ड** दर्ज करें और फिर **ट्रांसेक्शन भेजें**.

<div align="center"><div style="width:55%;">{{< imagesurlsheaders "cloud/disable-node2.png" >}}</div></div>

### पर्याप्त गैस नहीं है।

कभी-कभी वैलेट लेनदेन के लिए आवश्यक गैस की गणना करने में असमर्थ हो जाएगा और स्वचालित रूप से इसे 0 पर सेट कर देगा। इस स्थिति में, आप मैन्युअल रूप से समायोजित कर सकते हैं। जहां 0 लिखा है वहा क्लिक करके नयी राशि लिखें। इस उद्देश्य के लिए गैस की एक अच्छी मात्रा **121,000** है।

<div align="center"><div style="width:55%;">{{< imagesurlsheaders "cloud/confirm-gas.png" >}}</div></div>

## नॉटिलस में मास्टरनोड कॉन्ट्रैक्ट जोड़ना

**नॉटिलस खोलें** और ऊपरी दाएं कोने पर स्थित **कॉन्ट्रैक्ट** टैब पर जाएं।

![](https://cdn-images-1.medium.com/max/1600/0*OW_7W9P_u0k7ZdmZ.png)

और फिर **वॉच कॉन्ट्रैक्ट** बटन पर क्लिक करें।

![](https://cdn-images-1.medium.com/max/1600/0*wZbZlfAdjrUuhr53.png)

**कॉन्ट्रैक्ट एड्रेस** मे भरें `0x6c042141C302C354509d2bff30EEFDEF24dE1047`. **कॉन्ट्रैक्ट नाम** कुछ भी हो सकता है।  और अंत में  **JSON इंटरफ़ेस क्षेत्र** निमनलिखित भर देः

```
[{"constant":false,"inputs":[],"name":"nodeRegistration","outputs":[{"name":"paid","type":"bool"}],"payable":true,"stateMutability":"payable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeAddress","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"moderators","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"nodes","outputs":[{"name":"pirlAddress","type":"address"},{"name":"nodeStake","type":"uint256"},{"name":"nodeHash","type":"bytes20"},{"name":"stakeLocked","type":"bool"},{"name":"nodeEnabled","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNodeRegistration","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeCost","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getStakeLockedStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeCount","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"_admin","type":"address"}],"name":"setAdmin","outputs":[{"name":"set","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"owner","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNode","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeRegistrationEnabled","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNode","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[],"name":"withdrawStake","outputs":[{"name":"withdrawn","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"","type":"uint256"}],"name":"nodeAddresses","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeEnabledStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeStake","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNodeRegistration","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeHash","outputs":[{"name":"","type":"bytes20"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeFee","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"admin","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"inputs":[],"payable":false,"stateMutability":"nonpayable","type":"constructor"},{"payable":true,"stateMutability":"payable","type":"fallback"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeRegistered","type":"bool"},{"indexed":false,"name":"_dateRegistered","type":"uint256"}],"name":"MasterNodeRegistered","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeDisabled","type":"bool"},{"indexed":false,"name":"_dateDisabled","type":"uint256"}],"name":"MasterNodeDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeEnabled","type":"bool"},{"indexed":false,"name":"_dateEnabled","type":"uint256"}],"name":"MasterNodeEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodePaid","type":"bool"},{"indexed":false,"name":"_datePaid","type":"uint256"}],"name":"MasterNodeRewarded","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_stakeWithdrawn","type":"bool"},{"indexed":false,"name":"_dateWithdrawn","type":"uint256"}],"name":"StakeWithdrawn","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateEnabled","type":"uint256"},{"indexed":true,"name":"_registrationEnabled","type":"bool"}],"name":"MasterNodeRegistrationEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateDisabled","type":"uint256"},{"indexed":true,"name":"_registrationDisabled","type":"bool"}],"name":"MasterNodeRegistrationDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_admin","type":"address"},{"indexed":true,"name":"_adminSet","type":"bool"}],"name":"SetAdmin","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_newOwner","type":"address"},{"indexed":true,"name":"_ownerChanged","type":"bool"}],"name":"TransferOwnership","type":"event"}]

```

---
Author(s):

@Dptelecom

Contributor(s):
