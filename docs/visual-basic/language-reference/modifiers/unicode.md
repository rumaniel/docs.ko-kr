---
title: Unicode(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Unicode
helpviewer_keywords:
- Unicode, external references
- Declare statement [Visual Basic], marshaling strings
- Unicode keyword [Visual Basic]
- Unicode, marshaling strings
ms.assetid: 0021d5ff-3209-444e-8497-420f3e6ee075
ms.openlocfilehash: b3c9452f8d144fb18ea3efcb35b85caed80e8692
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61778679"
---
# <a name="unicode-visual-basic"></a>Unicode(Visual Basic)
Visual Basic 선언 되는 외부 프로시저의 이름에 관계 없이 유니코드 값으로 모든 문자열을 마샬링하고 지정 합니다.  
  
 프로젝트 외부에서 정의 된 프로시저를 호출할 때 Visual Basic 컴파일러는 절차를 올바르게 호출 하려면 있어야 정보에 액세스할 수 없습니다. 문자열 문자 집합 사용 및 프로시저 위치한, 식별 하는 방법이, 호출 시퀀스가 및 반환 형식으로이 정보 포함 됩니다. 합니다 [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md) 외부 프로시저에 대 한 참조를 만들고이 필요한 정보를 제공 합니다.  
  
 `charsetmodifier` 부분을 `Declare` 문 외부 프로시저를 호출 하는 동안 문자열을 마샬링하기 위한 문자 집합 정보를 제공 합니다. 또한 Visual Basic에서 외부 프로시저 이름에 대 한 외부 파일을 검색 하는 방식을 영향을 줍니다. `Unicode` 한정자는 Visual Basic에서 모든 문자열을 유니코드 값으로 마샬링하고 검색 하는 동안 이름을 수정 하지 않고 프로시저를 조회 해야 하도록 지정 합니다.  
  
 문자 집합 자가 지정 된 경우 `Ansi` 가 기본값입니다.  
  
## <a name="remarks"></a>설명  
 `Unicode` 한정자는이 컨텍스트에서 사용할 수 있습니다.  
  
 [Declare 문](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
## <a name="smart-device-developer-notes"></a>스마트 장치 개발자 노트  
 이 키워드는 지원 되지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [ANSI](../../../visual-basic/language-reference/modifiers/ansi.md)
- [자동](../../../visual-basic/language-reference/modifiers/auto.md)
- [키워드](../../../visual-basic/language-reference/keywords/index.md)
