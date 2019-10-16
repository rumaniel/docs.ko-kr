---
title: 암시적 숫자 변환 표 - C# 참조
ms.custom: seodec18
ms.date: 09/05/2018
helpviewer_keywords:
- conversions [C#], implicit numeric
- implicit numeric conversions [C#]
- numeric conversions [C#], implicit
- types [C#], implicit numeric conversions
ms.assetid: 72eb5a94-0491-48bf-8032-d7ebfdfeb8d8
ms.openlocfilehash: 516505ccacfd2a8a5c275b0de033e1316fa06d3a
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67661330"
---
# <a name="implicit-numeric-conversions-table-c-reference"></a>암시적 숫자 변환 표(C# 참조)

다음 표에서는 .NET 숫자 형식 간의 미리 정의된 암시적 숫자 변환을 보여 줍니다.
  
|시작|대상|  
|----------|--------|  
|[sbyte](../builtin-types/integral-numeric-types.md)|`short`, `int`, `long`, `float`, `double` 또는 `decimal`|  
|[byte](../builtin-types/integral-numeric-types.md)|`short`, `ushort`, `int`, `uint`, `long`, `ulong`, `float`, `double` 또는 `decimal`|  
|[char](char.md)|`ushort`, `int`, `uint`, `long`, `ulong`, `float`, `double` 또는 `decimal`|  
|[short](../builtin-types/integral-numeric-types.md)|`int`, `long`, `float`, `double` 또는 `decimal`|  
|[ushort](../builtin-types/integral-numeric-types.md)|`int`, `uint`, `long`, `ulong`, `float`, `double` 또는 `decimal`|  
|[int](../builtin-types/integral-numeric-types.md)|`long`, `float`, `double` 또는 `decimal`|  
|[uint](../builtin-types/integral-numeric-types.md)|`long`, `ulong`, `float`, `double` 또는 `decimal`|  
|[long](../builtin-types/integral-numeric-types.md)|`float`, `double`또는 `decimal`|  
|[ulong](../builtin-types/integral-numeric-types.md)|`float`, `double`또는 `decimal`|  
|[float](../builtin-types/floating-point-numeric-types.md)|`double`|  
  
## <a name="remarks"></a>설명  

- 모든 [정수 형식](../builtin-types/integral-numeric-types.md)은 암시적으로 모든 [부동 소수점 형식](../builtin-types/floating-point-numeric-types.md)으로 전환할 수 있습니다.

- `int`, `uint`, `long` 또는 `ulong`에서 `float`로 변환하고 `long` 또는 `ulong`에서 `double`로 변환하는 동안 전체 자릿수가 손실될 수도 있지만 크기는 손실되지 않습니다.  
  
- `char`, `byte` 및 `sbyte` 형식으로 암시적 변환은 없습니다.  

- `double` 및 `decimal` 형식에서 암시적 변환은 없습니다.
  
- `decimal` 형식과 `float` 또는 `double` 형식 간의 암시적 변환은 없습니다.  
  
- 형식 `int`의 상수 식 값(예: 정수 리터럴로 표시되는 값)은 대상 형식 범위 내에 있는 `sbyte`, `byte`, `short`, `ushort`, `uint` 또는 `ulong`으로 변환할 수 있습니다.

  ```csharp
  byte a = 13;    // Compiles
  byte b = 300;   // CS0031: Constant value '300' cannot be converted to a 'byte'
  ```

암시적 변환에 대한 자세한 내용은 [C# 언어 사양](../language-specification/index.md)의 [암시적 변환](~/_csharplang/spec/conversions.md#implicit-conversions) 섹션을 참조하세요.
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [정수 형식](../builtin-types/integral-numeric-types.md)
- [부동 소수점 형식 표](../builtin-types/floating-point-numeric-types.md)
- [기본 제공 형식 표](built-in-types-table.md)
- [명시적 숫자 변환 표](explicit-numeric-conversions-table.md)
- [캐스팅 및 형식 변환](../../programming-guide/types/casting-and-type-conversions.md)
