---
ms.openlocfilehash: ff4d67a1c821fc96130c4efbd88eb5c56766da06
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "66379656"
---
### <a name="wpf-dispatchersynchronizationcontextcreatecopy-now-returns-a-new-copy-instead-of-the-current-instance"></a>이제 WPF DispatcherSynchronizationContext.CreateCopy는 현재 인스턴스 대신 새 복사본을 반환

|   |   |
|---|---|
|세부 정보|.NET Framework 4에서 <xref:System.Windows.Threading.DispatcherSynchronizationContext.CreateCopy>는 주로 성능 최적화로서 현재 인스턴스에 대한 참조를 반환합니다. .NET Framework 4.5에서는 처음으로 동일한 참조가 실행 스레드를 올바른 동기화 컨텍스트에 나타내도록 마무리하는 것을 가능하게 하는 새 인스턴스를 반환합니다.  이러한 참조의 ID를 확인하는 코드가 영향을 받기는 어렵지만, 변경 내용 때문에 <xref:System.Windows.Threading.DispatcherSynchronizationContext.CreateCopy>를 호출하는 코드는 .NET Framework 4.5 이상으로의 마이그레이션 과정에서 테스트되어야 합니다.|
|제안 해결 방법|<xref:System.Windows.Threading.DispatcherSynchronizationContext.CreateCopy>는 새로운 <xref:System.Threading.SynchronizationContext?displayProperty=name> 개체를 반환합니다. 이전에는 이러한 방식으로 생성된 참조의 동등성을 사용한 코드는 적절한 컨텍스트에 있는지 실제로 확인되지 않았지만 .NET Framework 4.5 이상에 대해 빌드할 때는 확인됩니다.  문제가 발생할 가능성은 작지만 발생하는 경우 영향을 받은 코드 경로를 실행하는 것으로 확인하기에 충분할 것입니다.|
|범위|부|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Windows.Threading.DispatcherSynchronizationContext.CreateCopy?displayProperty=nameWithType></li></ul>|
