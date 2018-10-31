---
title: '방법: 사용자가 웹 컨트롤에 입력한 숫자를 숫자로 변환'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- numeric format strings [.NET Framework]
- formatting [.NET Framework], numbers
- number formatting [.NET Framework]
- parsing strings [.NET Framework], numeric strings
- converting numeric user input to number
- numbers [.NET Framework], converting numeric user input to number
ms.assetid: f27ddfb8-7479-4b79-8879-02a3bd8402d4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 663f9d88315f396b187cca874c930179f1dea523
ms.sourcegitcommit: fd8d4587cc26e53f0e27e230d6e27d828ef4306b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49349139"
---
# <a name="how-to-convert-numeric-user-input-in-web-controls-to-numbers"></a>방법: 사용자가 웹 컨트롤에 입력한 숫자를 숫자로 변환
전 세계 어디서든 웹 페이지를 표시할 수 있으므로 사용자가 거의 무제한의 형식으로 숫자 데이터를 <xref:System.Web.UI.WebControls.TextBox> 컨트롤에 입력할 수 있습니다. 따라서 웹 페이지 사용자의 로캘 및 문화권을 확인하는 것이 매우 중요합니다. 사용자 입력을 구문 분석할 때 사용자의 로캘 및 문화권에 의해 정의된 서식 지정 규칙을 적용할 수 있습니다.  
  
### <a name="to-convert-numeric-input-from-a-web-textbox-control-to-a-number"></a>웹 TextBox 컨트롤의 숫자 입력을 숫자로 변환하려면  
  
1.  <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 속성에서 반환한 문자열 배열이 채워졌는지 여부를 파악합니다. 배열이 채워져 있지 않으면 6단계를 진행합니다.  
  
2.  <xref:System.Web.HttpRequest.UserLanguages%2A> 속성에서 반환한 문자열 배열이 채워져 있는 경우 첫 번째 요소를 검색합니다. 첫 번째 요소는 사용자의 기본 설정 언어 및 지역을 나타냅니다.  
  
3.  <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=nameWithType> 생성자를 호출하여 사용자의 기본 설정 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 개체를 인스턴스화합니다.  
  
4.  사용자 입력을 변환하려는 숫자 형식의 `TryParse` 또는 `Parse` 메서드를 호출합니다. `TryParse` 또는 `Parse` 메서드의 오버로드를 `provider` 매개 변수와 함께 사용하고, 다음 중 하나를 전달합니다.  
  
    -   3단계에서 생성한 <xref:System.Globalization.CultureInfo> 개체  
  
    -   3단계에서 생성한 <xref:System.Globalization.CultureInfo> 개체의 <xref:System.Globalization.CultureInfo.NumberFormat%2A> 속성에서 반환하는 <xref:System.Globalization.NumberFormatInfo> 개체  
  
5.  변환에 실패하는 경우 <xref:System.Web.HttpRequest.UserLanguages%2A> 속성에서 반환한 문자열 배열의 나머지 요소 각각에 대해 2~4단계를 반복합니다.  
  
6.  여전히 변환에 실패하거나 <xref:System.Web.HttpRequest.UserLanguages%2A> 속성에서 반환한 문자열 배열이 비어 있는 경우 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 속성에서 반환하는 고정 문화권을 사용하여 문자열을 구문 분석합니다.  
  
## <a name="example"></a>예  
 다음 예제는 사용자에게 <xref:System.Web.UI.WebControls.TextBox> 컨트롤에 숫자 값을 입력하도록 요청하고 이 값을 숫자로 변환하는 웹 폼의 완벽한 코드 숨김 페이지입니다. 해당 숫자는 원래 입력과 동일한 서식 지정 규칙을 사용하여 double로 처리되고 표시됩니다.  
  
 [!code-csharp[Formatting.HowTo.ParseNumericInput#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.ParseNumericInput/cs/NumericUserInput1.aspx.cs#1)]
 [!code-vb[Formatting.HowTo.ParseNumericInput#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.ParseNumericInput/vb/NumericUserInput1.aspx.vb#1)]  
  
 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 속성은 HTTP 요청에 포함된 `Accept-Language` 헤더에 들어 있는 문화권 이름으로 채워집니다. 그러나 모든 브라우저가 해당 요청에 `Accept-Language` 헤더를 포함하는 것은 아니며, 사용자가 헤더를 완전히 숨길 수도 있습니다. 따라서 사용자 입력을 구문 분석할 때 대체 문화권을 갖는 것이 중요합니다. 일반적으로 대체 문화권은 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>에서 반환한 고정 문화권입니다. 또한 사용자가 텍스트 상자에 입력한 문화권 이름을 Internet Explorer에 제공할 수도 있으며, 이 경우 문화권 이름이 유효하지 않을 수도 있습니다. 따라서 <xref:System.Globalization.CultureInfo> 개체를 인스턴스화할 때 예외 처리를 사용하는 것이 중요합니다.  
  
 Internet Explorer에서 제출한 HTTP 요청에서 검색할 때 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 배열은 사용자 기본 설정 순서대로 채워집니다. 배열의 첫 번째 요소에는 사용자의 기본 문화권/지역 이름이 포함됩니다. 배열에 추가 항목이 포함되어 있는 경우 Internet Explorer는 문화권 이름과 세미콜론으로 구분되는 품질 지정자를 해당 항목에 임의로 할당합니다. 예를 들어 fr-FR 문화권에 대한 항목은 `fr-FR;q=0.7` 형식을 사용할 수 있습니다.  
  
 이 예제는 `useUserOverride` 매개 변수가 `false`로 설정된 <xref:System.Globalization.CultureInfo.%23ctor%2A> 생성자를 호출하여 새 <xref:System.Globalization.CultureInfo> 개체를 만듭니다. 이렇게 하면 문화권 이름이 서버의 기본 문화권 이름인 경우 클래스 생성자가 만든 새 <xref:System.Globalization.CultureInfo> 개체는 문화권의 기본 설정을 포함하며 서버의 **국가 및 언어 옵션** 응용 프로그램을 사용하여 재정의된 설정을 반영하지 않습니다. 서버에서 재정의된 설정의 값이 사용자 시스템에 존재하거나 사용자 입력에 반영될 가능성은 거의 없습니다.  
  
 코드는 사용자 입력이 변환될 숫자 형식의 `Parse` 또는 `TryParse` 메서드를 호출할 수 있습니다. 단일 구문 분석 작업을 수행하는 데 parse 메서드에 대한 반복적인 호출이 필요할 수 있습니다. 따라서 구문 분석 작업에 실패하는 경우 `false`가 반환되므로 `TryParse` 메서드가 더 좋습니다. 반면에, `Parse` 메서드에서 throw할 수 있는 반복적인 예외를 처리하는 것은 웹 응용 프로그램에서 매우 비용이 많이 드는 제안일 수 있습니다.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 코드를 컴파일하려면 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 코드 숨김 페이지로 코드를 복사하여 기존 코드를 모두 대체합니다. [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 웹 페이지에는 다음과 같은 컨트롤이 있어야 합니다.  
  
-   코드에서 참조되지 않는 <xref:System.Web.UI.WebControls.Label> 컨트롤. 해당 <xref:System.Web.UI.WebControls.TextBox.Text%2A> 속성을 “Enter a Number:”로 설정합니다.  
  
-   `NumericString`이라는 <xref:System.Web.UI.WebControls.TextBox> 컨트롤  
  
-   `OKButton`이라는 <xref:System.Web.UI.WebControls.Button> 컨트롤 해당 <xref:System.Web.UI.WebControls.Button.Text%2A> 속성을 “OK”로 설정합니다.  
  
 클래스 이름을 `NumericUserInput`에서 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 페이지에 있는 `Page` 지시문의 `Inherits` 특성으로 정의되는 클래스 이름으로 변경합니다. `NumericInput` 개체 참조의 이름을 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 페이지에 있는 `form` 태그의 `id` 특성으로 정의된 이름으로 변경합니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 사용자가 HTML 스트림에 스크립트를 삽입하지 못하게 하려면 서버 응답에서 사용자 입력을 곧바로 다시 에코해서는 안 됩니다. 대신 <xref:System.Web.HttpServerUtility.HtmlEncode%2A?displayProperty=nameWithType> 메서드를 사용하여 인코딩해야 합니다.  
  
## <a name="see-also"></a>참고 항목

- [서식 지정 작업 수행](../../../docs/standard/base-types/performing-formatting-operations.md)  
- [숫자 문자열 구문 분석](../../../docs/standard/base-types/parsing-numeric.md)
