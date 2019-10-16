---
title: GetType 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.GetType
helpviewer_keywords:
- GetType operator [Visual Basic]
- GetType keyword [Visual Basic]
ms.assetid: 4f733297-2503-4607-850c-15eba65fff90
ms.openlocfilehash: 2e3e05973f2ef72fef5e429bc98cc58b4b21f2c2
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71592147"
---
# <a name="gettype-operator-visual-basic"></a>GetType 연산자(Visual Basic)
지정 된 형식에 대 한 <xref:System.Type> 개체를 반환 합니다. @No__t-0 개체는 속성, 메서드 및 이벤트와 같은 형식에 대 한 정보를 제공 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
GetType(typename)  
```  
  
## <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|---|---|  
|`typename`|정보를 원하는 형식의 이름입니다.|  
  
## <a name="remarks"></a>설명  
 @No__t-0 연산자는 지정 된 `typename`에 대 한 <xref:System.Type> 개체를 반환 합니다. @No__t-0에서 정의 된 형식의 이름을 전달할 수 있습니다. 여기에는 다음이 포함됩니다.  
  
- @No__t-0 또는 `Date`과 같은 Visual Basic 데이터 형식입니다.  
  
- @No__t-0 또는 <xref:System.Double?displayProperty=nameWithType>과 같은 .NET Framework 클래스, 구조체, 모듈 또는 인터페이스입니다.  
  
- 응용 프로그램에 정의 된 클래스, 구조체, 모듈 또는 인터페이스입니다.  
  
- 응용 프로그램에서 정의 하는 배열입니다.  
  
- 응용 프로그램에서 정의 하는 대리자입니다.  
  
- Visual Basic, .NET Framework 또는 응용 프로그램에 의해 정의 되는 열거형입니다.  
  
 개체 변수의 형식 개체를 가져오려는 경우 <xref:System.Type.GetType%2A?displayProperty=nameWithType> 메서드를 사용 합니다.  
  
 @No__t-0 연산자는 다음과 같은 경우에 유용할 수 있습니다.  
  
- 런타임에 형식에 대 한 메타 데이터에 액세스 해야 합니다. @No__t-0 개체는 형식 멤버 및 배포 정보와 같은 메타 데이터를 제공 합니다. 예를 들어, 어셈블리를 반영 하기 위해 필요 합니다. 자세한 내용은 <xref:System.Reflection?displayProperty=nameWithType>을 참조하세요.  
  
- 두 개체 참조를 비교 하 여 동일한 형식의 인스턴스를 참조 하는지 여부를 확인 하려고 합니다. 이 경우 `GetType`은 동일한 <xref:System.Type> 개체에 대 한 참조를 반환 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 `GetType` 연산자를 사용 하는 방법을 보여 줍니다.  
  
 [!code-vb[VbVbalrOperators#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#26)]  
  
## <a name="see-also"></a>참조

- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [연산자 및 식](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)
