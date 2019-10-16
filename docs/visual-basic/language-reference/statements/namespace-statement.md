---
title: Namespace 문 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Namespace
helpviewer_keywords:
- namespaces [Visual Basic], root
- Namespace statement [Visual Basic]
- namespaces [Visual Basic], nested
- declaring namespaces [Visual Basic], syntax
- namespaces [Visual Basic], declaring
- root namespaces
- declarations [Visual Basic], namespaces
ms.assetid: a31fbd95-9ace-4c3d-bbb1-51222a2272b2
ms.openlocfilehash: 7f6b976af7933b3895f6992488d2d1532a8fc2f7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61784139"
---
# <a name="namespace-statement"></a>Namespace 문
네임 스페이스의 이름을 선언 하 고 해당 네임 스페이스에서 컴파일되도록 선언 뒤에 오는 소스 코드가 있습니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Namespace [Global.] { name | name.name }  
    [ componenttypes ]  
End Namespace  
```  
  
## <a name="parts"></a>요소  
 Global  
 선택 사항입니다. 프로젝트의 루트 네임 스페이스에서 네임 스페이스를 정의할 수 있습니다. 참조 [Visual Basic의 네임 스페이스](../../../visual-basic/programming-guide/program-structure/namespaces.md)합니다.  
  
 `name`  
 필수 요소. 네임 스페이스를 식별 하는 고유 이름입니다. 올바른 Visual Basic 식별자 여야 합니다. 자세한 내용은 [선언 요소 이름](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)합니다.  
  
 `componenttypes`  
 선택 사항입니다. 네임 스페이스를 구성 하는 요소입니다. 이러한 포함 되지만 열거형, 구조체, 인터페이스, 클래스, 모듈, 대리자 및 다른 네임 스페이스에 제한 되지 않습니다.  
  
 `End Namespace`  
 종료는 `Namespace` 블록입니다.  
  
## <a name="remarks"></a>설명  
 네임 스페이스는 조직 시스템으로 사용 됩니다. 분류 및 다른 프로그램 및 응용 프로그램에 노출 되는 프로그래밍 요소를 표시 하는 방법을 제공 합니다. 네임 스페이스 되어 있지는 *형식* 클래스 또는 구조체는 점에서-네임 스페이스의 데이터 형식이 프로그래밍 요소를 선언할 수 없습니다.  
  
 이후 선언 된 모든 프로그래밍 요소는 `Namespace` 문을 해당 네임 스페이스에 속합니다. Visual Basic 계속 중 하나를 발견할 때까지 마지막으로 선언 된 네임 스페이스에 요소를 컴파일하는 데는 `End Namespace` 문 또는 다른 `Namespace` 문입니다.  
  
 네임 스페이스를 이미 정의 되어 있으면, 프로젝트, 외부 에서도 프로그래밍 요소를 추가할 수 있습니다. 이 작업을 수행 하려면 사용을 `Namespace` Visual basic 네임 스페이스에 요소를 컴파일할 문입니다.  
  
 사용할 수는 `Namespace` 파일이 나 네임 스페이스 수준 에서만 문입니다. 즉, 합니다 *선언 컨텍스트* 네임 스페이스는 소스 파일 또는 다른 네임 스페이스 이어야 하며 클래스, 구조체, 모듈, 인터페이스 또는 프로시저 일 수 없습니다. 자세한 내용은 [선언 컨텍스트 및 기본 액세스 수준](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)을 참조하세요.  
  
 다른 내에서 하나의 네임 스페이스를 선언할 수 있습니다. 를 선언할 수 있지만 다른 코드에서 가장 안쪽의 네임 스페이스에 선언 된 요소에 액세스 하는 경우 중첩 된 계층의 모든 네임 스페이스 이름을 포함 하는 한정 문자열을 사용 해야 하는 중첩 수준의 엄격한 제한은 없습니다.  
  
## <a name="access-level"></a>액세스 수준  
 네임 스페이스는 있는 것 처럼 처리 됩니다는 `Public` 액세스 수준입니다. 네임 스페이스는 같은 프로젝트의 코드에서 해당 프로젝트를 참조 하는 다른 프로젝트 및 프로젝트에서 빌드된 어셈블리에서 액세스할 수 있습니다.  
  
 즉 네임 스페이스에 있지만 다른 요소에 포함 되지 않은 네임 스페이스 수준에서 선언 된 프로그래밍 요소를 가질 수 있습니다 `Public` 또는 `Friend` 액세스 합니다. 지정 하지 않으면 액세스 수준 등의 요소 사용 `Friend` 기본적으로 합니다. 클래스, 구조체, 모듈, 인터페이스, 열거형 및 대리자를 포함 하는 요소 네임 스페이스 수준에서 선언할 수 있습니다. 자세한 내용은 [선언 컨텍스트 및 기본 액세스 수준](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)을 참조하세요.  
  
## <a name="root-namespace"></a>루트 Namespace  
 프로젝트에서 모든 네임 스페이스 이름을 기반으로 한 *루트 네임 스페이스*합니다. Visual Studio는 프로젝트 이름을 프로젝트의 모든 코드에 대한 기본 루트 네임스페이스로 할당합니다. 예를 들어 프로젝트 이름이 `Payroll`이면 해당 프로그래밍 요소는 해당 네임스페이스 `Payroll`에 속합니다. 선언 하는 경우 `Namespace funding`, 해당 네임 스페이스의 전체 이름은 `Payroll.funding`합니다.  
  
 기존 네임 스페이스를 지정 하려는 경우는 `Namespace` 문을 제네릭 목록 클래스 예제에서는 null 값으로 루트 네임 스페이스를 설정할 수와 같은 합니다. 이 작업을 수행 하려면 **프로젝트 속성** 에서 합니다 **프로젝트** 메뉴와의 선택을 취소 합니다 **루트 네임 스페이스** 항목 입력란이 비어 있도록 합니다. 이 제네릭 목록 클래스 예제에서 수행 하지 않은 경우 Visual Basic 컴파일러 걸리는 `System.Collections.Generic` 프로젝트 내에서 새 네임 스페이스로 `Payroll`를의 전체 이름을 사용 하 여 `Payroll.System.Collections.Generic`합니다.  
  
 사용할 수 있습니다는 `Global` 프로젝트 외부에서 정의 된 네임 스페이스의 요소를 참조 하는 키워드입니다. 이렇게 하면 루트 네임 스페이스에 프로젝트 이름을 유지 합니다. 이렇게 하면 본의 아니게 기존 네임 스페이스와 함께 프로그래밍 요소를 병합할 가능성이 줄어듭니다. 자세한 내용은에서 "전역 키워드의 정규화 된 이름" 섹션을 참조 하세요 [Visual Basic의 네임 스페이스](../../../visual-basic/programming-guide/program-structure/namespaces.md)합니다.  
  
 `Global` 키워드 Namespace 문에서 사용할 수 있습니다. 이렇게 하면 프로젝트의 루트 네임스페이스에서 네임스페이스를 정의할 수 있습니다. 자세한 내용은 "Namespace 문을에서 전역 키워드" 섹션을 참조 하세요. [Visual Basic의 네임 스페이스](../../../visual-basic/programming-guide/program-structure/namespaces.md)합니다.  
  
 **문제를 해결 합니다.** 루트 네임 스페이스는 네임 스페이스 이름의 예기치 않은 연결 시킬 수 있습니다. 프로젝트 외부에서 정의 된 네임 스페이스에 대 한 참조를 만들면 Visual Basic 컴파일러는 해당 루트 네임 스페이스에서 중첩 된 네임 스페이스로 해석할 수 있습니다. 이러한 경우 컴파일러는 외부 네임 스페이스에 이미 정의 된 모든 형식을 인식 하지 못합니다. 이 방지 하려면 루트 네임 스페이스 "루트 Namespace,"에 설명 된 대로 null 값으로 설정 하거나 사용을 `Global` 요소 외부 네임 스페이스에 액세스 하는 키워드입니다.  
  
## <a name="attributes-and-modifiers"></a>특성 및 한정자  
 네임 스페이스에 특성을 적용할 수 없습니다. 특성 네임 스페이스와 같은 원본 분류자에 의미가 없는 어셈블리의 메타 데이터에 대 한 정보를 제공 합니다.  
  
 네임 스페이스에 대 한 액세스 또는 프로시저 한정자 또는 다른 한정자를 적용할 수 없습니다. 형식이 아니기 때문에 이러한 한정자는 의미가 없습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 다른 중첩 된 두 개의 네임 스페이스를 선언 합니다.  
  
 [!code-vb[VbVbalrStatements#43](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#43)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 단일 줄에 여러 개의 중첩 된 네임 스페이스를 선언 하 고 앞의 예와 동일 합니다.  
  
 [!code-vb[VbVbalrStatements#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#41)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 이전 예제에서 정의 된 클래스에 액세스 합니다.  
  
 [!code-vb[VbVbalrStatements#42](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#42)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 새 제네릭 목록 클래스의 기본 구조를 정의 하 고 추가 <xref:System.Collections.Generic?displayProperty=nameWithType> 네임 스페이스입니다.  
  
```vb  
Namespace System.Collections.Generic  
    Class specialSortedList(Of T)  
        Inherits List(Of T)  
        ' Insert code to define the special generic list class.  
    End Class  
End Namespace  
```  
  
## <a name="see-also"></a>참고자료

- [Imports 문(.NET 네임스페이스 및 형식)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
- [선언 요소 이름](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
- [Visual Basic의 네임 스페이스](../../../visual-basic/programming-guide/program-structure/namespaces.md)
