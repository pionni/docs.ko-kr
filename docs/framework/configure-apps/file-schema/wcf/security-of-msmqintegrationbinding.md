---
title: "&lt;msmqIntegrationBinding&gt;의 &lt;security&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ae5c68a8-14a2-4c6e-b9e0-3e94e3e9135e
caps.latest.revision: 13
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 13
---
# &lt;msmqIntegrationBinding&gt;의 &lt;security&gt;
MSMQ\(메시지 큐\) 통합 채널을 위한 전송 보안 설정을 정의합니다.  
  
## 구문  
  
```  
  
<msmqIntegrationBinding>  
   <binding>   
       <security mode="None/Transport">  
         <transport msmqAuthenticationMode="None/Windows/Certificate"  
            msmqEncryptionAlgorithm="RC4Stream/AES"  
            msmqProtectionLevel="None/Sign/EncryptAndSign"  
            msmqSecureHashAlgorithm="MD5/SHA1/SHA256/SHA512" />  
          <message  algorithmSuite="Aes128/Aes192/Aes256/Rsa15Aes128/ Rsa15Aes256/TripleDes"  
                        clientCredentialType="None/Windows/UserName/Certificate/CardSpace"  
            defaultProtectionLevel="None/Sign/EncryptAndSign" />  
       </security>  
   </binding>  
</msmqIntegrationBinding>   
```  
  
## 특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### 특성  
  
|특성|설명|  
|--------|--------|  
|모드|메시지 큐 통합 채널로 무결성, 기밀성 및 인증을 제어하는 보안 형식을 지정합니다.  유효한 값은 다음과 같습니다.<br /><br /> -   None: 보안을 사용할 수 없게 합니다.<br />-   Transport: 보호 및 인증이 전송에 의해 제공됩니다.  이는 두 큐 관리자 간의 메시지 보안에 적용됩니다.  응용 프로그램 및 큐 관리자 간에는 제공되는 보안이 없습니다.  기존 Msmq 응용 프로그램이 이러한 보안 모드 형식과 동일한 기능입니다.<br /><br /> 기본값은 `Transport`입니다.  이 특성은 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationSecurityMode> 형식입니다.|  
  
### 자식 요소  
  
|요소|설명|  
|--------|--------|  
|[\<transport\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-msmqintegrationbinding.md)|메시지 큐 통합 전송을 위한 보안 설정을 정의합니다.  이 요소는 <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement> 형식입니다.|  
  
### 부모 요소  
  
|요소|설명|  
|--------|--------|  
|[\<binding\>](../../../../../docs/framework/misc/binding.md)|[\<msmqIntegrationBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/msmqintegrationbinding.md)의 바인딩 요소입니다.|  
  
## 참고 항목  
 <xref:System.ServiceModel.Configuration.MsmqIntegrationSecurityElement>   
 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding.Security%2A>   
 <xref:System.ServiceModel.Configuration.MsmqIntegrationBindingElement.Security%2A>   
 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationSecurity>   
 [WCF의 큐](../../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)   
 [서비스 및 클라이언트에 보안 설정](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [바인딩](../../../../../docs/framework/wcf/bindings.md)   
 [시스템 제공 바인딩 구성](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/ko-kr/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<binding\>](../../../../../docs/framework/misc/binding.md)   
 [\<msmqIntegrationBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/msmqintegrationbinding.md)