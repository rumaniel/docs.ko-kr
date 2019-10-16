---
title: 개체 또는 클래스가 이벤트 집합을 지원하지 않습니다.
ms.date: 07/20/2015
f1_keywords:
- vbrID459
ms.assetid: 785df3f3-2aae-4a25-af36-1f9879d4e5fd
ms.openlocfilehash: ad9176b5332a75f03968e742501c3fce541055de
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61925764"
---
# <a name="object-or-class-does-not-support-the-set-of-events"></a>개체 또는 클래스가 이벤트 집합을 지원하지 않습니다.
사용 하려는 `WithEvents` 지정한 이벤트 집합에 대 한 이벤트 원본으로 작동할 수 없습니다. 구성 요소를 사용 하 여 변수입니다. 예를 들어, 하려는 개체의 이벤트를 다른 개체를 만들 `Implements` 첫 번째 개체입니다. 구현 된 개체에서 이벤트를 싱크할 수 생각 하지만이 아닌 경우 항상 대/소문자 `Implements` 메서드 및 속성에 대 한 인터페이스를 구현합니다. `WithEvents` 개인에 대 한 지원 되지 않습니다 `UserControls`이므로 발생 시키는 데 필요한 형식 정보를 `ObjectEvent` 런타임에 사용할 수 없는 합니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 이벤트 소스가 아닌 하는 구성 요소에 대 한 이벤트를 싱크할 수 없습니다.  
  
## <a name="see-also"></a>참고자료

- [WithEvents](../../../visual-basic/language-reference/modifiers/withevents.md)
- [Implements 문](../../../visual-basic/language-reference/statements/implements-statement.md)
