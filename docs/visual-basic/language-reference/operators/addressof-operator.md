---
title: AddressOf 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- AddressOf
- vb.AddressOf
helpviewer_keywords:
- AddressOf operator [Visual Basic]
- addresses, passing to API procedures
ms.assetid: 8105a59d-60d8-4ab5-b221-5899cdfacbf4
ms.openlocfilehash: 2ebadf5ded1a23fe46b8e16cf18ae265b5d3c255
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71591663"
---
# <a name="addressof-operator-visual-basic"></a>AddressOf 연산자(Visual Basic)
특정 프로시저를 참조 하는 대리자 인스턴스를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
AddressOf procedurename  
```  
  
## <a name="parts"></a>요소  
 `procedurename`  
 필수. 새로 만든 대리자가 참조 하는 프로시저를 지정 합니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 연산자는 `procedurename`로 지정 된 sub 또는 함수를 가리키는 대리자를 만듭니다. 지정 된 프로시저가 인스턴스 메서드인 경우 대리자는 인스턴스와 메서드를 모두 참조 합니다. 그런 다음 대리자가 호출 되 면 지정 된 인스턴스의 지정 된 메서드가 호출 됩니다.  
  
 @No__t-0 연산자는 대리자 생성자의 피연산자로 사용 하거나 컴파일러에서 대리자의 형식을 확인할 수 있는 컨텍스트에서 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 `AddressOf` 연산자를 사용 하 여 단추에 대 한 `Click` 이벤트를 처리할 대리자를 지정 합니다.  
  
 [!code-vb[VbVbalrDelegates#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#8)]  
  
## <a name="example"></a>예제  
 다음 예에서는 `AddressOf` 연산자를 사용 하 여 스레드에 대 한 시작 함수를 지정 합니다.  
  
 [!code-vb[VbVbalrDelegates#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#9)]  
  
## <a name="see-also"></a>참조

- [Declare 문](../../../visual-basic/language-reference/statements/declare-statement.md)
- [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)
- [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)
- [대리자](../../../visual-basic/programming-guide/language-features/delegates/index.md)
