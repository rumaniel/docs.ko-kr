---
title: 기본값 표 - C# 참조
ms.custom: seodec18
description: C# 형식의 기본값을 알아봅니다.
ms.date: 07/29/2019
helpviewer_keywords:
- default [C#]
- parameterless constructor [C#]
ms.openlocfilehash: d9889ce389eed73a9af0a3f72dcca6ec476cae15
ms.sourcegitcommit: bbfcc913c275885381820be28f61efcf8e83eecc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68796512"
---
# <a name="default-values-table-c-reference"></a>기본값 표(C# 참조)

다음 표는 C# 형식의 기본값을 보여줍니다.

|형식|기본값|
|---------|------------------|
|임의 참조 형식|`null`|
|임의 [기본 제공 정수 숫자 유형](../builtin-types/integral-numeric-types.md)|0(영)|
|임의 [기본 제공 부동 소수점 숫자 유형](../builtin-types/floating-point-numeric-types.md)|0(영)|
|[bool](bool.md)|`false`|
|[char](char.md)|`'\0'`(U+0000)|
|[enum](enum.md)|식 `(E)0`로 생성한 값이며 여기서 `E`는 열거형 식별자입니다.|
|[struct](struct.md)|모든 값 형식 필드를 기본값으로 설정하고 모든 참조 형식 필드를 `null`로 설정하여 생성한 값입니다.|
|Any [Null 허용 값 형식](../../programming-guide/nullable-types/index.md)|<xref:System.Nullable%601.HasValue%2A> 속성은 `false`이고 <xref:System.Nullable%601.Value%2A> 속성은 정의되지 않은 인스턴스입니다. 이 기본값은 null 허용 값 형식의 *null* 값으로도 알려져 있습니다.|

[기본 연산자](../operators/default.md)를 사용하여 다음 예제와 같이 형식의 기본값을 생성합니다.

```csharp
int a = default(int);
```

C# 7.1부터 [`default` 리터럴](../operators/default.md#default-literal)을 사용하여 해당 형식의 기본값으로 변수를 초기화할 수 있습니다.

```csharp
int a = default;
```

값 형식의 경우 암시적 매개 변수 없는 생성자를 사용하여 다음 예제와 같은 형식의 기본값도 생성할 수 있습니다.

```csharp-interactive
var n = new System.Numerics.Complex();
Console.WriteLine(n);  // output: (0, 0)
```

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 다음 섹션을 참조하세요.

- [기본값](~/_csharplang/spec/variables.md#default-values)
- [기본 생성자](~/_csharplang/spec/types.md#default-constructors)

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 키워드](index.md)
- [기본 제공 형식 표](built-in-types-table.md)
- [생성자](../../programming-guide/classes-and-structs/constructors.md)
