---
title: "'<propertyname>' 속성이 일부 코드 경로에 대해서만 값을 반환합니다."
ms.date: 07/20/2015
f1_keywords:
- bc42107
- vbc42107
helpviewer_keywords:
- BC42107
ms.assetid: 06800966-9c3b-4844-9f13-83ac95607d32
ms.openlocfilehash: a5cb28a024274e58da1755b437d6ba4ca6712610
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64661708"
---
# <a name="property-propertyname-doesnt-return-a-value-on-all-code-paths"></a>속성 '\<propertyname >' 일부 코드 경로의 값을 반환 하지 않습니다
속성 '\<propertyname >' 일부 코드 경로의 값을 반환 하지 않습니다. 이 결과를 사용하면 런타임에 null 참조 예외가 발생할 수 있습니다.  
  
 속성 `Get` 프로시저 값을 반환 하지 않는 해당 코드를 통해 하나 이상의 경로가 있습니다.  
  
 속성에서 값을 반환할 수 있습니다 `Get` 다음 방법 중 하나에서 프로시저:  
  
- 속성 이름에 값을 할당 하 고 다음을 수행할는 `Exit Property` 문입니다.  
  
- 속성 이름에 값을 할당 하 고 다음을 수행 합니다 `End Get` 문입니다.  
  
- 값을 포함 한 [Return 문이](../../../visual-basic/language-reference/statements/return-statement.md)합니다.  
  
 컨트롤을 전달 하는 경우 `Exit Property` 또는 `End Get` 속성 이름에 값을 할당 하지 않은 하 고는 `Get` 프로시저 속성의 데이터 형식의 기본 값을 반환 합니다. 자세한 내용은 "동작"를 참조 하세요 [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)합니다.  
  
 이 메시지는 기본적으로 경고입니다. 경고를 숨기거나 오류로 처리하는 방법에 대한 자세한 내용은 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)을 참조하세요.  
  
 **오류 ID:** BC42107  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 제어 흐름 논리를 확인 하 고 반환 하는 모든 문 앞에 값을 할당 해야 합니다.  
  
     항상 사용 하는 경우 프로시저에서 모든 반환 값을 반환 하는 데 쉽습니다는 `Return` 문입니다. 이렇게 하면, 앞의 마지막 문이 `End Get` 이어야 합니다는 `Return` 문입니다.  
  
## <a name="see-also"></a>참고자료

- [속성 프로시저](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)
- [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)
- [Get 문](../../../visual-basic/language-reference/statements/get-statement.md)
