---
ms.openlocfilehash: 38c35f3f6f2262d06409690d2326d9b982e1ec86
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804506"
---
### <a name="managed-browser-hosting-controls-from-the-net-framework-11-and-20-are-blocked"></a>.NET Framework 1.1 및 2.0에서 관리되는 브라우저 호스팅 컨트롤이 차단됩니다.

|   |   |
|---|---|
|세부 정보|이러한 컨트롤의 호스팅은 Internet Explorer에서 차단됩니다.|
|제안 해결 방법|Internet Explorer에서는 관리되는 브라우저 호스팅 컨트롤을 사용하는 애플리케이션을 시작하지 못합니다. x86 시스템 및 x64 시스템의 32비트 프로세스의 경우 레지스트리 하위 키 <code>HKLM/SOFTWARE/MICROSOFT/.NETFramework</code>의 EnableIEHosting 값을 <code>1</code>로 설정하고, x64 시스템의 64비트 프로세스의 경우 레지스트리 하위 키 <code>HKLM/SOFTWARE/Wow6432Node/Microsoft/.NETFramework</code>의 <code>EnableIEHosting</code> 값을 <code>1</code>로 설정하여 이전 동작을 복원할 수 있습니다.|
|범위|부|
|버전|4.5|
|형식|런타임|
