---
title: "사용자 지정 인코더 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fa0e1d7f-af36-4bf4-aac9-cd4eab95bc4f
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 사용자 지정 인코더
이 항목에서는 사용자 지정 인코더를 만드는 방법을 설명합니다.  
  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]에서는 *바인딩*을 사용하여 네트워크를 통해 끝점 간에 데이터를 전송하는 방법을 지정합니다.  바인딩은 일련의 *바인딩 요소*로 구성됩니다.  바인딩에는 선택적 프로토콜 바인딩 요소\(예: 보안\), 필수 *메시지 인코더* 바인딩 요소 및 필수 전송 바인딩 요소가 포함됩니다.  메시지 인코더는 메시지 인코딩 바인딩 요소로 표시됩니다.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에는 이진, MTOM\(Message Transmission Optimization Mechanism\) 및 텍스트의 세 가지 메시지 인코더가 포함되어 있습니다.  
  
 메시지 인코딩 바인딩 요소는 보내는 <xref:System.ServiceModel.Channels.Message>를 serialize한 다음 전송으로 전달하거나, 전송에서 serialize된 메시지 형식을 받은 다음 프로토콜 계층이 있으면 프로토콜 계층에 전달하고 없으면 응용 프로그램에 전달합니다.  
  
 메시지 인코더는 <xref:System.ServiceModel.Channels.Message> 인스턴스를 연결 표시로 또는 그 반대로 변환합니다.  인코더가 채널 스택에서 전송 계층 위에 있는 것으로 설명될지라도 전송 계층 내부에 있습니다.  전송\(예: HTTP\)은 전송 표준 요구 사항에 따라 메시지의 형식을 지정하며  인코더\(예: Text Xml\)는 단지 메시지를 인코딩합니다.  
  
 기존 클라이언트 또는 서버에 연결할 경우에는 특정 메시지 인코딩을 사용하지 못할 수 있습니다.  그러나 여러 끝점을 통해 각각 서로 다른 메시지 인코더를 사용하여 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스에 액세스할 수 있습니다.  단일 인코더가 서비스의 전체 대상을 수용하지 못하는 경우 여러 끝점을 통해 서비스를 공개해 보세요.  그러면 클라이언트 응용 프로그램에서 가장 적합한 끝점을 선택할 수 있습니다.  여러 끝점을 사용하면 여러 메시지 인코더의 이점을 다른 바인딩 요소와 결합할 수 있습니다.  
  
## 시스템 제공 인코더  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]는 가장 일반적인 응용 프로그램 시나리오를 다루도록 고안된 여러 개의 시스템 제공 바인딩을 제공합니다.  이러한 각 바인딩은 전송, 메시지 인코더 및 기타 옵션\(예: 보안\)을 결합합니다.  이 항목에서는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에 포함된 `Text`, `Binary` 및 `MTOM` 메시지 인코더를 확장하거나 고유의 사용자 지정 인코더를 만드는 방법에 대해 설명합니다.  텍스트 메시지 인코더는 일반 XML 인코딩뿐 아니라 SOAP 인코딩을 모두 지원합니다.  텍스트 메시지 인코더의 일반 XML 인코딩 모드는 텍스트 기반 SOAP 인코딩과 구별하기 위해 POX\("Plain Old Xml"\) 인코더라고 합니다.  
  
 시스템 제공 바인딩이 제공하는 여러 가지 바인딩 요소의 조합[!INCLUDE[crabout](../../../../includes/crabout-md.md)] [전송 선택](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)의 해당 단원을 참조하세요.  
  
## 시스템 제공 인코더 작업 방법  
 인코딩은 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>에서 파생된 클래스를 사용하여 바인딩에 추가됩니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 텍스트, 이진 및 MTOM\(Message Transmission Optimization Mechanism\) 인코딩에 제공할 수 있는 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> 클래스에서 파생된 다음과 같은 형식의 바인딩 요소를 제공합니다.  
  
-   <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>: 상호 운용성이 가장 뛰어나지만 XML 메시지에 대해서는 효율성이 가장 낮은 인코더입니다.  웹 서비스 또는 웹 서비스 클라이언트는 일반적으로 텍스트 XML을 이해할 수 있습니다.  대량의 이진 데이터 블록을 텍스트로 전송하는 것은 비효율적입니다.  
  
-   <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>: 이진 기반 XML 메시지에 사용되는 문자 인코딩 및 메시지 버전 관리를 지정하는 바인딩 요소를 나타냅니다.  가장 효율적인 인코딩 옵션인 반면 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 끝점에서만 지원하기 때문에 상호 운용성이 가장 낮습니다.  
  
-   <xref:System.ServiceModel.Channels.MTOMMessageEncodingBindingElement>: MTOM\(Message Transmission Optimization Mechanism\) 인코딩을 사용하여 메시지에 사용되는 문자 인코딩 및 메시지 버전 관리를 지정하는 바인딩 요소를 나타냅니다..  MTOM은 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 메시지의 이진 데이터를 효율적으로 전송하는 기술입니다.  MTOM 인코더는 효율성과 호환성 간의 균형을 유지하려고 합니다.  MTOM 인코딩은 대부분의 XML을 텍스트 형식으로 전송하지만, 큰 이진 데이터 블록의 경우에는 텍스트로 변환하지 않고 있는 그대로 전송하여 최적화합니다.  
  
 바인딩 요소는 이진, MTOM 또는 텍스트 <xref:System.ServiceModel.Channels.MessageEncoderFactory>를 만듭니다.  팩터리는 이진, MTOM 또는 텍스트 <xref:System.ServiceModel.Channels.MessageEncoder> 인스턴스를 만듭니다.  일반적으로 인스턴스는 하나만 있습니다.  그러나 세션을 사용하는 경우에는 세션마다 다른 인코더가 제공될 수 있습니다.  이진 인코더는 이를 사용하여 동적 사전을 조정합니다\(XML 인프라 참조\).  
  
 <xref:System.ServiceModel.Channels.MessageEncoder.ReadMessage%2A> 및 <xref:System.ServiceModel.Channels.MessageEncoder.WriteMessage%2A> 메서드는 인코더의 핵심입니다.  이러한 메서드를 사용하면 스트림 또는 <xref:System.Byte> 배열에서 메시지를 읽을 수 있습니다.  전송이 버퍼링 모드에서 작동할 때는 바이트 배열이 사용됩니다.  메시지는 항상 스트림에 기록됩니다.  메시지를 버퍼링해야 하는 경우 전송은 버퍼링을 수행하는 스트림을 제공합니다.  
  
 나머지 멤버는 지원 콘텐츠, 미디어 유형 및 <xref:System.ServiceModel.Channels.MessageEncoder.MessageVersion%2A>과 함께 작동합니다.  전송에서는 이러한 인코더 메서드를 호출하여 들어오는 메시지를 디코딩할 수 있는지 여부를 테스트하거나 보내는 메시지가 이 인코더에 유효한지를 확인합니다.  
  
 세 가지 각 인코더 구현은 특정 인코딩과 관련된 속성을 추가하며 완전히 구성 가능합니다.  인코더는 또한 보안 기본값을 갖는 판독기 할당량을 공개합니다.  할당량에 대한 자세한 내용은 XML 인프라를 참조하세요.  
  
## 시스템 제공 인코더의 기능  
 시스템 제공 인코더는 다양한 기능을 제공합니다.  
  
### Pooling  
 각 인코더 구현에서는 가능한 한 많이 풀링하려고 합니다.  관리 코드의 성능을 향상시키기 위한 주요 방법은 할당을 줄이는 것입니다.  이 풀링을 수행하기 위해 구현에서는 `SynchronizedPool` 클래스를 사용합니다.  C\# 파일에는 이 클래스에서 사용하는 추가 최적화에 대한 설명이 포함되어 있습니다.  
  
 `XmlDictionaryReader` 및 `XmlDictionaryWriter` 인스턴스를 풀링하고 다시 초기화하여 각 메시지의 새 인스턴스가 할당되지 않도록 합니다.  판독기의 경우 `Close()`가 호출될 때 `OnClose` 콜백이 판독기를 회수합니다.  인코더는 또한 메시지를 구성할 때 사용된 일부 메시지 상태 개체를 재활용합니다.  이러한 풀의 크기는 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>에서 파생된 세 가지 각 클래스에 대한 `MaxReadPoolSize` 및 `MaxWritePoolSize` 속성으로 구성할 수 있습니다.  
  
### 이진 인코딩  
 이진 인코딩에서 세션을 사용하는 경우 동적 사전 문자열을 메시지 수신자에게 전달해야 합니다.  이 작업은 동적 사전 문자열을 메시지의 접두사로 지정하여 수행합니다.  수신자는 문자열을 제거하여 세션에 추가한 다음 메시지를 처리합니다.  사전 문자열을 올바르게 전달하려면 전송을 버퍼링해야 합니다.  
  
 문자열은 내부 `AddSessionInformationToMessage` 메서드에 의해 메시지에 추가됩니다.  이 메서드는 해당 문자열의 길이로 접두사가 지정된 메시지 앞에 문자열을 UTF\-8로 추가합니다.  그런 다음 이 데이터의 길이를 전체 사전 헤더의 접두사로 지정합니다.  이 반대 작업은 내부 `ExtractSessionInformationFromMessage` 메서드에 의해 수행됩니다.  
  
 동적 사전 키를 처리하는 이외에도 성공적으로 버퍼링된 메시지를 고유한 방식으로 수신합니다.  이진 인코더는 문서에 대한 판독기를 만들어 문서를 처리하는 대신 내부 `MessagePatterns` 클래스를 사용하여 이진 스트림을 해체합니다.  대부분의 메시지에는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서 생성된 순서대로 표시되는 특정 헤더 집합이 있습니다.  패턴 시스템은 필요에 따라 메시지를 분리합니다.  성공하면 XML을 구문 분석하지 않고 <xref:System.ServiceModel.Channels.MessageHeaders> 개체를 초기화합니다.  실패하면 표준 메서드로 변경됩니다.  
  
### MTOM 인코딩  
 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> 클래스에는 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement.MaxBufferSize%2A>라는 추가 구성 속성이 있습니다.  이 속성은 메시지를 읽는 동안 버퍼링할 수 있는 데이터의 크기에 대한 상한을 지정합니다.  모든 MIME 부분을 단일 메시지로 다시 어셈블하려면 XML Infoset\(정보 집합\) 또는 다른 MIME 부분을 버퍼링해야 할 수도 있습니다.  
  
 HTTP에서 올바로 작동하기 위해 내부 MTOM 메시지 인코더 클래스는 내부 `GetContentType` 및 public이며 재정의 가능한 `WriteMessage`에 대한 몇 가지 내부 API를 제공합니다.  HTTP 헤더의 값과 MIME 헤더의 값이 일치하려면 더 많은 통신이 수행되어야 합니다.  
  
 내부적으로 MTOM 메시지 인코더는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]의 텍스트 판독기를 사용하며 텍스트 인코더와 비슷합니다.  주된 차이점은 MTOM 메시지 인코더는 대량의 이진, 즉 "BLOB"\(Binary Large Object\)를 메시지 바이트에 포함하기 전에 Base\-64 인코딩으로 변환하지 않음으로써 최적화한다는 데 있습니다.  대신 이러한 BLOB는 추출되어 MIME 첨부 파일로 참조됩니다.  
  
## 사용자 고유의 인코더 작성  
 사용자 지정 메시지 인코더를 구현하려면 다음 추상 기본 클래스에 대한 사용자 지정 구현을 제공해야 합니다.  
  
-   <xref:System.ServiceModel.Channels.MessageEncoder>  
  
-   <xref:System.ServiceModel.Channels.MessageEncoderFactory>  
  
-   <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>  
  
 메시지의 메모리 내 표현을 스트림에 기록할 수 있는 표현으로 변환하여 <xref:System.ServiceModel.Channels.MessageEncoder> 클래스 내에 캡슐화합니다. 이 클래스는 특정 유형의 XML 인코딩을 지원하는 XML 판독기 및 XML 작성기의 팩터리 역할을 합니다.  
  
-   재정의해야 하는 이 클래스의 주요 메서드는 다음과 같습니다.  
  
-   <xref:System.ServiceModel.Channels.MessageEncoder.WriteMessage%2A> \- <xref:System.ServiceModel.Channels.Message> 개체를 가져와서 <xref:System.IO.Stream> 개체에 씁니다.  
  
-   <xref:System.ServiceModel.Channels.MessageEncoder.ReadMessage%2A> \- <xref:System.IO.Stream> 개체와 최대 헤더 크기를 가져오고 <xref:System.ServiceModel.Channels.Message> 개체를 반환합니다.  
  
 이러한 메서드에 작성하는 코드로, 표준 전송 프로토콜과 사용자 지정 인코딩 간의 변환을 처리합니다.  
  
 다음으로는 사용자 지정 인코더를 만드는 팩터리 클래스를 코딩해야 합니다.  사용자 지정 <xref:System.ServiceModel.Channels.MessageEncoder>의 인스턴스를 반환하도록 <xref:System.ServiceModel.Channels.MessageEncoderFactory.Encoder%2A>를 재정의합니다.  
  
 그런 다음 이 팩터리의 인스턴스를 반환하도록 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.CreateMessageEncoderFactory%2A> 메서드를 재정의하여 서비스 또는 클라이언트를 구성하는 데 사용되는 바인딩 요소 스택에 사용자 지정 <xref:System.ServiceModel.Channels.MessageEncoderFactory>를 연결합니다.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]에서는 샘플 코드를 사용하여 이 프로세스를 설명하는 두 가지 샘플 [Custom Message Encoder: Custom Text Encoder](../../../../docs/framework/wcf/samples/custom-message-encoder-custom-text-encoder.md) 및 [사용자 지정 메시지 인코더: 압축 인코더](../../../../docs/framework/wcf/samples/custom-message-encoder-compression-encoder.md)를 제공합니다.  
  
## 참고 항목  
 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>   
 <xref:System.ServiceModel.Channels.MessageEncoderFactory>   
 <xref:System.ServiceModel.Channels.MessageEncoder>   
 [데이터 전송 아키텍처 개요](../../../../docs/framework/wcf/feature-details/data-transfer-architectural-overview.md)   
 [메시지 인코더 선택](../../../../docs/framework/wcf/feature-details/choosing-a-message-encoder.md)   
 [전송 선택](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)