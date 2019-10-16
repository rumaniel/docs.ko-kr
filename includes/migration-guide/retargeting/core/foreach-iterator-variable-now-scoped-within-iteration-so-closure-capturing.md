---
ms.openlocfilehash: 1805c26f1eff46719f30de8a14ca6d35f01948a6
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774413"
---
### <a name="foreach-iterator-variable-is-now-scoped-within-the-iteration-so-closure-capturing-semantics-are-different-in-c5"></a>Foreach 반복자 변수는 이제 반복 내에서 범위가 지정되므로 클로저 캡처 의미가 다름(C#5에서)

|   |   |
|---|---|
|세부 정보|C#5(Visual Studio 2012)부터 <code>foreach</code> 반복기 변수는 반복 내에서 범위가 지정됩니다. 이것은 코드가 이전에 <code>foreach</code>의 클로저에 포함되지 않기 위해 변수에 종속되었던 경우 중단이 발생할 수 있습니다. 이러한 변경의 증상은 대리자에게 전달된 반복기 변수가 대리자가 호출된 때의 값이 아닌 대리자가 생성된 때의 값으로 처리된다는 것입니다.|
|제안 해결 방법|이상적으로 코드는 새 컴파일러 동작을 예상하도록 업데이트되어야 합니다. 이전의 의미 체계가 필요한 경우 반복기 변수는 루프 외부에 명시적으로 배치된 별도의 변수로 대체할 수 있습니다.|
|범위|주요함|
|버전|4.5|
|형식|대상 변경|
