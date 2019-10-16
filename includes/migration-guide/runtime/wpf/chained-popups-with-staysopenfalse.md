---
ms.openlocfilehash: 2bb40294685c987de84138ee889e6b88f7184bb0
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67857267"
---
### <a name="chained-popups-with-staysopenfalse"></a>StaysOpen = False인 연결된 팝업

|   |   |
|---|---|
|세부 정보|StaysOpen = False인 팝업은 팝업 외부를 클릭하면 닫히게 되어 있습니다. 이러한 팝업이 두 개 이상 연결된 경우(즉, 한 팝업에 다른 팝업이 포함된 경우) 다음과 같은 여러 문제가 발생했습니다.<ul><li>두 수준을 열고 P2의 외부이면서 P1의 내부인 부분을 클릭합니다.  아무 반응이 없습니다.</li><li>두 수준을 열고 P1 외부를 클릭합니다.  두 팝업이 닫힙니다.</li><li>두 수준을 열고 닫습니다.  그런 다음, P2를 다시 열어봅니다.  아무 반응이 없습니다.</li><li>세 가지 수준을 열어봅니다.  열리지 않습니다.  (클릭한 위치에 따라 아무 일도 일어나지 않거나 처음 두 수준이 닫힙니다.) 이러한 경우(및 다른 변형)는 이제 정상적으로 작동합니다.</li></ul>|
|범위|Microsoft Edge|
|버전|4.7.1|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Windows.Controls.Primitives.Popup.StaysOpen?displayProperty=nameWithType></li></ul>|

