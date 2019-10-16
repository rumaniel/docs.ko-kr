---
title: Value Types and Reference Types
ms.date: 07/20/2015
helpviewer_keywords:
- reference data types [Visual Basic]
- reference types [Visual Basic]
- value types [Visual Basic]
- value data types [Visual Basic]
- types [Visual Basic]
- data types [Visual Basic], value types
- data types [Visual Basic], reference types
ms.assetid: fc82ce15-5a40-4c5c-a1e1-a556830e7391
ms.openlocfilehash: f25caec43b7118b7b64db1b14516b0c5ea80f4f6
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67504885"
---
# <a name="value-types-and-reference-types"></a>Value Types and Reference Types
두 가지 종류의 Visual Basic의 형식: 형식 및 값 형식을 참조 합니다. 참조 형식의 변수에는 데이터(개체)에 대한 참조가 저장되며, 값 형식의 변수에는 해당 데이터가 직접 포함됩니다. 참조 형식에서는 두 가지 변수가 같은 개체를 참조할 수 있으므로 한 변수에 대한 작업이 다른 변수에서 참조하는 개체에 영향을 미칠 수 있습니다. 값 형식에서는 각 변수에 데이터의 자체 복사본 및 작업으로 다른 변수를 하나에 대 한 불가능 (의 경우를 제외 하 고는 [ByRef 매개 변수 한정자](../../../language-reference/modifiers/byref.md)).
  
## <a name="value-types"></a>값 형식  
 데이터 형식은 *값 형식* 자신의 메모리 할당 데이터 보유 하는 경우. 값 형식은 다음과 같습니다.  
  
- 모든 숫자 데이터 형식  
  
- `Boolean`, `Char`및 `Date`  
  
- 해당 멤버 참조 형식인 경우에 모든 구조  
  
- 해당 기본 형식이 항상 이므로 열거형 `SByte`, `Short`를 `Integer`, `Long`를 `Byte`를 `UShort`, `UInteger`, 또는 `ULong`  
  
 모든 구조체가 값 형식이 참조 형식 멤버를 포함 하는 경우에 합니다. 이 따라서가에 대 한 값과 같은 형식이 `Char` 고 `Integer` .net 구조체에서 구현 됩니다.  
  
 예를 들어, 예약 된 키워드를 사용 하 여 값 형식을 선언할 수 있습니다 `Decimal`합니다. 사용할 수도 있습니다는 `New` 값 형식을 초기화 하는 키워드입니다. 형식 매개 변수를 사용 하는 생성자가 하는 경우 특히 유용 합니다. 이 예로 <xref:System.Decimal.%23ctor%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%2CSystem.Byte%29> 새 빌드는 생성자 `Decimal` 에서 제공 된 값입니다.  
  
## <a name="reference-types"></a>참조 형식  
 A *유형을 참조* 해당 데이터에 대 한 참조를 저장 합니다. 참조 형식은 다음과 같습니다.  
  
- `String`  
  
- 모든 배열의 해당 요소 값 형식인 경우에  
  
- 클래스 형식 <xref:System.Windows.Forms.Form>  
  
- 대리자  
  
 클래스는 *유형을 참조*합니다. 모든 배열은 참조 형식 인지, 해당 멤버 값 형식인 경우에 참고 합니다.  
  
 모든 참조 형식을 나타내므로 기본.NET Framework 클래스를 사용 해야 합니다 [New 연산자](../../../../visual-basic/language-reference/operators/new-operator.md) 초기화할 때 키워드입니다. 다음 문은 배열을 초기화합니다.  
  
```  
Dim totals() As Single = New Single(8) {}  
```  
  
## <a name="elements-that-are-not-types"></a>형식 없는 요소  
 그 중 하나에서 선언 된 요소에 대 한 데이터 형식으로 지정할 수 없으므로 다음 프로그래밍 요소 형식으로 적합 하지 않습니다.  
  
- 네임스페이스  
  
- 모듈  
  
- 이벤트  
  
- 속성 및 절차  
  
- 변수, 상수 및 필드  
  
## <a name="working-with-the-object-data-type"></a>개체 데이터 형식 사용  
 참조 형식 또는 값 형식 변수에 할당할 수 있습니다는 `Object` 데이터 형식입니다. `Object` 변수 항상 데이터를 데이터 자체에 대 한 참조를 보유 합니다. 그러나 값 형식을 할당 하는 경우는 `Object` 변수인 것 처럼 동작 자체 데이터를 보유 합니다. 자세한 내용은 [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md)합니다.  
  
 여부를 확인할 수 있습니다는 `Object` 변수 역할을 하는 참조 형식 또는 값 형식을 전달 하 여는 <xref:Microsoft.VisualBasic.Information.IsReference%2A> 에서 메서드는 <xref:Microsoft.VisualBasic.Information> 의 클래스는 <xref:Microsoft.VisualBasic?displayProperty=nameWithType> 네임 스페이스입니다. <xref:Microsoft.VisualBasic.Information.IsReference%2A?displayProperty=nameWithType> 반환 `True` 경우의 콘텐츠는 `Object` 변수에 참조 형식을 나타냅니다.  
  
## <a name="see-also"></a>참고자료

- [Nullable 값 형식](../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)
- [Visual Basic의 형식 변환](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
- [Structure 문](../../../../visual-basic/language-reference/statements/structure-statement.md)
- [데이터 형식의 효율적 사용](../../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
- [Object 데이터 형식](../../../../visual-basic/language-reference/data-types/object-data-type.md)
- [데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
