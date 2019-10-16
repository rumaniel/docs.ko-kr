---
ms.openlocfilehash: 78f4d533f1efdc8d43a9ab96508b84a77e3260bc
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67803172"
---
### <a name="no-longer-able-to-set-enableviewstatemac-to-false"></a>더 이상 EnableViewStateMac를 false로 설정할 수 없음

|   |   |
|---|---|
|세부 정보|ASP.NET에서 개발자는 더 이상 <code>&lt;pages enableViewStateMac=&quot;false&quot;/&gt;</code> 또는 <code>&lt;@Page EnableViewStateMac=&quot;false&quot; %&gt;</code>를 지정할 수 없습니다. 포함된 뷰 상태가 사용된 모든 요청에 뷰 상태 MAC(메시지 인증 코드)가 적용됩니다. EnableViewStateMac 속성이 <code>false</code>로 명시적으로 설정된 앱에만 영향을 줍니다.|
|제안 해결 방법|EnableViewStateMac은 true로 간주되어야 하고 모든 결과 MAC 오류는(MAC 오류 원인의 세부 정보에 따른 여러 해결 방법을 포함하는 [이 지침](https://support.microsoft.com/kb/2915218)에 설명된 대로) 해결되어야 합니다.|
|범위|주요함|
|버전|4.5.2|
|형식|런타임|

