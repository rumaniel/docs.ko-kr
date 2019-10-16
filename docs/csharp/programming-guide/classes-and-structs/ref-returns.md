---
title: 참조 반환 값 및 참조 로컬(C# 가이드)
description: 참조 반환 및 참조 로컬 값을 정의하고 사용하는 방법을 알아봅니다.
author: rpetrusha
ms.author: ronpet
ms.date: 04/04/2018
ms.openlocfilehash: e23007deffea0f542d623be918cd1c61496d1362
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353890"
---
# <a name="ref-returns-and-ref-locals"></a>참조 반환 및 참조 로컬

C# 7.0부터 C#에서 참조 반환 값(ref return)을 지원합니다. 참조 반환 값을 사용하면 메서드가 값이 아니라 변수 참조를 호출자에게 다시 반환할 수 있습니다. 그러면 호출자는 반환된 변수를 마치 값이나 참조로 반환된 것처럼 처리하도록 선택할 수 있습니다. 호출자는 참조 로컬이라고 하는, 반환된 값에 대한 참조 자체인 새 변수를 만들 수 있습니다.

## <a name="what-is-a-reference-return-value"></a>참조 반환 값이란?

대부분의 개발자는 호출된 메서드에 인수를 *참조로* 전달하는 데 익숙합니다. 호출된 메서드의 인수 목록에는 참조로 전달되는 변수가 포함됩니다. 호출자는 호출된 메서드에 의한 해당 값의 변경 내용을 관찰합니다. ‘참조 반환 값’은 메서드가 일부 변수에 대한 ‘참조’(또는 별칭)를 반환한다는 것을 의미합니다.   해당 변수의 범위는 메서드를 포함해야 합니다. 해당 변수의 수명은 메서드의 반환 이후로 연장되어야 합니다. 호출자가 메서드의 반환 값을 수정하면 메서드가 반환한 변수가 수정됩니다.

메서드가 ‘참조 반환 값’을 반환한다는 선언은 메서드가 변수에 별칭을 반환함을 나타냅니다.  설계 의도에 따라 호출 코드가 변수 수정을 비롯하여 별칭을 통해 해당 변수에 액세스할 수 있어야 합니다. 결과적으로 참조로 반환하는 메서드는 `void` 반환 형식을 사용할 수 없습니다.

메서드가 참조 반환 값으로 반환할 수 있는 식에는 몇 가지 제한 사항이 있습니다. 제한 사항은 다음과 같습니다.

- 반환 값의 수명은 메서드 실행 이후까지 연장되어야 합니다. 즉, 반환하는 메서드의 지역 변수일 수 없습니다. 클래스의 인스턴스 또는 정적 필드이거나 메서드에 전달된 인수일 수 있습니다. 지역 변수를 반환하려고 하면 컴파일러 오류 CS8168, “’obj’ 로컬은 참조 로컬이 아니므로 참조로 반환할 수 없습니다.”가 생성됩니다.

- 반환 값은 리터럴 `null`일 수 없습니다. `null`을 반환하면 컴파일러 오류 CS8156, “식이 참조로 반환될 수 없으므로 이 컨텍스트에서 해당 식을 사용할 수 없습니다.”가 생성됩니다.

   참조 반환이 있는 메서드는 값이 현재 null(인스턴스화되지 않음) 값이거나 값 형식이 [nullable 값 형식](../nullable-types/index.md)인 변수에 별칭을 반환할 수 있습니다.

- 반환 값은 상수, 열거형 멤버, 속성의 값 형식 반환 값 또는 `class`나 `struct`의 메서드일 수 없습니다. 이 규칙을 위반하면 컴파일러 오류 CS8156, “식이 참조로 반환될 수 없으므로 이 컨텍스트에서 해당 식을 사용할 수 없습니다.”가 생성됩니다.

또한 참조 반환 값은 비동기 메서드에서 허용되지 않습니다. 비동기 메서드는 실행을 마치기 전에 반환할 수 있지만 반환 값을 여전히 알 수 없습니다.

## <a name="defining-a-ref-return-value"></a>참조 반환 값 정의

*참조 반환 값*을 반환하는 메서드는 다음 2가지 조건을 충족해야 합니다.

- 메서드 시그니처에는 반환 형식 앞에 [ref](../../language-reference/keywords/ref.md) 키워드가 포함됩니다.
- 메서드 본문의 각 [return](../../language-reference/keywords/return.md) 문에는 반환된 인스턴스의 이름 앞에 [ref](../../language-reference/keywords/ref.md) 키워드가 포함됩니다.

다음 예제에서는 이러한 조건을 충족하면서 `p`라는 이름의 `Person` 개체에 대한 참조를 반환하는 메서드를 보여줍니다.

```csharp
public ref Person GetContactInformation(string fname, string lname)
{
    // ...method implementation...
    return ref p;
}
```

## <a name="consuming-a-ref-return-value"></a>참조 반환 값 사용

참조 반환 값은 호출된 메서드 범위 내 다른 변수에 대한 별칭입니다. 참조 반환의 사용은 다음과 같이 별칭이 있는 변수를 사용하는 것으로 해석할 수 있습니다.

- 해당 값을 할당할 경우 별칭이 있는 변수에 값을 할당하는 것입니다.
- 해당 값을 읽을 경우 별칭이 있는 변수의 값을 읽는 것입니다.
- ‘참조로’ 반환하는 경우 동일한 변수에 대한 별칭을 반환하는 것입니다. 
- 다른 메서드에 ‘참조로’ 전달하는 경우 별칭이 있는 변수에 대한 참조를 전달하는 것입니다. 
- [참조 로컬](#ref-locals) 별칭을 만들 경우 동일한 변수에 대한 새 별칭을 만드는 것입니다.

## <a name="ref-locals"></a>참조 로컬

`GetContactInformation` 메서드가 다음과 같이 참조 반환으로 선언된다고 가정합니다.

```csharp
public ref Person GetContactInformation(string fname, string lname)
```

값 형식 할당은 변수의 값을 읽고 다음과 같이 새 변수에 해당 값을 할당합니다.

```csharp
Person p = contacts.GetContactInformation("Brandie", "Best");
```

이전의 할당은 `p`를 지역 변수로 선언합니다. 초기 값은 `GetContactInformation`으로 반환된 값을 읽은 것에서 복사됩니다. 향후 `p`에 대한 할당이 `GetContactInformation`으로 반환된 변수의 값을 변경하지 않습니다. `p` 변수는 더 이상 반환된 변수에 대한 별칭이 아닙니다.

‘참조 로컬’ 변수를 선언하여 원래 값에 대한 별칭을 복사합니다.  다음 할당에서 `p`는 `GetContactInformation`에서 반환된 변수에 대한 별칭입니다.

```csharp
ref Person p = ref contacts.GetContactInformation("Brandie", "Best");
```

`p`가 해당 변수의 별칭이므로 이후 `p` 사용은 `GetContactInformation`에서 반환된 변수를 사용하는 것과 같습니다. 또한 `p`를 변경하면 `GetContactInformation`에서 반환된 변수도 변경됩니다.

`ref` 키워드는 지역 변수 선언 앞, ‘그리고’ 메서드 호출 앞에 사용됩니다.  

동일한 방법으로 참조로 값에 액세스할 수 있습니다. 경우에 따라 참조로 값에 액세스하면 비용이 많이 들 수 있는 복사 작업을 피함으로써 성능이 향상됩니다. 예를 들어, 다음 명령문은 값을 참조하는 데 사용되는 참조 로컬 값을 정의하는 방법을 보여줍니다.

```csharp
ref VeryLargeStruct reflocal = ref veryLargeStruct;
```

`ref` 키워드는 지역 변수 선언 앞 ‘그리고’ 두 번째 예의 값 앞에 사용됩니다.  두 예에서 변수 선언과 할당에 `ref` 키워드를 둘 다 포함하지 않으면 컴파일러 오류 CS8172, "값을 사용하여 참조 형식 변수를 초기화할 수 없습니다."가 생성됩니다. 

C# 7.3 이전에 참조 로컬 변수는 초기화되기 전에 다른 스토리지 공간을 참조하도록 다시 할당될 수 없었습니다. 해당 제한 사항이 제거되었습니다. 다음 예제에서는 재할당을 보여줍니다.

```csharp
ref VeryLargeStruct reflocal = ref veryLargeStruct; // initialization
refLocal = ref anotherVeryLargeStruct; // reassigned, refLocal refers to different storage.
```

 참조 로컬 변수는 선언될 때 초기화되어야 합니다.

## <a name="ref-returns-and-ref-locals-an-example"></a>참조 반환 및 참조 로컬: 예제

다음 예제에서는 정수 값의 배열을 저장하는 `NumberStore` 클래스를 정의합니다. `FindNumber` 메서드는 인수로 전달된 숫자보다 크거나 같은 첫 번째 숫자를 참조로 반환합니다. 인수보다 크거나 같은 숫자가 없으면 메서드는 인덱스 0의 숫자를 반환합니다. 

[!code-csharp[ref-returns](../../../../samples/snippets/csharp/programming-guide/ref-returns/NumberStore.cs#1)]

다음 예제에서는 `NumberStore.FindNumber` 메서드를 호출하여 16보다 크거나 같은 첫 번째 값을 검색합니다. 그런 다음 호출자가 메서드에서 반환된 값을 두 배로 만듭니다. 예제의 출력에서는 `NumberStore` 인스턴스의 배열 요소 값에 반영된 변경 내용을 보여줍니다.

[!code-csharp[ref-returns](../../../../samples/snippets/csharp/programming-guide/ref-returns/NumberStore.cs#2)]

참조 반환 값이 지원되지 않을 경우 이러한 작업은 해당 값과 함께 배열 요소의 인덱스를 반환하여 수행됩니다. 그런 다음 호출자는 이 인덱스를 사용하여 별도 메서드 호출에서 값을 수정할 수 있습니다. 그러나 호출자가 인덱스를 수정하여 다른 배열 값에 액세스하고 수정할 수도 있습니다.  

다음 예제에서는 C# 7.3 이후에 `FindNumber` 메서드를 다시 작성하여 참조 로컬 재할당을 사용하는 방법을 보여줍니다.

[!code-csharp[ref-returns](../../../../samples/snippets/csharp/programming-guide/ref-returns/NumberStoreUpdated.cs#1)]

이 두 번째 버전은 검색된 수가 배열의 끝에 더 가까운 시나리오에서 더 긴 시퀀스를 사용하여 더욱 효율적입니다.

## <a name="see-also"></a>참고 항목

- [ref 키워드](../../language-reference/keywords/ref.md)
- [안전하고 효율적인 코드 작성](../../write-safe-efficient-code.md)
