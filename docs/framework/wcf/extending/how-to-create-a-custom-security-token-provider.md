---
title: "방법: 사용자 지정 보안 토큰 공급자 만들기 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "보안 [WCF], 자격 증명 제공"
ms.assetid: db8cb478-aa43-478b-bf97-c6489ad7c7fd
caps.latest.revision: 10
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 10
---
# 방법: 사용자 지정 보안 토큰 공급자 만들기
이 항목에서는 사용자 지정 보안 토큰 공급자를 사용하여 새 토큰 형식을 만드는 방법과 공급자를 사용자 지정 보안 토큰 관리자와 통합하는 방법에 대해 설명합니다.  
  
> [!NOTE]
>  <xref:System.IdentityModel.Tokens>에 있는 시스템 제공 토큰이 요구 사항에 맞지 않을 경우 사용자 지정 토큰 공급자를 만드세요.  
  
 보안 토큰 공급자는 클라이언트 또는 서비스 자격 증명의 정보를 기반으로 보안 토큰 표현을 만듭니다.  [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 보안에서 사용자 지정 보안 토큰 공급자를 사용하려면 사용자 지정 자격 증명과 보안 토큰 관리자 구현을 만들어야 합니다.  
  
 사용자 지정 자격 증명과 보안 토큰 관리자에 대한 자세한 내용은 [연습: 사용자 지정 클라이언트 및 서비스 자격 증명 만들기](../../../../docs/framework/wcf/extending/walkthrough-creating-custom-client-and-service-credentials.md)를 참조하세요.  
  
 자격 증명, 보안 토큰 관리자, 공급자 및 인증자 클래스에 대한 자세한 내용은 [Security Architecture](http://msdn.microsoft.com/ko-kr/16593476-d36a-408d-808c-ae6fd483e28f)를 참조하세요.  
  
### 사용자 지정 보안 토큰 공급자를 만들려면  
  
1.  <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 클래스에서 파생된 새 클래스를 정의합니다.  
  
2.  <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%28System.TimeSpan%29> 메서드를 구현합니다.  이 메서드는 보안 토큰의 인스턴스를 만들고 반환합니다.  다음 예제에서는 `MySecurityTokenProvider`라는 클래스를 만들고, <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%28System.TimeSpan%29> 메서드를 재정의하여 <xref:System.IdentityModel.Tokens.X509SecurityToken> 클래스의 인스턴스를 반환합니다.  클래스 생성자에 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> 클래스의 인스턴스가 필요합니다.  
  
     [!code-csharp[c_CustomTokenProvider#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenprovider/cs/source.cs#1)]
     [!code-vb[c_CustomTokenProvider#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenprovider/vb/source.vb#1)]  
  
### 사용자 지정 보안 토큰 공급자를 사용자 지정 보안 토큰 관리자와 통합하려면  
  
1.  <xref:System.IdentityModel.Selectors.SecurityTokenManager> 클래스에서 파생된 새 클래스를 정의합니다.  아래 예제는 <xref:System.IdentityModel.Selectors.SecurityTokenManager> 클래스에서 파생된 <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> 클래스에서 파생됩니다.  
  
2.  아직 재정의되지 않은 경우 <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenProvider%28System.IdentityModel.Selectors.SecurityTokenRequirement%29> 메서드를 재정의합니다.  
  
     <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenProvider%28System.IdentityModel.Selectors.SecurityTokenRequirement%29> 메서드는 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 보안 프레임워크에서 메서드로 전달한 <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> 매개 변수에 적합한 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 클래스의 인스턴스를 반환합니다.  적절한 보안 토큰 매개 변수를 사용하여 메서드를 호출할 때 이전 절차에서 만든 사용자 지정 보안 토큰 공급자 구현을 반환하도록 메서드를 수정합니다.  보안 토큰 관리자에 대한 자세한 내용은 [연습: 사용자 지정 클라이언트 및 서비스 자격 증명 만들기](../../../../docs/framework/wcf/extending/walkthrough-creating-custom-client-and-service-credentials.md)를 참조하세요.  
  
3.  메서드에 논리를 추가하여 <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> 매개 변수를 기반으로 사용자 지정 보안 토큰 공급자를 반환할 수 있도록 합니다.  다음 예제에서는 토큰 요구 사항에 맞을 경우 사용자 지정 보안 토큰 공급자를 반환합니다.  요구 사항에는 X.509 보안 토큰 및 토큰이 메시지 출력에 사용되는 메시지 방향이 포함됩니다.  다른 모든 경우에서 코드는 기본 클래스를 호출하여 다른 보안 토큰 요구 사항에 대한 시스템 제공 동작을 유지 관리합니다.  
  
 [!code-csharp[c_CustomTokenProvider#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenprovider/cs/source.cs#2)]
 [!code-vb[c_CustomTokenProvider#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenprovider/vb/source.vb#2)]  
  
## 예제  
 다음 예제에서는 해당 <xref:System.IdentityModel.Selectors.SecurityTokenManager> 구현과 함께 전체 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 구현을 보여 줍니다.  
  
 [!code-csharp[c_CustomTokenProvider#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenprovider/cs/source.cs#0)]
 [!code-vb[c_CustomTokenProvider#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenprovider/vb/source.vb#0)]  
  
## 참고 항목  
 <xref:System.IdentityModel.Selectors.SecurityTokenProvider>   
 <xref:System.IdentityModel.Selectors.SecurityTokenRequirement>   
 <xref:System.IdentityModel.Selectors.SecurityTokenManager>   
 <xref:System.IdentityModel.Tokens.X509SecurityToken>   
 [연습: 사용자 지정 클라이언트 및 서비스 자격 증명 만들기](../../../../docs/framework/wcf/extending/walkthrough-creating-custom-client-and-service-credentials.md)   
 [방법: 사용자 지정 보안 토큰 인증자 만들기](../../../../docs/framework/wcf/extending/how-to-create-a-custom-security-token-authenticator.md)   
 [Security Architecture](http://msdn.microsoft.com/ko-kr/16593476-d36a-408d-808c-ae6fd483e28f)