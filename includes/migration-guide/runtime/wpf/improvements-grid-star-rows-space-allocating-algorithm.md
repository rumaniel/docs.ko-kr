---
ms.openlocfilehash: 8e0c934cd8c3cb8c08a526c7e145436db6ecf4a5
ms.sourcegitcommit: 4d8efe00f2e5ab42e598aff298d13b8c052d9593
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68237607"
---
### <a name="improvements-to-grid-star-rows-space-allocating-algorithm"></a>그리드 별 행 공간 할당 알고리즘 개선

|   |   |
|---|---|
|세부 정보|.NET Framework 4.7에 도입된<xref:System.Windows.Controls.Grid> [에서 크기를 에 할당하기 위한  알고리즘의](https://github.com/Microsoft/dotnet/blob/master/Documentation/compatibility/wpf-grid-allocation-of-space-to-star-columns.md) 버그가 수정되었습니다.  빈 행이 포함된 <code>Height=&quot;Auto&quot;</code>가 있는 그리드와 같은 일부 경우에는 행이 잘못된 위치에 정렬되었으며 그리드 외부에 배치되었을 수 있습니다.|
|제안 해결 방법|애플리케이션이 이러한 변경의 이점을 활용하도록 하기 위해 .NET Framework 4.8 이상에서 실행해야 합니다.|
|범위|주요함|
|버전|4.8|
|형식|런타임|
