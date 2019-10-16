---
title: WCF 분석 추적
ms.date: 03/30/2017
ms.assetid: 6029c7c7-3515-4d36-9d43-13e8f4971790
ms.openlocfilehash: ba4f1778059f7b960eebd42822048fa031e6961e
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044540"
---
# <a name="wcf-analytic-tracing"></a>WCF 분석 추적
이 샘플에서는에서 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]ETW에 쓰기를 Windows Communication Foundation 하는 분석 추적 스트림에 사용자 고유의 추적 이벤트를 추가 하는 방법을 보여 줍니다. 분석 추적은 성능을 크게 저하시키지 않으면서 서비스를 쉽게 확인할 수 있도록 하기 위한 것입니다. 이 샘플에서는 <xref:System.Diagnostics.Eventing?displayProperty=nameWithType> api를 사용 하 여 WCF 서비스와 통합 되는 이벤트를 작성 하는 방법을 보여 줍니다.  
  
 <xref:System.Diagnostics.Eventing?displayProperty=nameWithType> Api에 대 한 자세한 내용은을 참조 <xref:System.Diagnostics.Eventing?displayProperty=nameWithType>하십시오.  
  
 Windows에서 이벤트 추적에 대 한 자세한 내용은 [ETW를 사용한 디버깅 및 성능 조정 개선](https://go.microsoft.com/fwlink/?LinkId=166488)을 참조 하세요.  
  
## <a name="disposing-eventprovider"></a>EventProvider 삭제  
 이 샘플에서는 <xref:System.Diagnostics.Eventing.EventProvider?displayProperty=nameWithType>을 구현하는 <xref:System.IDisposable?displayProperty=nameWithType> 클래스를 사용합니다. WCF 서비스에 대 한 추적을 구현 하는 경우 서비스 수명 동안 <xref:System.Diagnostics.Eventing.EventProvider>의 리소스를 사용할 수 있습니다. 이러한 이유로, 또한 읽기 쉽게 하려는 목적으로 이 샘플에서는 래핑된 <xref:System.Diagnostics.Eventing.EventProvider>를 삭제하지 않습니다. 어떤 이유로 서비스에 다른 추적 요구 사항이 있으며 이 리소스를 삭제해야 하는 경우 관리되지 않는 리소스를 삭제하기 위한 최선의 방법에 따라 이 샘플을 수정해야 합니다. 관리 되지 않는 리소스를 삭제 하는 방법에 대 한 자세한 내용은 [Dispose 메서드 구현](https://go.microsoft.com/fwlink/?LinkId=166436)을 참조 하세요.  
  
## <a name="self-hosting-vs-web-hosting"></a>자체 호스팅 및 웹 호스팅  
 웹 호스팅 서비스의 경우 WCF의 분석 추적은 추적을 내보내는 서비스를 식별 하는 데 사용 되는 "HostReference" 라는 필드를 제공 합니다. 확장 가능한 사용자 추적이 이 모델에 관여할 수 있으며 이 샘플에서는 이 작업을 수행하기 위한 최선의 방법을 보여 줍니다. 파이프 '&#124;' 문자가 실제로 결과 문자열에 표시 되는 경우 웹 호스트 참조의 형식은 다음 중 하나일 수 있습니다.  
  
- 응용 프로그램이 루트에 없는 경우  
  
     \<SiteName>\<ApplicationVirtualPath>&#124;\<ServiceVirtualPath>&#124;\<ServiceName>  
  
- 응용 프로그램이 루트에 있는 경우  
  
     \<SiteName>&#124;\<ServiceVirtualPath>&#124;\<ServiceName>  
  
 자체 호스팅 서비스의 경우 WCF의 분석 추적은 "HostReference" 필드를 채우지 않습니다. 이 샘플의 `WCFUserEventProvider` 클래스는 자체 호스팅 서비스에서 사용될 때 일관성 있게 동작합니다.  
  
## <a name="custom-event-details"></a>사용자 지정 이벤트 상세 정보  
 WCF의 ETW 이벤트 공급자 매니페스트는 WCF 서비스 작성자가 서비스 코드 내에서 내보내도록 디자인 된 세 개의 이벤트를 정의 합니다. 다음 표에서는 세 개의 이벤트를 간략하게 설명합니다.  
  
|이벤트|설명|이벤트 ID|  
|-----------|-----------------|--------------|  
|UserDefinedInformationEventOccurred|문제는 아니지만 중요한 사항이 서비스에 발생하면 이 이벤트를 내보냅니다. 예를 들어 데이터베이스를 성공적으로 호출한 후 이벤트를 내보낼 수 있습니다.|301|  
|UserDefinedWarningOccurred|이후에 오류를 초래할 수 있는 문제가 발생하면 이 이벤트를 내보냅니다. 예를 들어 데이터베이스에 대한 호출에 실패했지만 중복 데이터 저장소를 대신 사용하여 복구할 수 있는 경우 경고 이벤트를 내보낼 수 있습니다.|302|  
|UserDefinedErrorOccurred|서비스가 예상한 대로 동작하지 않으면 이 이벤트를 내보냅니다. 예를 들어 데이터베이스에 대한 호출에 실패하고 다른 위치에서 데이터를 검색할 수 없는 경우 이벤트를 내보낼 수 있습니다.|303|  
  
#### <a name="to-use-this-sample"></a>이 샘플을 사용하려면  
  
1. Visual Studio 2012을 사용 하 여 WCFAnalyticTracingExtensibility 솔루션 파일을 엽니다.  
  
2. Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.  
  
3. Ctrl+F5를 눌러 솔루션을 실행합니다.  
  
     웹 브라우저에서 **계산기 .svc**를 클릭 합니다. 서비스의 WSDL 문서에 대한 URI가 브라우저에 나타납니다. 이 URI를 복사합니다.  
  
4. WCF 테스트 클라이언트 (Wcftestclient.exe)를 실행 합니다.  
  
     WCF 테스트 클라이언트 (Wcftestclient.exe)는에 `\<Visual Studio 2012 Install Dir>\Common7\IDE\WcfTestClient.exe`있습니다. 기본 Visual Studio 2012 설치 디렉터리 `C:\Program Files\Microsoft Visual Studio 10.0`는입니다.  
  
5. WCF 테스트 클라이언트 내에서 **파일**을 선택 하 고 **서비스 추가**를 선택 하 여 서비스를 추가 합니다.  
  
     입력 상자에 엔드포인트 주소를 추가합니다.  
  
6. **확인** 을 클릭 하 여 대화 상자를 닫습니다.  
  
     ICalculator 서비스가 **내 서비스 프로젝트**아래의 왼쪽 창에 추가 됩니다.  
  
7. 이벤트 뷰어 애플리케이션을 엽니다.  
  
     서비스를 호출 하기 전에 이벤트 뷰어를 시작 하 고 이벤트 로그가 WCF 서비스에서 내보낸 추적 이벤트를 수신 대기 하 고 있는지 확인 합니다.  
  
8. **시작** 메뉴에서 **관리 도구**를 선택한 다음 **이벤트 뷰어**합니다. **분석** 및 **디버그** 로그를 사용 하도록 설정 합니다.  
  
9. 이벤트 뷰어의 트리 뷰에서 **이벤트 뷰어**, **응용 프로그램 및 서비스 로그**, **Microsoft**, **Windows**, **응용 프로그램 서버-응용**프로그램으로 이동 합니다. **응용 프로그램 서버-응용 프로그램**을 마우스 오른쪽 단추로 클릭 하 고 **보기**를 선택한 다음 **분석 및 디버그 로그 표시**를 선택 합니다.  
  
     **분석 및 디버그 로그 표시** 옵션이 선택 되어 있는지 확인 합니다. **분석** 로그를 사용 하도록 설정 합니다.  
  
     이벤트 뷰어의 트리 뷰에서 **이벤트 뷰어**, **응용 프로그램 및 서비스 로그**, **Microsoft**, **Windows**, **응용 프로그램 서버-응용**프로그램, **분석**으로 이동 합니다. **분석** 을 마우스 오른쪽 단추로 클릭 하 고 **로그 사용**을 선택 합니다.  
  
10. WCF 테스트 클라이언트를 사용하여 서비스를 테스트합니다.  
  
    1. WCF 테스트 클라이언트에서 ICalculator service 노드의 **Add ()** 를 두 번 클릭 합니다.  
  
         **Add ()** 메서드는 두 개의 매개 변수를 사용 하 여 오른쪽 창에 표시 됩니다.  
  
    2. 첫 번째 매개 변수에 2를 입력하고 두 번째 매개 변수에 3을 입력합니다.  
  
    3. **호출** 을 클릭 하 여 메서드를 호출 합니다.  
  
11. 이미 열려 있는 **이벤트 뷰어** 창으로 이동 합니다. **이벤트 뷰어**, **응용 프로그램 및 서비스 로그**, **Microsoft**, **Windows**, **응용 프로그램 서버-응용**프로그램으로 이동 합니다.  
  
12. **분석** 노드를 마우스 오른쪽 단추로 클릭 하 고 **새로 고침**을 선택 합니다.  
  
     오른쪽 창에 이벤트가 나타납니다.  
  
13. ID가 303인 이벤트를 찾아서 두 번 클릭하여 열고 해당 내용을 검사합니다.  
  
     이 이벤트는 ICalculator 서비스의 `Add()` 메서드에서 내보내고 "2 + 3 = 5"와 같은 페이로드를 가집니다.  
  
#### <a name="to-clean-up-optional"></a>정리하려면(옵션)  
  
1. **이벤트 뷰어**를 엽니다.  
  
2. **이벤트 뷰어**, **응용 프로그램 및 서비스 로그**, **Microsoft**, **Windows**, **응용 프로그램-서버-** 응용 프로그램으로 이동 합니다. **분석** 을 마우스 오른쪽 단추로 클릭 하 고 **로그 사용 안 함**을 선택 합니다.  
  
3. **이벤트 뷰어**, **응용 프로그램 및 서비스 로그**, **Microsoft**, **Windows**, 응용 프로그램- **서버-응용 프로그램**, **분석**으로 이동 합니다. **분석** 을 마우스 오른쪽 단추로 클릭 하 고 **로그 지우기**를 선택 합니다.  
  
4. **지우기** 를 클릭 하 여 이벤트를 지웁니다.  
  
## <a name="known-issue"></a>알려진 문제  
 **이벤트 뷰어** 에는 ETW 이벤트를 디코딩하는 데 실패할 수 있는 알려진 문제가 있습니다. 다음과 같은 오류 메시지가 표시 될 수 있습니다. "소스 Microsoft-Windows 응용 \<프로그램 서버의 이벤트 id id >에 대 한 설명을 찾을 수 없습니다. 이 이벤트를 발생시킨 구성 요소가 로컬 컴퓨터에 설치되어 있지 않거나 설치가 손상되었습니다. 로컬 컴퓨터에 구성 요소를 설치 하거나 복구할 수 있습니다. " 이 오류가 발생 하는 경우 **작업** 메뉴에서 **새로 고침** 을 선택 합니다. 그러면 이벤트가 올바르게 디코딩됩니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\ETWTrace`  
  
## <a name="see-also"></a>참고자료

- [AppFabric 모니터링 샘플](https://go.microsoft.com/fwlink/?LinkId=193959)
