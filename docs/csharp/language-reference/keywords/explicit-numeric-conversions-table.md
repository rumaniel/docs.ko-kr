---
title: 명시적 숫자 변환 표(C# 참조)
ms.date: 09/06/2018
helpviewer_keywords:
- conversions [C#], explicit numeric
- numeric conversions [C#], explicit
- explicit numeric conversion [C#]
- numeric data types [C#]
- types [C#], explicit numeric conversions
- type conversion [C#], explicit numeric
ms.assetid: f3bb9e76-6b92-4df7-bc36-f866c24e1dfd
ms.openlocfilehash: 948961d19518343c1f8ee14cd48dc33ec72cf23d
ms.sourcegitcommit: b22705f1540b237c566721018f974822d5cd8758
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2018
ms.locfileid: "49478928"
---
# <a name="explicit-numeric-conversions-table-c-reference"></a>명시적 숫자 변환 표(C# 참조)

다음 표에서는 [암시적 변환](implicit-numeric-conversions-table.md)이 없는 .NET 숫자 형식 간의 미리 정의된 명시적 변환을 보여 줍니다.

|시작|대상|  
|----------|--------|  
|[sbyte](sbyte.md)|`byte`, `ushort`, `uint`, `ulong` 또는 `char`|  
|[byte](byte.md)|`sbyte` 또는 `char`|  
|[short](short.md)|`sbyte`, `byte`, `ushort`, `uint`, `ulong` 또는 `char`|  
|[ushort](ushort.md)|`sbyte`, `byte`, `short` 또는 `char`|  
|[int](int.md)|`sbyte`, `byte`, `short`, `ushort`, `uint`, `ulong` 또는 `char`|  
|[uint](uint.md)|`sbyte`, `byte`, `short`, `ushort`, `int` 또는 `char`|  
|[long](long.md)|`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `ulong` 또는 `char`|  
|[ulong](ulong.md)|`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long` 또는 `char`|  
|[char](char.md)|`sbyte`, `byte`또는 `short`|  
|[float](float.md)|`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char` 또는 `decimal`|  
|[double](double.md)|`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float` 또는 `decimal`|  
|[decimal](decimal.md)|`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float` 또는 `double`|  
  
## <a name="remarks"></a>설명  
  
- 명시적 숫자 변환으로 인해 자릿수 손실 또는 예외(일반적으로 <xref:System.OverflowException>)가 throw될 수 있습니다.  

- 정수 형식의 값을 다른 정수 형식으로 변환하면 결과는 오버플로 [검사 컨텍스트](checked-and-unchecked.md)에 따라 달라집니다. 확인된 컨텍스트에서 소스 값이 대상 형식의 범위 내에 있으면 변환이 성공합니다. 그렇지 않으면 <xref:System.OverflowException>이 throw됩니다. 확인되지 않은 컨텍스트에서 변환은 항상 성공하고 다음과 같이 진행됩니다.

  - 소스 형식이 대상 형식보다 큰 경우 소스 값은 가장 중요한 비트인 해당 "extra"를 삭제함으로써 잘립니다. 그런 다음, 결과는 대상 형식의 값으로 처리됩니다.

  - 소스 형식이 대상 형식보다 작은 경우 소스 값은 대상 형식과 크기가 같도록 부호 확장 또는 0 확장 중 하나입니다. 부호 확장은 소스 형식이 서명된 경우 사용되며, 소스 형식이 서명되지 않은 경우 0 확장이 사용됩니다. 그런 다음, 결과는 대상 형식의 값으로 처리됩니다.

  - 소스 형식이 대상 형식과 동일한 크기인 경우 소스 값은 대상 형식의 값으로 처리됩니다.
  
- `decimal` 값을 정수 형식으로 변환하면, 이 값은 0을 향한 방향으로 가장 가까운 정수값으로 반올림됩니다. 결과 정수 값이 대상 형식 범위에서 벗어났을 경우 <xref:System.OverflowException>이 throw됩니다.  
  
- `double` 또는 `float` 값을 정수 형식으로 변환하면, 이 값은 0을 향한 방향으로 가장 가까운 정수값으로 반올림됩니다. 결과 정수 값이 대상 형식 범위에서 벗어났을 경우 결과는 오버플로 [검사 컨텍스트](checked-and-unchecked.md)에 따라 달라집니다. Checked 컨텍스트에서는 <xref:System.OverflowException>이 throw됩니다. 반면 Unchecked 컨텍스트에서 결과는 지정되지 않은 대상 형식 값이 됩니다.  
  
- `double`을 `float`로 변환할 경우 `double` 값을 가장 가까운 `float` 값으로 반올림합니다. `double` 값이 너무 크거나 작아서 대상 형식에 맞출 수 없을 경우 결과 값은 0 또는 무한대가 됩니다.  
  
- `float` 또는 `double`을 `decimal`로 변환할 경우 소스 값을 `decimal` 표현으로 변환한 다음 필요한 경우 가장 가까운 소수점 이하 28번째 자리로 반올림합니다. 소스 값에 따라 다음 결과 중 하나가 발생할 수 있습니다.  

  - 소스 값이 너무 작아서 `decimal`로 나타낼 수 없을 경우 결과 값은 0이 됩니다.  

  - 소스 값이 NaN(숫자가 아님), 무한대 또는 너무 커서 `decimal`로 나타낼 수 없을 경우 <xref:System.OverflowException>을 throw합니다.  
  
- `decimal`을 `float` 또는 `double`로 변환할 경우 `decimal` 값을 가장 가까운 `double` 또는 `float` 값으로 반올림합니다.  
  
 명시적 변환에 대한 자세한 내용은 [C# 언어 사양](../language-specification/index.md)의 [명시적 변환](~/_csharplang/spec/conversions.md#explicit-conversions) 섹션을 참조하세요.
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [캐스팅 및 형식 변환](../../programming-guide/types/casting-and-type-conversions.md)
- [() 연산자](../operators/invocation-operator.md)
- [정수 계열 형식 표](integral-types-table.md)
- [부동 소수점 형식 표](floating-point-types-table.md)
- [기본 제공 형식 표](built-in-types-table.md)
- [암시적 숫자 변환 표](implicit-numeric-conversions-table.md)
