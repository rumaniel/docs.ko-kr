---
title: 응용 프로그램 추적 및 조율
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tracing [.NET Framework]
- debugging [.NET Framework], instrumentation
- performance monitoring, instrumentation
- instrumentation, about instrumentation
- tracing [.NET Framework], about tracing
- performance monitoring, tracing code
- Trace class, instrumentation for .NET applications
ms.assetid: 773b6fc4-9013-4322-b728-5dec7a72e743
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c71e95b3fd1276d2fae4268ed59818e5fafc8a79
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052249"
---
# <a name="tracing-and-instrumenting-applications"></a>응용 프로그램 추적 및 조율
추적은 실행되는 동안 응용 프로그램의 실행을 모니터링할 수 있는 방법입니다. 개발할 때 .NET Framework 응용 프로그램에 추적 및 디버깅 계측을 추가할 수 있으며, 응용 프로그램을 개발하는 동안 및 배포한 후에 해당 계측을 모두 사용할 수 있습니다. <xref:System.Diagnostics.Trace?displayProperty=nameWithType>, <xref:System.Diagnostics.Debug?displayProperty=nameWithType> 및 <xref:System.Diagnostics.TraceSource?displayProperty=nameWithType> 클래스를 사용하여 나중에 분석할 수 있도록 오류 및 응용 프로그램 실행 정보를 로그, 텍스트 파일 또는 다른 장치에 기록할 수 있습니다.  
  
 *계측*이란 용어는 제품의 성능 수준을 모니터링하거나 측정하고 오류를 진단하는 기능을 가리킵니다. 프로그래밍에서 이 용어는 다음을 통합하는 응용 프로그램 기능을 의미합니다.  
  
- **코드 추적** - 런타임에 응용 프로그램의 실행에 대한 정보 메시지를 받습니다.  
  
- **디버깅** - 개발 중인 응용 프로그램에서 프로그래밍 오류를 추적하고 수정합니다. 자세한 내용은 [디버깅](/visualstudio/debugger/debugging-in-visual-studio)을 참조하세요.  
  
- **성능 카운터** - 응용 프로그램의 성능을 추적할 수 있게 해주는 구성 요소입니다. 자세한 내용은 [성능 카운터](performance-counters.md)를 참조하세요.  
  
- **이벤트 로그** - 응용 프로그램의 실행에서 주요 이벤트를 수신하고 추적할 수 있게 해주는 구성 요소입니다. 자세한 내용은 <xref:System.Diagnostics.EventLog> 클래스를 참조하세요.  
  
 분산 응용 프로그램에서는 코드의 전략적 위치에 trace 문을 배치하여 응용 프로그램을 계측하는 것이 특히 유용합니다. trace 문을 통해 응용 프로그램을 계측하여 문제가 발생할 때 정보를 표시하는 것은 물론 응용 프로그램의 성능을 모니터링할 수 있습니다.  
  
 <xref:System.Diagnostics.TraceSource> 클래스는 향상된 추적 기능을 제공하며, 이전 <xref:System.Diagnostics.Trace> 및 <xref:System.Diagnostics.Debug> 추적 클래스의 정적 메서드 대신 사용할 수 있습니다. 익숙한 <xref:System.Diagnostics.Trace> 및 <xref:System.Diagnostics.Debug> 클래스가 여전히 널리 사용되지만 <xref:System.Diagnostics.TraceSource.TraceEvent%2A> 및 <xref:System.Diagnostics.TraceSource.TraceData%2A>와 같은 새 추적 명령에는 <xref:System.Diagnostics.TraceSource> 클래스를 사용하는 것이 좋습니다.  
  
 <xref:System.Diagnostics.Trace> 및 <xref:System.Diagnostics.Debug> 클래스는 <xref:System.Diagnostics.Debug> 클래스와 달리 <xref:System.Diagnostics.Trace> 클래스의 해당 프로시저와 함수가 기본적으로 릴리스 빌드로 컴파일된다는 점을 제외하고 동일합니다.  
  
 <xref:System.Diagnostics.Trace> 및 <xref:System.Diagnostics.Debug> 클래스는 개발 중이나 배포 후에 응용 프로그램 성능을 모니터링하고 검사할 수 있는 수단을 제공합니다. 예를 들어, 배포된 응용 프로그램에서 특정 동작 유형(예: 새 데이터베이스 연결 만들기)이 발생할 때 <xref:System.Diagnostics.Trace> 클래스를 사용하여 해당 동작을 추적할 수 있으므로 응용 프로그램의 효율성을 모니터링할 수 있습니다.  
  
## <a name="code-tracing-and-debugging"></a>코드 추적 및 디버깅  
 개발하는 동안 <xref:System.Diagnostics.Debug> 클래스의 출력 메서드를 사용하여 Visual Studio IDE(통합 개발 환경)의 출력 창에 메시지를 표시할 수 있습니다. 예를 들어:  
  
```vb  
Trace.WriteLine("Hello World!")  
Debug.WriteLine("Hello World!")  
```  
  
```csharp  
System.Diagnostics.Trace.WriteLine("Hello World!");  
System.Diagnostics.Debug.WriteLine("Hello World!");  
```  
  
 각 예제에서 응용 프로그램을 디버거에서 실행하는 경우 “Hello World!”가 출력 창에 표시됩니다.  
  
 이 경우 응용 프로그램을 디버그하고 테스트 환경에서의 해당 동작에 따라 성능을 최적화할 수 있습니다. 모든 디버깅 출력을 받을 수 있도록 <xref:System.Diagnostics.Debug> 조건부 특성을 설정한 상태로 디버그 빌드에서 응용 프로그램을 디버깅할 수 있습니다. 응용 프로그램을 릴리스할 준비가 된 경우, <xref:System.Diagnostics.Debug> 조건부 특성을 설정하지 않고 릴리스 빌드를 컴파일하면 컴파일러가 디버깅 코드를 최종 실행 파일에 포함시키지 않도록 할 수 있습니다. 자세한 내용은 [방법: 추적 및 디버그를 사용한 조건부 컴파일](how-to-compile-conditionally-with-trace-and-debug.md) 애플리케이션의 다양한 빌드 구성에 대한 자세한 내용은 [컴파일 및 빌드](/visualstudio/ide/compiling-and-building-in-visual-studio)를 참조하세요.  
  
 또한 <xref:System.Diagnostics.Trace> 클래스의 메서드를 사용하여 설치된 응용 프로그램에서 코드 실행을 추적할 수 있습니다. 코드에 [추적 스위치](trace-switches.md)를 배치하면 추적 발생 여부와 추적 범위를 제어할 수 있습니다. 이 경우 프로덕션 환경에서 응용 프로그램의 상태를 모니터링할 수 있습니다. 이 기능은 여러 컴퓨터에서 실행되는 여러 구성 요소를 사용하는 비즈니스 응용 프로그램에서 특히 중요합니다. 배포 후 구성 파일을 통해 스위치를 사용하는 방법을 제어할 수 있습니다. 자세한 내용은 [방법: 추적 스위치](how-to-create-initialize-and-configure-trace-switches.md)만들기, 초기화 및 구성  
  
 추적을 사용하려는 응용 프로그램을 개발하는 경우 일반적으로 추적 및 디버깅 메시지 둘 다를 응용 프로그램 코드에 포함합니다. 애플리케이션을 배포할 준비가 되면 **디버그** 조건부 특성을 설정하지 않고 릴리스 빌드를 컴파일할 수 있습니다. 그러나 컴파일러가 실행 파일에 추적 코드를 포함하도록 **추적** 조건부 특성을 설정할 수 있습니다. 자세한 내용은 [방법: 추적 및 디버그를 사용한 조건부 컴파일](how-to-compile-conditionally-with-trace-and-debug.md)  
  
### <a name="phases-of-code-tracing"></a>코드 추적 단계  
 코드 추적에는 다음 세 단계가 있습니다.  
  
1. **계측** - 응용 프로그램에 추적 코드를 추가합니다.  
  
2. **추적** - 추적 코드가 지정된 대상에 정보를 씁니다.  
  
3. **분석** - 추적 정보를 평가하여 응용 프로그램의 문제를 식별하고 파악합니다.  
  
 개발 중에 모든 디버그 및 추적 출력 메서드는 기본적으로 Visual Studio의 출력 창에 정보를 씁니다. 배포된 응용 프로그램에서 메서드는 지정된 대상에 추적 정보를 씁니다. 추적 또는 디버깅의 출력 대상을 지정하는 방법에 대한 자세한 내용은 [추적 수신기](trace-listeners.md)를 참조하세요.  
  
 다음은 추적을 사용하여 배포 된 응용 프로그램의 잠재적 문제를 분석 및 해결하는 작업과 일반적으로 관련된 주요 단계를 전체적으로 보여 줍니다. 이러한 단계를 수행하는 방법에 대한 자세한 내용은 해당 링크를 참조하세요.  
  
##### <a name="to-use-tracing-in-an-application"></a>응용 프로그램에서 추적을 사용하려면  
  
1. 응용 프로그램을 배포한 후 온사이트에서 수신할 추적 출력을 고려합니다.  
  
2. 스위치 집합을 만듭니다. 자세한 내용은 [방법: 추적 스위치](how-to-create-initialize-and-configure-trace-switches.md)를 구성 합니다.  
  
3. 응용 프로그램 코드에 trace 문을 추가합니다.  
  
4. 추적 출력을 표시할 위치를 결정하고 적절한 수신기를 추가합니다. 자세한 내용은 [추적 수신기 만들기 및 초기화](how-to-create-and-initialize-trace-listeners.md)를 참조하세요.  
  
5. 응용 프로그램 및 응용 프로그램에 포함된 추적 코드를 테스트 및 디버그합니다.  
  
6. 다음 절차 중 하나를 사용하여 응용 프로그램을 실행 코드로 컴파일합니다.  
  
    - **솔루션 탐색기**에서 **속성 페이지** 대화 상자의 **디버그** 페이지와 함께 **빌드** 메뉴를 사용합니다. 이 절차는 Visual Studio에서 컴파일할 때 사용합니다.  
  
         \- 또는 -  
  
    - 컴파일의 명령줄 메서드에 대한 **추적** 및 **디버그** 컴파일러 지시문을 사용합니다. 자세한 내용은 [추적 및 디버그를 사용한 조건부 컴파일](how-to-compile-conditionally-with-trace-and-debug.md)을 참조하세요. 이 절차는 명령줄에서 컴파일할 때 사용합니다.  
  
7. 런타임 중에 문제가 발생하는 경우 적절한 추적 스위치를 설정합니다. 자세한 내용은 [추적 스위치 구성](how-to-create-initialize-and-configure-trace-switches.md)을 참조하세요.  
  
     추적 코드는 지정된 대상(예: 화면, 텍스트 파일 또는 이벤트 로그)에 추적 메시지를 씁니다. **Trace.Listeners** 컬렉션에 포함된 수신기의 형식에 따라 대상이 결정됩니다.  
  
8. 추적 메시지를 분석하여 응용 프로그램의 문제를 식별하고 파악합니다.  
  
## <a name="trace-instrumentation-and-distributed-applications"></a>추적 계측 및 분산 응용 프로그램  
 분산 응용 프로그램을 만드는 경우 사용되는 방식으로 응용 프로그램을 테스트하기 어려울 수 있습니다. 운영 체제나 웹 브라우저의 가능한 모든 조합(모든 지역화된 언어 옵션 포함)을 테스트하거나 동시에 응용 프로그램에 액세스하는 다수의 사용자를 시뮬레이션할 수 있는 개발 팀은 거의 없습니다. 이러한 상황에서는 분산 응용 프로그램이 높은 볼륨, 다양한 설정 및 고유한 최종 사용자 동작에 응답하는 방식을 테스트할 수 없습니다. 또한 분산 응용 프로그램의 많은 부분에는 이러한 부분과 직접 상호 작용하거나 해당 활동을 볼 수 있는 사용자 인터페이스가 없습니다.  
  
 그러나 애플리케이션을 *계측*(즉, 코드의 전략적 위치에 trace 문 배치)하여 분산 애플리케이션이 특히 발생한 문제와 같은 특정 이벤트를 시스템 관리자에게 설명할 수 있게 하면 이 기능을 보완할 수 있습니다. 그러면 런타임에 예기치 않은 문제가 발생할 경우(예: 과도하게 느린 응답 시간) 가능성이 높은 원인을 확인할 수 있습니다.  
  
 trace 문을 통해 원래 소스 코드를 검사, 수정 및 다시 컴파일하고 디버깅 환경 내에서 런타임 오류 생성을 시도하는 어려운 작업을 피할 수 있습니다. 응용 프로그램을 계측하여 오류를 표시하는 것은 물론 성능을 모니터링할 수도 있습니다.  
  
## <a name="strategic-placement-of-trace-statements"></a>Trace 문의 전략적 배치  
 런타임 중에 사용하기 위해 trace 문을 배치할 때는 특별히 주의해야 합니다. 가능한 모든 추적 시나리오가 적절하게 처리되도록 배포된 응용 프로그램에서 필요할 가능성이 큰 추적 정보를 고려해야 합니다. 그러나 추적을 사용하는 응용 프로그램은 매우 광범위하기 대문에 추적의 전략적 배치에 대한 일반적인 지침은 없습니다. 추적 문 [배치에 대 한 자세한 내용은 방법: 응용 프로그램 코드](how-to-add-trace-statements-to-application-code.md)에 Trace 문을 추가 합니다.  
  
## <a name="output-from-tracing"></a>추적 출력  
 추적 출력은 *수신기*라는 개체에 의해 수집됩니다. 수신기는 추적 출력을 받아 출력 장치(일반적으로 창, 로그 또는 텍스트 파일)에 쓰는 개체입니다. 새로 만든 추적 수신기는 일반적으로 <xref:System.Diagnostics.Trace.Listeners%2A?displayProperty=nameWithType> 컬렉션에 추가되므로 수신기가 모든 추적 출력을 받을 수 있습니다.  
  
 추적 정보는 최소한 기본 <xref:System.Diagnostics.Trace> 출력 대상인 <xref:System.Diagnostics.DefaultTraceListener>에는 항상 기록됩니다. 어떤 이유로든 다른 수신기를 <xref:System.Diagnostics.DefaultTraceListener> 컬렉션에 추가하지 않고 <xref:System.Diagnostics.Trace.Listeners%2A>를 삭제한 경우에는 추적 메시지를 받지 못하게 됩니다. 자세한 내용은 [추적 수신기](trace-listeners.md)를 참조하세요.  
  
 추적 정보를 기록하는 여섯 가지 <xref:System.Diagnostics.Debug> 멤버 및 <xref:System.Diagnostics.Trace> 메서드는 다음 표에 나와 있습니다.  
  
|메서드|출력|  
|------------|------------|  
|**Assert**|지정된 텍스트 또는 지정되지 않은 경우 호출 스택입니다. **Assert** 문에서 인수로 지정된 조건이 **false**인 경우에만 출력이 기록됩니다.|  
|**Fail**|지정된 텍스트 또는 지정되지 않은 경우 호출 스택입니다.|  
|**Write**|지정된 텍스트입니다.|  
|**WriteIf**|**WriteIf** 문에서 인수로 지정된 조건이 충족되는 경우 지정된 텍스트입니다.|  
|**WriteLine**|지정된 텍스트와 캐리지 리턴입니다.|  
|**WriteLineIf**|**WriteLineIf** 문에서 인수로 지정된 조건이 충족되는 경우 지정된 텍스트와 캐리지 리턴입니다.|  
  
 <xref:System.Diagnostics.Trace.Listeners%2A> 컬렉션의 모든 수신기는 위 표에 설명된 메시지를 받지만 메시지를 받는 수신기의 종류에 따라 다른 동작이 수행될 수 있습니다. 예를 들어 <xref:System.Diagnostics.DefaultTraceListener>는 **Fail** 또는 **Assert** 오류 알림을 받을 경우 어설션 대화 상자를 표시하지만 <xref:System.Diagnostics.TextWriterTraceListener>는 출력을 해당 스트림에 쓰기만 합니다.  
  
 고유한 수신기를 구현하여 사용자 지정 결과를 생성할 수 있습니다. 예를 들어 사용자 지정 추적 수신기는 메시지 상자에 메시지를 표시하거나 데이터베이스에 연결하여 테이블에 메시지를 추가할 수 있습니다. 모든 사용자 지정 수신기는 위에서 언급한 6가지 메서드를 지원해야 합니다. 개발자 정의 수신기를 만드는 방법에 대한 자세한 내용은 .NET Framework 참조에서 <xref:System.Diagnostics.TraceListener>를 참조하세요.  
  
 **Write** 및 **WriteLine** 메서드는 항상 지정된 텍스트를 씁니다. **Assert**, **WriteIf** 및 **WriteLineIf**에는 지정된 텍스트를 쓸지 여부를 제어하는 부울 인수를 사용해야 합니다. 이들 메서드는 식이 **true**(**WriteIf** 및 **WriteLineIf**) 또는 **false**(**Assert**)인 경우에만 지정된 텍스트를 씁니다. **Fail** 메서드는 항상 지정된 텍스트를 씁니다. 자세한 내용은 [방법: 응용 프로그램 코드](how-to-add-trace-statements-to-application-code.md) 및 .NET Framework 참조에 Trace 문을 추가 합니다.  
  
## <a name="security-concerns"></a>보안 고려 사항  
 ASP.NET 응용 프로그램을 배포하기 전에 추적 및 디버깅을 사용하지 않도록 설정하지 않으면 응용 프로그램이 해당 정보를 노출하여 악성 프로그램에서 악용될 수 있습니다. 자세한 내용은 [방법: 추적 및 디버그](how-to-compile-conditionally-with-trace-and-debug.md), [컴파일 및 빌드](/visualstudio/ide/compiling-and-building-in-visual-studio)및 [방법을 사용 하 여 조건부로 컴파일합니다. 추적 스위치](how-to-create-initialize-and-configure-trace-switches.md)만들기, 초기화 및 구성 IIS(인터넷 정보 서비스)를 통해 디버깅을 구성할 수도 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Diagnostics.Trace>
- <xref:System.Diagnostics.TraceSource>
- [코드 계약](code-contracts.md)
- [C#, F#, and Visual Basic Project Types](/visualstudio/debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types)(C#, F# 및 Visual Basic 프로젝트 형식)
- [방법: 응용 프로그램 코드에 Trace 문 추가](how-to-add-trace-statements-to-application-code.md)
- [방법: 추적 및 디버그를 사용한 조건부 컴파일](how-to-compile-conditionally-with-trace-and-debug.md)
- [방법: 추적 스위치 만들기, 초기화 및 구성](how-to-create-initialize-and-configure-trace-switches.md)
- [방법: 추적 소스 만들기 및 초기화](how-to-create-and-initialize-trace-sources.md)
- [방법: 추적 수신기와 함께 TraceSource 및 필터 사용](how-to-use-tracesource-and-filters-with-trace-listeners.md)
- [추적 수신기](trace-listeners.md)
- [추적 스위치](trace-switches.md)
