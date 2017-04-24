---
title: "찾기 및 FindCriteria | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 99016fa4-1778-495b-b4cc-0e22fbec42c6
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 찾기 및 FindCriteria
찾기 작업은 하나 이상의 서비스를 검색하는 클라이언트에 의해 시작되며 검색 작업의 주요 동작 중 하나입니다.찾기를 수행하면 네트워크를 통해 WS\-Discovery Probe 메시지가 보내집니다.지정된 조건과 일치하는 서비스는 WS\-Discovery ProbeMatch 메시지를 사용하여 응답합니다.검색 메시지에 대한 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]는 [WS\-Discovery 사양](http://go.microsoft.com/fwlink/?LinkID=122347)\(영문 페이지일 수 있음\)을 참조하십시오.  
  
## DiscoveryClient  
 <xref:System.ServiceModel.Discovery.DiscoveryClient> 클래스는 찾기 작업을 수행하는 메커니즘을 제공하고 검색 클라이언트 작업을 손쉽게 수행할 수 있게 합니다.여기에는 동기\(블로킹\) 찾기를 수행하는 <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> 메서드와 비동기\(비블로킹\) 찾기를 시작하는 <xref:System.ServiceModel.Discovery.DiscoveryClient.FindAsync%2A> 메서드가 포함됩니다.두 메서드는 모두 <xref:System.ServiceModel.Discovery.FindCriteria> 매개 변수를 사용하며 <xref:System.ServiceModel.Discovery.FindResponse> 개체를 통해 결과를 사용자에게 제공합니다.  
  
## FindCriteria  
 <xref:System.ServiceModel.Discovery.FindCriteria>에는 찾을 서비스를 지정하는 검색 조건 및 검색 지속 기간을 지정하는 찾기 종료 조건으로 그룹화할 수 있는 여러 속성이 있습니다.<xref:System.ServiceModel.Discovery.FindCriteria>에는 여러 개의 검색 조건이 포함되어 있을 수 있습니다.기본적으로 서비스는 이러한 모든 검색 조건과 일치해야 합니다. 그렇지 않으면 스스로를 일치하는 서비스로 간주하지 않습니다.일부 조건만 일치하는 서비스를 찾으려면 서비스에 대해 사용자 지정 찾기 논리를 구현하거나 여러 쿼리를 사용하면 됩니다.  
  
 검색 조건은 다음과 같습니다.  
  
-   <xref:System.ServiceModel.Discovery.ContractTypeNames%2A> \- 선택적 요소로서,검색할 서비스의 계약 이름이거나 서비스를 검색할 때 일반적으로 사용되는 조건입니다.둘 이상의 계약 이름이 지정되면 모든 계약과 일치하는 서비스 끝점만 응답합니다.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 하나의 끝점이 하나의 계약만 지원할 수 있습니다.  
  
-   <xref:System.ServiceModel.Discovery.Scopes%2A> \- 선택적 요소로서,개별 서비스 끝점을 분류하는 데 사용되는 절대 URI입니다.여러 끝점이 동일한 계약을 노출하는 상태에서 끝점의 하위 집합을 검색하려는 경우 이 조건을 사용할 수 있습니다.둘 이상의 범위가 지정되면 모든 범위와 일치하는 서비스 끝점만 응답합니다.  
  
-   <xref:System.ServiceModel.Discovery.ScopeMatchBy%2A> \- Probe 메시지의 범위와 끝점의 범위를 일치시키는 동안 사용할 일치 알고리즘을 지정합니다.다음과 같은 다섯 가지 범위 일치 규칙이 지원됩니다.  
  
    -   <xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByExact%2A>는 기본 대\/소문자 구분 문자열 비교를 수행합니다.  
  
    -   <xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByPrefix%2A>는 “\/”로 구분된 세그멘트별로 일치시킵니다.예를 들어 http:\/\/contoso\/building1을 검색하면 범위가 http:\/\/contoso\/building\/floor1인 서비스가 일치하는 항목으로 검색됩니다.http:\/\/contoso\/building100은 마지막 두 세그먼트가 일치하지 않으므로 일치하는 항목으로 검색되지 않습니다.  
  
    -   <xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByLdap%2A>는 LDAP URL을 사용하여 세그먼트별로 범위를 일치시킵니다.  
  
    -   <xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByUuid%2A>는 UUID 문자열을 사용하여 범위를 정확히 일치시킵니다.  
  
    -   <xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByNone%2A>은 범위를 지정하지 않은 서비스만 일치시킵니다.  
  
     범위 일치 규칙이 지정되지 않은 경우 <xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByPrefix%2A>가 사용됩니다.  
  
 종료 조건은 다음과 같습니다.  
  
1.  <xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A> \- 네트워크에서 서비스의 응답을 기다리는 최대 시간입니다.기본 시간은 20초입니다.  
  
2.  <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> \- 기다릴 응답의 최대 수입니다.<xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A>이 경과하기 전에 <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> 응답을 받으면 찾기 작업이 종료됩니다.  
  
## FindResponse  
 <xref:System.ServiceModel.Discovery.FindResponse>에는 네트워크에서 일치하는 서비스가 보낸 응답을 포함하는 <xref:System.ServiceModel.Discovery.FindResponse.Endpoints%2A> 컬렉션 속성이 있습니다.응답하는 서비스가 없으면 컬렉션이 비어 있습니다.하나 이상의 서비스가 응답하면 서비스 주소 및 계약을 비롯한 서비스에 대한 일부 추가 정보가 포함된 <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> 개체에 각 응답이 저장됩니다.  
  
 다음 예제에서는 코드에서 찾기 작업을 수행하는 방법을 보여 줍니다.  
  
```  
// Create DiscoveryClient  
DiscoveryClient discoveryClient = new DiscoveryClient(new UdpDiscoveryEndpoint());  
  
// Create FindCriteria  
FindCriteria findCriteria = new FindCriteria(typeof(IPrinterService));  
findCriteria.Scopes.Add(new Uri("http://www.contoso.com/building1/floor1"));  
findCriteria.Duration = TimeSpan.FromSeconds(10);   
  
// Find ICalculatorService endpoints              
FindResponse findResponse = discoveryClient.Find(findCriteria);  
  
Console.WriteLine("Found {0} ICalculatorService endpoint(s).", findResponse.Endpoints.Count)  
  
```  
  
## 참고 항목  
 [WCF Discovery 개요](../../../../docs/framework/wcf/feature-details/wcf-discovery-overview.md)   
 [Discovery 클라이언트 채널 사용](../../../../docs/framework/wcf/feature-details/using-the-discovery-client-channel.md)   
 [범위를 사용한 검색](../../../../docs/framework/wcf/samples/discovery-with-scopes-sample.md)   
 [비동기 찾기](../../../../docs/framework/wcf/samples/asynchronous-find-sample.md)   
 [Basic](../../../../docs/framework/wcf/samples/basic-sample.md)