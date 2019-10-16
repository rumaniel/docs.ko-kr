---
title: Object 데이터 형식 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Object
- vb.Variant
helpviewer_keywords:
- object variables [Visual Basic], Object type
- data types [Visual Basic], assigning
- Object data type
- Object data type [Visual Basic], reference
ms.assetid: 61ea4a7c-3b3d-48d4-adc4-eacfa91779b2
ms.openlocfilehash: 1ac906494c49810e3d389591b1044f412e7320bc
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68513043"
---
# <a name="object-data-type"></a>Object Data Type

개체를 참조 하는 주소를 포함 합니다. `Object` 변수에 모든 참조 형식 (문자열, 배열, 클래스 또는 인터페이스)을 할당할 수 있습니다. 변수 `Object` 는 모든 값 형식 ( `Char`숫자, `Boolean` `Date`,,, 구조체 또는 열거형)의 데이터를 참조할 수도 있습니다.

## <a name="remarks"></a>설명

데이터 `Object` 형식은 응용 프로그램에서 인식 하는 모든 개체 인스턴스를 포함 하 여 모든 데이터 형식의 데이터를 가리킬 수 있습니다. 컴파일 `Object` 시간에 변수가 가리키는 데이터 형식을 알 수 없는 경우에 사용 합니다.

`Object` 의`Nothing` 기본값은 (null 참조)입니다.

## <a name="data-types"></a>데이터 형식

모든 데이터 형식의 `Object` 변수, 상수 또는 식을 변수에 할당할 수 있습니다. `Object` 변수가 현재 참조 하는 데이터 형식을 확인 하려면 <xref:System.Type?displayProperty=nameWithType> 클래스의 메서드를 <xref:System.Type.GetTypeCode%2A> 사용할 수 있습니다. 다음은 이에 대한 예입니다.

```vb
Dim myObject As Object
' Suppose myObject has now had something assigned to it.
Dim datTyp As Integer
datTyp = Type.GetTypeCode(myObject.GetType())
```

`Object` 데이터 형식이 참조 형식입니다. 그러나 Visual Basic는 값 형식의 `Object` 데이터를 참조할 때 변수를 값 형식으로 처리 합니다.

## <a name="storage"></a>스토리지

참조 하는 데이터 형식에 관계 없이 `Object` 변수는 데이터 값 자체를 포함 하지 않고 값에 대 한 포인터를 포함 합니다. 컴퓨터 메모리에서 항상 4 바이트를 사용 하지만 변수의 값을 나타내는 데이터의 저장소는 포함 하지 않습니다. 포인터를 사용 하 여 데이터 `Object` 를 찾는 코드로 인해 값 형식을 포함 하는 변수는 명시적으로 형식화 된 변수에 액세스 하는 속도가 약간 느립니다.

## <a name="programming-tips"></a>프로그래밍 팁

- **Interop 고려 사항** .NET Framework 용으로 작성 되지 않은 구성 요소 (예: Automation 또는 COM 개체)와 상호 작용 하는 경우 다른 환경의 포인터 형식은 Visual Basic `Object` 형식과 호환 되지 않는다는 점에 유의 하세요.

- **성능.** `Object` 형식을 사용 하 여 선언 하는 변수는 개체에 대 한 참조를 포함할 수 있을 만큼 유연 합니다. 그러나 이러한 변수에 대 한 메서드나 속성을 호출 하면 런타임에 *바인딩이* 항상 발생 합니다. 컴파일 시간에 *초기 바인딩을* 적용 하 고 성능을 향상 시키려면 특정 클래스 이름을 사용 하 여 변수를 선언 하거나 특정 데이터 형식으로 캐스팅 합니다.

  개체 변수를 선언 하는 경우 일반화 <xref:System.OperatingSystem> `Object` 된 형식 대신 특정 클래스 형식 (예:)을 사용 하십시오. 또한 속성 및 메서드에 액세스할 수 있도록 <xref:System.Windows.Forms.TextBox> <xref:System.Windows.Forms.Control>대신 사용 가능한 가장 구체적인 클래스 (예:)를 사용 해야 합니다. 일반적으로 **개체 브라우저** 의 **클래스** 목록을 사용 하 여 사용 가능한 클래스 이름을 찾을 수 있습니다.

- **넓혀.** 모든 데이터 형식과 모든 참조 형식은 `Object` 데이터 형식으로 확장 됩니다. 즉, <xref:System.OverflowException?displayProperty=nameWithType> 오류가 발생 하지 않고 모든 형식을 `Object` 로 변환할 수 있습니다.

  그러나 값 형식과 `Object`Visual Basic 사이를 변환 하는 경우 실행 속도가 느려질 수 있도록 *boxing* 및 *unboxing*이라는 작업을 수행 합니다.

- **문자를 입력 합니다.** `Object`에는 리터럴 형식 문자 또는 식별자 형식 문자가 없습니다.

- **프레임 워크 형식입니다.** .NET Framework에서 해당 하는 형식은 <xref:System.Object?displayProperty=nameWithType> 클래스입니다.

## <a name="example"></a>예제

다음 예제에서는 개체 인스턴스 `Object` 를 가리키는 변수를 보여 줍니다.

```vb
Dim objDb As Object
Dim myCollection As New Collection()
' Suppose myCollection has now been populated.
objDb = myCollection.Item(1)
```

## <a name="see-also"></a>참고자료

- <xref:System.Object>
- [데이터 형식](../../../visual-basic/language-reference/data-types/index.md)
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [변환 요약](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [데이터 형식의 효율적 사용](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
- [방법: 두 개체가 관련 되어 있는지 확인](../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-related.md)
- [방법: 두 개체가 동일한 지 확인](../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-identical.md)
