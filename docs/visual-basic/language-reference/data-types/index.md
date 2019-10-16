---
title: 데이터 형식 요약(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- Boolean data type [Visual Basic], supported types in Visual Basic
- storage [Visual Basic], order of storage
- data types [Visual Basic], Visual Basic
- Single data type [Visual Basic], supported types in Visual Basic
- notation [Visual Basic], scientific
- memory requirements, data types
- user-defined data types [Visual Basic], Visual Basic
- Date data type [Visual Basic], Visual Basic
- Visual Basic, data types
- storage [Visual Basic], allocation
- Integer data type [Visual Basic], Visual Basic data types
- storage [Visual Basic], space
- Variant data types [Visual Basic], supported types in Visual Basic
- Char data type [Visual Basic], Visual Basic data types
- intrinsic data types [Visual Basic]
- memory consumption [Visual Basic], data types
- single-precision numbers
- data types [Visual Basic], order of storage
- Long data type [Visual Basic], supported types in Visual Basic
- String data type [Visual Basic], Visual Basic data types
- storage order, data types
- StructLayoutAttribute class, Visual Basic data type storage
- scientific notation
- Double data type [Visual Basic], Visual Basic data types
- Byte data type [Visual Basic], Visual Basic data types
- Object data type [Visual Basic], supported types in Visual Basic
- data types [Visual Basic], storage allocation
- double-precision numbers
- data types [Visual Basic], summary
- dates [Visual Basic], data types
- strings [Visual Basic], data types
- memory consumption
- storage order, controlling in Visual Basic
- data types [Visual Basic], memory requirements
ms.assetid: e975cdb6-64d8-4a4a-ae27-f3b3ed198ae0
ms.openlocfilehash: 57f6caa00806f4874cb8070805e8b6784ec82e40
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956798"
---
# <a name="data-type-summary-visual-basic"></a>데이터 형식 요약(Visual Basic)
다음 표에서는 Visual Basic 데이터 형식, 지원 되는 공용 언어 런타임 형식, 해당 명목상 저장소 할당 및 해당 값 범위를 보여 줍니다.  
  
|Visual Basic 형식|공용 언어 런타임 형식 구조|명목상 저장소 할당|값 범위|  
|-----------------------|--------------------------------------------|--------------------------------|-----------------|  
|[Boolean](../../../visual-basic/language-reference/data-types/boolean-data-type.md)|<xref:System.Boolean>|구현 플랫폼에 따라 달라 집니다.|`True` 또는 `False`|  
|[Byte](../../../visual-basic/language-reference/data-types/byte-data-type.md)|<xref:System.Byte>|1바이트|0-255 (부호 없음)|  
|[Char](../../../visual-basic/language-reference/data-types/char-data-type.md) (단일 문자)|<xref:System.Char>|2바이트|0-65535 (부호 없음)|  
|[Date](../../../visual-basic/language-reference/data-types/date-data-type.md)|<xref:System.DateTime>|8바이트|01 년 1 월 1 일 0:00:00 (자정), 11:59:59 년 12 월 9999 31 일 오후|  
|[Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md)|<xref:System.Decimal>|16바이트|0부터 +/-79228162514264337593543950335 (+/-7.9...E + 28) <sup>†</sup> (소수점 없음) 0부터 +/-7.9228162514264337593543950335, 소수 오른쪽에 28 개 위치<br /><br /> 0이 아닌 가장 작은 숫자는 +/-0.0000000000000000000000000001 (+/-1E-28) <sup>†</sup> 입니다.|  
|[Double](../../../visual-basic/language-reference/data-types/double-data-type.md) (배정밀도 부동 소수점)|<xref:System.Double>|8바이트|-1.79769313486231570 e + 308 ~-4.94065645841246544 E-324 <sup>†</sup> (음수 값)<br /><br /> 4.94065645841246544 e-324 ~ 1.79769313486231570 E + 308 <sup>†</sup> (양수 값)|  
|[Integer](../../../visual-basic/language-reference/data-types/integer-data-type.md)|<xref:System.Int32>|4바이트|-2147483648 ~ 2147483647 (부호 있음)|  
|[Long](../../../visual-basic/language-reference/data-types/long-data-type.md) (long 정수)|<xref:System.Int64>|8바이트|-9223372036854775808 ~ 9223372036854775807 (9.2 ... E + 18 <sup>†</sup>) (부호 있음)|  
|[개체](../../../visual-basic/language-reference/data-types/object-data-type.md)|<xref:System.Object>클래스|32 비트 플랫폼에서 4 바이트<br /><br /> 64 비트 플랫폼에서 8 바이트|모든 형식을 형식의 변수에 저장할 수 있습니다.`Object`|  
|[SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|<xref:System.SByte>|1바이트|-128 ~ 127 (부호 있음)|  
|[Short](../../../visual-basic/language-reference/data-types/short-data-type.md) (short 정수)|<xref:System.Int16>|2바이트|-32768 ~ 32767 (부호 있음)|  
|[단일](../../../visual-basic/language-reference/data-types/single-data-type.md) (단 정밀도 부동 소수점)|<xref:System.Single>|4바이트|-3.4028235 e + 38 ~-1.401298 E-45 <sup>†</sup> (음수 값)<br /><br /> 1.401298 e-45 ~ 3.4028235 E + 38 <sup>†</sup> (양수 값)|  
|[문자열](../../../visual-basic/language-reference/data-types/string-data-type.md) (가변 길이)|<xref:System.String>클래스|구현 플랫폼에 따라 달라 집니다.|0 ~ 약 20억 유니코드 문자|  
|[UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|<xref:System.UInt32>|4바이트|0-4294967295 (부호 없음)|  
|[ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md)|<xref:System.UInt64>|8바이트|0-18446744073709551615 (1.8 ... E + 19 <sup>†</sup>) (부호 없음)|  
|[사용자 정의](../../../visual-basic/language-reference/data-types/user-defined-data-type.md) 구조체나|(에서 <xref:System.ValueType>상속)|구현 플랫폼에 따라 달라 집니다.|구조체의 각 멤버는 데이터 형식에 따라 결정 되 고 다른 멤버의 범위에 독립적으로 범위가 결정 됩니다.|  
|[UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md)|<xref:System.UInt16>|2바이트|0-65535 (부호 없음)|  
  
 <sup>†</sup> *과학적 표기법*에서 "E"는 10의 거듭제곱을 나타냅니다. 따라서 3.56 E + 2는 3.56 x 10<sup>2</sup> 또는 356을 의미 하 고, 3.56 e-2는 3.56/10<sup>2</sup> 또는 0.0356을 의미 합니다.  
  
> [!NOTE]
> 텍스트를 포함 하는 <xref:Microsoft.VisualBasic.Strings.StrConv%2A> 문자열의 경우 함수를 사용 하 여 텍스트 형식을 다른 형식으로 변환 합니다.  
  
 선언 문에서 데이터 형식을 지정 하는 것 외에도 형식 문자를 사용 하 여 일부 프로그래밍 요소의 데이터 형식을 강제할 수 있습니다. [형식 문자](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)를 참조 하십시오.  
  
## <a name="memory-consumption"></a>메모리 소비  
 기본 데이터 형식을 선언 하는 경우 메모리 소비가 명목상 저장소 할당과 동일 하다 고 가정 하는 것은 안전 하지 않습니다. 이는 다음과 같은 고려 사항으로 인해 발생 합니다.  
  
- **저장소 할당.** 공용 언어 런타임은 응용 프로그램이 실행 중인 플랫폼의 현재 특성에 따라 저장소를 할당할 수 있습니다. 메모리가 거의 가득 찬 경우 선언 된 요소를 가능한 한 가깝게 압축할 수 있습니다. 다른 경우에는 성능 최적화를 위해 메모리 주소를 자연 하드웨어 경계에 맞출 수 있습니다.  
  
- **플랫폼 너비입니다.** 64 비트 플랫폼의 저장소 할당은 32 비트 플랫폼에 할당 된 것과 다릅니다.  
  
### <a name="composite-data-types"></a>복합 데이터 형식  
 구조 또는 배열과 같은 복합 데이터 형식의 각 멤버에도 동일한 고려 사항이 적용 됩니다. 단순히 형식의 멤버에 대 한 명목상 저장소 할당을 추가 하는 것에는 의존해 서는 안 됩니다. 또한 다음과 같은 다른 고려 사항도 있습니다.  
  
- **헤드만.** 일부 복합 형식에는 추가 메모리 요구 사항이 있습니다. 예를 들어 배열에는 배열 자체와 각 차원에 대 한 추가 메모리가 사용 됩니다. 32 비트 플랫폼에서이 오버 헤드는 현재 12 바이트와 각 차원에 대 한 8 바이트를 더한 값입니다. 64 비트 플랫폼에서는이 요구 사항이 두 배가 됩니다.  
  
- **저장소 레이아웃.** 메모리의 저장소 순서가 선언 순서와 동일 하다는 것을 안전 하 게 가정할 수 없습니다. 2 바이트 또는 4 바이트 경계와 같은 바이트 맞춤에 대 한 가정을 수행할 수도 없습니다. 클래스 또는 구조체를 정의 하 고 해당 멤버의 저장소 레이아웃을 제어 해야 하는 경우 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 특성을 클래스나 구조체에 적용할 수 있습니다.  
  
### <a name="object-overhead"></a>개체 오버 헤드  
 기본 `Object` 또는 복합 데이터 형식을 참조 하는는 데이터 형식에 포함 된 데이터 외에 4 바이트를 사용 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.Strings.StrConv%2A>
- <xref:System.Runtime.InteropServices.StructLayoutAttribute>
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [변환 요약](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [형식 문자](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)
- [데이터 형식의 효율적 사용](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
