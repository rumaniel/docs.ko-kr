---
title: WMI Provider
ms.date: 03/30/2017
ms.assetid: 462f0db3-f4a4-4a4b-ac26-41fc25c670a4
ms.openlocfilehash: 89e2d370919519953e714cb0d0020587b3f53c9d
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70038506"
---
# <a name="wmi-provider"></a>WMI Provider
이 샘플에서는 WCF에서 빌드된 WMI(Windows Management Instrumentation) (WMI) 공급자를 사용 하 여 런타임에 WCF (Windows Communication Foundation) 서비스에서 데이터를 수집 하는 방법을 보여 줍니다. 또한 사용자 정의 WMI 개체를 서비스에 추가하는 방법도 보여 줍니다. 이 샘플에서는 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md) 에 대해 WMI 공급자를 활성화 하 고 런타임에 `ICalculator` 서비스에서 데이터를 수집 하는 방법을 보여 줍니다.  
  
 WMI는 Microsoft에서 구현한 WBEM(Web-Based Enterprise Management) 표준입니다. WMI SDK에 대 한 자세한 내용은 [WMI(Windows Management Instrumentation)](/windows/desktop/WmiSdk/wmi-start-page)를 참조 하세요. WBEM은 애플리케이션에서 외부 관리 도구에 관리 계측을 노출하는 방법을 지정하는 산업 표준입니다.  
  
 WCF는 런타임에 WBEM 호환 인터페이스를 통해 계측을 노출 하는 구성 요소인 WMI 공급자를 구현 합니다. 관리 도구는 런타임에 인터페이스를 통해 서비스에 연결될 수 있습니다. WCF는 주소, 바인딩, 동작 및 수신기와 같은 서비스 특성을 노출 합니다.  
  
 기본 제공 WMI 공급자는 애플리케이션의 구성 파일에서 활성화합니다. 이 작업은 다음 샘플 `wmiProviderEnabled` 구성에 표시 된 것 처럼 [ \<system.servicemodel >](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) 섹션에서 [ \<진단 >](../../../../docs/framework/configure-apps/file-schema/wcf/diagnostics.md) 의 특성을 통해 수행 됩니다.  
  
```xml  
<system.serviceModel>  
    ...  
    <diagnostics wmiProviderEnabled="true" />  
    ...  
</system.serviceModel>  
```  
  
 이 구성 항목은 WMI 인터페이스를 노출합니다. 관리 애플리케이션이 이 인터페이스를 통해 연결하여 애플리케이션의 관리 계측에 액세스할 수 있습니다.  
  
## <a name="custom-wmi-object"></a>사용자 지정 WMI 개체  
 서비스에 WMI 개체를 추가하면 기본 제공 WMI 공급자 정보와 함께 사용자 정의 정보를 표시할 수 있습니다. 그러려면 Installutil.exe 애플리케이션을 사용하여 WMI에 서비스의 스키마를 게시합니다. 이 작업을 수행하기 위한 지침과 자세한 설명은 항목 끝 부분에 있는 설치 지침을 참조하십시오.  
  
## <a name="accessing-wmi-information"></a>WMI 정보 액세스  
 다양한 방식으로 WMI 데이터에 액세스할 수 있습니다. Microsoft에서는 스크립트, Visual Basic 응용 프로그램, C++ 응용 프로그램 및 .NET Framework ()https://docs.microsoft.com/windows/desktop/wmisdk/using-wmi) 용 WMI api를 제공 합니다.  
  
 이 샘플에서는 두 개의 Java 스크립트를 사용합니다. 하나는 컴퓨터에서 실행 중인 서비스를 속성과 함께 나열하고, 다른 하나는 사용자 정의 WMI 데이터를 표시합니다. 스크립트에서는 WMI 공급자에 대한 연결을 열고, 데이터를 구문 분석하고, 수집된 데이터를 표시합니다.  
  
 샘플을 시작 하 여 WCF 서비스의 실행 중인 인스턴스를 만듭니다. 서비스가 실행 중인 동안 명령 프롬프트에서 다음 명령을 사용하여 각 Java 스크립트를 실행합니다.  
  
```  
cscript EnumerateServices.js  
```  
  
 스크립트에서는 서비스에 포함된 계측에 액세스하여 다음 출력을 생성합니다.  
  
```  
Microsoft (R) Windows Script Host Version 5.6  
Copyright © Microsoft Corporation 1996-2001. All rights reserved.  
  
1 service(s) found.  
|-PID:           5776  
|-DistinguishedName:  CalculatorService@http://localhost/ServiceModelSamples/service.svc  
|-Endpoints:     1 endpoints  
  |-CalculatorService.ICalculator@http://localhost/ServiceModelSamples/service.svc  
    |-Address:                        http://localhost/ServiceModelSamples/service.svc  
    |-CounterInstanceName:  
    |-AddressHeaders:                 0  
    |-ContractType:                   Contract.Name='ICalculator'  
    |-BindingElements:                4 bindings  
      |-BindingElements[0]  
        |-Type:                       TransactionFlowBindingElement  
      |-BindingElements[1]  
        |-Type:                       SymmetricSecurityBindingElement  
      |-BindingElements[2]  
        |-Type:                       TextMessageEncodingBindingElement  
        |-MaxReadPoolSize:            64  
        |-MaxWritePoolSize:           16  
      |-BindingElements[3]  
        |-Type:                       HttpTransportBindingElement  
        |-ManualAddressing:           false  
        |-MaxBufferSize:              65536  
        |-AllowCookies:               false  
        |-AuthenticationScheme:       Anonymous  
        |-BypassProxyOnLocal:         false  
        |-HostNameComparisonMode:     StrongWildcard  
        |-ProxyAddress:               null  
        |-ProxyAuthenticationScheme:  Anonymous  
        |-Realm:  
        |-TransferMode:               Buffered  
        |-UseDefaultWebProxy:         true  
|-Behaviors:     5 behaviors  
      |-Behavior[0]  
      |-Type:                       ServiceBehaviorAttribute  
        |-AddressFilterMode:               Exact  
        |-AutomaticSessionShutdown:        true  
        |-ConcurrencyMode:                 Single  
        |-IncludeExceptionDetailInFaults:  false  
        |-InstanceContextMode:             PerSession  
        |-TransactionIsolationLevel:       Unspecified  
        |-TransactionTimeout:              null  
        |-ValidateMustUnderstand:          true  
      |-Behavior[1]  
      |-Type:                       AspNetCompatibilityRequirementsAttribute  
      |-Behavior[2]  
      |-Type:                       ServiceDebugBehavior  
      |-Behavior[3]  
      |-Type:                       ServiceAuthorizationBehavior  
      |-Behavior[4]  
      |-Type:                       Behavior  
```  
  
 다음으로 두 번째 Java Script를 실행하여 사용자 정의 WMI 데이터를 표시합니다.  
  
```  
cscript EnumerateCustomObjects.js  
```  
  
 스크립트에서는 서비스에 포함된 사용자 정의 계측에 액세스하여 다음 출력을 생성합니다.  
  
```  
1 WMIObject(s) found.  
|-PID:           30285bfd-9d66-4c4e-9be2-310499c5cef5  
|-InstanceId:    3839  
|-WMIInfo:       User Defined WMI Information.  
```  
  
 컴퓨터에서 단일 서비스가 실행되고 있다는 것이 출력에 표시됩니다. 서비스에서는 `ICalculator` 계약을 구현하는 엔드포인트 하나를 노출합니다. 엔드포인트에서 구현하는 동작 및 바인딩 설정은 메시징 스택에 있는 개별 요소의 합으로 나열됩니다.  
  
 WMI는 WCF 인프라의 관리 계측을 노출 하는 것으로 제한 되지 않습니다. 같은 메커니즘을 통해 자체 도메인별 데이터 항목을 노출할 수 있습니다. WMI는 웹 서비스의 검사 및 제어를 위한 통합 메커니즘입니다.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3. 호스팅 디렉터리에 있는 service.dll 파일에서 InstallUtil.exe(기본 위치는 "%WINDIR%\Microsoft.NET\Framework\v4.0.30319")를 실행하여 WMI에 서비스 스키마를 게시합니다. 이 단계는 service.dll 파일이 수정된 경우에만 수행되어야 합니다.
  
4. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
    > [!NOTE]
    > ASP.NET를 설치한 후 WCF를 설치한 경우 "% WINDIR% \을 (를) 실행 해야 할 수 있습니다. Net\Framework\v3.0\Windows 통신 Foundation\servicemodelreg.exe "-r-x를 사용 하 여 ASPNET 계정에 WMI 개체를 게시할 수 있는 권한을 부여 합니다.  
  
5. `cscript EnumerateServices.js` 또는 `cscript EnumerateCustomObjects.js` 명령을 사용하여 WMI를 통해 표시된 샘플의 데이터를 봅니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\WMIProvider`  
  
## <a name="see-also"></a>참고자료

- [AppFabric 모니터링 샘플](https://go.microsoft.com/fwlink/?LinkId=193959)
