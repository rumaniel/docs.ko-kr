---
ms.openlocfilehash: c1a2d76b4e596acc395da6cefed008078e57a336
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67858603"
---
### <a name="null-coalescer-values-are-not-visible-in-debugger-until-one-step-later"></a>디버거에서 한 단계가 지날 때까지 null 병합기 값을 볼 수 없습니다.

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5의 버그로 인해 64 비트 버전의 Framework에서 실행 중인 경우 할당 작업이 실행된 직후 null 병합 작업을 통해 설정된 값이 디버거에 표시되지 않습니다.|
|제안|디버거에서 한 단계 더 실행하면 로컬/필드의 값이 올바르게 업데이트됩니다. 또한 이 문제는 .NET Framework 4.6에서 해결되어 해당 버전의 Framework로 업그레이드하여 문제를 해결할 수 있습니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|

