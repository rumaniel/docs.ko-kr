---
title: Windows용 WCF 서비스 및 이벤트 추척
ms.date: 03/30/2017
ms.assetid: eda4355d-0bd0-4dc9-80a2-d2c832152272
ms.openlocfilehash: 100f9c0ce71eedaa4061fc894521597074b21b00
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198291"
---
# <a name="wcf-services-and-event-tracing-for-windows"></a>Windows용 WCF 서비스 및 이벤트 추척
이 샘플에서 이벤트 추적에 대 한 Windows (ETW) 이벤트를 내보내는 분석 추적을 Windows Communication Foundation (WCF)를 사용 하는 방법을 보여 줍니다. 분석 추적은 프로덕션 환경에서 WCF 서비스의 문제를 해결할 수 있는 WCF 스택의 주요 지점에서 내보내는 이벤트입니다.

 WCF 서비스의 분석 추적은 추적을 켤 수 있지만 프로덕션 환경에서 성능에 미치는 영향이 최소화 합니다. 이러한 추적은 ETW 세션에 이벤트로 내보내집니다.

 이 샘플 이벤트 뷰어를 사용 하 여 볼 수 있는 이벤트 로그에 이벤트 서비스에서 내보낸 된 기본적인 WCF 서비스를 포함 합니다. WCF 서비스에서 이벤트를 수신 하는 전용된 ETW 세션을 시작 하는 것도 가능 합니다. 이 샘플에는 이벤트 뷰어를 사용하여 읽을 수 있는 이진 파일에 이벤트를 저장하는 전용 ETW 세션을 만드는 스크립트가 포함되어 있습니다.

#### <a name="to-use-this-sample"></a>이 샘플을 사용하려면

1.  EtwAnalyticTraceSample.sln 솔루션 파일을 열고 Visual Studio 2012를 사용 합니다.

2.  Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.

3.  Ctrl+F5를 눌러 솔루션을 실행합니다.

     웹 브라우저에서 클릭 **Calculator.svc**합니다. 서비스의 WSDL 문서에 대한 URI가 브라우저에 나타납니다. 이 URI를 복사합니다.

     기본적으로 서비스 1378 포트에서 요청 수신을 시작 `http://localhost:1378/Calculator.svc`합니다.

4.  WCF 테스트 클라이언트 (WcfTestClient.exe)를 실행 합니다.

     WCF 테스트 클라이언트 (WcfTestClient.exe)에 위치한 `\<Visual Studio 2012 Install Dir>\Common7\IDE\WcfTestClient.exe`합니다.  기본 Visual Studio 2012 설치 디렉터리는 `C:\Program Files\Microsoft Visual Studio 10.0`합니다.

5.  WCF 테스트 클라이언트 내에서 선택 하 여 서비스를 추가할 **파일**를 차례로 **서비스 추가**합니다.

     입력 상자에 엔드포인트 주소를 추가합니다. 기본값은 `http://localhost:1378/Calculator.svc`입니다.

6.  이벤트 뷰어 응용 프로그램을 엽니다.

     서비스를 호출 하기 전에 이벤트 뷰어를 시작 하 고 WCF 서비스에서 내보낸 추적 이벤트에 대 한 이벤트 로그에서이 수신 대기 하는지 확인 합니다.

7.  **시작** 메뉴에서 **관리 도구**를 차례로 **이벤트 뷰어**합니다.  사용 하도록 설정 합니다 **분석** 하 고 **디버그** 로그 합니다.

8.  이동할 이벤트 뷰어의 트리 뷰에서 **이벤트 뷰어**, **Applications and Services Logs**를 **Microsoft**를 **Windows**, 한 다음 **응용 프로그램 서버-응용 프로그램**합니다. 마우스 오른쪽 단추로 클릭 **응용 프로그램 서버-응용 프로그램**를 선택 **뷰**를 차례로 **분석 및 디버그 로그 표시**합니다.

     있는지 확인 합니다 **분석 및 디버그 로그 표시** 옵션을 선택 합니다.

9. 사용 하도록 설정 합니다 **분석** 로그 합니다.

     이동할 이벤트 뷰어의 트리 뷰에서 **이벤트 뷰어**, **Applications and Services Logs**를 **Microsoft**를 **Windows**, 한 다음 **응용 프로그램 서버-응용 프로그램**합니다. 마우스 오른쪽 단추로 클릭 **분석** 선택한 **로그 사용**합니다.

#### <a name="to-test-the-service"></a>서비스를 테스트하려면

1.  WCF 테스트 클라이언트를 다시 전환 하 고 두 번 클릭 `Divide` 0의 분모를 지정 하는 기본값을 그대로 유지 하 고 있습니다.

     분모가 0이면 서비스에서는 오류를 throw합니다.

2.  서비스에서 내보낸 이벤트를 확인합니다.

     이벤트 뷰어로 다시 전환 하 고 이동할 **이벤트 뷰어**를 **Applications and Services Logs**를 **Microsoft**를 **Windows**, 고 **응용 프로그램 서버-응용 프로그램**합니다. 마우스 오른쪽 단추로 클릭 **분석** 선택한 **새로 고침**합니다.

     WCF 분석 추적 이벤트가 이벤트 뷰어에 표시됩니다. 서비스에서 오류가 throw되었으므로 이벤트 뷰어에 오류 추적 이벤트가 표시됩니다.

3.  1-2단계를 반복하되 이번에는 유효한 입력을 사용합니다. `N2` 매개 변수 값으로는 0 이외의 모든 숫자를 사용할 수 있습니다.

     분석 채널을 새로 고쳐 WCF 이벤트에 오류 이벤트가 포함되어 있지 않은지 확인합니다.

 이 샘플에서는 WCF 서비스에서 내보낸 분석 추적 이벤트를 보여 줍니다.

#### <a name="to-cleanup-optional"></a>정리하려면(옵션)

1.  이벤트 뷰어를 엽니다.

2.  이동할 **이벤트 뷰어**를 **Applications and Services Logs**를 **Microsoft**를 **Windows**를 차례로  **응용 프로그램 서버-응용 프로그램**합니다. 마우스 오른쪽 단추로 클릭 **분석** 선택한 **로그 사용 안 함**합니다.

3.  이동할 **이벤트 뷰어**를 **Applications and Services Logs**를 **Microsoft**를 **Windows**를 차례로  **응용 프로그램 서버-응용 프로그램**합니다. 마우스 오른쪽 단추로 클릭 **분석** 선택한 **로그 지우기**합니다.

4.  선택 된 **의 선택을 취소** 이벤트를 지우려면 옵션입니다.

> [!IMPORTANT]
>  컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  이 디렉터리가 없으면로 이동 [Windows Communication Foundation (WCF) 및.NET Framework 4 용 Windows WF (Workflow Foundation) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 모든 Windows Communication Foundation (WCF)를 다운로드 하 고 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플. 이 샘플은 다음 디렉터리에 있습니다.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\ETWTracing`  
  
## <a name="see-also"></a>참고 항목  
 [AppFabric 모니터링 샘플](https://go.microsoft.com/fwlink/?LinkId=193959)
