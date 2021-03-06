---
title: "WCF 서비스를 사용한 ASMX 클라이언트 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3ea381ee-ac7d-4d62-8c6c-12dc3650879f
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# WCF 서비스를 사용한 ASMX 클라이언트
이 샘플에서는 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]를 사용하여 서비스를 만든 다음 ASMX 클라이언트와 같은 비[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 클라이언트에서 서비스에 액세스하는 방법을 보여 줍니다.  
  
> [!NOTE]
>  이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 이 샘플은 IIS\(인터넷 정보 서비스\)에 의해 호스팅되는 클라이언트 콘솔 프로그램\(.exe\) 및 서비스 라이브러리\(.dll\)로 구성됩니다.이 서비스는 요청\-회신 통신 패턴을 정의하는 계약을 구현합니다.계약은 수학 연산\(`Add`, `Subtract`, `Multiply` 및 `Divide`\)을 노출하는 `ICalculator` 인터페이스에 의해 정의됩니다.ASMX 클라이언트에서 수학 작업을 동기적으로 요청하면 서비스에서 결과로 회신합니다.  
  
 서비스는 다음 코드에 정의된 대로 `ICalculator` 계약을 구현합니다.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples"), XmlSerializerFormat]  
public interface ICalculator  
{  
    [OperationContract]  
    double Add(double n1, double n2);  
    [OperationContract]  
    double Subtract(double n1, double n2);  
    [OperationContract]  
    double Multiply(double n1, double n2);  
    [OperationContract]  
    double Divide(double n1, double n2);  
}  
  
```  
  
 <xref:System.Runtime.Serialization.DataContractSerializer> 및 <xref:System.Xml.Serialization.XmlSerializer>는 CLR 형식을 XML 표현에 매핑합니다.<xref:System.Runtime.Serialization.DataContractSerializer>에서는 일부 XML 표현을 XmlSerializer와 다르게 해석합니다.Wsdl.exe와 같은 비[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 프록시 생성기에서는 XmlSerializer를 사용하는 경우에 좀더 사용하기 좋은 인터페이스를 생성합니다.<xref:System.ServiceModel.XmlSerializerFormatAttribute>는 CLR 형식을 XML에 매핑하는 데 XmlSerializer를 사용하도록 `ICalculator` 인터페이스에 적용됩니다.이 서비스 구현에서는 해당 결과를 계산하여 반환합니다.  
  
 서비스에서는 구성 파일\(Web.config\)을 사용하여 서비스와 통신하기 위한 단일 끝점을 노출합니다.끝점은 하나의 주소, 바인딩 및 계약으로 구성됩니다.서비스에서는 IIS\(인터넷 정보 서비스\) 호스트에서 제공되는 기본 주소에서 끝점을 노출합니다.`binding` 특성은 다음 샘플 구성에 표시된 것과 같이 WS\-I BasicProfile 1.1과 호환되는 SOAP 1.1을 사용하는 HTTP 통신을 제공하는 basicHttpBinding으로 설정됩니다.  
  
```  
<services>  
   <service   
       name="Microsoft.ServiceModel.Samples.CalculatorService"  
       behaviorConfiguration="CalculatorServiceBehavior">  
       <!-- This endpoint is exposed at the base address provided by the host: http://localhost/servicemodelsamples/service.svc.  -->  
      <endpoint address=""  
               binding="basicHttpBinding"   
               contract="Microsoft.ServiceModel.Samples.ICalculator" />  
   </service>  
</services>  
  
```  
  
 ASMX 클라이언트에서는 WSDL\(웹 서비스 기술 언어\) 유틸리티\(Wsdl.exe\)에서 생성되는, 형식이 지정된 프록시를 사용하여 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 서비스와 통신합니다.형식이 지정된 프록시는 generatedClient.cs 파일에 포함되어 있습니다.WSDL 유틸리티는 지정된 서비스의 메타데이터를 검색하여 통신할 클라이언트에서 사용되는, 형식이 지정된 프록시를 생성합니다.기본적으로 프레임워크에서는 메타데이터를 노출하지 않습니다.프록시 생성에 필요한 메타데이터를 노출하려면 [\<serviceMetadata\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicemetadata.md)를 추가하고 다음 구성에 표시된 것과 같이 `httpGetEnabled` 특성을 `True`로 설정해야 합니다.  
  
```  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      <!-- Setting httpGetEnabled to True on the serviceMetadata  
           behavior exposes the service's wsdl at <base address>?wsdl :  
           http://localhost/servicemodelsamples/service.svc?wsdl -->  
      <serviceMetadata httpGetEnabled="True"/>  
      <serviceDebug includeExceptionDetailInFaults="False" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 클라이언트 디렉터리의 명령 프롬프트에서 다음 명령을 실행하여 형식화된 프록시를 생성합니다.  
  
```  
wsdl /n:Microsoft.ServiceModel.Samples /o:generatedClient.cs /urlkey:CalculatorServiceAddress http://localhost/servicemodelsamples/service.svc?wsdl  
  
```  
  
 생성된, 형식이 지정된 프록시를 사용하면 클라이언트에서 적절한 주소를 구성하여 지정된 서비스 끝점에 액세스할 수 있습니다.클라이언트에서는 구성 파일\(App.config\)을 사용하여 통신할 끝점을 지정합니다.  
  
```  
<appSettings>  
      <add key="CalculatorServiceAddress"   
      value="http://localhost/ServiceModelSamples/service.svc"/>  
</appSettings>  
  
```  
  
 클라이언트 구현에서는 형식이 지정된 프록시의 인스턴스를 구성하여 서비스와의 통신을 시작합니다.  
  
```  
// Create a client to the CalculatorService.  
using (CalculatorService client = new CalculatorService())  
{  
    // Call the Add service operation.  
    double value1 = 100.00D;  
    double value2 = 15.99D;  
    double result = client.Add(value1, value2);  
    Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
    // Call the Subtract service operation.  
    value1 = 145.00D;  
    value2 = 76.54D;  
    result = client.Subtract(value1, value2);  
    Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);  
  
    // Call the Multiply service operation.  
    value1 = 9.00D;  
    value2 = 81.25D;  
    result = client.Multiply(value1, value2);  
    Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);  
  
    // Call the Divide service operation.  
    value1 = 22.00D;  
    value2 = 7.00D;  
    result = client.Divide(value1, value2);  
    Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
  
}  
  
Console.WriteLine();  
Console.WriteLine("Press <ENTER> to terminate client.");  
Console.ReadLine();  
  
```  
  
 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다.클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
  
```  
  
### 샘플을 설치, 빌드 및 실행하려면  
  
1.  [Windows Communication Foundation 샘플의 일회 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행했는지 확인합니다.  
  
2.  C\# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3.  단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따릅니다.  
  
> [!NOTE]
>  복합 데이터 형식을 전달하고 반환하는 방법[!INCLUDE[crabout](../../../../includes/crabout-md.md)][Windows 폼 클라이언트 내 데이터 바인딩](../../../../docs/framework/wcf/samples/data-binding-in-a-windows-forms-client.md), [Wndows Presentation Foundation 클라이언트에서 데이터 바인딩](../../../../docs/framework/wcf/samples/data-binding-in-a-wpf-client.md) 및 [ASP.NET 클라이언트에서 데이터 바인딩](../../../../docs/framework/wcf/samples/data-binding-in-an-aspnet-client.md)을 참조하십시오.  
  
> [!IMPORTANT]
>  컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다.계속하기 전에 다음\(기본\) 디렉터리를 확인하십시오.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  이 디렉터리가 없으면 [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780)로 이동하여 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 모두 다운로드하십시오.이 샘플은 다음 디렉터리에 있습니다.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Interop\ASMX`  
  
## 참고 항목