---
title: '방법: 사용자 지정 숫자 형식 공급 기업 정의 및 사용'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- numeric format strings [.NET Framework]
- formatting [.NET Framework], numbers
- number formatting [.NET Framework]
- custom numeric format strings
- numbers [.NET Framework], custom numeric format strings
- displaying date and time data
- format providers [.NET Framework]
- custom format strings
ms.assetid: a281bfbf-6596-45ed-a2d6-3782d535ada2
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b3898caa90c695ae681c2d9b20abbba57a2a9f61
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65590476"
---
# <a name="how-to-define-and-use-custom-numeric-format-providers"></a>방법: 사용자 지정 숫자 형식 공급 기업 정의 및 사용
.NET Framework에서는 숫자 값의 문자열 표현을 광범위하게 제어할 수 있습니다. 숫자 값의 형식을 사용자 지정하기 위한 다음과 같은 기능을 지원합니다.  
  
- 숫자를 해당 문자열 표현으로 변환하기 위한 미리 정의된 형식 집합을 제공하는 표준 숫자 형식 문자열입니다. `format` 매개 변수가 있는 숫자 서식 지정 메서드(예: <xref:System.Decimal.ToString%28System.String%29?displayProperty=nameWithType>)와 함께 사용할 수 있습니다. 자세한 내용은 [표준 숫자 형식 문자열](../../../docs/standard/base-types/standard-numeric-format-strings.md)을 참조하세요.  
  
- 함께 결합되어 사용자 지정 숫자 형식 지정자를 정의할 수 있는 기호 집합을 제공하는 사용자 지정 숫자 형식 문자열입니다. 또한 `format` 매개 변수가 있는 숫자 서식 지정 메서드(예: <xref:System.Decimal.ToString%28System.String%29?displayProperty=nameWithType>)와 함께 사용할 수도 있습니다. 자세한 내용은 [사용자 지정 숫자 형식 문자열](../../../docs/standard/base-types/custom-numeric-format-strings.md)을 참조하세요.  
  
- 숫자 값의 문자열 표현을 표시하는 데 사용되는 기호 및 형식 패턴을 정의하는 사용자 지정 <xref:System.Globalization.CultureInfo> 또는 <xref:System.Globalization.NumberFormatInfo> 개체입니다. `provider` 매개 변수가 있는 숫자 서식 지정 메서드(예: <xref:System.Int32.ToString%2A>)와 함께 사용할 수 있습니다. 일반적으로 `provider` 매개 변수는 문화권별 서식 지정에 사용됩니다.  
  
 애플리케이션에서 형식이 지정된 계정 번호, ID 번호 또는 우편 번호를 표시해야 하는 경우와 같이 이 세 가지 방법이 부적절한 경우도 있습니다. .NET Framework에서는 <xref:System.Globalization.CultureInfo> 또는 <xref:System.Globalization.NumberFormatInfo> 개체가 아닌 서식 지정 개체를 정의하여 숫자 값의 서식 지정 방법을 결정할 수도 있습니다. 이 항목에서는 이러한 개체를 구현하기 위한 단계별 지침을 제공하고 전화 번호 형식을 지정하는 예제를 제공합니다.  
  
### <a name="to-define-a-custom-format-provider"></a>사용자 지정 형식 공급자를 정의하려면  
  
1. <xref:System.IFormatProvider> 및 <xref:System.ICustomFormatter> 인터페이스를 구현하는 클래스를 정의합니다.  
  
2. <xref:System.IFormatProvider.GetFormat%2A?displayProperty=nameWithType> 메서드를 구현합니다. <xref:System.IFormatProvider.GetFormat%2A>은 서식 지정 메서드(예: <xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> 메서드)가 실제로 사용자 지정 서식 지정을 수행하는 개체를 검색하기 위해 호출하는 콜백 메서드입니다. 일반적인 <xref:System.IFormatProvider.GetFormat%2A> 구현에서는 다음 작업을 수행합니다.  
  
    1. 메서드 매개 변수로 전달되는 <xref:System.Type> 개체가 <xref:System.ICustomFormatter> 인터페이스를 나타내는지 여부를 결정합니다.  
  
    2. 매개 변수가 <xref:System.ICustomFormatter> 인터페이스를 나타내지 않는 경우 <xref:System.IFormatProvider.GetFormat%2A>은 사용자 지정 서식 지정을 제공하는 <xref:System.ICustomFormatter> 인터페이스를 구현하는 개체를 반환합니다. 일반적으로 사용자 지정 형식 지정 개체 자체가 반환됩니다.  
  
    3. 매개 변수가 <xref:System.ICustomFormatter> 인터페이스를 나타내지 않는 경우 <xref:System.IFormatProvider.GetFormat%2A>은 `null`을 반환합니다.  
  
3. <xref:System.ICustomFormatter.Format%2A> 메서드를 구현합니다. 이 메서드는 <xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> 메서드에 의해 호출되며 숫자의 문자열 표현을 반환합니다. 일반적으로 메서드를 구현하는 과정은 다음과 같습니다.  
  
    1. 필요에 따라 `provider` 매개 변수를 검사하여 메서드가 서식 지정 서비스를 제공하기에 적합한지 확인합니다. <xref:System.IFormatProvider>와 <xref:System.ICustomFormatter>를 둘 다 구현하는 서식 지정 개체의 경우 `provider` 매개 변수가 현재 서식 지정 개체와 같은지 테스트해야 합니다.  
  
    2. 형식 지정 개체가 사용자 지정 형식 지정자를 지원해야 하는지 여부를 결정합니다. 예를 들어 "N" 형식 지정자는 미국 전화 번호가 NANP 형식으로, "I" 형식 지정자는 ITU-T 권장 E.123 형식으로 출력되어야 함을 나타낼 수 있습니다. 형식 지정자가 사용된 경우 메서드에서 특정 형식 지정자를 처리해야 합니다. 지정자는 `format` 매개 변수의 메서드에 전달됩니다. 지정자가 없는 경우 `format` 매개 변수의 값은 <xref:System.String.Empty?displayProperty=nameWithType>입니다.  
  
    3. 메서드에 `arg` 매개 변수로 전달된 숫자 값을 검색합니다. 문자열 표현으로 변환하는 데 필요한 조작을 수행합니다.  
  
    4. `arg` 매개 변수의 문자열 표현을 반환합니다.  
  
### <a name="to-use-a-custom-numeric-formatting-object"></a>사용자 지정 숫자 형식 지정 개체를 사용하려면  
  
1. 사용자 지정 형식 지정 클래스의 새 인스턴스를 만듭니다.  
  
2. <xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> 서식 지정 메서드를 호출하여 사용자 지정 서식 지정 개체, 형식 지정자(또는 지정자를 사용하지 않는 경우 <xref:System.String.Empty?displayProperty=nameWithType>) 및 서식을 지정할 숫자 값을 전달합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 미국 전화 번호를 나타내는 숫자를 NANP 또는 E.123 형식으로 변환하는 `TelephoneFormatter`라는 사용자 지정 숫자 형식 공급자를 정의합니다. 메서드는 두 가지 형식 지정자 "N"(NANP 형식 출력)과 "I"(국제 E.123 형식 출력)를 처리합니다.  
  
 [!code-csharp[Formatting.HowTo.NumericValue#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.NumericValue/cs/Telephone1.cs#1)]
 [!code-vb[Formatting.HowTo.NumericValue#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.NumericValue/vb/Telephone1.vb#1)]  
  
 사용자 지정 숫자 형식 공급자는 <xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> 메서드에서만 사용할 수 있습니다. <xref:System.IFormatProvider> 형식의 매개 변수가 있는 숫자 서식 지정 메서드의 다른 오버로드(예: `ToString`)는 모두 <xref:System.Globalization.NumberFormatInfo> 형식을 나타내는 <xref:System.Type> 개체를 <xref:System.IFormatProvider.GetFormat%2A?displayProperty=nameWithType> 구현에 전달합니다. 반환 시 메서드가 <xref:System.Globalization.NumberFormatInfo> 개체를 반환할 것으로 예상합니다. 반환하지 않을 경우 사용자 지정 숫자 형식 공급자는 무시되고 현재 문화권에 대한 <xref:System.Globalization.NumberFormatInfo> 개체가 대신 사용됩니다. 예제에서 `TelephoneFormatter.GetFormat` 메서드는 메서드 매개 변수를 검사하고 <xref:System.ICustomFormatter> 이외의 다른 형식을 나타내는 경우 `null`을 반환하여 숫자 서식 지정 메서드에 부적절하게 전달될 수 있는 가능성을 처리합니다.  
  
 사용자 지정 숫자 형식 공급자가 형식 지정자 집합을 지원하는 경우 <xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> 메서드 호출에 사용된 형식 항목에 형식 지정자가 제공되지 않은 경우의 기본 동작을 제공해야 합니다. 예제에서는 "N"이 기본 형식 지정자입니다. 이렇게 하면 명시적 형식 지정자를 제공하여 숫자를 형식이 지정된 전화 번호로 변환할 수 있습니다. 다음 예제에서는 이러한 메서드 호출을 보여 줍니다.  
  
 [!code-csharp[Formatting.HowTo.NumericValue#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.NumericValue/cs/Telephone1.cs#2)]
 [!code-vb[Formatting.HowTo.NumericValue#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.NumericValue/vb/Telephone1.vb#2)]  
  
 그러나 형식 지정자가 없는 경우에도 변환을 수행할 수 있습니다. 다음 예제에서는 이러한 메서드 호출을 보여 줍니다.  
  
 [!code-csharp[Formatting.HowTo.NumericValue#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.NumericValue/cs/Telephone1.cs#3)]
 [!code-vb[Formatting.HowTo.NumericValue#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.NumericValue/vb/Telephone1.vb#3)]  
  
 기본 형식 지정자가 정의되어 있지 않으면 .NET이 코드에서 지원하지 않는 서식 지정을 제공할 수 있도록 <xref:System.ICustomFormatter.Format%2A?displayProperty=nameWithType> 메서드 구현에 다음과 같은 코드를 포함해야 합니다.  
  
 [!code-csharp[System.ICustomFormatter.Format#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.ICustomFormatter.Format/cs/format.cs#1)]
 [!code-vb[System.ICustomFormatter.Format#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.ICustomFormatter.Format/vb/Format.vb#1)]  
  
 이 예제의 경우 <xref:System.ICustomFormatter.Format%2A?displayProperty=nameWithType>을 구현하는 메서드는 <xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> 메서드에 대한 콜백 메서드 역할을 하기 위한 것입니다. 따라서 이 메서드는 `formatProvider` 매개 변수를 검사하여 현재 `TelephoneFormatter` 개체에 대한 참조가 있는지 여부를 확인합니다. 그러나 코드에서 메서드를 직접 호출할 수도 있습니다. 이 경우 `formatProvider` 매개 변수를 사용하여 문화권별 서식 지정 정보를 제공하는 <xref:System.Globalization.CultureInfo> 또는 <xref:System.Globalization.NumberFormatInfo> 개체를 제공할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [서식 지정 작업 수행](../../../docs/standard/base-types/performing-formatting-operations.md)
