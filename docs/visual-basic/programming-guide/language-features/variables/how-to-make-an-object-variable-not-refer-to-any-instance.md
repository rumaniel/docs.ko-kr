---
title: '방법: 개체 변수가 인스턴스를 참조 하지 않도록 설정 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- Nothing keyword [Visual Basic], variable assignment
- object variables [Visual Basic], null reference
ms.assetid: e6d30578-bdae-4142-a3ac-a10697bf696a
ms.openlocfilehash: e647f2f891b06aa1767faac49b01df98ea31ec1c
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004910"
---
# <a name="how-to-make-an-object-variable-not-refer-to-any-instance-visual-basic"></a>방법: 개체 변수가 인스턴스를 참조 하지 않도록 설정 (Visual Basic)
개체 변수를 [Nothing](../../../../visual-basic/language-reference/nothing.md)으로 설정 하 여 개체 인스턴스의 연관을 해제할 수 있습니다.  
  
### <a name="to-disassociate-an-object-variable-from-any-object-instance"></a>개체 인스턴스에서 개체 변수를 분리 하려면  
  
- 대입문에서 변수를 `Nothing`으로 설정 합니다.  
  
    ```vb  
    ' Assume account is a defined class  
    Dim currentAccount As account  
    currentAccount = Nothing  
    ```  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 코드에서 `Nothing`으로 설정 된 개체 변수의 멤버에 액세스 하려고 하면 <xref:System.NullReferenceException>이 발생 합니다. 개체 변수를 `Nothing`으로 자주 설정 하거나 변수가 초기화 되지 않은 경우 `Try...Catch...Finally` 블록에 멤버 액세스를 묶는 것이 좋습니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 기밀 데이터 나 중요 한 데이터가 포함 된 개체에 개체 변수를 사용 하는 경우 해당 개체 중 하나를 적극적으로 처리 하지 않을 때 변수를 `Nothing`으로 설정할 수 있습니다. 이렇게 하면 악의적인 코드가 데이터에 액세스 하는 가능성을 줄일 수 있습니다.  
  
## <a name="see-also"></a>참조

- <xref:System.NullReferenceException>
- [개체 변수](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)
- [개체 변수 할당](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)
- [Nothing](../../../../visual-basic/language-reference/nothing.md)
- [Try...Catch...Finally 문](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)
