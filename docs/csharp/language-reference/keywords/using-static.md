---
title: using 정적 지시문 - C# 참조
ms.custom: seodec18
ms.date: 03/10/2017
helpviewer_keywords:
- using static directive [C#]
ms.assetid: 8b8f9e34-c75e-469b-ba85-6f2eb4090314
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4fa8dc3c043665ca2f56facf516cb03e5c6bb9d7
ms.sourcegitcommit: 10986410e59ff29f2ec55c6759bde3eb4d1a00cb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66421760"
---
# <a name="using-static-directive-c-reference"></a>using 정적 지시문(C# 참조)

`using static` 지시문은 형식 이름을 지정하지 않고 정적 멤버 및 중첩 형식에 액세스할 수 있는 형식을 지정합니다. 사용되는 구문은 다음과 같습니다.

```csharp
using static <fully-qualified-type-name>;
```

여기서 *fully-qualified-type-name*은 형식 이름을 지정하지 않고 정적 멤버 및 중첩 형식을 참조할 수 있는 형식의 이름입니다. 정규화된 형식 이름(전체 네임스페이스 및 형식 이름)을 제공하지 않으면 C#에 컴파일러 오류 [CS0246](../compiler-messages/cs0246.md): “‘type/namespace’ 형식 또는 네임스페이스 이름을 찾을 수 없습니다(사용 중인 지시문 또는 어셈블리 참조가 없습니까?).”가 발생합니다.

`using static` 지시문은 정적 멤버(또는 중첩 형식)가 있는 모든 형식에 적용됩니다(인스턴스 멤버가 있는 경우에도). 그러나 인스턴스 멤버는 형식 인스턴스를 통해서만 호출할 수 있습니다.

`using static` 지시문은 C# 6에서 도입되었습니다.

## <a name="remarks"></a>주의

일반적으로 정적 멤버를 호출할 때 멤버 이름과 함께 형식 이름을 제공합니다. 형식의 멤버를 호출하기 위해 동일한 형식 이름을 반복해서 입력하면 코드가 복잡하고 난해해질 수 있습니다. 예를 들어 `Circle` 클래스에 대한 다음 정의에서는 <xref:System.Math> 클래스의 많은 멤버를 참조합니다.

[!code-csharp[using-static#1](~/samples/snippets/csharp/language-reference/keywords/using/using-static1.cs#1)]

멤버를 참조할 때마다 <xref:System.Math> 클래스를 명시적으로 참조할 필요가 없으므로 `using static` 지시문은 훨씬 깔끔한 코드를 생성합니다.

[!code-csharp[using-static#2](~/samples/snippets/csharp/language-reference/keywords/using/using-static2.cs#1)]

`using static`은 액세스 가능한 정적 멤버와 지정된 형식에 선언된 중첩된 형식만 가져옵니다.  상속된 멤버는 가져오지 않습니다.  using static 지시문을 사용하여 Visual Basic 모듈을 포함한 모든 명명된 형식에서 가져올 수 있습니다.  F# 최상위 함수가 메타데이터에서 이름이 유효한 C# 식별자인 명명된 형식의 정적 멤버로 나타나면 F# 함수를 가져올 수 있습니다.

 `using static`을 사용하면 지정된 형식에 선언된 확장 메서드를 확장 메서드 조회에 사용할 수 있습니다.  그러나 확장명 메서드의 이름은 코드의 정규화되지 않은 참조에 대한 범위로 가져오지 않습니다.

 같은 컴파일 단위 또는 네임스페이스에서 여러 `using static` 지시문을 통해 다양한 형식에서 가져온 같은 이름을 사용하는 메서드는 메서드 그룹을 구성합니다.  이들 메서드 그룹 내에서 오버로드 확인은 일반 C# 규칙을 따릅니다.

## <a name="example"></a>예제

다음 예제에서는 형식 이름을 지정할 필요 없이 `using static` 지시문을 사용하여 <xref:System.Console>, <xref:System.Math> 및 <xref:System.String> 클래스의 정적 멤버를 사용 가능하게 합니다.

[!code-csharp[using-static#3](~/samples/snippets/csharp/language-reference/keywords/using/using-static3.cs)]

이 예제에서는 `using static` 지시문을 <xref:System.Double> 형식에 적용했을 수도 있습니다. 이 경우 형식 이름을 지정하지 않고도 <xref:System.Double.TryParse(System.String,System.Double@)> 메서드를 호출할 수 있습니다. 그러나 이렇게 하면 코드 가독성이 떨어집니다. 어떤 숫자 형식의 `TryParse` 메서드가 호출되었는지 알아보기 위해 `using static` 문을 확인해야 하기 때문입니다.

## <a name="see-also"></a>참고 항목

- [using 지시문](using-directive.md)
- [C# 참조](../index.md)
- [C# 키워드](index.md)
- [네임스페이스 사용](../../programming-guide/namespaces/using-namespaces.md)
- [네임스페이스](../../programming-guide/namespaces/index.md)
