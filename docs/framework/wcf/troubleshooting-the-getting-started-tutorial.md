---
title: Windows Communication Foundation 시작 자습서 문제 해결
ms.date: 01/25/2019
ms.assetid: 69a21511-0871-4c41-9a53-93110e84d7fd
ms.openlocfilehash: 10a2f8f718d802a7aab067b882f0d5cf3dc28dca
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928573"
---
# <a name="troubleshoot-the-get-started-with-windows-communication-foundation-tutorials"></a>Windows Communication Foundation 시작 자습서 문제 해결

이 문서에서는 [자습서의 단계를 수행할 때 발생할 수 있는 가장 일반적인 문제 및 오류에 대 한 해결 방법을 제공 합니다. Windows Communication Foundation 응용 프로그램](getting-started-tutorial.md)을 시작 하세요. 
  
## <a name="common-problems"></a>일반적인 문제

**하드 드라이브에서 프로젝트 파일을 찾을 수 없습니다.**

 Visual Studio에서 프로젝트 파일을 *C:\Users\\&lt;사용자 이름&gt;\source\repos*에 저장 합니다.  

***Svcutil.exe*에서 생성 한 *app.config* 파일을 찾을 수 없습니다.**

 Visual Studio에서 **기존 항목 추가** 창에는 기본적으로 다음 확장의 파일만 표시 됩니다. 

- *.cs* 
- *.resx* 
- *.settings*
- *.xsd* 
- *.wsdl*

모든 파일 형식을 표시 하려면 **기존 항목 추가** 창의 오른쪽 아래에 있는 드롭다운 목록에서 **\*모든 파일 (.\*)** 을 선택 합니다.  
  
## <a name="common-errors"></a>일반적인 오류

### <a name="compile-the-service-application"></a>서비스 응용 프로그램 컴파일 

**' GettingStartedHost '에서 BC30420 ' Sub m a s e '를 찾을 수 없습니다.**

Visual Basic 응용 프로그램에 대 한 진입점이 잘못 되었습니다. 다음과 같이 변경 합니다.

   1. **솔루션 탐색기** 창에서 **GettingStartedHost** 폴더를 선택 하 고 바로 가기 메뉴에서 **속성** 을 선택 합니다.
    a. **GettingStartedHost** 창에서 **시작 개체**에 대해 목록에서 **Service. Program** (또는 특정 응용 프로그램의 진입점)을 선택 합니다. 
    b. 주 메뉴에서 **파일** > **모두 저장**을 선택 합니다.

### <a name="run-the-service-application"></a>서비스 응용 프로그램 실행 

**Http에서 URL ' http:\//+: 8000/getCalculatorService started/'를 등록할 수 없습니다. 사용자의 프로세스에 이 네임스페이스에 액세스할 수 있는 권한이 없습니다.** 

 적절 한 액세스를 위해 관리 권한을 사용 하 여 WCF (Windows Communication Foundation) 서비스를 호스트 하는 프로세스를 시작 합니다.

- Visual Studio의 경우: **시작** 메뉴에서 Visual Studio 프로그램 **을 선택 하** > 고 바로 가기 메뉴에서**관리자 권한으로 실행** 을 선택 합니다.
- 콘솔 창의 경우: **시작** 메뉴에서 **명령 프롬프트** **를 선택 하** > 고 바로 가기 메뉴에서**관리자 권한으로 실행** 을 선택 합니다.
- Windows 탐색기: 실행 파일을 선택 하 고 바로 가기 메뉴에서 **관리자 권한으로 실행** 을 선택 합니다.

### <a name="compile-the-client-application"></a>클라이언트 응용 프로그램 컴파일

**' CalculatorClient '에 '\<method name > '에 대 한 정의가 포함 되어 있지 않으며 ' CalculatorClient ' 형식의 첫 번째 인수를 허용 하는 확장 메서드 '\<method name > '이 (가) 없습니다. using 지시문 또는이 (가) 없습니다. 어셈블리 참조)**  

`ServiceOperationAttribute` 특성으로 표시 된 메서드만 공개적으로 노출 됩니다. 인터페이스의 메서드에서 `ServiceOperationAttribute` 특성을 생략 하면 컴파일하는 동안이 오류 메시지가 표시 됩니다. `ICalculator`  

**' CalculatorClient ' 형식 또는 네임 스페이스 이름을 찾을 수 없습니다. using 지시문 또는 어셈블리 참조가 있는지 확인 하십시오.**

 Svcutil.exe 도구를 사용 하 여 *generatedProxy.cs* (또는 *generatedproxy*) 파일을 생성 한 경우이 파일을 클라이언트 프로젝트에 추가 하지 않으면이 오류가 표시 됩니다.  

### <a name="run-the-client-application"></a>클라이언트 응용 프로그램 실행

**처리 되지 않은 예외: System.ServiceModel.EndpointNotFoundException: ' Http:\//dhosts: 8000/getCalculatorService started/'에 연결할 수 없습니다. TCP 오류 코드 10061: 대상 컴퓨터에서 연결을 거부 하 여 연결을 설정할 수 없습니다.**

이 오류는 서비스를 먼저 시작 하지 않고 클라이언트 응용 프로그램을 실행 하는 경우에 발생 합니다. 먼저 호스트 응용 프로그램을 실행 하 여 서비스를 시작한 다음 클라이언트 응용 프로그램을 실행 합니다.

### <a name="use-the-svcutilexe-tool"></a>Svcutil.exe 도구 사용
   
**' Svcutil.exe '는 내부 또는 외부 명령, 실행할 수 있는 프로그램 또는 배치 파일로 인식 되지 않습니다.**

 *Svcutil.exe* 는 시스템 경로에 있어야 합니다. 가장 쉬운 솔루션은 Visual Studio 명령 프롬프트를 사용 하는 것입니다. **시작** 메뉴에서 **Visual Studio \<버전 >** 디렉터리를 선택한 다음  **\<VS 버전 > 개발자 명령 프롬프트**를 선택 합니다. 이 명령 프롬프트는 Visual Studio의 일부로 제공 되는 모든 도구의 올바른 위치로 시스템 경로를 설정 합니다.  
  
### <a name="run-the-service-and-client-applications"></a>서비스 및 클라이언트 응용 프로그램 실행

**System.ServiceModel.Security.SecurityNegotiationException: 대상 ' http:\/\//shosts: 8000/getCalculatorService started/CalculatorService '에 대 한 SOAP 보안 협상이 ' http:/chosts: 8000/gettingstarted/'와 함께 실패 했습니다.**  

이 오류는 네트워크에 연결 되지 않은 도메인에 가입 된 컴퓨터에서 발생 합니다. 컴퓨터를 네트워크에 연결 하거나 서비스와 클라이언트 모두에 대해 보안을 해제 합니다. 

보안을 해제 하려면:

- 서비스의 경우를 `WSHttpBinding` 만드는 코드를 다음 코드로 바꿉니다.  
  
    ```csharp
    // Step 3: Add a service endpoint.
    selfhost.AddServiceEndpoint(typeof(ICalculator), new WSHttpBinding(SecurityMode.None), "CalculatorService");  
    ```

- 클라이언트의 경우 구성 파일에서 다음과 같이  **\<binding >** 요소 아래의  **\<security >** 요소를 업데이트 합니다.  
  
    ```xml
    <binding name="WSHttpBinding_ICalculator" security mode="None" />
    ```  

## <a name="see-also"></a>참고자료  
 [WCF 응용 프로그램 시작](getting-started-tutorial.md)  
 [WCF 문제 해결 퀵 스타트](wcf-troubleshooting-quickstart.md)  
 [설치 문제 해결](troubleshooting-setup-issues.md)
