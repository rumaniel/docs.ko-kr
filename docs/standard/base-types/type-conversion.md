---
title: .NET Framework의 형식 변환
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- widening conversions
- explicit conversions
- narrowing conversions
- type conversion, about type conversion
- type conversion
- converting types
- narrowing coercion
- Explicit operator
- IConvertible interface
- base types, converting
- op_Implicit method
- widening coercion
- op_Explicit method
- Convert class
- implicit conversions
- Implicit operator
- data types [.NET Framework], converting
ms.assetid: ba36154f-064c-47d3-9f05-72f93a7ca96d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a8fc6f59b7a295cb73489a644da80976345cb172
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922686"
---
# <a name="type-conversion-in-the-net-framework"></a>.NET Framework의 형식 변환
<a name="top"></a> 모든 값에는 연결된 형식이 있으며, 이러한 형식은 값에 할당되는 공간, 포함할 수 있는 값의 범위, 값을 통해 사용할 수 있는 멤버 등의 특성을 정의합니다. 대부분의 값들은 하나 이상의 형식으로 표현될 수 있습니다. 예를 들어, 4라는 값은 정수 값 또는 부동 소수점 값으로 표현될 수 있습니다. 형식 변환을 수행하면 이전 형식과 동일한 값을 가지는 새 형식이 만들어지지만, 원래 개체의 ID(또는 실제 값)가 항상 동일하게 유지되지는 않습니다.  
  
 .NET Framework는 다음과 같은 변환을 자동으로 지원합니다.  
  
- 파생 클래스에서 기본 클래스로 변환. 예를 들어, 클래스 또는 구조체 인스턴스가 <xref:System.Object> 인스턴스로 변환될 수 있다는 의미입니다.  이러한 변환에는 캐스팅 또는 변환 연산자가 필요하지 않습니다.  
  
- 기본 클래스에서 원본 파생 클래스로 다시 변환. C#에서는 이러한 변환에 캐스팅 연산자가 필요합니다. Visual Basic에서는 `Option Strict`가 on이면 `CType` 연산자가 필요합니다.  
  
- 인터페이스를 구현하는 형식에서 그 인터페이스를 나타내는 인터페이스 개체로 변환. 이러한 변환에는 캐스팅 또는 변환 연산자가 필요하지 않습니다.  
  
- 인터페이스 개체에서 그 인터페이스를 구현하는 원래 형식으로 다시 변환.  C#에서는 이러한 변환에 캐스팅 연산자가 필요합니다. Visual Basic에서는 `Option Strict`가 on이면 `CType` 연산자가 필요합니다.  
  
 이러한 자동 변환 외에 .NET Framework는 사용자 지정 형식 변환을 지원하는 몇 가지 기능을 제공합니다. 이러한 요구 사항은 다음과 같습니다.  
  
- 사용 가능한 형식 간 확대 변환을 정의하는 `Implicit` 연산자. 자세한 내용은 [암시적 연산자를 사용한 암시적 변환](#implicit_conversion_with_the_implicit_operator) 섹션을 참조하세요.  
  
- 사용 가능한 형식 간 축소 변환을 정의하는 `Explicit` 연산자. 자세한 내용은 [명시적 연산자를 사용한 명시적 변환](#explicit_conversion_with_the_explicit_operator) 섹션을 참조하세요.  
  
- 기본 .NET Framework 데이터 형식 각각에 대한 변환을 정의하는 <xref:System.IConvertible> 인터페이스. 자세한 내용은 [IConvertible 인터페이스](#the_iconvertible_interface) 섹션을 참조하세요.  
  
- <xref:System.Convert> 인터페이스의 메서드를 구현하는 메서드 집합을 제공하는 <xref:System.IConvertible> 클래스. 자세한 내용은 [Convert 클래스](#Convert) 섹션을 참조하세요.  
  
- 지정된 형식을 임의의 형식으로 변환하는 작업을 지원하도록 확장될 수 있는 기본 클래스인 <xref:System.ComponentModel.TypeConverter> 클래스. 자세한 내용은 [TypeConverter 클래스](#the_typeconverter_class) 섹션을 참조하세요.  
  
<a name="implicit_conversion_with_the_implicit_operator"></a>   
## <a name="implicit-conversion-with-the-implicit-operator"></a>암시적 연산자를 사용한 암시적 변환  
 확대 변환에는 대상 형식보다 제한적인 범위나 제한적인 멤버 목록이 있는 기존 형식의 값에서 새 값을 만드는 작업이 포함됩니다. 확대 변환을 수행하면 정밀도 손실은 발생할 수 있어도 데이터 손실은 발생할 수 없습니다. 데이터 손실이 발생할 수 없기 때문에 컴파일러에서 명시적 변환 메서드나 캐스팅 연산자를 사용할 필요 없이 변환을 암시적이나 투명하게 처리할 수 있습니다.  
  
> [!NOTE]
> 암시적 변환을 수행하는 코드에서 변환 메서드를 호출하거나 캐스팅 연산자를 사용할 수 있지만 암시적 변환을 지원하는 컴파일러에서는 이렇게 할 필요가 없습니다.  
  
 예를 들어, <xref:System.Decimal> 형식은 <xref:System.Byte>, <xref:System.Char>, <xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.SByte>, <xref:System.UInt16>, <xref:System.UInt32> 및 <xref:System.UInt64> 값에서의 암시적 변환을 지원합니다. 다음 예제에서는 값을 <xref:System.Decimal> 변수에 할당할 때의 이러한 암시적 변환을 보여 줍니다.  
  
 [!code-csharp[Conceptual.Conversion#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/implicit1.cs#1)]
 [!code-vb[Conceptual.Conversion#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/implicit1.vb#1)]  
  
 특정 언어 컴파일러에서 오버로드된 사용자 지정 연산자를 지원하는 경우 고유한 사용자 지정 형식에서 암시적 변환을 정의할 수도 있습니다. 다음 예제에서는 부호 및 크기 표현을 사용하는 `ByteWithSign`이라는 부호 있는 바이트 데이터 형식을 부분적으로 구현합니다. 이 예제에서는 <xref:System.Byte> 및 <xref:System.SByte> 값을 `ByteWithSign` 값으로 암시적으로 변환하는 작업을 지원합니다.  
  
 [!code-csharp[Conceptual.Conversion#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/implicit1.cs#2)]
 [!code-vb[Conceptual.Conversion#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/implicit1.vb#2)]  
  
 클라이언트 코드에서는 다음 예제와 같이 명시적 변환을 수행하거나 캐스팅 연산자를 사용하지 않고 `ByteWithSign` 변수를 선언하여 <xref:System.Byte> 및 <xref:System.SByte> 값에 할당할 수 있습니다.  
  
 [!code-csharp[Conceptual.Conversion#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/implicit1.cs#3)]
 [!code-vb[Conceptual.Conversion#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/implicit1.vb#3)]  
  
 [맨 위로 이동](#top)  
  
<a name="explicit_conversion_with_the_explicit_operator"></a>   
## <a name="explicit-conversion-with-the-explicit-operator"></a>명시적 연산자를 사용한 명시적 변환  
 축소 변환에는 대상 형식보다 큰 범위나 큰 멤버 목록이 있는 기존 형식의 값에서 새 값을 만드는 작업이 포함됩니다. 축소 변환을 수행하면 데이터 손실이 발생할 수 있기 때문에 컴파일러에서 변환 메서드 호출이나 캐스팅 연산자를 통해 명시적으로 변환을 수행하도록 요구하는 경우가 많습니다. 즉, 개발자 코드에서 변환이 명시적으로 처리되어야 합니다.  
  
> [!NOTE]
> 축소 변환에 변환 메서드나 캐스팅 연산자를 요구하는 주요 목적은 개발자가 데이터 손실이나 <xref:System.OverflowException>의 가능성을 인식하여 코드에서 처리할 수 있게 하는 것입니다. 그러나 일부 컴파일러에서는 이 요구 사항을 완화할 수 있습니다. 예를 들어, Visual Basic에서 `Option Strict`가 해제(기본 설정)되면 Visual Basic 컴파일러에서 축소 변환을 암시적으로 수행하려고 합니다.  
  
 예를 들어, 다음 표와 같이 <xref:System.UInt32>, <xref:System.Int64> 및 <xref:System.UInt64> 데이터 형식은 <xref:System.Int32> 데이터 형식을 초과하는 범위를 포함합니다.  
  
|형식|Int32 범위와 비교|  
|----------|------------------------------------|  
|<xref:System.Int64>|<xref:System.Int64.MaxValue?displayProperty=nameWithType>가 <xref:System.Int32.MaxValue?displayProperty=nameWithType>보다 크고 <xref:System.Int64.MinValue?displayProperty=nameWithType>가 <xref:System.Int32.MinValue?displayProperty=nameWithType>보다 작은 경우(보다 큰 음의 범위를 포함하는 경우)|  
|<xref:System.UInt32>|<xref:System.UInt32.MaxValue?displayProperty=nameWithType>가 <xref:System.Int32.MaxValue?displayProperty=nameWithType>보다 큰 경우|  
|<xref:System.UInt64>|<xref:System.UInt64.MaxValue?displayProperty=nameWithType>가 <xref:System.Int32.MaxValue?displayProperty=nameWithType>보다 큰 경우|  
  
 이러한 축소 변환을 처리하기 위해 .NET Framework에서는 형식에서 `Explicit` 연산자를 정의할 수 있게 합니다. 그러면 개별 언어 컴파일러에서 고유 구문을 사용하여 이 연산자를 구현할 수 있거나 변환을 수행하기 위해 <xref:System.Convert> 클래스의 멤버가 호출될 수 있습니다. (<xref:System.Convert> 클래스에 대한 자세한 내용은 이 항목의 뒷부분에서 [Convert 클래스](#Convert)를 참조하세요.) 다음 예제에서는 언어 기능을 사용하여 범위를 벗어날 수 있는 이러한 정수 값을 <xref:System.Int32> 값으로 명시적으로 변환하는 작업을 처리하는 방법을 보여줍니다.  
  
 [!code-csharp[Conceptual.Conversion#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/explicit1.cs#4)]
 [!code-vb[Conceptual.Conversion#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/explicit1.vb#4)]  
  
 명시적 변환의 결과는 언어마다 다를 수 있으며 해당 <xref:System.Convert> 메서드에서 반환하는 값에 따라서도 다를 수 있습니다. 예를 들어, <xref:System.Double> 값 12.63251이 <xref:System.Int32>로 변환되면 Visual Basic `CInt` 메서드와 .NET Framework <xref:System.Convert.ToInt32%28System.Double%29?displayProperty=nameWithType> 메서드는 <xref:System.Double>을 반올림하여 값 13을 반환하지만 C# `(int)` 연산자는 <xref:System.Double>을 잘라 값 12를 반환합니다. 마찬가지로 C# `(int)` 연산자는 부울을 정수로 변환하는 것을 지원하지만 Visual Basic `CInt` 메서드는 값 `true`를 -1로 변환합니다. 반면에 <xref:System.Convert.ToInt32%28System.Boolean%29?displayProperty=nameWithType> 메서드는 값 `true`를 1로 변환합니다.  
  
 대부분의 컴파일러에서는 검사 변환 방식이나 비검사 변환 방식으로 명시적 변환을 수행할 수 있습니다. 검사 변환을 수행하는 경우 변환할 형식의 값이 대상 형식의 범위를 벗어나면 <xref:System.OverflowException>이 throw됩니다. 같은 조건에서 비검사 변환을 수행하면 예외가 throw되지는 않지만 정확한 동작이 정의되지 않으며 잘못된 결과 값이 생성될 수 있습니다.  
  
> [!NOTE]
> C#에서 검사 변환을 수행하려면 캐스팅 연산자와 함께 `checked` 키워드를 사용하거나 `/checked+` 컴파일러 옵션을 지정합니다. 반대로 비검사 변환을 수행하려면 캐스팅 연산자와 함께 `unchecked` 키워드를 사용하거나 `/checked-` 컴파일러 옵션을 지정합니다. 기본적으로 명시적 변환은 검사되지 않습니다. Visual Basic에서 검사 변환을 수행하려면 프로젝트의 **고급 컴파일러 설정** 대화 상자에서 **정수 오버플로 검사 해제** 확인란의 선택을 취소하거나 `/removeintchecks-` 컴파일러 옵션을 지정합니다. 반대로 비검사 변환을 수행하려면 프로젝트의 **고급 컴파일러 설정** 대화 상자에서 **정수 오버플로 검사 해제** 확인란을 선택하거나 `/removeintchecks+` 컴파일러 옵션을 지정합니다. 기본적으로 명시적 변환은 검사됩니다.  
  
 다음 C# 예제에서는 `checked` 및 `unchecked` 키워드를 사용하여 <xref:System.Byte> 범위 밖에 있는 값을 <xref:System.Byte>로 변환할 때 동작이 어떻게 다른지 보여 줍니다. 검사 변환은 예외를 throw하지만 비검사 변환은 <xref:System.Byte.MaxValue?displayProperty=nameWithType>를 <xref:System.Byte> 변수에 할당합니다.  
  
 [!code-csharp[Conceptual.Conversion#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/explicit1.cs#12)]  
  
 특정 언어 컴파일러에서 오버로드된 사용자 지정 연산자를 지원하는 경우 고유한 사용자 지정 형식에서 명시적 변환을 정의할 수도 있습니다. 다음 예제에서는 부호 및 크기 표현을 사용하는 `ByteWithSign`이라는 부호 있는 바이트 데이터 형식을 부분적으로 구현합니다. 이 예제에서는 <xref:System.Int32> 및 <xref:System.UInt32> 값을 `ByteWithSign` 값으로 명시적으로 변환하는 작업을 지원합니다.  
  
 [!code-csharp[Conceptual.Conversion#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/explicit1.cs#5)]
 [!code-vb[Conceptual.Conversion#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/explicit1.vb#5)]  
  
 클라이언트 코드에서는 할당에 캐스팅 연산자나 변환 메서드가 포함된 경우 다음 예제와 같이 `ByteWithSign` 변수를 선언하여 <xref:System.Int32> 및 <xref:System.UInt32> 값에 할당할 수 있습니다.  
  
 [!code-csharp[Conceptual.Conversion#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/explicit1.cs#6)]
 [!code-vb[Conceptual.Conversion#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/explicit1.vb#6)]  
  
 [맨 위로 이동](#top)  
  
<a name="the_iconvertible_interface"></a>   
## <a name="the-iconvertible-interface"></a>IConvertible 인터페이스  
 형식을 공용 언어 런타임 기본 형식으로 변환하는 작업을 지원하기 위해 .NET Framework에서는 <xref:System.IConvertible> 인터페이스를 제공합니다. 구현하는 형식은 다음을 제공해야 합니다.  
  
- 구현하는 형식의 <xref:System.TypeCode>를 반환하는 메서드  
  
- 구현하는 형식을 각 공용 언어 런타임 기본 형식(<xref:System.Boolean>, <xref:System.Byte>, <xref:System.DateTime>, <xref:System.Decimal>, <xref:System.Double> 등)으로 변환하는 메서드  
  
- 구현하는 형식의 인스턴스를 다른 지정된 형식으로 변환하는 일반화된 변환 메서드. 지원되지 않는 변환은 <xref:System.InvalidCastException>을 throw해야 합니다.  
  
 각 공용 언어 런타임 기본 형식(즉, <xref:System.Boolean>, <xref:System.Byte>, <xref:System.Char>, <xref:System.DateTime>, <xref:System.Decimal>, <xref:System.Double>, <xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.SByte>, <xref:System.Single>, <xref:System.String>, <xref:System.UInt16>, <xref:System.UInt32> 및 <xref:System.UInt64>)과 <xref:System.DBNull> 및 <xref:System.Enum> 형식은 <xref:System.IConvertible> 인터페이스를 구현합니다. 그러나 이러한 구현은 명시적 인터페이스 구현입니다. 변환 메서드는 다음 예제와 같이 <xref:System.IConvertible> 인터페이스 변수를 통해서만 호출할 수 있습니다. 이 예제에서는 <xref:System.Int32> 값을 해당하는 <xref:System.Char> 값으로 변환합니다.  
  
 [!code-csharp[Conceptual.Conversion#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/iconvertible1.cs#7)]
 [!code-vb[Conceptual.Conversion#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/iconvertible1.vb#7)]  
  
 구현하는 형식이 아니라 인터페이스에 대해 변환 메서드를 호출해야 하기 때문에 명시적 인터페이스 구현 비용이 비교적 높아집니다. 따라서 공용 언어 런타임 기본 형식 간에 변환하려면 이 방법 대신 <xref:System.Convert> 클래스의 적절한 멤버를 호출하는 것이 좋습니다. 자세한 내용은 다음에 나오는 [Convert 클래스](#Convert) 섹션을 참조하세요.  
  
> [!NOTE]
> .NET Framework에서 제공하는 <xref:System.Convert> 클래스와 <xref:System.IConvertible> 인터페이스 외에도 개별 언어에서 변환을 수행하는 방법을 제공할 수 있습니다. 예를 들어, C#에서는 캐스팅 연산자가 사용되고, Visual Basic에서는 `CType`, `CInt` 및 `DirectCast` 등의 컴파일러 구현 변환 함수가 사용됩니다.  
  
 대부분의 경우 <xref:System.IConvertible> 인터페이스는 .NET Framework에서 기본 형식 간의 변환을 지원하도록 설계되었습니다. 그러나 사용자 지정 형식에서도 이 인터페이스를 구현하여 해당 사용자 지정 형식을 다른 사용자 지정 형식으로 변환하는 작업을 지원할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [ChangeType 메서드를 사용한 사용자 지정 변환](#ChangeType) 섹션을 참조하세요.  
  
 [맨 위로 이동](#top)  
  
<a name="Convert"></a>   
## <a name="the-convert-class"></a>Convert 클래스  
 각 기본 형식의 <xref:System.IConvertible> 인터페이스 구현을 호출하여 형식 변환을 수행할 수 있지만 <xref:System.Convert?displayProperty=nameWithType> 클래스의 메서드를 호출하는 것이 한 기본 형식에서 다른 형식으로 변환하는 데 권장되는 언어와 무관한 방법입니다. 또한 <xref:System.Convert.ChangeType%28System.Object%2CSystem.Type%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 메서드를 사용하여 지정된 사용자 지정 형식을 다른 형식으로 변환할 수 있습니다.  
  
### <a name="conversions-between-base-types"></a>기본 형식 간 변환  
 <xref:System.Convert> 클래스를 사용하여 언어와 무관하게 기본 형식 간의 변환을 수행할 수 있으므로 공용 언어 런타임을 대상으로 하는 모든 언어에서 이 클래스를 사용할 수 있습니다. 이 클래스는 확대 및 축소 변환을 위한 전체 메서드 집합을 제공하며 지원되지 않는 변환(<xref:System.InvalidCastException> 값을 정수 값으로 변환하는 등)의 경우 <xref:System.DateTime>을 throw합니다. 축소 변환은 checked 컨텍스트에서 수행되며 변환이 실패하는 경우 <xref:System.OverflowException>이 throw됩니다.  
  
> [!IMPORTANT]
> <xref:System.Convert> 클래스에 각 기본 형식으로 변환하거나 각 기본 형식에서 변환하는 메서드가 포함되어 있기 때문에 각 기본 형식의 <xref:System.IConvertible> 명시적 인터페이스 구현을 호출할 필요가 없습니다.  
  
 다음 예제에서는 <xref:System.Convert?displayProperty=nameWithType> 클래스를 사용하여 .NET Framework 기본 형식 간의 몇 가지 축소 및 확대 변환을 수행하는 방법을 보여 줍니다.  
  
 [!code-csharp[Conceptual.Conversion#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/convert1.cs#8)]
 [!code-vb[Conceptual.Conversion#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/convert1.vb#8)]  
  
 부동 소수점 값으로 변환하거나 부동 소수점 값에서 변환하는 등의 경우에는 변환을 수행할 때 <xref:System.OverflowException>이 throw되지 않아도 정밀도가 손실될 수 있습니다. 다음 예제에서는 이러한 정밀도 손실을 보여 줍니다. 첫 번째 경우에 <xref:System.Decimal> 값은 <xref:System.Double>로 변환될 때 정밀도가 낮아집니다(유효 자릿수가 적어짐). 두 번째 경우에 <xref:System.Double> 값은 변환을 완료하기 위해 42.72에서 43으로 반올림됩니다.  
  
 [!code-csharp[Conceptual.Conversion#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/convert1.cs#9)]
 [!code-vb[Conceptual.Conversion#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/convert1.vb#9)]  
  
 <xref:System.Convert> 클래스에서 지원하는 확대 및 축소 변환의 목록이 포함된 표는 [형식 변환표](../../../docs/standard/base-types/conversion-tables.md)를 참조하세요.  
  
<a name="ChangeType"></a>   
### <a name="custom-conversions-with-the-changetype-method"></a>ChangeType 메서드를 사용한 사용자 지정 변환  
 각 기본 형식에 대한 변환을 지원하는 것 외에도 <xref:System.Convert> 클래스를 사용하여 사용자 지정 형식을 하나 이상의 미리 정의된 형식으로 변환할 수 있습니다. 이 변환은 <xref:System.Convert.ChangeType%28System.Object%2CSystem.Type%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 메서드로 수행됩니다. 이 메서드는 <xref:System.IConvertible.ToType%2A?displayProperty=nameWithType> 매개 변수의 `value` 메서드에 대한 호출을 래핑합니다. 즉, `value` 매개 변수가 나타내는 개체가 <xref:System.IConvertible> 인터페이스의 구현을 제공해야 합니다.  
  
> [!NOTE]
> <xref:System.Convert.ChangeType%28System.Object%2CSystem.Type%29?displayProperty=nameWithType> 및 <xref:System.Convert.ChangeType%28System.Object%2CSystem.Type%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 메서드는 <xref:System.Type> 개체를 사용하여 `value`가 변환되는 대상 값을 지정하기 때문에, 이런 메서드를 사용하여 컴파일 타임에 형식을 알 수 없는 개체로 동적 변환을 수행할 수 있습니다. 하지만, <xref:System.IConvertible>의 `value` 구현에서는 이 변환을 계속 지원해야 합니다.  
  
 다음 예제에서는 <xref:System.IConvertible> 개체와 `TemperatureCelsius` 개체 간을 변환할 수 있게 하는 `TemperatureFahrenheit` 인터페이스의 가능한 구현을 보여 줍니다. 이 예제에서는 `Temperature` 인터페이스를 구현하고 <xref:System.IConvertible> 메서드를 재정의하는 기본 클래스 <xref:System.Object.ToString%2A?displayProperty=nameWithType>를 정의합니다. 파생된 `TemperatureCelsius` 및 `TemperatureFahrenheit` 클래스는 기본 클래스의 `ToType` 및 `ToString` 메서드를 각각 재정의합니다.  
  
 [!code-csharp[Conceptual.Conversion#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/iconvertible2.cs#10)]
 [!code-vb[Conceptual.Conversion#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/iconvertible2.vb#10)]  
  
 다음 예제에서는 이러한 <xref:System.IConvertible> 구현을 몇 번 호출하여 `TemperatureCelsius` 개체와 `TemperatureFahrenheit` 개체 간에 변환하는 방법을 보여 줍니다.  
  
 [!code-csharp[Conceptual.Conversion#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/iconvertible2.cs#11)]
 [!code-vb[Conceptual.Conversion#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/iconvertible2.vb#11)]  
  
 [맨 위로 이동](#top)  
  
<a name="the_typeconverter_class"></a>   
## <a name="the-typeconverter-class"></a>TypeConverter 클래스  
 .NET Framework에서는 <xref:System.ComponentModel.TypeConverter?displayProperty=nameWithType> 클래스를 확장하고 <xref:System.ComponentModel.TypeConverterAttribute?displayProperty=nameWithType> 특성을 통해 형식 변환기를 해당 형식과 연결하여 사용자 지정 형식에 대한 형식 변환기를 정의할 수 있습니다. 다음 표에는 이 방법과 사용자 지정 형식에 대한 <xref:System.IConvertible> 인터페이스를 구현하는 방법의 차이점이 나와 있습니다.  
  
> [!NOTE]
> 사용자 지정 형식에 대해 형식 변환기가 정의되어 있는 경우에만 사용자 지정 형식에 디자인 타임 지원이 제공될 수 있습니다.  
  
|TypeConverter를 사용한 변환|IConvertible를 사용한 변환|  
|------------------------------------|-----------------------------------|  
|<xref:System.ComponentModel.TypeConverter>에서 별도의 클래스를 파생시켜 사용자 지정 형식에 대해 구현됩니다. 이 파생 클래스는 <xref:System.ComponentModel.TypeConverterAttribute> 특성을 적용하여 사용자 지정 형식과 연결됩니다.|변환을 수행하기 위해 사용자 지정 형식에 의해 구현됩니다. 형식의 사용자가 해당 형식에 대해 <xref:System.IConvertible> 변환 메서드를 호출합니다.|  
|디자인 타임 및 런타임 모두에서 사용할 수 있습니다.|런타임에서만 사용할 수 있습니다.|  
|리플렉션을 사용합니다. 따라서 <xref:System.IConvertible>로 활성화된 변환보다 느립니다.|리플렉션을 사용하지 않습니다.|  
|사용자 지정 형식에서 다른 데이터 형식으로, 다른 데이터 형식에서 사용자 지정 형식으로의 양방향 형식 변환을 허용합니다. 예를 들어, <xref:System.ComponentModel.TypeConverter>에 대해 정의된 `MyType`를 사용하여 `MyType`에서 <xref:System.String>으로 변환하고 <xref:System.String>에서 `MyType`으로 변환할 수 있습니다.|사용자 지정 형식에서 다른 데이터 형식으로의 변환은 허용하지만, 다른 데이터 형식에서 사용자 지정 형식으로의 변환은 허용하지 않습니다.|  
  
 변환기를 사용하여 변환을 수행하는 방법에 대한 자세한 내용은 <xref:System.ComponentModel.TypeConverter?displayProperty=nameWithType>를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Convert?displayProperty=nameWithType>
- <xref:System.IConvertible>
- [형식 변환표](../../../docs/standard/base-types/conversion-tables.md)
