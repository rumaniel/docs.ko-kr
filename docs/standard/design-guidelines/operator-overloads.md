---
title: 연산자 오버로드
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- operators [.NET Framework], overloads
- names [.NET Framework], overloaded operators
- member design guidelines, operators
- overloaded operators
ms.assetid: 37585bf2-4c27-4dee-849a-af70e3338cc1
author: KrzysztofCwalina
ms.openlocfilehash: 441dc2777cd8d221300c526b6b31a647af60ca71
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61756860"
---
# <a name="operator-overloads"></a>연산자 오버로드
연산자 오버 로드 framework 형식을 기본 제공 언어 기본 형식 것 처럼 표시할 수 있습니다.  
  
 허용 및 일부 경우에 유용 하지만 연산자 오버 로드를 신중 하 게 사용 되어야 합니다. In 연산자는 오버 로드에 되었습니다 악용 프레임 워크 디자이너는 간단한 방법을 해야 하는 작업에 대 한 연산자를 사용 하기 시작 하는 경우와 같은 많은 경우가 있습니다. 다음 지침은 시간과 연산자 오버 로드를 사용 하는 방법을 결정 하는 데 도움이 됩니다.  
  
 **X AVOID** 기본 (기본 제공) 형식 느낌을 해야 하는 형식을 제외 하 고 연산자 오버 로드를 정의 합니다.  
  
 **✓ CONSIDER** 기본 형식 처럼 있어야 하는 형식에서 연산자 오버 로드를 정의 합니다.  
  
 예를 들어 <xref:System.String?displayProperty=nameWithType> 했습니다 `operator==` 고 `operator!=` 정의 합니다.  
  
 **✓ DO** 번호를 나타내는 구조체에서 연산자 오버 로드를 정의 (예: <xref:System.Decimal?displayProperty=nameWithType>).  
  
 **X DO NOT** 연산자 오버 로드를 정의 하는 경우 간단한 수 있습니다.  
  
 연산자 오버 로드는 즉시 알아낼 됩니다 하는 작업의 결과 경우에 유용 합니다. 예를 들어 편이 1을 뺍니다 있으려면 <xref:System.DateTime> 다른 `DateTime` 가져오고를 <xref:System.TimeSpan>입니다. 그러나 두 데이터베이스 쿼리에 union, union 논리 연산자를 사용 하 여 또는 시프트 연산자를 사용 하 여 스트림에 쓸 적합 하지 않습니다.  
  
 **X DO NOT** 연산자는 오버 로드를 정의 하는 형식은 피연산자 중 하나 이상을 아닌 경우 오버 로드를 제공 합니다.  
  
 **✓ DO** 대칭 방식에서 연산자를 오버 로드 합니다.  
  
 예를 들어 오버 로드는 `operator==`, 연산자도 오버 로드 해야는 `operator!=`합니다. 마찬가지로, 오버 로드 하면 합니다 `operator<`, 연산자도 오버 로드 해야는 `operator>`등입니다.  
  
 **✓ CONSIDER** 각 오버 로드 된 연산자에 해당 하는 이름을 가진 메서드를 제공 합니다.  
  
 다양 한 언어 연산자 오버 로드를 지원 하지 않습니다. 연산자를 오버 로드는 동일한 기능을 제공 하는 적절 한 도메인별 이름으로 보조 메서드를 포함 하는 것이 좋습니다.  
  
 다음 표에서 연산자와 해당 하는 친숙 한 메서드 이름을의 목록을 포함합니다.  
  
|C# 연산자 기호|메타 데이터 이름|이름|  
|-------------------------|-------------------|-------------------|  
|`N/A`|`op_Implicit`|`To<TypeName>/From<TypeName>`|  
|`N/A`|`op_Explicit`|`To<TypeName>/From<TypeName>`|  
|`+ (binary)`|`op_Addition`|`Add`|  
|`- (binary)`|`op_Subtraction`|`Subtract`|  
|`* (binary)`|`op_Multiply`|`Multiply`|  
|`/`|`op_Division`|`Divide`|  
|`%`|`op_Modulus`|`Mod or Remainder`|  
|`^`|`op_ExclusiveOr`|`Xor`|  
|`& (binary)`|`op_BitwiseAnd`|`BitwiseAnd`|  
|<code>&#124;</code>|`op_BitwiseOr`|`BitwiseOr`|  
|`&&`|`op_LogicalAnd`|`And`|  
|<code>&#124;&#124;</code>|`op_LogicalOr`|`Or`|  
|`=`|`op_Assign`|`Assign`|  
|`<<`|`op_LeftShift`|`LeftShift`|  
|`>>`|`op_RightShift`|`RightShift`|  
|`N/A`|`op_SignedRightShift`|`SignedRightShift`|  
|`N/A`|`op_UnsignedRightShift`|`UnsignedRightShift`|  
|`==`|`op_Equality`|`Equals`|  
|`!=`|`op_Inequality`|`Equals`|  
|`>`|`op_GreaterThan`|`CompareTo`|  
|`<`|`op_LessThan`|`CompareTo`|  
|`>=`|`op_GreaterThanOrEqual`|`CompareTo`|  
|`<=`|`op_LessThanOrEqual`|`CompareTo`|  
|`*=`|`op_MultiplicationAssignment`|`Multiply`|  
|`-=`|`op_SubtractionAssignment`|`Subtract`|  
|`^=`|`op_ExclusiveOrAssignment`|`Xor`|  
|`<<=`|`op_LeftShiftAssignment`|`LeftShift`|  
|`%=`|`op_ModulusAssignment`|`Mod`|  
|`+=`|`op_AdditionAssignment`|`Add`|  
|`&=`|`op_BitwiseAndAssignment`|`BitwiseAnd`|  
|<code>&#124;=</code>|`op_BitwiseOrAssignment`|`BitwiseOr`|  
|`,`|`op_Comma`|`Comma`|  
|`/=`|`op_DivisionAssignment`|`Divide`|  
|`--`|`op_Decrement`|`Decrement`|  
|`++`|`op_Increment`|`Increment`|  
|`- (unary)`|`op_UnaryNegation`|`Negate`|  
|`+ (unary)`|`op_UnaryPlus`|`Plus`|  
|`~`|`op_OnesComplement`|`OnesComplement`|  
  
### <a name="overloading-operator-"></a>연산자 오버 로드 = =  
 오버 로드 `operator ==` 상당히 복잡 합니다. 연산자의 의미 체계와 같은 몇 가지 다른 멤버와 호환 되도록 필요한 <xref:System.Object.Equals%2A?displayProperty=nameWithType>합니다.  
  
### <a name="conversion-operators"></a>변환 연산자  
 변환 연산자는 다른 형식 간에 변환할 수 있는 단항 연산자입니다. 연산자는 피연산자 또는 반환 형식에서 정적 구성원으로 정의 되어야 합니다. 변환 연산자의 두 종류가 있습니다: 명시적 및 암시적입니다.  
  
 **X DO NOT** 이러한 변환의 최종 사용자가 예상 되는 것은 명확 하 게 경우 변환 연산자를 제공 합니다.  
  
 **X DO NOT** 형식의 도메인 외부에서 변환 연산자를 정의 합니다.  
  
 예를 들어 <xref:System.Int32>, <xref:System.Double>, 및 <xref:System.Decimal> 는 모든 숫자 형식, <xref:System.DateTime> 아닙니다. 없는 변환 연산자를 해야 하므로 `Double(long)` 에 `DateTime`합니다. 생성자는 이러한 경우 것이 좋습니다.  
  
 **X DO NOT** 변환이 손실 될 수 있는 경우에 암시적 변환 연산자를 제공 합니다.  
  
 예를 들어 안으로 암시적으로 변환할 `Double` 에 `Int32` 있으므로 `Double` 보다 범위가 더 넓은 `Int32`합니다. 변환 손실 될 수 있는 경우에 명시적 변환 연산자를 제공할 수 있습니다.  
  
 **X DO NOT** 암시적 캐스트에서 예외를 throw 합니다.  
  
 최종 사용자는 변환이 일어나지는 인식 되지 않을 수도 있습니다 때문에 상황을 이해 하기 매우 어렵습니다.  
  
 **✓ DO** throw <xref:System.InvalidCastException?displayProperty=nameWithType> 하면 캐스트 연산자에 대 한 호출 손실 변환와 연산자의 계약 손실 변환을 허용 하지 않습니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [멤버 디자인 지침](../../../docs/standard/design-guidelines/member.md)
- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
