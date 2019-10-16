---
title: 특성 목록(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- attribute list
- attributes [Visual Basic], applying
ms.assetid: 5880073a-68a4-4b6b-8a07-ace32959a4e2
ms.openlocfilehash: 771757afe214919649e13fda3990e1154be8e1e1
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004531"
---
# <a name="attribute-list-visual-basic"></a>특성 목록(Visual Basic)
선언 된 프로그래밍 요소에 적용할 특성을 지정 합니다. 여러 특성은 쉼표로 구분합니다. 다음은 한 특성에 대 한 구문입니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
[ attributemodifier ] attributename [ ( attributearguments | attributeinitializer ) ]  
```  
  
## <a name="parts"></a>요소  
|||
|---|---|
|`attributemodifier`|소스 파일의 시작 부분에 적용 되는 특성에 필요 합니다. [어셈블리](../../../visual-basic/language-reference/modifiers/assembly.md) 또는 [모듈인](../../../visual-basic/language-reference/modifiers/module-keyword.md)수 있습니다.|
|`attributename`| 필수. 특성의 이름입니다.|
|`attributearguments`|(선택 사항) 이 특성의 위치 인수 목록입니다. 여러 인수를 쉼표로 구분 합니다.|
|`attributeinitializer`|(선택 사항) 이 특성에 대 한 변수 또는 속성 이니셜라이저의 목록입니다. 여러 이니셜라이저는 쉼표로 구분 됩니다.|
  
## <a name="remarks"></a>설명  
 거의 모든 프로그래밍 요소 (형식, 프로시저, 속성 등)에 하나 이상의 특성을 적용할 수 있습니다. 특성은 어셈블리의 메타 데이터에 표시 되며, 코드에 주석을 달고 특정 프로그래밍 요소를 사용 하는 방법을 지정 하는 데 도움이 될 수 있습니다. Visual Basic 및 .NET Framework에 의해 정의 된 특성을 적용 하 고 사용자 고유의 특성을 정의할 수 있습니다.  

 특성을 사용 하는 경우에 대 한 자세한 내용은 [특성 개요](../../../visual-basic/programming-guide/concepts/attributes/index.md)를 참조 하세요. 특성 이름에 대 한 자세한 내용은 [선언 된 요소 이름](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)을 참조 하세요.  
  
## <a name="rules"></a>규칙  
  
- **배치가.** 대부분의 선언 된 프로그래밍 요소에 특성을 적용할 수 있습니다. 하나 이상의 특성을 적용 하려면 요소 선언의 시작 부분에 *특성 블록* 을 추가 합니다. 특성 목록의 각 항목은 적용 하려는 특성을 지정 하 고이 특성 호출에 사용 하는 한정자 및 인수를 지정 합니다.  
  
- **꺾쇠 괄호입니다.** 특성 목록을 제공 하는 경우 꺾쇠 괄호 ("`<`" 및 "`>`")로 묶어야 합니다.  
  
- **선언의 일부입니다.** 특성은 별도의 문이 아니라 요소 선언의 일부 여야 합니다. 줄 연속 시퀀스 ("`_`")를 사용 하 여 선언문을 여러 소스 코드 줄로 확장할 수 있습니다.  
  
- **수정자.** 소스 파일의 시작 부분에 있는 프로그래밍 요소에 적용 되는 모든 특성에는 특성 한정자 (`Assembly` 또는 `Module`)가 필요 합니다. 소스 파일의 시작 부분이 아닌 요소에 적용 된 특성에는 특성 한정자를 사용할 수 없습니다.  
  
- **인수의.** 특성의 모든 위치 인수는 모든 변수 또는 속성 이니셜라이저 앞에와 야 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 <xref:System.Runtime.InteropServices.DllImportAttribute> 특성을 `Function` 프로시저의 기본 정의에 적용 합니다.  
  
 [!code-vb[VbVbalrStatements#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#1)]  
  
 <xref:System.Runtime.InteropServices.DllImportAttribute>은 특성 사용 프로시저가 관리 되지 않는 DLL (동적 연결 라이브러리)의 진입점을 나타내는지 여부를 나타냅니다. 특성은 DLL 이름을 위치 인수로 제공 하 고 다른 정보를 변수 이니셜라이저로 제공 합니다.  
  
## <a name="see-also"></a>참조

- [어셈블리](../../../visual-basic/language-reference/modifiers/assembly.md)
- [모듈 \<키워드>](../../../visual-basic/language-reference/modifiers/module-keyword.md)
- [특성 개요](../../../visual-basic/programming-guide/concepts/attributes/index.md)
- [방법: 코드에서 문 분리 및 결합](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
