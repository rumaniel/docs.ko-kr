---
ms.openlocfilehash: 480cbdecd681408a7e1d6fa366e3f1a4b131ab42
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67857481"
---
### <a name="unicode-standard-version-80-categories-now-supported"></a>유니코드 표준 버전 8.0 범주가 이제 지원됨

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6.2에서 유니코드 데이터가 유니코드 표준 버전 6.3에서 8.0으로 업그레이드되었습니다.  .NET Framework 4.6.2에서 유니코드 문자 범주를 요청할 때 일부 결과가 이전 .NET Framework 버전의 결과와 일치하지 않을 수 있습니다.  이러한 변경은 주로 체로키어 음절 및 New Tai Lue 모음 기호 및 성조 표시에 영향을 미칩니다.|
|제안|코드를 검토하고 하드 코드된 유니코드 문자 범주에 종속된 논리를 제거/변경해야 합니다.|
|범위|부|
|버전|4.6.2|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Char.GetUnicodeCategory(System.Char)?displayProperty=nameWithType></li><li><xref:System.Globalization.CharUnicodeInfo.GetUnicodeCategory(System.Char)?displayProperty=nameWithType></li><li><xref:System.Globalization.CharUnicodeInfo.GetUnicodeCategory(System.String,System.Int32)?displayProperty=nameWithType></li></ul>|

