---
title: '방법: 웹 사용자에게 지역화된 날짜 및 시간 정보 표시'
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- formatting [.NET Framework], dates
- parsing strings [.NET Framework], date and time strings
- localization [.NET Framework], date and time displays
- formatting [.NET Framework], localized data
- displaying date and time data
- localized date displays [.NET Framework]
ms.assetid: 377fe93c-32be-421a-a30a-be639a46ede8
dev_langs:
- csharp
- vb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4c50cdf93d8cfcefeffd35290d26dfa432a241e1
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65882483"
---
# <a name="how-to-display-localized-date-and-time-information-to-web-users"></a>방법: 웹 사용자에게 지역화된 날짜 및 시간 정보 표시
웹 페이지는 전 세계 어디에서든 표시될 수 있으므로 날짜 및 시간 값의 구문 분석 및 서식 지정 작업은 사용자와 상호 작용할 때 기본 형식(대체로 웹 서버의 현지 문화권 형식임)을 사용해서는 안 됩니다. 대신 사용자가 입력한 날짜 및 시간 문자열을 처리하는 Web Forms는 사용자의 기본 설정 문화권을 사용하여 문자열을 구문 분석해야 합니다. 마찬가지로 날짜 및 시간 데이터는 사용자의 문화권을 따르는 형식으로 사용자에게 표시되어야 합니다. 이 항목에서는 프로젝션의 형식을 제어하는 방법을 보여 줍니다.  
  
## <a name="to-parse-date-and-time-strings-input-by-the-user"></a>사용자가 입력한 날짜 및 시간 문자열을 구문 분석하려면  
  
1. <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 속성에서 반환한 문자열 배열이 채워졌는지 여부를 파악합니다. 배열이 채워져 있지 않으면 6단계를 진행합니다.  
  
2. <xref:System.Web.HttpRequest.UserLanguages%2A> 속성에서 반환한 문자열 배열이 채워져 있는 경우 첫 번째 요소를 검색합니다. 첫 번째 요소는 사용자의 기본 설정 언어 및 지역을 나타냅니다.  
  
3. <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=nameWithType> 생성자를 호출하여 사용자의 기본 설정 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 개체를 인스턴스화합니다.  
  
4. <xref:System.DateTime> 또는 <xref:System.DateTimeOffset> 형식의 `TryParse` 또는 `Parse` 메서드를 호출하여 변환을 시도합니다. `TryParse` 또는 `Parse` 메서드의 오버로드를 `provider` 매개 변수와 함께 사용하고, 다음 중 하나를 전달합니다.  
  
    - 3단계에서 생성한 <xref:System.Globalization.CultureInfo> 개체  
  
    - 3단계에서 생성한 <xref:System.Globalization.CultureInfo> 개체의 <xref:System.Globalization.CultureInfo.DateTimeFormat%2A> 속성에서 반환하는 <xref:System.Globalization.DateTimeFormatInfo> 개체  
  
5. 변환에 실패하는 경우 <xref:System.Web.HttpRequest.UserLanguages%2A> 속성에서 반환한 문자열 배열의 나머지 요소 각각에 대해 2~4단계를 반복합니다.  
  
6. 여전히 변환에 실패하거나 <xref:System.Web.HttpRequest.UserLanguages%2A> 속성에서 반환한 문자열 배열이 비어 있는 경우 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 속성에서 반환하는 고정 문화권을 사용하여 문자열을 구문 분석합니다.  
  
## <a name="to-parse-the-local-date-and-time-of-the-users-request"></a>사용자 요청의 로컬 날짜 및 시간을 구문 분석하려면  
  
1. 웹 폼에 <xref:System.Web.UI.WebControls.HiddenField> 컨트롤을 추가합니다.  
  
2. 현재 날짜 및 시간과 로컬 표준 시간대 오프셋을 UTC(협정 세계시)에서 <xref:System.Web.UI.WebControls.HiddenField.Value%2A> 속성으로 작성하여 `Submit` 단추의 `onClick` 이벤트를 처리하는 JavaScript 함수를 만듭니다. 구분 기호(예: 세미콜론)를 사용하여 문자열의 두 구성 요소를 구분합니다.  
  
3. 스크립트의 텍스트를 <xref:System.Web.UI.ClientScriptManager.RegisterClientScriptBlock%28System.Type%2CSystem.String%2CSystem.String%2CSystem.Boolean%29?displayProperty=nameWithType> 메서드에 전달하여 웹 폼의 <xref:System.Web.UI.Control.PreRender> 이벤트를 사용해 HTML 출력 스트림에 함수를 삽입합니다.  
  
4. `Submit` 단추의 `OnClientClick` 특성에 JavaScript 함수의 이름을 제공하여 이벤트 처리기를 `Submit` 단추의 `onClick` 이벤트에 연결합니다.  
  
5. `Submit` 단추의 <xref:System.Web.UI.WebControls.Button.Click> 이벤트에 대한 처리기를 만듭니다.  
  
6. 이벤트 처리기에서, <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 속성으로 반환된 문자열 배열이 채워졌는지 여부를 파악합니다. 문자열 배열이 채워져 있지 않으면 14단계로 진행합니다.  
  
7. <xref:System.Web.HttpRequest.UserLanguages%2A> 속성에서 반환한 문자열 배열이 채워져 있는 경우 첫 번째 요소를 검색합니다. 첫 번째 요소는 사용자의 기본 설정 언어 및 지역을 나타냅니다.  
  
8. <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=nameWithType> 생성자를 호출하여 사용자의 기본 설정 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 개체를 인스턴스화합니다.  
  
9. <xref:System.Web.UI.WebControls.HiddenField.Value%2A> 속성에 할당된 문자열을 <xref:System.String.Split%2A> 메서드에 전달하여 사용자 로컬 날짜 및 시간의 문자열 표현과 사용자 로컬 표준 시간대 오프셋의 문자열 표현을 별도의 배열 요소에 저장합니다.  
  
10. <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> 또는 <xref:System.DateTime.TryParse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%2CSystem.DateTime%40%29?displayProperty=nameWithType> 메서드를 호출하여 사용자 요청의 날짜 및 시간을 <xref:System.DateTime> 값으로 변환합니다. 메서드의 오버로드를 `provider` 매개 변수와 함께 사용하고, 다음 중 하나를 전달합니다.  
  
    - 8단계에서 생성한 <xref:System.Globalization.CultureInfo> 개체  
  
    - 8단계에서 생성한 <xref:System.Globalization.CultureInfo> 개체의 <xref:System.Globalization.CultureInfo.DateTimeFormat%2A> 속성에서 반환하는 <xref:System.Globalization.DateTimeFormatInfo> 개체  
  
11. 10단계의 구문 분석 작업이 실패하는 경우 13단계로 이동합니다. 구문 분석에 성공한 경우 <xref:System.UInt32.Parse%28System.String%29?displayProperty=nameWithType> 메서드를 호출하여 사용자 표준 시간대 오프셋의 문자열 표현을 정수로 변환합니다.  
  
12. <xref:System.DateTimeOffset.%23ctor%28System.DateTime%2CSystem.TimeSpan%29?displayProperty=nameWithType> 생성자를 호출하여 사용자의 로컬 시간을 나타내는 <xref:System.DateTimeOffset>을 인스턴스화합니다.  
  
13. 10단계의 변환에 실패하는 경우 <xref:System.Web.HttpRequest.UserLanguages%2A> 속성에서 반환한 문자열 배열의 나머지 요소 각각에 대해 7~12단계를 반복합니다.  
  
14. 여전히 변환에 실패하거나 <xref:System.Web.HttpRequest.UserLanguages%2A> 속성에서 반환한 문자열 배열이 비어 있는 경우 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 속성에서 반환하는 고정 문화권을 사용하여 문자열을 구문 분석합니다. 그런 다음, 7~12단계를 반복합니다.  
  
 결과는 웹 페이지의 사용자 로컬 시간을 나타내는 <xref:System.DateTimeOffset> 개체입니다. 그러면 <xref:System.DateTimeOffset.ToUniversalTime%2A> 메서드를 호출하여 해당 UTC를 확인할 수 있습니다. 또한 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> 메서드를 호출해 시간을 변환할 표준 시간대로 <xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> 값을 전달하여 웹 서버의 해당 날짜 및 시간도 확인할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에는 HTML 소스와 사용자에게 날짜 및 시간 값을 입력하도록 요청하는 ASP.NET Web Forms의 코드가 모두 들어 있습니다. 또한 클라이언트 쪽 스크립트는 사용자 요청의 로컬 날짜 및 시간과 사용자 표준 시간대의 오프셋에 대한 정보를 UTC에서 숨겨진 필드로 작성합니다. 그러면 사용자 입력을 표시하는 웹 페이지를 반환하는 서버가 이 정보를 구문 분석합니다. 또한 사용자의 로컬 시간, 서버의 시간 및 UTC를 사용하여 사용자 요청의 날짜 및 시간을 표시합니다.  
  
 [!code-aspx-csharp[Formatting.HowTo.ParseDateInput#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.ParseDateInput/cs/GetDateInfo.aspx#1)]
 [!code-aspx-vb[Formatting.HowTo.ParseDateInput#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.ParseDateInput/vb/GetDateInfo.aspx#1)]
  
 클라이언트 쪽 스크립트는 JavaScript `toLocaleString` 메서드를 호출합니다. 이에 따라 사용자 로캘의 서식 지정 규칙을 따르는 문자열이 생성되며, 이렇게 하면 서버에서 성공적으로 구문 분석될 가능성이 큽니다.  
  
 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 속성은 HTTP 요청에 포함된 `Accept-Language` 헤더에 들어 있는 문화권 이름으로 채워집니다. 그러나 모든 브라우저가 해당 요청에 `Accept-Language` 헤더를 포함하는 것은 아니며, 사용자가 헤더를 완전히 숨길 수도 있습니다. 따라서 사용자 입력을 구문 분석할 때 대체 문화권을 갖는 것이 중요합니다. 일반적으로 대체 문화권은 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>에서 반환한 고정 문화권입니다. 또한 사용자가 텍스트 상자에 입력한 문화권 이름을 Internet Explorer에 제공할 수도 있으며, 이 경우 문화권 이름이 유효하지 않을 수도 있습니다. 따라서 <xref:System.Globalization.CultureInfo> 개체를 인스턴스화할 때 예외 처리를 사용하는 것이 중요합니다.  
  
 Internet Explorer에서 제출한 HTTP 요청에서 검색할 때 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 배열은 사용자 기본 설정 순서대로 채워집니다. 배열의 첫 번째 요소에는 사용자의 기본 문화권/지역 이름이 포함됩니다. 배열에 추가 항목이 포함되어 있는 경우 Internet Explorer는 문화권 이름과 세미콜론으로 구분되는 품질 지정자를 해당 항목에 임의로 할당합니다. 예를 들어 fr-FR 문화권에 대한 항목은 `fr-FR;q=0.7` 형식을 사용할 수 있습니다.  
  
 이 예제는 `useUserOverride` 매개 변수가 `false`로 설정된 <xref:System.Globalization.CultureInfo.%23ctor%2A> 생성자를 호출하여 새 <xref:System.Globalization.CultureInfo> 개체를 만듭니다. 이렇게 하면 문화권 이름이 서버의 기본 문화권 이름인 경우 클래스 생성자가 만든 새 <xref:System.Globalization.CultureInfo> 개체는 문화권의 기본 설정을 포함하며 서버의 **국가 및 언어 옵션** 애플리케이션을 사용하여 재정의된 설정을 반영하지 않습니다. 서버에서 재정의된 설정의 값이 사용자 시스템에 존재하거나 사용자 입력에 반영될 가능성은 거의 없습니다.  
  
 이 예제는 날짜 및 시간의 두 문자열 표현(사용자가 입력한 문자열과 숨겨진 필드에 저장된 문자열)을 구문 분석하므로 사전에 필요할 가능성이 있는 <xref:System.Globalization.CultureInfo> 개체를 정의합니다. 그리고 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=nameWithType> 속성에서 반환한 요소 수보다 하나 더 많은 <xref:System.Globalization.CultureInfo> 개체의 배열을 만듭니다. 그런 다음, 각 언어/지역 문자열에 대한 <xref:System.Globalization.CultureInfo> 개체를 인스턴스화하고, <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>를 나타내는 <xref:System.Globalization.CultureInfo> 개체도 인스턴스화합니다.  
  
 코드는 <xref:System.DateTime.Parse%2A> 또는 <xref:System.DateTime.TryParse%2A> 메서드를 호출하여 날짜 및 시간의 사용자 문자열 표현을 <xref:System.DateTime> 값으로 변환할 수 있습니다. 단일 구문 분석 작업을 수행하는 데 parse 메서드에 대한 반복적인 호출이 필요할 수 있습니다. 따라서 구문 분석 작업에 실패하는 경우 `false`가 반환되므로 <xref:System.DateTime.TryParse%2A> 메서드가 더 좋습니다. 반면에, <xref:System.DateTime.Parse%2A> 메서드에서 throw할 수 있는 반복적인 예외를 처리하는 것은 웹 애플리케이션에서 매우 비용이 많이 드는 제안일 수 있습니다.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 코드를 컴파일하려면 코드 숨김을 사용하지 않고 ASP.NET 웹 페이지를 만듭니다. 그런 다음, 예제를 웹 페이지에 복사하여 기존의 모든 코드를 대체합니다. ASP.NET 웹 페이지에는 다음과 같은 컨트롤이 있어야 합니다.  
  
- 코드에서 참조되지 않는 <xref:System.Web.UI.WebControls.Label> 컨트롤. 해당 <xref:System.Web.UI.WebControls.TextBox.Text%2A> 속성을 “Enter a Number:”로 설정합니다.  
  
- `DateString`이라는 <xref:System.Web.UI.WebControls.TextBox> 컨트롤  
  
- `OKButton`이라는 <xref:System.Web.UI.WebControls.Button> 컨트롤 해당 <xref:System.Web.UI.WebControls.Button.Text%2A> 속성을 “OK”로 설정합니다.  
  
- `DateInfo`이라는 <xref:System.Web.UI.WebControls.HiddenField> 컨트롤  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 사용자가 HTML 스트림에 스크립트를 삽입하지 못하게 하려면 서버 응답에서 사용자 입력을 곧바로 다시 에코해서는 안 됩니다. 대신 <xref:System.Web.HttpServerUtility.HtmlEncode%2A?displayProperty=nameWithType> 메서드를 사용하여 인코딩해야 합니다.  
  
## <a name="see-also"></a>참고 항목

- [서식 지정 작업 수행](../../../docs/standard/base-types/performing-formatting-operations.md)
- [표준 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)
- [사용자 지정 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)
- [날짜 및 시간 문자열 구문 분석](../../../docs/standard/base-types/parsing-datetime.md)
