---
title: '방법: 추적 및 디버그를 사용하여 조건부 컴파일'
ms.date: 03/30/2017
helpviewer_keywords:
- trace compiler options
- trace statements
- compiling source code, trace statements
- tracing [.NET Framework], enabling or disabling
- tracing [.NET Framework], compiling conditionally
- TRACE directive
- conditional compilation, tracing code
ms.assetid: 56d051c3-012c-42c1-9a58-7270edc624aa
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d06d1ef8e1508aefa8c9ed9327b89f58ff6976fa
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052756"
---
# <a name="how-to-compile-conditionally-with-trace-and-debug"></a>방법: 추적 및 디버그를 사용하여 조건부 컴파일
개발 중에 응용 프로그램을 디버그하는 동안 추적 및 디버깅 출력은 둘 다 Visual Studio의 출력 창으로 이동합니다. 그러나 배포된 애플리케이션에 추적 기능을 포함하려면 **TRACE** 컴파일러 지시문을 사용하도록 설정하여 계측된 애플리케이션을 컴파일해야 합니다. 이렇게 하면 추적 코드를 응용 프로그램의 릴리스 버전으로 컴파일할 수 있습니다. **TRACE** 지시문을 사용하지 않으면 모든 추적 코드가 컴파일 중에 무시되고 배포할 실행 코드에 포함되지 않습니다.  
  
 추적 및 디버깅 메서드에는 연결된 조건부 특성이 포함됩니다. 예를 들어 추적에 대한 조건부 특성이 **true**이면 모든 trace 문이 어셈블리(컴파일된 .exe 파일 또는 .dll) 내에 포함되고, **Trace** 조건부 특성이 **false**이면 trace 문이 포함되지 않습니다.  
  
 빌드에 대해 **Trace** 또는 **Debug** 조건부 특성의 하나를 설정하거나, 둘 다 설정하거나, 아무것도 설정하지 않을 수 있습니다. 따라서 빌드에는 다음 네 가지 유형이 있습니다. **디버그**, **추적**, 둘 다 또는 둘 다 지정 하지 않습니다. 프로덕션 배포의 일부 릴리스 빌드에는 아무것도 포함되지 않을 수 있습니다. 대부분 디버깅 빌드에는 둘 다 포함됩니다.  
  
 여러 가지 방법으로 응용 프로그램에 대한 컴파일러 설정을 지정할 수 있습니다.  
  
- 속성 페이지  
  
- 명령줄  
  
- **#CONST**(Visual Basic의 경우) 및 **#define**(C#의 경우)  
  
### <a name="to-change-compile-settings-from-the-property-pages-dialog-box"></a>속성 페이지 대화 상자에서 컴파일 설정을 변경하려면  
  
1. **솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭합니다.  
  
2. 바로 가기 메뉴에서 **속성**을 선택합니다.  
  
    - Visual Basic에서 속성 페이지의 왼쪽 창에 있는 **컴파일** 탭을 클릭하고 **고급 컴파일 옵션** 단추를 클릭하여 **고급 컴파일러 설정** 대화 상자를 표시합니다. 사용하도록 설정할 컴파일러 설정의 확인란을 선택합니다. 사용하지 않도록 설정할 설정의 확인란을 선택 취소합니다.  
  
    - C#에서 속성 페이지의 왼쪽 창에 있는 **빌드** 탭을 클릭하고 사용하도록 설정할 컴파일러 설정의 확인란을 선택합니다. 사용하지 않도록 설정할 설정의 확인란을 선택 취소합니다.  
  
### <a name="to-compile-instrumented-code-using-the-command-line"></a>명령줄을 사용하여 계측된 코드를 컴파일하려면  
  
1. 명령줄에서 조건부 컴파일러 스위치를 설정합니다. 컴파일러는 실행 파일에 추적 및 디버그 코드를 포함합니다.  
  
     예를 들어 명령줄에 입력된 다음 컴파일러 명령은 컴파일된 실행 파일에 추적 코드를 포함합니다.  
  
     Visual Basic: **vbc-r:System.dll-d:TRACE = TRUE-d:DEBUG = FALSE MyApplication .vb**  
  
     C#: **R:System.dll-d:TRACE-d:DEBUG = FALSE MyApplication.cs**  
  
    > [!TIP]
    > 애플리케이션 파일을 두 개 이상 컴파일하려면 파일 이름 사이에 공백을 남깁니다(예: **MyApplication1.vb MyApplication2.vb MyApplication3.vb** 또는 **MyApplication1.cs MyApplication2.cs MyApplication3.cs**).  
  
     위 예제에서 사용된 조건부 컴파일 지시문의 의미는 다음과 같습니다.  
  
    |지시문|의미|  
    |---------------|-------------|  
    |`vbc`|Visual Basic 컴파일러|  
    |`csc`|C# 컴파일러|  
    |`-r:`|외부 어셈블리(EXE 또는 DLL)를 참조합니다.|  
    |`-d:`|조건부 컴파일 기호를 정의합니다.|  
  
    > [!NOTE]
    > TRACE 또는 DEBUG를 대문자로 사용해야 합니다. 조건부 컴파일 명령에 대한 자세한 내용을 보려면 명령 프롬프트에 `vbc /?`(Visual Basic의 경우) 또는 `csc /?`(C#의 경우)를 입력합니다. 자세한 내용은 [명령줄에서 빌드](../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)(C#) 또는 [명령줄 컴파일러 호출](../../visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md)(Visual Basic)을 참조하세요.  
  
### <a name="to-perform-conditional-compilation-using-const-or-define"></a>#CONST 또는 #define을 사용하여 조건부 컴파일을 수행하려면  
  
1. 소스 코드 파일의 위쪽에서 프로그래밍 언어에 대한 적절한 문을 입력합니다.  
  
    |언어|문|결과|  
    |--------------|---------------|------------|  
    |**Visual Basic**|**#CONST TRACE = true**|추적 사용|  
    ||**#CONST TRACE = false**|추적 사용 안 함|  
    ||**#CONST DEBUG = true**|디버깅 사용|  
    ||**#CONST DEBUG = false**|디버깅 사용 안 함|  
    |**C#**|**#define TRACE**|추적 사용|  
    ||**#undef TRACE**|추적 사용 안 함|  
    ||**#define DEBUG**|디버깅 사용|  
    ||**#undef DEBUG**|디버깅 사용 안 함|  
  
### <a name="to-disable-tracing-or-debugging"></a>추적 또는 디버깅을 사용하지 않으려면  
  
소스 코드에서 컴파일러 지시문을 삭제합니다.  
  
\- 또는 -  
  
컴파일러 지시문을 주석으로 처리합니다.  
  
> [!NOTE]
> 컴파일할 준비가 되면 **빌드** 메뉴에서 **빌드**를 선택하거나, **d:** 을 입력하지 않고 명령줄 메서드를 사용하여 조건부 컴파일 기호를 정의합니다.  
  
## <a name="see-also"></a>참고자료

- [응용 프로그램 추적 및 조율](tracing-and-instrumenting-applications.md)
- [방법: 추적 스위치 만들기, 초기화 및 구성](how-to-create-initialize-and-configure-trace-switches.md)
- [추적 스위치](trace-switches.md)
- [추적 수신기](trace-listeners.md)
- [방법: 응용 프로그램 코드에 Trace 문 추가](how-to-add-trace-statements-to-application-code.md)
- [방법: Visual Studio 명령줄에 필요한 환경 변수 설정](../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)
- [방법: 명령줄 컴파일러 호출](../../visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md)
