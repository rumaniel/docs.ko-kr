---
title: '#Region 지시문 (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.Region
- vb.#Region
helpviewer_keywords:
- Visual Basic compiler, compiler directives
- '#region directive'
- region directive (#region)
- '#Region keyword [Visual Basic]'
ms.assetid: 90a6a104-3cbf-47d0-bdc4-b585d0921b87
ms.openlocfilehash: eaaf0f8279ec905767be3f364a88357f0d393bba
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61812647"
---
# <a name="region-directive"></a>#Region 지시문
Visual Basic 파일에서 코드 섹션을 축소하고 숨깁니다.  
  
## <a name="syntax"></a>구문  

```vb
#Region "identifier_string"  
#End Region  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`identifier_string`|필수 요소. 축소된 경우 영역의 제목 역할을 하는 문자열입니다. 영역은 기본적으로 축소되어 있습니다.|  
|`#End Region`|`#Region` 블록을 종료합니다.|  
  
## <a name="remarks"></a>설명  
 `#Region` 지시문을 사용하면 Visual Studio 코드 편집기의 개요 기능을 사용할 때 확장하거나 축소할 코드 블록을 지정할 수 있습니다. 배치할 수 있습니다 또는 *중첩*, 비슷한 영역을 함께 그룹화 할 다른 지역 내의 영역입니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 `#Region` 지시문을 사용합니다.  
  
 [!code-vb[VbVbalrConditionalComp#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConditionalComp/VB/Class1.vb#4)]  
  
## <a name="see-also"></a>참고자료

- [#If...Then...#Else 지시문](../../../visual-basic/language-reference/directives/if-then-else-directives.md)
- [개요](/visualstudio/ide/outlining)
- [방법: 코드 섹션 축소 및 숨기기](../../../visual-basic/programming-guide/program-structure/how-to-collapse-and-hide-sections-of-code.md)
