---
title: 지시문(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- directives, Visual Basic compiler
- Visual Basic code, directives
- directives
ms.assetid: 20d5fe65-490a-4c23-88c2-ee4f490ed762
ms.openlocfilehash: 38d54feae5cf7bf41a825d1f6000811e2b56f319
ms.sourcegitcommit: 4c41ec195caf03d98b7900007c3c8e24eba20d34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67268198"
---
# <a name="directives-visual-basic"></a>지시문(Visual Basic)
이 섹션의 항목에서는 Visual Basic 소스 코드 컴파일러 지시문을 문서화합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [#Const 지시문](../../../visual-basic/language-reference/directives/const-directive.md) -컴파일러 상수를 정의 합니다.  
  
 [#ExternalSource 지시문](../../../visual-basic/language-reference/directives/externalsource-directive.md) -소스 줄과 소스 외부에 있는 텍스트 간의 매핑을 나타냅니다  
  
 [#If... ... #Else 지시문](../../../visual-basic/language-reference/directives/if-then-else-directives.md) -선택한 코드 블록을 컴파일  
  
 [#Region 지시문](../../../visual-basic/language-reference/directives/region-directive.md) -섹션 축소 및 숨기기 Visual Studio 편집기에서 코드  
  
 **#Disable, #Enable** -사용 하지 않도록 설정 하 고 코드 영역에 대 한 특정 경고를 사용 하도록 설정 합니다.  
  
```vb  
#Disable Warning BC42356 ' suppress warning about no awaits in this method  
    Async Function TestAsync() As Task  
        Console.WriteLine("testing")  
    End Function  
#Enable Warning BC42356  
```  
  
 쉼표로 구분된 경고 코드 목록도 사용하거나 사용하지 않도록 설정할 수 있습니다.  
  
## <a name="related-sections"></a>관련 단원  
 [Visual Basic 언어 참조](../../../visual-basic/language-reference/index.md)  
  
 [Visual Basic](../../../visual-basic/index.md)
