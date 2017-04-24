---
title: "TCP 활성화 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bf8c215c-0228-4f4f-85c2-e33794ec09a7
caps.latest.revision: 34
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 34
---
# TCP 활성화
이 샘플에서는 net.tcp 프로토콜을 통해 통신하는 서비스를 활성화하기 위해 WAS\(Windows Process Activation Service\)를 사용하는 서비스를 호스트하는 방법을 보여 줍니다.  이 샘플은 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)을 기반으로 합니다.  
  
> [!NOTE]
>  이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
> [!IMPORTANT]
>  컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다.  계속하기 전에 다음\(기본\) 디렉터리를 확인하세요.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  이 디렉터리가 없으면 [.NET Framework 4용 WCF\(Windows Communication Foundation\) 및 Windows WF\(Workflow Foundation\) 샘플](http://go.microsoft.com/fwlink/?LinkId=150780)\(영문\)로 이동하여 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 모두 다운로드하세요.  이 샘플은 다음 디렉터리에 있습니다.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WASHost\TCPActivation`  
  
 이 샘플은 WAS에 의해 활성화된 작업자 프로세스에서 호스트되는 서비스 라이브러리\(.dll\) 및 클라이언트 콘솔 프로그램\(.exe\)으로 구성됩니다.  콘솔 창에는 클라이언트 동작이 표시됩니다.  
  
 이 서비스는 요청\-회신 통신 패턴을 정의하는 계약을 구현합니다.  다음 샘플 코드와 같이 계약은 수학 작업\(Add, Subtract, Multifly 및 Divide\)을 노출시키는 `ICalculator` 인터페이스에 의해 정의됩니다.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
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
  
 서비스 구현에서는 해당 결과를 계산하여 반환합니다.  
  
```  
// Service class that implements the service contract.  
public class CalculatorService : ICalculator  
{  
    public double Add(double n1, double n2)  
    {  
        return n1 + n2;  
    }  
    public double Subtract(double n1, double n2)  
    {  
        return n1 - n2;  
    }  
    public double Multiply(double n1, double n2)  
    {  
        return n1 * n2;  
    }  
    public double Divide(double n1, double n2)  
    {  
        return n1 / n2;  
    }  
}  
```  
  
 TCP 포트 공유가 설정되고 보안이 해제된 net.tcp 바인딩 변형이 샘플에 사용됩니다.  보안된 TCP 바인딩을 사용하려면 서버의 보안 모드를 원하는 설정으로 변경하고 클라이언트에서 Svcutil.exe를 다시 실행하여 업데이트 클라이언트 구성 파일을 생성합니다.  
  
 다음 샘플에서는 서비스에 대한 구성을 보여 줍니다.  
  
```  
<system.serviceModel>  
  
    <services>  
      <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
               behaviorConfiguration="CalculatorServiceBehavior">  
        <!-- This endpoint is exposed at the base address provided by host: net.tcp://localhost/servicemodelsamples/service.svc  -->  
        <endpoint binding="netTcpBinding" bindingConfiguration="PortSharingBinding"  
          contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <!-- the mex endpoint is explosed at net.tcp://localhost/servicemodelsamples/service.svc/mex -->  
        <endpoint address="mex"  
                  binding="mexTcpBinding"  
                  contract="IMetadataExchange" />  
      </service>  
    </services>  
    <bindings>  
      <netTcpBinding>  
        <binding name="PortSharingBinding" portSharingEnabled="true">  
          <security mode="None" />  
        </binding>  
      </netTcpBinding>  
    </bindings>  
  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="CalculatorServiceBehavior">  
          <serviceMetadata />  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
  </system.serviceModel>  
```  
  
 다음 샘플 코드와 같이 클라이언트의 끝점이 구성됩니다.  
  
```  
<system.serviceModel>  
    <bindings>  
        <netTcpBinding>  
          <binding name="NetTcpBinding_ICalculator">  
            <security mode="None"/>  
          </binding>  
        </netTcpBinding>  
    </bindings>  
    <client>  
        <endpoint address="net.tcp://localhost/servicemodelsamples/service.svc"  
            binding="netTcpBinding" bindingConfiguration="NetTcpBinding_ICalculator"  
            contract="Microsoft.ServiceModel.Samples.ICalculator" name="NetTcpBinding_ICalculator" />  
    </client>  
</system.serviceModel>  
```  
  
 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다.  클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### 샘플을 설치, 빌드 및 실행하려면  
  
1.  [!INCLUDE[iisver](../../../../includes/iisver-md.md)]이 설치되어 있는지 확인합니다.  [!INCLUDE[iisver](../../../../includes/iisver-md.md)]은 WAS 활성화에 필요합니다.  
  
2.  [Windows Communication Foundation 샘플의 일회 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행했는지 확인합니다.  
  
     또한 HTTP가 아닌 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 활성화 구성 요소를 설치해야 합니다.  
  
    1.  **시작** 메뉴에서 **제어판**을 선택합니다.  
  
    2.  **프로그램 및 기능**을 선택합니다.  
  
    3.  **Windows 구성 요소 사용\/사용 안 함**을 클릭합니다.  
  
    4.  **Microsoft .NET Framework 3.0** 노드를 확장하고 **Windows Communication Foundation 비\-HTTP 활성화** 기능을 선택합니다.  
  
3.  TCP 활성화를 지원하도록 WAS를 구성합니다.  
  
     편의를 위해 다음 두 단계는 샘플 디렉터리에 있는 AddNetTcpSiteBinding.cmd라는 배치 파일에서 구현됩니다.  
  
    1.  net.tcp 활성화를 지원하려면 먼저 기본 웹 사이트를 net.tcp 포트에 바인딩해야 합니다.  IIS\(인터넷 정보 서비스\) 7.0 관리 도구 집합과 함께 설치되는 Appcmd.exe를 사용하여 이 작업을 수행할 수 있습니다.  관리자 수준 명령 프롬프트에서 다음 명령을 실행합니다.  
  
        ```  
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" -+bindings.[protocol='net.tcp',bindingInformation='808:*']  
        ```  
  
        > [!TIP]
        >  이 명령은 줄 바꿈 없이 한 줄로 입력해야 합니다.  이 명령은 임의의 호스트 이름을 사용하여 TCP 포트 808에서 수신 대기하는 기본 웹 사이트에 net.tcp 사이트 바인딩을 추가합니다.  
  
    2.  사이트 내의 모든 응용 프로그램이 공통된 net.tcp 바인딩을 공유하지만 각 응용 프로그램에서 개별적으로 net.tcp 지원을 사용하도록 설정할 수 있습니다.  \/servicemodelsamples 응용 프로그램에 대해 net.tcp를 사용하도록 설정하려면 관리자 수준 명령 프롬프트에서 다음 명령을 실행합니다.  
  
        ```  
        %windir%\system32\inetsrv\appcmd.exe set app   
        "Default Web Site/servicemodelsamples" /enabledProtocols:http,net.tcp  
        ```  
  
        > [!NOTE]
        >  이 명령은 줄 바꿈 없이 한 줄로 입력해야 합니다.  이 명령을 실행하면 http:\/\/localhost\/servicemodelsamples와 net.tcp:\/\/localhost\/servicemodelsamples를 모두 사용하여 \/servicemodelsamples 응용 프로그램에 액세스할 수 있습니다.  
  
4.  C\# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
5.  단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따릅니다.  
  
     이 샘플에 대해 추가한 net.tcp 사이트 바인딩을 제거합니다.  
  
     편의를 위해 다음 두 단계는 샘플 디렉터리에 있는 RemoveNetTcpSiteBinding.cmd라는 배치 파일에서 구현됩니다.  
  
    1.  관리자 수준 명령 프롬프트에서 다음 명령을 실행하여 사용하도록 설정된 프로토콜 목록에서 net.tcp를 제거합니다.  
  
        ```  
        %windir%\system32\inetsrv\appcmd.exe set app   
        "Default Web Site/servicemodelsamples" /enabledProtocols:http  
        ```  
  
        > [!NOTE]
        >  이 명령은 줄 바꿈 없이 한 줄로 입력해야 합니다.  
  
    2.  관리자 수준 명령 프롬프트에서 다음 명령을 실행하여 net.tcp 사이트 바인딩을 제거합니다.  
  
        ```  
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"   
        --bindings.[protocol='net.tcp',bindingInformation='808:*']  
        ```  
  
        > [!NOTE]
        >  이 명령은 줄 바꿈 없이 한 줄로 입력해야 합니다.  
  
## 참고 항목  
 [AppFabric 호스팅 및 지속성 샘플](http://go.microsoft.com/fwlink/?LinkId=193961)