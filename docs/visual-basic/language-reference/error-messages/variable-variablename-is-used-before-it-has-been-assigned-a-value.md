---
title: 값이 할당되기 전에 '<variablename>' 변수를 사용했습니다.
ms.date: 07/20/2015
f1_keywords:
- vbc42104
- BC42104
helpviewer_keywords:
- BC42104
ms.assetid: 6909aa0b-b4a1-46f5-a18c-ba3e565c1dd8
ms.openlocfilehash: a2ba752b95933d146da090a58c416015db75e106
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662681"
---
# <a name="variable-variablename-is-used-before-it-has-been-assigned-a-value"></a>변수 '\<variablename >'에 값이 할당 되기 전에
변수 '\<variablename >'에 값이 할당 되기 전에 사용 됩니다. 런타임에 null 참조 예외가 발생할 수 있습니다.  
  
 응용 프로그램에 값이 할당 되기 전에 변수를 읽는 해당 코드를 통해 하나 이상의 경로가 있습니다.  
  
 변수에 값이 할당되지 않으면 해당 데이터 형식에 대한 기본값을 유지합니다. 참조 데이터 형식의 경우 해당 기본값은 [Nothing](../../../visual-basic/language-reference/nothing.md)입니다. 값이 `Nothing` 인 참조 변수를 읽으면 일부 환경에서 <xref:System.NullReferenceException> 이 발생할 수 있습니다.  
  
 이 메시지는 기본적으로 경고입니다. 경고를 숨기거나 오류로 처리하는 방법에 대한 자세한 내용은 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)을 참조하세요.  
  
 **오류 ID:** BC42104  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 제어 흐름 논리를 확인 하 고 변수를 읽는 모든 문으로 제어가 전달 하기 전에 유효한 값에 있는지 확인 합니다.  
  
- 변수의 유효한 값을 항상 포함 하는 데는 한 가지 방법은 해당 선언의 일부로 초기화 하는 것입니다. "초기화"를 참조 하세요 [Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md)
- [변수 선언](../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)
- [변수 문제 해결](../../../visual-basic/programming-guide/language-features/variables/troubleshooting-variables.md)
