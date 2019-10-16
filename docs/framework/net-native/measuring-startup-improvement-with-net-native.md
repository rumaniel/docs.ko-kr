---
title: .NET 네이티브로 시작 속도 개선 측정
ms.date: 03/30/2017
ms.assetid: c4d25b24-9c1a-4b3e-9705-97ba0d6c0289
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 74011a4c70cc8f7da3973698a43b1e97cffb9f9b
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70927076"
---
# <a name="measuring-startup-improvement-with-net-native"></a>.NET 네이티브로 시작 속도 개선 측정
.NET 네이티브 앱의 시작 시간을 크게 향상 시킵니다. 이러한 속도 개선은 휴대용 저전력 디바이스와 복잡한 앱에서 특히 두드러지게 나타납니다. 이 항목에서는 이러한 시작 속도 개선을 측정하는 데 필요한 기본적인 계측을 시작하는 방법을 설명합니다.  
  
 성능을 쉽게 조사할 수 있도록 .NET Framework 및 Windows에서는 이벤트 발생 시 앱이 도구에 이벤트를 알릴 수 있도록 하는 ETW(Windows용 이벤트 추적)라는 이벤트 프레임워크를 사용합니다. ETW 이벤트 알림을 받으면 PerfView라는 도구를 사용하여 해당 이벤트를 쉽게 확인하고 분석할 수 있습니다. 이 항목에서는 다음 작업을 수행하는 방법을 설명합니다.  
  
- <xref:System.Diagnostics.Tracing.EventSource> 클래스를 사용하여 이벤트를 내보냅니다.  
  
- PerfView를 사용하여 이러한 이벤트를 수집합니다.  
  
- PerfView를 사용하여 이러한 이벤트를 표시합니다.  
  
## <a name="using-eventsource-to-emit-events"></a>EventSource를 사용하여 이벤트 내보내기  
 <xref:System.Diagnostics.Tracing.EventSource>는 사용자 지정 이벤트 공급자를 만드는 데 사용할 수 있는 기본 클래스를 제공합니다. 일반적으로는 <xref:System.Diagnostics.Tracing.EventSource>의 하위 클래스를 만든 다음 `Write*` 메서드를 고유한 이벤트 메서드로 래핑합니다. 각 <xref:System.Diagnostics.Tracing.EventSource>에는 보통 singleton 패턴이 사용됩니다.  
  
 예를 들어 다음 예제의 클래스를 사용하면 두 가지 성능 특성을 측정할 수 있습니다.  
  
- `App` 클래스 생성자가 호출될 때까지의 시간  
  
- `MainPage` 생성자가 호출될 때까지의 시간  
  
 [!code-csharp[ProjectN_ETW#1](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_etw/cs/etw1.cs#1)]  
  
 위의 코드에서 몇 가지 사항을 살펴보고 넘어가겠습니다. 먼저, singleton은 `AppEventSource.Log`에서 작성됩니다. 이 인스턴스가 모든 로깅에 사용됩니다. 둘째로, 각 이벤트 메서드에는 <xref:System.Diagnostics.Tracing.EventAttribute>가 있습니다. 따라서 도구가 <xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A> 메서드의 인덱스를 인덱스 `AppEventSource`에서 호출된 메서드에 연결할 수 있습니다.  
  
 이러한 이벤트는 전적으로 설명을 위해 제공되는 것이며, 대부분의 앱 코드는 이러한 이벤트가 발생한 후에 실행됩니다. 코드에서 사용자 상호 작용에 해당하는 이벤트를 파악하고 측정한 다음 해당 벤치마크를 개선해야 합니다. 또한 이벤트 자체는 한 번에 하나의 인스턴스만 기록합니다. 그러나 모든 작업에서는 시작 이벤트와 중지 이벤트가 쌍으로 발생하면 유용한 경우가 많습니다. 앱 시작을 검사할 때 시작 이벤트는 대개 운영 체제에서 내보내는 “Process/Start” 이벤트입니다.  
  
 RSS 판독기를 만드는 경우를 예로 들어 보겠습니다. 이벤트가 기록되는 몇 가지 주요 시기는 다음과 같습니다.  
  
- 기본 페이지를 처음 렌더링할 때  
  
- 이전 RSS 스토리를 로컬 스토리지에서 deserialize할 때  
  
- 앱이 새 스토리 동기화를 시작할 때  
  
- 앱이 새 스토리 동기화를 완료할 때  
  
 앱을 계측 하는 것은 간단 합니다. 파생 클래스에서 적절 한 메서드를 호출 하기만 하면 됩니다. 이전 예제에서는 `AppEventSource`를 사용하면 다음과 같이 앱을 계측할 수 있습니다.  
  
 [!code-csharp[ProjectN_ETW#2](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_etw/cs/etw2.cs#2)]  
  
 앱이 계측되고 나면 이벤트를 수집할 수 있습니다.  
  
## <a name="gathering-events-with-perfview"></a>PerfView를 사용하여 이벤트 수집  
 PerfView는 앱에서 모든 종류의 성능 조사를 수행할 수 있도록 ETW 이벤트를 활용합니다. 또한 다양한 이벤트 유형에 대한 로깅을 설정하거나 해제할 수 있도록 구성 GUI도 포함되어 있습니다. PerfView는 무료 도구이며 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=28567)에서 다운로드할 수 있습니다. 자세한 내용은 [PerfView 자습서 비디오](https://channel9.msdn.com/Series/PerfView-Tutorial)를 보세요.  
  
> [!NOTE]
> PerfView를 사용하여 ARM 시스템에 대한 이벤트를 수집할 수는 없습니다. ARM 시스템에 대한 이벤트를 수집하려면 WPR(Windows Performance Recorder)를 사용합니다. 자세한 내용은 [Vance Morrison의 블로그 게시물](https://blogs.msdn.microsoft.com/vancem/2012/12/19/collecting-etwperfview-data-on-an-windows-rt-winrt-arm-surface-device/)을 참조하세요.  
  
 명령줄에서 PerfView를 호출할 수도 있습니다. 공급자의 이벤트만 기록하려면 명령 프롬프트 창을 열고 다음 명령을 입력합니다.  
  
```console
perfview -KernelEvents:Process -OnlyProviders:*MyCompany-MyApp collect outputFile   
```  
  
 각 항목이 나타내는 의미는 다음과 같습니다.  
  
 `-KernelEvents:Process`  
 프로세스가 시작 및 중지되는 시기를 확인할 것임을 나타냅니다. 이 경우 다른 이벤트 시간에서 앱의 Process/Start 이벤트 시간을 빼야 하므로 해당 이벤트를 확인해야 합니다.  
  
 `-OnlyProviders:*MyCompany-MyApp`  
 PerfView가 기본적으로 설정하는 기타 공급자를 해제하고 MyCompany-MyApp 공급자를 설정합니다.  별표는 이 공급자가 <xref:System.Diagnostics.Tracing.EventSource>임을 나타냅니다.  
  
 `collect outputFile`  
 수집을 시작하고 데이터를 outputFile.etl.zip에 저장할 것임을 나타냅니다.  
  
 PerfView를 시작한 후 앱을 실행 합니다. 앱을 실행할 때는 다음과 같은 사항에 유념해야 합니다.  
  
- 디버그 빌드가 아닌 릴리스 빌드를 사용합니다. 디버그 빌드에는 오류 검사 및 오류 처리 코드가 추가로 포함되어 있는 경우가 많아 앱 실행 속도가 예상보다 느릴 수 있습니다.  
  
- 디버거를 연결하여 앱을 실행하면 앱 성능이 저하됩니다.  
  
- Windows에서는 앱 시작 시간을 단축하기 위해 여러 가지 캐싱 전략을 사용합니다. 현재 메모리에 캐시되어 있어 디스크에서 로드할 필요가 없는 앱은 빠르게 시작됩니다. 일관성을 유지하려면 시작 시간을 측정하기 전에 앱을 몇 번 시작했다가 닫으세요.  
  
 PerfView가 내보내기된 이벤트를 수집할 수 있도록 앱을 실행했으면 **수집 중지** 단추를 선택합니다. 일반적으로는 불필요한 이벤트가 수집되지 않도록 앱을 닫기 전에 컬렉션을 중지해야 합니다. 그러나 종료 또는 일시 중단 성능을 측정하는 경우에는 컬렉션을 계속해도 됩니다.  
  
## <a name="displaying-the-events"></a>이벤트 표시  
 이미 수집된 이벤트를 보려면 PerfView를 사용하여 작성한 .etl 또는 .etl.zip 파일을 열고 **이벤트**를 선택합니다. ETW는 다른 프로세스의 이벤트를 비롯하여 많은 이벤트에 대한 정보를 수집합니다. 특정 이벤트만 중점적으로 조사하려면 이벤트 뷰에서 다음 텍스트 상자에 정보를 입력합니다.  
  
- **프로세스 필터** 상자에 “.exe”를 제외한 앱 이름을 지정합니다.  
  
- **이벤트 형식 필터** 상자에 `Process/Start | MyCompany-MyApp`를 지정합니다. 그러면 MyCompany-MyApp의 이벤트와 Windows Kernel/Process/Start 이벤트에 대한 필터가 설정됩니다.  
  
 Ctrl+A를 눌러 왼쪽 창에 나열된 모든 이벤트를 선택하고 **Enter** 키를 누릅니다. 이제 각 이벤트에서 타임스탬프를 확인할 수 있습니다. 이러한 타임스탬프는 추적 시작 시간을 기준으로 하므로 프로세스 시작 시간에서 각 이벤트의 시간을 빼서 시작 이후 경과된 시간을 확인해야 합니다. Ctrl 키를 누른 상태로 두 타임스탬프를 클릭하여 선택하면 해당 타임스탬프 간의 차이가 페이지 아래쪽 상태 표시줄에 표시됩니다. 따라서 표시된 두 이벤트(프로세스 시작 포함) 간에 경과된 시간을 쉽게 확인할 수 있습니다. 뷰의 바로 가기 메뉴를 열고 CSV 파일로 내보내기, Microsoft Excel을 열어 데이터 저장/처리 등의 여러 유용한 옵션 중에서 원하는 항목을 선택할 수 있습니다.  
  
 원본 앱과 .NET 네이티브 도구 체인을 사용 하 여 빌드한 버전 모두에 대해이 절차를 반복 하면 성능 차이를 비교할 수 있습니다.   .NET 네이티브 앱은 일반적으로 non-.NET 네이티브 앱 보다 빠르게 시작 됩니다. 관련 정보를 보다 자세하게 파악하려는 경우 PerfView를 통해 시간이 가장 많이 걸리는 코드 부분도 확인할 수 있습니다. 자세한 내용은 [PerfView 자습서](https://channel9.msdn.com/Series/PerfView-Tutorial)를 보거나 [Vance Morrison의 블로그 게시물](https://blogs.msdn.microsoft.com/vancem/2011/12/28/publication-of-the-perfview-performance-analysis-tool/)을 읽으세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Diagnostics.Tracing.EventSource>
