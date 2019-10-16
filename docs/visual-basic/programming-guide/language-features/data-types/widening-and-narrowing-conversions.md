---
title: 확대 변환과 축소 변환(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- widening conversions [Visual Basic]
- narrowing conversions [Visual Basic]
- conversions [Visual Basic], type
- data types [Visual Basic], changing
- variables [Visual Basic], changing data type
- conversions [Visual Basic], exceptions during conversion
- type conversion [Visual Basic], exceptions during conversion
- conversions [Visual Basic], data type
- conversions [Visual Basic], narrowing
- type conversion [Visual Basic], narrowing
- data type conversion [Visual Basic], widening
- data type conversion [Visual Basic], narrowing
- changing data types [Visual Basic]
- type conversion [Visual Basic], widening
- data type conversion [Visual Basic], exceptions during conversion
- conversions [Visual Basic], widening
ms.assetid: 058c3152-6c28-4268-af44-2209e774f0bd
ms.openlocfilehash: 858b2b2e154b659470fa61b21f25ab61eabda012
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965651"
---
# <a name="widening-and-narrowing-conversions-visual-basic"></a>확대 변환과 축소 변환(Visual Basic)
형식 변환의 중요 한 고려 사항은 변환 결과가 대상 데이터 형식의 범위 내에 있는지 여부입니다.  
  
 *확대 변환* 에서는 원래 데이터의 가능한 값을 허용할 수 있는 데이터 형식으로 값을 변경 합니다.  확대 변환은 원본 값을 유지 하지만 표시를 변경할 수 있습니다. 이는 정수 계열 형식 `Decimal`에서로 변환 하거나 `String`에서 `Char` 로 변환 하는 경우에 발생 합니다.  
  
 *축소 변환* 은 가능한 값의 일부를 저장하지 못할 수도 있는 데이터 형식으로 값을 변경합니다. 예를 들어 정수 계열 형식으로 변환 될 때 소수 값이 반올림 되 고 변환 `Boolean` 되는 숫자 형식이 `True` 또는 `False`로 줄어듭니다.  
  
## <a name="widening-conversions"></a>확대 변환  
 다음 표에서는 표준 확대 변환을 보여 줍니다.  
  
|데이터 형식|데이터 형식 확대 <sup>1</sup>|  
|---|---|  
|[SByte](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|`SByte`, `Short`, `Integer`, `Long`, `Decimal`, `Single`, `Double`|  
|[Byte](../../../../visual-basic/language-reference/data-types/byte-data-type.md)|`Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`|  
|[Short](../../../../visual-basic/language-reference/data-types/short-data-type.md)|`Short`, `Integer`, `Long`, `Decimal`, `Single`, `Double`|  
|[UShort](../../../../visual-basic/language-reference/data-types/ushort-data-type.md)|`UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`|  
|[Integer](../../../../visual-basic/language-reference/data-types/integer-data-type.md)|`Integer`, `Long`, `Decimal`, `Single`, `Double`<sup>2</sup>|  
|[UInteger](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|`UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`<sup>2</sup>|  
|[Long](../../../../visual-basic/language-reference/data-types/long-data-type.md)|`Long`, `Decimal`, `Single`, `Double`<sup>2</sup>|  
|[ULong](../../../../visual-basic/language-reference/data-types/ulong-data-type.md)|`ULong`, `Decimal`, `Single`, `Double`<sup>2</sup>|  
|[Decimal](../../../../visual-basic/language-reference/data-types/decimal-data-type.md)|`Decimal`, `Single`, `Double`<sup>2</sup>|  
|[Single](../../../../visual-basic/language-reference/data-types/single-data-type.md)|`Single`, `Double`|  
|[Double](../../../../visual-basic/language-reference/data-types/double-data-type.md)|`Double`|  
|모든 열거 형식 ([열거형](../../../../visual-basic/language-reference/statements/enum-statement.md))|기본 정수 형식 및 기본 형식이 확대 되는 모든 형식입니다.|  
|[Char](../../../../visual-basic/language-reference/data-types/char-data-type.md)|`Char`, `String`|  
|`Char` 배열|`Char`배열과`String`|  
|모든 형식|[개체](../../../../visual-basic/language-reference/data-types/object-data-type.md)|  
|모든 파생 형식|파생 되는 기본 형식 <sup>3</sup>입니다.|  
|모든 형식|구현 하는 인터페이스입니다.|  
|[Nothing](../../../../visual-basic/language-reference/nothing.md)|모든 데이터 형식 또는 개체 유형입니다.|  
  
 <sup>1</sup> 정의에 따라 모든 데이터 형식이 그 자체로 확대 됩니다.  
  
 <sup>2</sup> `Integer`, ,,`Double` 또는에서 또는 로`Single` 변환 하면 전체 자릿수가 손실 될 수 있지만 크기는 손실 되지 않습니다. `Decimal` `Long` `UInteger` `ULong` 이러한 의미에서는 정보 손실이 발생 하지 않습니다.  
  
 <sup>3</sup> 파생 형식에서 해당 기본 형식 중 하나로 변환 하는 것은 확대 된 것 처럼 보일 수 있습니다. 양쪽 맞춤은 파생 된 형식에 기본 형식의 모든 멤버가 포함 되어 있으므로 기본 형식의 인스턴스로 한정 된다는 것입니다. 반대 방향으로 기본 형식에는 파생 형식으로 정의 된 새 멤버가 포함 되지 않습니다.  
  
 확대 변환은 런타임에 항상 성공 하며 데이터 손실이 발생 하지 않습니다. [Option Strict 문이](../../../../visual-basic/language-reference/statements/option-strict-statement.md) 유형 검사 `On` 를 또는로 `Off`설정 하는지 여부에 관계 없이 항상 암시적으로이를 수행할 수 있습니다.  
  
## <a name="narrowing-conversions"></a>축소 변환  
 표준 축소 변환에는 다음이 포함 됩니다.  
  
- 위의 표에서 확대 변환의 반대 방향 (모든 형식이 자체로 확대 됨을 제외 하 고)  
  
- 두 방향 모두에서 [부울](../../../../visual-basic/language-reference/data-types/boolean-data-type.md) 과 임의의 숫자 형식으로 변환  
  
- 모든 숫자 형식에서 열거형 형식으로 변환 (`Enum`)  
  
- [문자열과](../../../../visual-basic/language-reference/data-types/string-data-type.md) 숫자 형식, `Boolean`또는 [날짜](../../../../visual-basic/language-reference/data-types/date-data-type.md) 사이에서 두 방향으로 변환  
  
- 데이터 형식 또는 개체 형식에서 파생 된 형식으로 변환  
  
 축소 변환은 런타임에 항상 성공 하지 않으며 데이터 손실이 발생 하거나 실패할 수 있습니다. 대상 데이터 형식이 변환 중인 값을 받을 수 없는 경우 오류가 발생 합니다. 예를 들어 숫자를 변환 하면 오버플로가 발생할 수 있습니다. [Option Strict 문이](../../../../visual-basic/language-reference/statements/option-strict-statement.md) 형식 확인 스위치를로 `Off`설정 하지 않으면 컴파일러에서 축소 변환을 암시적으로 수행할 수 없습니다.  
  
> [!NOTE]
> `For Each…Next` 컬렉션의 요소에서 루프 제어 변수로의 변환에 대 한 축소 변환 오류는 무시 됩니다. 자세한 내용 및 예제는 각 항목에 대 한 "축소 변환" 섹션을 참조 하세요. [ 다음 문](../../../../visual-basic/language-reference/statements/for-each-next-statement.md).  
  
### <a name="when-to-use-narrowing-conversions"></a>축소 변환을 사용 하는 경우  
 원본 값이 오류 또는 데이터 손실 없이 대상 데이터 형식으로 변환 될 수 있다는 것을 알고 있는 경우 축소 변환을 사용 합니다. 예를 들어 사용자에 게 " `String` True" 또는 "False"가 포함 된 경우 `CBool` 키워드를 사용 하 여로 `Boolean`변환할 수 있습니다.  
  
## <a name="exceptions-during-conversion"></a>변환 하는 동안 발생 하는 예외  
 확대 변환은 항상 성공 하므로 예외를 throw 하지 않습니다. 축소 변환은 실패할 경우 가장 일반적으로 다음과 같은 예외를 throw 합니다.  
  
- <xref:System.InvalidCastException>-두 형식 간에 변환이 정의 되지 않은 경우  
  
- <xref:System.OverflowException>-(정수 계열 형식에만 해당) 변환 된 값이 대상 형식에 비해 너무 클 경우  
  
 클래스 또는 구조체에서 해당 클래스 또는 구조체에 대 한 변환 연산자로 사용할 [CType 함수](../../../../visual-basic/language-reference/functions/ctype-function.md) 를 정의 하는 `CType` 경우 적절 한 하다 고 판단 예외를 throw 할 수 있습니다. 또한 Visual Basic 함수나 .NET Framework `CType` 메서드를 호출 하 여 다양 한 예외를 throw 할 수 있습니다.  
  
## <a name="changes-during-reference-type-conversions"></a>참조 형식 변환 중 변경  
 *참조 형식* 에서의 변환은 포인터만 값에 복사 합니다. 값 자체는 어떠한 방식으로든 복사 되거나 변경 되지 않습니다. 변경할 수 있는 유일한 사항은 포인터를 포함 하는 변수의 데이터 형식입니다. 다음 예제에서는 데이터 형식이 파생 클래스에서 기본 클래스로 변환 되지만 이제 두 변수가 가리키는 개체가 변경 되지 않습니다.  
  
```  
' Assume class cSquare inherits from class cShape.  
Dim shape As cShape  
Dim square As cSquare = New cSquare  
' The following statement performs a widening  
' conversion from a derived class to its base class.  
shape = square  
```  
  
## <a name="see-also"></a>참고자료

- [데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
- [Visual Basic 형식 변환](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
- [암시적 변환과 명시적 변환](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [문자열과 다른 형식 사이의 변환](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)
- [방법: Visual Basic에서 개체를 다른 형식으로 변환](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)
- [배열 규칙](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)
- [데이터 형식](../../../../visual-basic/language-reference/data-types/index.md)
- [형식 변환 함수](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
