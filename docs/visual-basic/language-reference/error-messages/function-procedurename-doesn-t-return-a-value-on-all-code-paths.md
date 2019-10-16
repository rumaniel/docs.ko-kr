---
title: "'<procedurename>' 함수가 일부 코드 경로에 대해서만 값을 반환합니다."
ms.date: 07/20/2015
f1_keywords:
- bc42105
- vbc42105
helpviewer_keywords:
- BC42105
ms.assetid: b6929bf4-a365-4a70-8dc9-6b0fc09e1468
ms.openlocfilehash: 5564f95048f6b44a48229c7e5be9331839803439
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662099"
---
# <a name="function-procedurename-doesnt-return-a-value-on-all-code-paths"></a>함수 '\<procedurename >' 일부 코드 경로의 값을 반환 하지 않습니다
함수 '\<procedurename >' 일부 코드 경로의 값을 반환 하지 않습니다. 'Return' 문이 누락 되었습니까?  
  
 `Function` 프로시저 값을 반환 하지 않는 해당 코드를 통해 하나 이상의 경로가 있습니다.  
  
 값을 반환할 수는 `Function` 다음 방법 중 하나에서 프로시저:  
  
- 값을 포함 한 [Return 문이](../../../visual-basic/language-reference/statements/return-statement.md)합니다.  
  
- 에 값을 할당 합니다 `Function` 프로시저 이름을 지정 하 고 다음을 수행할는 `Exit Function` 문.  
  
- 에 값을 할당 합니다 `Function` 프로시저 이름을 지정 하 고 다음을 수행 합니다 `End Function` 문.  
  
 컨트롤을 전달 하는 경우 `Exit Function` 또는 `End Function` 프로시저 이름에 값을 할당 하지 않은, 프로시저 반환 데이터 형식의 기본값을 반환 합니다. 자세한 내용은 "동작"를 참조 하세요 [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)합니다.  
  
 이 메시지는 기본적으로 경고입니다. 경고를 숨기거나 오류로 처리하는 방법에 대한 자세한 내용은 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)을 참조하세요.  
  
 **오류 ID:** BC42105  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 제어 흐름 논리를 확인 하 고 반환 하는 모든 문 앞에 값을 할당 해야 합니다.  
  
     항상 사용 하는 경우 프로시저에서 모든 반환 값을 반환 하는 데 쉽습니다는 `Return` 문입니다. 이렇게 하면, 앞의 마지막 문이 `End Function` 이어야 합니다는 `Return` 문입니다.  
  
## <a name="see-also"></a>참고자료

- [Function 프로시저](../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)
- [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)
- [프로젝트 디자이너, 컴파일 페이지(Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)
