---
title: .NET Framework 성능
ms.date: 03/30/2017
helpviewer_keywords:
- performance [.NET Framework]
- reliability [.NET Framework]
ms.assetid: c1676cca-3f1a-41ec-b469-9029566074fc
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3d3e26c835a96bba3c97e471075f5d02b5330461
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50201571"
---
# <a name="net-framework-performance"></a>.NET Framework 성능
성능이 우수한 앱을 만들려면 앱의 다른 모든 기능을 디자인하는 것처럼 성능을 디자인하고 계획해야 합니다. 앱의 성능을 측정할 수 있도록 Microsoft에서 제공하는 도구를 사용하고 필요한 경우 메모리 사용, 코드 처리량 및 응답성을 향상시킬 수 있습니다. 이 항목에는 Microsoft에서 제공하는 성능 분석 도구가 나열되어 있으며, 앱 개발의 특정 영역에 대한 성능을 설명하는 다른 항목의 링크가 제공되어 있습니다.  
  
## <a name="designing-and-planning-for-performance"></a>성능 디자인 및 계획  
 성능이 우수한 앱을 만들려면 다른 모든 기능을 디자인하는 것처럼 앱에 성능을 디자인해야 합니다. 앱에서 성능이 중요한 시나리오를 확인하고 성능 목표를 설정하며 이러한 앱 시나리오에 대한 성능을 조기에 그리고 자주 측정해야 합니다. 각 앱이 다르고 각 앱의 성능이 중요한 실행 경로도 다르므로 이러한 경로를 조기에 확인하여 노력을 집중하면 생산성을 극대화할 수 있습니다.  
  
 고성능 앱을 만들기 위해 대상 플랫폼에 완벽하게 익숙해질 필요는 없습니다. 그러나 대상 플랫폼의 어느 부분이 성능 측면에서 비용이 많이 드는지에 대한 이해도를 높여야 합니다. 개발 프로세스에서 조기에 성능을 측정하여 이렇게 할 수 있습니다.  
  
 성능에 중요한 영역을 확인하고 성능 목표를 설정하려면 항상 사용자 경험을 고려합니다. 시작 시간과 응답성은 사용자의 앱에 대한 인식에 영향을 미치는 두 주요 영역입니다. 앱이 메모리를 많이 사용하는 경우 사용자에게 느리게 보이거나 시스템에서 실행되고 있는 다른 앱에 영향을 미칠 수 있습니다. 또는 일부 경우 Windows 스토어 또는 Windows Phone 스토어 전송 프로세스가 실패할 수 있습니다. 또한 코드의 어느 부분이 더 자주 실행되는지 확인하면 코드의 이러한 부분이 잘 최적화되었는지도 확인할 수 있습니다.  
  
## <a name="analyzing-performance"></a>성능 분석  
 전체 개발 계획의 일부로, 개발 중에 앱의 성능을 측정하고 결과를 이전에 설정한 목표와 비교하는 지점을 설정합니다. 사용자가 사용할 것으로 예상되는 환경 및 하드웨어에서 앱을 측정합니다. 조기에 그리고 자주 앱의 성능을 분석함으로써 개발 주기의 나중 단계에서 수정할 경우 비용이 많이 들게 될 아키텍처 관련 결정 사항을 변경할 수 있습니다. 다음 섹션에서는 앱을 분석하는 데 사용할 수 있는 성능 도구를 설명하고, 이러한 도구에서 사용되는 이벤트 추적을 설명합니다.  
  
### <a name="performance-tools"></a>성능 도구  
 다음은 .NET Framework 앱에 사용할 수 있는 몇 가지 성능 도구입니다.  
  
|도구|설명|  
|----------|-----------------|  
|Visual Studio 성능 분석|Windows 운영 체제를 실행하는 컴퓨터에 배포할 .NET Framework 앱의 CPU 사용률을 분석하는 데 사용합니다.<br /><br /> 이 도구는 Visual Studio에서 프로젝트를 연 후 **디버그** 메뉴에서 사용할 수 있습니다. 자세한 내용은 [성능 탐색기](/visualstudio/profiling/performance-explorer)을 비롯한 다양한 도구를 사용할 수 있습니다. **참고:** Windows Phone을 대상으로 할 경우 Windows Phone 응용 프로그램 분석(다음 행 참조)을 사용하세요.|  
|Windows Phone 응용 프로그램 분석|Windows Phone 앱의 CPU 및 메모리, 네트워크 데이터 전송 속도, 앱 응답성 및 배터리 소비를 분석하는 데 사용합니다.<br /><br /> 이 도구는 [Windows Phone SDK](https://go.microsoft.com/fwlink/?LinkId=265773)를 설치한 후 Visual Studio에서 Windows Phone 프로젝트의 **디버그** 메뉴에서 사용할 수 있습니다. 자세한 내용은 [App profiling for Windows Phone](https://msdn.microsoft.com/library/windowsphone/develop/jj215908\(v=vs.105\).aspx)(Windows Phone 앱 프로파일링)을 참조하세요.|  
|[PerfView](https://www.microsoft.com/download/details.aspx?id=28567)|CPU 및 메모리 관련 성능 문제를 식별하는 데 사용합니다. 이 도구는 ETW(Windows용 이벤트 추적) 및 CLR 프로파일링 API를 사용하여 가비지 컬렉션 및 JIT 컴파일에 대한 정보와 고급 메모리 및 CPU 확인 기능을 제공합니다. PerfView 사용 방법에 대한 자세한 내용은 앱에 포함된 자습서 및 도움말 파일, [Channel 9 비디오 자습서](https://channel9.msdn.com/Series/PerfView-Tutorial) 및 [블로그 게시물](https://blogs.msdn.com/b/vancem/archive/tags/perfview/)을 참조하세요.<br /><br /> 메모리 관련 문제는 [Using PerfView for Memory Investigations](https://channel9.msdn.com/Series/PerfView-Tutorial/PerfView-Tutorial-9-NET-Memory-Investigation-Basics-of-GC-Heap-Snapshots)(메모리 확인에 PerfView 사용)를 참조하세요.|  
|[Windows Performance Analyzer](https://www.microsoft.com/download/details.aspx?id=30652)|동일한 컴퓨터에서 여러 앱이 실행되고 있는 경우 앱의 메모리 및 저장소 사용과 같은 전체 시스템 성능을 확인하는 데 사용합니다. 이 도구는 다운로드 센터에서 [!INCLUDE[win8](../../../includes/win8-md.md)]용 Windows ADK(평가 및 배포 키트)의 일부로 사용할 수 있습니다. 자세한 내용은 [Windows Performance Analyzer](/windows-hardware/test/wpt/windows-performance-analyzer)를 참조하세요.|  
  
### <a name="event-tracing-for-windows-etw"></a>ETW(Windows용 이벤트 추적)  
 ETW는 실행 중인 코드에 대한 진단 정보를 얻을 수 있는 기술로서, 앞에서 언급한 여러 성능 도구에 필수적입니다. ETW는 .NET Framework 앱 및 Windows에서 특정 이벤트가 발생하면 로그를 만듭니다. ETW를 사용하면 동적으로 로깅을 사용하거나 사용하지 않도록 설정할 수 있어 앱을 다시 시작하지 않고도 프로덕션 환경에서 자세한 추적을 수행할 수 있습니다. .NET Framework는 ETW 이벤트에 대한 지원을 제공하고, ETW는 성능 데이터를 생성하기 위해 여러 프로파일링 및 성능 도구에서 사용됩니다. 이러한 도구는 ETW 이벤트를 자주 사용하거나 사용하지 않도록 설정하므로 익숙해지는 것이 좋습니다. 특정 ETW 이벤트를 사용하여 앱의 특정 구성 요소에 대한 성능 정보를 수집할 수 있습니다. .NET Framework의 ETW 지원에 대한 자세한 내용은 [공용 언어 런타임의 ETW 이벤트](../../../docs/framework/performance/etw-events-in-the-common-language-runtime.md) 및 [작업 병렬 라이브러리 및 PLINQ의 ETW 이벤트](../../../docs/framework/performance/etw-events-in-task-parallel-library-and-plinq.md)를 참조하세요.  
  
## <a name="performance-by-app-type"></a>응용 프로그램 종류별 성능  
 .NET Framework 앱 형식마다 성능을 평가하기 위한 모범 사례, 고려 사항 및 도구가 다릅니다. 다음 테이블에는 특정 .NET Framework 앱 형식에 대한 성능 항목 링크가 표시되어 있습니다.  
  
|앱 형식|참조|  
|--------------|---------|  
|모든 플랫폼용 .NET Framework 앱|[가비지 수집 및 성능](../../../docs/standard/garbage-collection/performance.md)<br /><br /> [성능 팁](../../../docs/framework/performance/performance-tips.md)|  
|C++, C# 및 Visual Basic으로 작성된 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱|[C++, C# 및 Visual Basic을 사용하는 Windows 스토어 앱의 성능 모범 사례](https://docs.microsoft.com/previous-versions/windows/apps/hh750313%28v=win.10%29)|  
|Windows Phone|[App performance considerations for Windows Phone](https://msdn.microsoft.com/library/windowsphone/develop/ff967560\(v=vs.105\).aspx)(Windows Phone의 앱 성능 고려 사항)<br /><br /> [Windows Phone Application Analysis](https://msdn.microsoft.com/library/windowsphone/develop/hh202934\(v=vs.105\).aspx)(Windows Phone 응용 프로그램 분석)<br /><br /> [Get Your Windows Phone Applications in the Marketplace Faster](https://msdn.microsoft.com/magazine/hh781024.aspx)(Windows Phone 응용 프로그램을 Marketplace에 더 빨리 등록하는 방법)|  
|WPF(Windows Presentation Foundation)|[WPF 성능 제품군](https://msdn.microsoft.com/library/67cafaad-57ad-4ecb-9c08-57fac144393e)|  
|Silverlight|[성능 팁](https://msdn.microsoft.com/library/cc189071\(v=vs.95\).aspx)|  
|ASP.NET|[ASP.NET 성능 개요](https://msdn.microsoft.com/library/f882bf1b-a009-4312-ac06-74370ffabc0b)|  
|Windows Forms|[Practical Tips for Boosting the Performance of Windows Forms Apps](https://msdn.microsoft.com/magazine/cc163630.aspx)(Windows Forms 앱의 성능을 향상시키기 위한 실제 팁)|  
  
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[.NET Framework 응용 프로그램에서 캐시](../../../docs/framework/performance/caching-in-net-framework-applications.md)|데이터를 캐시하여 앱 성능을 향상시키는 방법을 설명합니다.|  
|[초기화 지연](../../../docs/framework/performance/lazy-initialization.md)|필요한 대로 개체를 초기화하여 성능을 향상시키는 방법을 설명합니다(특히, 앱 시작 시).|  
|[안정성](../../../docs/framework/performance/reliability.md)|서버 환경에서의 비동기 예외 방지에 대한 정보를 제공합니다.|  
|[대형 응답성 .NET Framework 앱 작성](../../../docs/framework/performance/writing-large-responsive-apps.md)|C# 및 Visual Basic 컴파일러를 관리 코드로 다시 작성하면서 수집한 성능 팁을 제공하고, C# 컴파일러의 실제 몇 가지 예가 포함되어 있습니다.|
