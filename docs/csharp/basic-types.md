---
title: 기본 형식 - C# 가이드
description: 모든 C# 프로그램의 핵심 형식(숫자, 문자열 및 개체)을 알아봅니다.
ms.date: 10/10/2016
ms.assetid: 95c686ba-ae4f-440e-8e94-0dbd6e04d11f
ms.openlocfilehash: b65e6ba61bd8886223403f869aa301703f89e8ba
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834243"
---
# <a name="types-variables-and-values"></a>형식, 변수 및 값

C#은 강력한 형식의 언어입니다. 모든 변수 및 상수에는 값으로 계산되는 모든 식을 실행하는 형식이 있습니다. 모든 메서드 시그니처는 각 입력 매개 변수 및 반환 값의 형식을 지정합니다. .NET Framework 클래스 라이브러리는 기본 제공 숫자 형식 집합 및 날짜, 개체의 배열, 컬렉션, 네트워크 연결, 파일 시스템과 같은 더 복잡한 형식을 정의합니다. 일반 C# 프로그램에서는 클래스 라이브러리의 형식 및 프로그램의 문제 도메인에 관련된 개념을 모델링하는 사용자 정의 형식을 사용합니다.  
  
형식에 저장된 정보에는 다음이 포함될 수 있습니다.  
  
- 형식 변수에 필요한 스토리지 공간.  
  
- 형식이 나타낼 수 있는 최대값 및 최소값.  
  
- 형식에 포함되는 멤버(메서드, 필드, 이벤트 등).  
  
- 형식이 상속하는 기본 형식.  
  
- 런타임에 변수에 대한 메모리가 할당될 위치.  
  
- 허용되는 작업 유형.  
  
컴파일러는 형식 정보를 사용하여 코드에서 수행되는 모든 작업이 *형식이 안전*한지 확인합니다. 예를 들어 [int](language-reference/builtin-types/integral-numeric-types.md) 형식의 변수를 선언할 경우 컴파일러를 통해 더하기 및 빼기 작업에서 변수를 사용할 수 있습니다. [bool](language-reference/keywords/bool.md) 형식의 변수에 대해 같은 작업을 수행하려고 하면 컴파일러는 다음 예제와 같이 오류를 생성합니다.  
  
[!code-csharp[Type Safety](../../samples/snippets/csharp/concepts/basic-types/type-safety.cs)]  
  
> [!NOTE]  
> C 및 C++ 개발자는 C#에서 [bool](language-reference/keywords/bool.md)이 [int](language-reference/builtin-types/integral-numeric-types.md)로 변환될 수 없음을 알고 있습니다.  
  
컴파일러는 형식 정보를 실행 파일에 메타데이터로 포함합니다. CLR(공용 언어 런타임)는 런타임에 이 메타데이터를 사용하여 메모리를 할당 및 회수할 때 형식 안정성을 추가로 보장합니다.  

## <a name="specifying-types-in-variable-declarations"></a>변수 선언에서 형식 지정

프로그램에서 변수나 상수를 선언할 때 컴파일러가 형식을 유추하게 하려면 형식을 지정하거나 [var](language-reference/keywords/var.md) 키워드를 사용해야 합니다. 다음 예제에서는 기본 제공 숫자 형식 및 복잡한 사용자 정의 형식을 둘 다 사용하는 일부 변수 선언을 보여 줍니다.  
  
[!code-csharp[Variable Declaration](../../samples/snippets/csharp/concepts/basic-types/variable-declaration.cs)]  
  
메서드 매개 변수 및 반환 값의 형식은 메서드 시그니처에서 지정됩니다. 다음 시그니처는 입력 인수로 [int](language-reference/builtin-types/integral-numeric-types.md)가 필요하고 문자열을 반환하는 메서드를 보여 줍니다.  
  
[!code-csharp[Method Signature](../../samples/snippets/csharp/concepts/basic-types/method-signature.cs)]  
  
변수가 선언된 후에는 새 형식으로 다시 선언될 수 없고 선언된 형식과 호환되지 않는 값이 할당될 수 없습니다. 예를 들어 [int](language-reference/builtin-types/integral-numeric-types.md)를 선언하고 [true](language-reference/keywords/true-literal.md)의 부울 값을 여기에 할당할 수 있습니다. 그러나 값은 새 변수에 할당되거나 메서드 인수로 전달될 경우 다른 형식으로 변환할 수 있습니다. 데이터 손실을 일으키지 않는 *형식 변환*은 컴파일러에서 자동으로 수행됩니다. 데이터 손실을 일으킬 수 있는 변환의 경우 소스 코드에 *캐스트*가 있어야 합니다.

자세한 내용은 [캐스팅 및 형식 변환](programming-guide/types/casting-and-type-conversions.md)을 참조하세요.

## <a name="built-in-types"></a>기본 제공 형식

C#에서는 정수, 부동 소수점 값, 부울 식, 텍스트 문자, 10진수 값 및 기타 데이터 형식을 표현하는 기본 제공 숫자 형식의 표준 집합을 제공합니다. 기본 제공 **string** 및 **object** 형식도 있습니다. 이러한 형식을 모든 C# 프로그램에서 사용할 수 있습니다. 기본 제공 형식에 대한 자세한 내용은 [기본 제공 형식에 대한 참조 테이블](language-reference/keywords/built-in-types-table.md)을 참조하세요.  
  
## <a name="custom-types"></a>사용자 지정 형식

[struct](language-reference/keywords/class.md), [class](language-reference/keywords/class.md), [interface](language-reference/keywords/interface.md) 및 [enum](language-reference/keywords/enum.md) 구문을 사용하여 자체 사용자 지정 형식을 만듭니다. .NET Framework 클래스 라이브러리 자체는 자체 애플리케이션에서 사용할 수 있는 Microsoft에서 제공되는 사용자 지정 형식의 컬렉션입니다. 기본적으로 클래스 라이브러리의 가장 자주 사용되는 형식을 모든 C# 프로그램에서 사용할 수 있습니다. 기타 형식은 정의되어 있는 어셈블리에 대한 프로젝트 참조를 명시적으로 추가할 경우에만 사용할 수 있습니다. 컴파일러에 어셈블리에 대한 참조가 포함된 후에는 소스 코드에서 해당 어셈블리에 선언된 형식의 변수(및 상수)를 선언할 수 있습니다.
  
## <a name="generic-types"></a>제네릭 형식

클라이언트 코드가 형식의 인스턴스를 만들 때 제공하는 실제 형식(*구체적 형식*)에 대한 자리 표시자로 사용되는 하나 이상의 *형식 매개 변수*를 사용하여 형식을 선언할 수 있습니다. 해당 형식을 *제네릭 형식*이라고 합니다. 예를 들어 .NET Framework 형식 <xref:System.Collections.Generic.List%601>에는 변환을 통해 이름 *T*가 제공되는 하나의 형식 매개 변수가 있습니다. 형식의 인스턴스를 만들 때 목록에 포함될 개체의 형식(예: 문자열)을 지정합니다.  
  
[!code-csharp[Generic types](../../samples/snippets/csharp/concepts/basic-types/generic-type.cs)]
  
형식 매개 변수를 사용하면 각 요소를 [개체](language-reference/keywords/object.md)로 변환할 필요 없이 같은 클래스를 재사용하여 요소 형식을 포함할 수 있습니다. 컴파일러는 컬렉션 요소의 특정 형식을 인식하며, 예를 들어 이전 예제에서 `strings` 개체에 정수를 추가하려는 경우 컴파일 시간에 오류를 발생시킬 수 있기 때문에 제네릭 컬렉션 클래스를 *강력한 형식의 컬렉션*이라고 합니다. 자세한 내용은 [제네릭](programming-guide/generics/index.md)을 참조하세요.

## <a name="implicit-types-anonymous-types-and-tuple-types"></a>암시적 형식, 무명 형식 및 튜플 형식

앞에서 설명한 대로 [var](language-reference/keywords/var.md) 키워드를 사용하여 클래스 멤버가 아닌 지역 변수를 암시적으로 형식화할 수 있습니다. 이 변수는 컴파일 시간에 형식을 받지만 형식은 컴파일러에서 제공됩니다. 자세한 내용은 [암시적으로 형식화된 지역 변수](programming-guide/classes-and-structs/implicitly-typed-local-variables.md)를 참조하세요.  
  
경우에 따라 저장하거나 메서드 경계 외부로 전달할 의도가 없는 관련 값의 단순 집합에 대한 명명된 형식을 만드는 것은 불편합니다. 이 목적으로는 *무명 형식*을 만들 수 있습니다. 자세한 내용은 [무명 형식](programming-guide/classes-and-structs/anonymous-types.md)을 참조하세요.

메서드에서 값을 두 개 이상 반환하려는 것이 일반적입니다. 단일 메서드 호출에서 여러 값을 반환하는 *튜플 형식*을 만들 수 있습니다. 자세한 내용은 [튜플](tuples.md)을 참조하세요.

## <a name="the-common-type-system"></a>공용 형식 시스템

.NET Framework의 형식 시스템에 대한 두 가지 기초 사항을 이해해야 합니다.  
  
- 형식 시스템은 상속 원칙을 지원합니다. 형식은 *기본 형식*이라는 다른 형식에서 파생될 수 있습니다. 파생 형식은 기본 형식의 메서드, 속성 및 기타 멤버를 상속합니다(몇 가지 제한 사항 있음). 기본 형식이 다른 형식에서 파생될 수도 있습니다. 이 경우 파생 형식은 상속 계층 구조에 있는 두 기본 형식의 멤버를 상속합니다. <xref:System.Int32> (C# 키워드: `int`)와 같은 기본 제공 숫자 형식을 포함한 모든 형식은 기본적으로 단일 기본 형식 <xref:System.Object> (C# 키워드: `object`)에서 파생됩니다. 이 통합 형식 계층 구조를 CTS([공용 형식 시스템](../standard/common-type-system.md))라고 합니다. C#의 상속에 대한 자세한 내용은 [상속](programming-guide/classes-and-structs/inheritance.md)을 참조하세요.  
  
- CTS의 각 형식은 *값 형식* 또는 *참조 형식*으로 정의됩니다. 여기에는 .NET Framework 클래스 라이브러리의 모든 사용자 지정 형식과 자체 사용자 지정 형식도 포함됩니다. [struct](language-reference/keywords/struct.md)를 사용하여 정의한 형식은 값 형식이고, 모든 기본 제공 숫자 형식은 **구조체**입니다. 값 형식에 대한 자세한 내용은 [구조체](structs.md)를 참조하세요. [class](language-reference/keywords/class.md) 키워드를 사용하여 정의한 형식은 참조 형식입니다. 참조 형식에 대한 자세한 내용은 [클래스](classes.md)를 참조하세요. 참조 형식과 값 형식의 컴파일 시간 규칙 및 런타임 동작은 서로 다릅니다.

## <a name="see-also"></a>참고 항목

- [구조체](structs.md)
- [클래스](classes.md)
