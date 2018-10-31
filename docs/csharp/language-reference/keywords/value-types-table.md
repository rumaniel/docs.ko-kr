---
title: 값 형식 표(C# 참조)
ms.date: 08/24/2018
helpviewer_keywords:
- value types [C#], table
- types [C#], value types
- types [C#], suffixes
ms.assetid: 67d8f631-b6e3-4d83-9910-5ec497f8c5f3
ms.openlocfilehash: aa37e2237ca0cffe7ff2e64aa53739b6ffafd24a
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50182752"
---
# <a name="value-types-table-c-reference"></a>값 형식 표(C# 참조)

다음 표에서는 C# 값 형식을 보여 줍니다.  
  
|값 형식|범주|형식 접미사|  
|----------------|--------------|-----------------|  
|[bool](bool.md)|부울||  
|[byte](byte.md)|부호 없음, 숫자, [정수](integral-types-table.md)||  
|[char](char.md)|부호 없음, 숫자, [정수](integral-types-table.md)||  
|[decimal](decimal.md)|숫자, [부동 소수점](floating-point-types-table.md)|M 또는 m|  
|[double](double.md)|숫자, [부동 소수점](floating-point-types-table.md)|D 또는 d|  
|[enum](enum.md)|열거형||  
|[float](float.md)|숫자, [부동 소수점](floating-point-types-table.md)|F 또는 f|  
|[int](int.md)|부호 있음, 숫자, [정수](integral-types-table.md)||  
|[long](long.md)|부호 있음, 숫자, [정수](integral-types-table.md)|L 또는 l|  
|[sbyte](sbyte.md)|부호 있음, 숫자, [정수](integral-types-table.md)||  
|[short](short.md)|부호 있음, 숫자, [정수](integral-types-table.md)||  
|[struct](struct.md)|사용자 정의 구조||  
|[uint](uint.md)|부호 없음, 숫자, [정수](integral-types-table.md)|U 또는 u|  
|[ulong](ulong.md)|부호 없음, 숫자, [정수](integral-types-table.md)|UL, Ul, uL, ul, LU, Lu, lU 또는 lu|  
|[ushort](ushort.md)|부호 없음, 숫자, [정수](integral-types-table.md)||  

## <a name="remarks"></a>설명

형식 접미사를 사용하여 숫자 리터럴의 형식을 지정합니다. 예:

```csharp
decimal a = 0.1M;
```

[정수 숫자 리터럴](~/_csharplang/spec/lexical-structure.md#integer-literals)에 접미사가 없는 경우 해당 값을 표시할 수 있는 `int`, `uint`, `long`, `ulong` 형식 중 첫 번째 형식입니다.

[실제 숫자 리터럴](~/_csharplang/spec/lexical-structure.md#real-literals)에 접미사가 없는 경우 `double` 형식입니다.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [형식 참조 테이블](reference-tables-for-types.md)
- [기본값 표](default-values-table.md)
- [값 형식](value-types.md)
- [숫자 결과 형식 지정 표](formatting-numeric-results-table.md)
