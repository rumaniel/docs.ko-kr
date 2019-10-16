---
title: Windows용 WCF 서비스 및 이벤트 추척
ms.date: 03/30/2017
ms.assetid: eda4355d-0bd0-4dc9-80a2-d2c832152272
ms.openlocfilehash: e1ee7154e2ad5b22ff0debcdd15d5809fc55df13
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044525"
---
# <a name="wcf-services-and-event-tracing-for-windows"></a>Windows용 WCF 서비스 및 이벤트 추척
이 샘플에서는 Windows Communication Foundation (WCF)에서 분석 추적을 사용 하 여 ETW (ETW(Windows용 이벤트 추적))에서 이벤트를 내보내는 방법을 보여 줍니다. 분석 추적은 프로덕션 환경에서 WCF 서비스의 문제를 해결할 수 있는 WCF 스택의 주요 지점에서 발생 하는 이벤트입니다.

 WCF 서비스의 분석 추적은 성능에 미치는 영향을 최소화 하면서 프로덕션 환경에서 설정 될 수 있는 추적입니다. 이러한 추적은 ETW 세션에 이벤트로 내보내집니다.

 이 샘플에는 서비스에서 이벤트 로그로 이벤트를 내보내는 기본 WCF 서비스가 포함 되어 있습니다 .이 서비스는 이벤트 뷰어을 사용 하 여 볼 수 있습니다. 또한 WCF 서비스에서 이벤트를 수신 대기 하는 전용 ETW 세션을 시작할 수 있습니다. 이 샘플에는 이벤트 뷰어를 사용하여 읽을 수 있는 이진 파일에 이벤트를 저장하는 전용 ETW 세션을 만드는 스크립트가 포함되어 있습니다.

#### <a name="to-use-this-sample"></a>이 샘플을 사용하려면

1. Visual Studio 2012을 사용 하 여 EtwAnalyticTraceSample 솔루션 파일을 엽니다.

2. Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.

3. Ctrl+F5를 눌러 솔루션을 실행합니다.

     웹 브라우저에서 **계산기 .svc**를 클릭 합니다. 서비스의 WSDL 문서에 대한 URI가 브라우저에 나타납니다. 이 URI를 복사합니다.

     기본적으로 서비스는 포트 1378 `http://localhost:1378/Calculator.svc`에서 요청 수신을 시작 합니다.

4. WCF 테스트 클라이언트 (Wcftestclient.exe)를 실행 합니다.

     WCF 테스트 클라이언트 (Wcftestclient.exe)는에 `\<Visual Studio 2012 Install Dir>\Common7\IDE\WcfTestClient.exe`있습니다.  기본 Visual Studio 2012 설치 디렉터리 `C:\Program Files\Microsoft Visual Studio 10.0`는입니다.

5. WCF 테스트 클라이언트 내에서 **파일**을 선택 하 고 **서비스 추가**를 선택 하 여 서비스를 추가 합니다.

     입력 상자에 엔드포인트 주소를 추가합니다. 기본값은 `http://localhost:1378/Calculator.svc`입니다.

6. 이벤트 뷰어 애플리케이션을 엽니다.

     서비스를 호출 하기 전에 이벤트 뷰어를 시작 하 고 이벤트 로그가 WCF 서비스에서 내보낸 추적 이벤트를 수신 대기 하 고 있는지 확인 합니다.

7. **시작** 메뉴에서 **관리 도구**를 선택한 다음 **이벤트 뷰어**합니다.  **분석** 및 **디버그** 로그를 사용 하도록 설정 합니다.

8. 이벤트 뷰어의 트리 뷰에서 **이벤트 뷰어**, **응용 프로그램 및 서비스 로그**, **Microsoft**, **Windows**, **응용 프로그램 서버-응용**프로그램으로 이동 합니다. **응용 프로그램 서버-응용 프로그램**을 마우스 오른쪽 단추로 클릭 하 고 **보기**를 선택한 다음 **분석 및 디버그 로그 표시**를 선택 합니다.

     **분석 및 디버그 로그 표시** 옵션이 선택 되어 있는지 확인 합니다.

9. **분석** 로그를 사용 하도록 설정 합니다.

     이벤트 뷰어의 트리 뷰에서 **이벤트 뷰어**, **응용 프로그램 및 서비스 로그**, **Microsoft**, **Windows**, **응용 프로그램 서버-응용**프로그램으로 이동 합니다. **분석** 을 마우스 오른쪽 단추로 클릭 하 고 **로그 사용**을 선택 합니다.

#### <a name="to-test-the-service"></a>서비스를 테스트하려면

1. WCF 테스트 클라이언트로 다시 전환 하 고 분모를 0 `Divide` 으로 지정 하는 기본값을 두 번 클릭 하 고 유지 합니다.

     분모가 0이면 서비스에서는 오류를 throw합니다.

2. 서비스에서 내보낸 이벤트를 확인합니다.

     이벤트 뷰어으로 다시 전환 하 고 **이벤트 뷰어**, **응용 프로그램 및 서비스 로그**, **Microsoft**, **Windows**, **응용 프로그램 서버-응용**프로그램으로 이동 합니다. **분석** 을 마우스 오른쪽 단추로 클릭 하 고 **새로 고침**을 선택 합니다.

     WCF 분석 추적 이벤트가 이벤트 뷰어에 표시됩니다. 서비스에서 오류가 throw되었으므로 이벤트 뷰어에 오류 추적 이벤트가 표시됩니다.

3. 1-2단계를 반복하되 이번에는 유효한 입력을 사용합니다. `N2` 매개 변수 값으로는 0 이외의 모든 숫자를 사용할 수 있습니다.

     분석 채널을 새로 고쳐 WCF 이벤트에 오류 이벤트가 포함되어 있지 않은지 확인합니다.

 이 샘플에서는 WCF 서비스에서 내보낸 분석 추적 이벤트를 보여 줍니다.

#### <a name="to-cleanup-optional"></a>정리하려면(옵션)

1. 이벤트 뷰어를 엽니다.

2. **이벤트 뷰어**, **응용 프로그램 및 서비스 로그**, **Microsoft**, **Windows**, **응용 프로그램-서버-** 응용 프로그램으로 이동 합니다. **분석** 을 마우스 오른쪽 단추로 클릭 하 고 **로그 사용 안 함**을 선택 합니다.

3. **이벤트 뷰어**, **응용 프로그램 및 서비스 로그**, **Microsoft**, **Windows**, **응용 프로그램-서버-** 응용 프로그램으로 이동 합니다. **분석** 을 마우스 오른쪽 단추로 클릭 하 고 **로그 지우기**를 선택 합니다.

4. **지우기** 옵션을 선택 하 여 이벤트를 지웁니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\ETWTracing`  
  
## <a name="see-also"></a>참고자료

- [AppFabric 모니터링 샘플](https://go.microsoft.com/fwlink/?LinkId=193959)
