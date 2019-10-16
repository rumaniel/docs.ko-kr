---
title: 기본 형식
description: 에 사용 되는 기본 기본 형식을 검색 합니다 F# 언어입니다.
ms.date: 07/09/2018
ms.openlocfilehash: fb9f275490cb402ff36e959774cd65450de77115
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645596"
---
# <a name="basic-types"></a>기본 형식

이 항목에 정의 된 기본 유형을 나열 합니다 F# 언어입니다. 이러한 유형은에서 가장 기본적인 F#, 거의 모든의 토대를 형성할 F# 프로그램입니다. 이들은.NET 기본 형식의 상위 집합입니다.

|형식|.NET 형식|설명|
|----|---------|-----------|
|`bool`|<xref:System.Boolean>|가능한 값은 `true`와 `false`입니다.|
|`byte`|<xref:System.Byte>|0에서 255 사이의 값입니다.|
|`sbyte`|<xref:System.SByte>|-128에서 127 까지의 값입니다.|
|`int16`|<xref:System.Int16>|-32768에서 32767 까지의 값입니다.|
|`uint16`|<xref:System.UInt16>|0에서 65535 까지의 값입니다.|
|`int`|<xref:System.Int32>|-2,147,483,648에서 2,147,483,647 까지의 값입니다.|
|`uint32`|<xref:System.UInt32>|0에서 4,294,967,295 사이의 값입니다.|
|`int64`|<xref:System.Int64>|-9223372036854775808 때문에 9,223,372,036,854,775,807 까지의 값입니다.|
|`uint64`|<xref:System.UInt64>|0에서 18446744073709551615 값입니다.|
|`nativeint`|<xref:System.IntPtr>|부호 있는 정수로 네이티브 포인터입니다.|
|`unativeint`|<xref:System.UIntPtr>|부호 없는 정수는 네이티브 포인터입니다.|
|`char`|<xref:System.Char>|유니코드 문자 값입니다.|
|`string`|<xref:System.String>|유니코드 텍스트입니다.|
|`decimal`|<xref:System.Decimal>|부동 소수점 데이터 형식에 적어도 28 개의 유효 숫자입니다.|
|`unit`|적용할 수 없음|실제 값이 없음을 나타냅니다. 형식에 표시 되는 정식 값 하나만 `()`합니다. 단위 값 `()`, 여기서는 값이 필요 하지만 실제 값 수 또는 적합 한 자리 표시자로 흔히 사용 됩니다.|
|`void`|<xref:System.Void>|없는 형식 또는 값을 나타냅니다.|
|`float32`, `single`|<xref:System.Single>|32 비트 부동 소수점 형식입니다.|
|`float`, `double`|<xref:System.Double>|64 비트 부동 소수점 형식입니다.|

> [!NOTE]
> 사용 하 여 64 비트 정수 형식에 대해 너무 큰 정수를 사용 하 여 계산을 수행할 수 있습니다 합니다 [bigint](https://msdn.microsoft.com/library/dc8be18d-4042-46c4-b136-2f21a84f6efa) 형식입니다. `bigint` 기본 형식으로 간주 되지 않습니다. 약어 `System.Numerics.BigInteger`합니다.

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
