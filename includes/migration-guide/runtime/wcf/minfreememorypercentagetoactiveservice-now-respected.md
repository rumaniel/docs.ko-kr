---
ms.openlocfilehash: fa472b3a142f55f0cbdd83eabbbb00bddd9786d8
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59235637"
---
### <a name="minfreememorypercentagetoactiveservice-is-now-respected"></a>MinFreeMemoryPercentageToActiveService가 지금 적용됩니다.

|   |   |
|---|---|
|세부 정보|이 설정은 WCF 서비스 활성화를 위해 서버에서 사용할 수 있는 최소 메모리를 지정합니다. 또한 이 설정은 <xref:System.OutOfMemoryException?displayProperty=name> 예외가 발생되지 않도록 설계되었습니다. .NET Framework 4.5에서 이 설정은 영향을 주지 않았습니다. .NET Framework 4.5.1에서 해당 설정이 적용됩니다.|
|제안 해결 방법|웹 서버의 사용 가능한 메모리가 구성 설정에서 정의된 백분율보다 적은 경우 예외가 발생합니다. 성공적으로 시작되었지만 제한된 메모리 환경에서 실행되는 일부 WCF 서비스의 경우 실패할 수 있습니다.|
|범위|부|
|버전|4.5.1|
|형식|런타임|
