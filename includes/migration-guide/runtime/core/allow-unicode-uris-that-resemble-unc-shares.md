---
ms.openlocfilehash: d3c6818861f8b0261a9a71a4654029143d928d08
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67856989"
---
### <a name="allow-unicode-in-uris-that-resemble-unc-shares"></a>UNC 공유와 비슷한 URI에서 유니코드 허용

|   |   |
|---|---|
|세부 정보|<xref:System.Uri?displayProperty=fullName>에서 UNC 공유 이름 및 유니코드 문자 모두를 포함하는 파일 URI를 생성하면 더 이상 잘못된 내부 상태의 URI를 발생하지 않습니다. 이 동작은 다음의 모든 것이 True인 경우에만 변경됩니다.<ul><li>URI는 구성표 <code>file:</code>을 보유하며 4개 이상의 슬래시가 뒤따라야 합니다.</li><li>호스트 이름은 밑줄 또는 기타 예약되지 않은 기호로 시작합니다.</li><li>URI에 유니코드 문자가 포함되어 있습니다.</li></ul>|
|제안|지속적으로 유니코드를 포함하는 URI를 사용하여 작동하는 애플리케이션은 UNC 공유에 대한 참조를 허용하지 않기 위해 이 동작을 사용했습니다. 이러한 애플리케이션은 대신 <xref:System.Uri.IsUnc>을 사용해야 합니다.|
|범위|Microsoft Edge|
|버전|4.7.2|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Uri?displayProperty=nameWithType></li></ul>|

