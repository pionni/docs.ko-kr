---
title: "&lt;wsDualHttpBinding&gt;의 &lt;security&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 869c05e7-4ebe-467d-95ab-c8f8de4e6b9e
caps.latest.revision: 15
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 15
---
# &lt;wsDualHttpBinding&gt;의 &lt;security&gt;
[\<wsDualHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md)의 보안 기능을 정의합니다.  
  
## 구문  
  
```  
  
<security mode="Message/None">  
   <message  
      algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
      clientCredentialType="Certificate/IssuedToken/None/UserName/Windows"  
      negotiateServiceCredential="Boolean"/>  
</security>  
```  
  
## 특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### 특성  
  
|특성|설명|  
|--------|--------|  
|모드|-   선택 사항입니다.  적용되는 보안 형식을 지정합니다.  기본값은 `Message`입니다.  이 특성은 <xref:System.ServiceModel.WSDualHttpSecurityMode> 형식입니다.|  
  
## Mode 특성  
  
|값|설명|  
|-------|--------|  
|없음|보안이 해제되어 있습니다.|  
|메시지|SOAP 메시지 보안을 사용하여 보안이 제공됩니다.|  
  
### 자식 요소  
  
|요소|설명|  
|--------|--------|  
|[\<message\>](../../../../../docs/framework/configure-apps/file-schema/wcf/message-of-wsdualhttpbinding.md)|메시지 수준 보안 설정을 정의합니다.  이 요소는 <xref:System.ServiceModel.MessageSecurityOverHttp> 형식입니다.|  
  
### 부모 요소  
  
|요소|설명|  
|--------|--------|  
|[\<binding\>](../../../../../docs/framework/misc/binding.md)|[\<wsDualHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md)의 모든 바인딩 기능을 정의합니다.|  
  
## 설명  
 이중 바인딩은 클라이언트의 IP 주소를 서비스에 노출합니다.  클라이언트는 보안을 사용하여 신뢰하는 서비스에만 연결해야 합니다.  
  
## 참고 항목  
 <xref:System.ServiceModel.WSDualHttpSecurity>   
 <xref:System.ServiceModel.WsDualHttpBinding.Security%2A>   
 <xref:System.ServiceModel.Configuration.WsDualHttpBindingElement.Security%2A>   
 <xref:System.ServiceModel.Configuration.WsDualHttpSecurityElement>   
 <xref:System.ServiceModel.BasicHttpSecurity>   
 [서비스 및 클라이언트에 보안 설정](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [바인딩](../../../../../docs/framework/wcf/bindings.md)   
 [시스템 제공 바인딩 구성](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/ko-kr/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<binding\>](../../../../../docs/framework/misc/binding.md)