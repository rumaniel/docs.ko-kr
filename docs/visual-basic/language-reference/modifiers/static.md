---
title: Static(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Static
helpviewer_keywords:
- static modifier
- Static keyword [Visual Basic]
ms.assetid: 19013910-4658-47b6-a22e-1744b527979e
ms.openlocfilehash: f1031fe005a2fc264b50116b8ea3311dc7065dbc
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64647636"
---
# <a name="static-visual-basic"></a>Static(Visual Basic)
계속 존재 하 고 선언 된 프로시저가 종료 된 후 최신 값을 보유 하는 하나 이상의 선언 된 지역 변수를 지정 합니다.  
  
## <a name="remarks"></a>설명  
 일반적으로 프로시저에서 지역 변수 소멸 프로시저를 중지 하는 즉시 합니다. 정적 변수는 계속 존재 하 고 최신 값을 유지 합니다. 프로시저를 호출 하는 코드 다음에 변수가 다시 초기화 되지 않습니다 및에 할당 되는 최신 값을 계속 유지 합니다. 정적 변수 계속에 정의 된 클래스 또는 모듈의 수명 동안 존재 합니다.  
  
## <a name="rules"></a>규칙  
  
- **선언 컨텍스트입니다.** 사용할 수 있습니다 `Static` 로컬 변수 에서만. 즉, 선언 컨텍스트는 `Static` 변수는 프로시저 또는 프로시저에서 블록 이어야 합니다 하 고 소스 파일, 네임 스페이스, 클래스, 구조체 또는 모듈 수 없습니다.  
  
     사용할 수 없습니다 `Static` 구조 프로시저 내에서.  
  
- 데이터 형식의 `Static` 로컬 변수를 유추할 수 없습니다. 자세한 내용은 [로컬 형식 유추](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)합니다.  
  
- **결합 된 한정자입니다.** 지정할 수 없습니다 `Static` 와 함께 `ReadOnly`를 `Shadows`, 또는 `Shared` 같은 선언에 있습니다.  
  
## <a name="behavior"></a>동작  
 정적 변수를 선언 하는 경우는 `Shared` 절차, 정적 변수 복사본 하나만 전체 응용 프로그램에서 사용할 수 있습니다. 호출을 `Shared` 클래스를 사용 하 여 프로시저 이름, 클래스의 인스턴스를 가리키는 변수 없습니다.  
  
 되지 않는 프로시저에서 정적 변수를 선언 하는 경우 `Shared`만 변수의 복사본 하나를 클래스의 각 인스턴스에 대해 사용할 수 있습니다. 클래스의 특정 인스턴스를 가리키는 변수를 사용 하는 비공유 프로시저를 호출 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 `Static`의 사용법을 보여줍니다.  
  
 [!code-vb[VbVbalrKeywords#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class1.vb#5)]  
  
 합니다 `Static` 변수 `totalSales` 한 번만 0으로 초기화 됩니다. 입력할 때마다 `updateSales`, `totalSales` 아직 최신 값에 대 한 계산입니다.  
  
 `Static` 한정자는이 컨텍스트에서 사용할 수 있습니다.  
  
 [Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
## <a name="see-also"></a>참고자료

- [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)
- [공유](../../../visual-basic/language-reference/modifiers/shared.md)
- [Visual Basic의 수명](../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)
- [변수 선언](../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)
- [구조체](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [지역 형식 유추](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [개체 및 클래스](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
