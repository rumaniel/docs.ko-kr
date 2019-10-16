---
title: 지역화 대비 애플리케이션 개발을 위한 최선의 구현 방법
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- global applications, best practices
- world-ready applications, best practices
- globalization [.NET Framework], best practices
- international applications [.NET Framework], best practices
ms.assetid: f08169c7-aad8-4ec3-9a21-9ebd3b89986c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d96e223b85178c7f2784a523e5609057d1432488
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59310540"
---
# <a name="best-practices-for-developing-world-ready-applications"></a>지역화 대비 애플리케이션 개발을 위한 모범 사례

이 단원에서는 지역화 대비 애플리케이션을 개발할 때 따라야 할 최선의 구현 방법을 소개합니다.

## <a name="globalization-best-practices"></a>세계화 모범 사례

1. 애플리케이션에서 내부적으로 유니코드를 사용합니다.

2. <xref:System.Globalization> 네임스페이스에서 제공하는 문화권 인식 클래스를 사용하여 데이터를 조작하고 형식을 지정합니다.

    - 정렬할 때는 <xref:System.Globalization.SortKey> 클래스 및 <xref:System.Globalization.CompareInfo> 클래스를 사용합니다.

    - 문자열을 비교할 때는 <xref:System.Globalization.CompareInfo> 클래스를 사용합니다.

    - 날짜 및 시간 형식을 지정할 때는 <xref:System.Globalization.DateTimeFormatInfo> 클래스를 사용합니다.

    - 숫자 형식을 지정할 때는 <xref:System.Globalization.NumberFormatInfo> 클래스를 사용합니다.

    - 그레고리오력 및 그레고리오력이 아닌 달력을 사용하려면 <xref:System.Globalization.Calendar> 클래스 또는 특정 달력 구현 중 하나를 사용합니다.

3. <xref:System.Globalization.CultureInfo?displayProperty=nameWithType> 클래스에서 제공하는 문화권 속성 설정을 적절한 상황에서 사용합니다. 날짜 및 시간 또는 숫자 형식 지정과 같은 형식 지정 작업에는 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> 속성을 사용합니다. 리소스를 검색하려면 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> 속성을 사용합니다. `CurrentCulture` 및 `CurrentUICulture` 속성을 스레드별로 설정할 수 있습니다.

4. 애플리케이션에서 <xref:System.Text> 네임스페이스의 인코딩 클래스를 사용하여 다양한 인코딩 간에 데이터를 읽고 쓸 수 있도록 합니다. ASCII 데이터가 입력될 것으로 예상하지 말고, 사용자가 텍스트를 입력할 수 있는 모든 위치에 국제 문자가 제공될 것으로 가정합니다. 예를 들어, 애플리케이션에서는 서버 이름, 디렉터리, 파일 이름, 사용자 이름 및 URL에서 국제 문자를 사용할 수 있습니다.

5. <xref:System.Text.UTF8Encoding> 클래스를 사용할 때는 보안상의 이유로 이 클래스가 제공하는 오류 검색 기능을 사용합니다. 오류 검색 기능을 설정하려면 `throwOnInvalidBytes` 매개 변수를 사용하는 생성자를 사용하여 클래스의 인스턴스를 만들고 이 매개 변수의 값을 `true`로 설정합니다.

6. 가능하면 문자열을 일련의 개별 문자가 아니라 전체 문자열로 처리합니다. 이것은 하위 문자열을 검색하거나 정렬할 때 특히 중요합니다. 이를 통해 조합된 문자의 구문을 분석할 때 발생하는 문제를 방지할 수 있습니다. <xref:System.Globalization.StringInfo?displayProperty=nameWithType> 클래스를 사용하여 단일 문자가 아닌 텍스트 단위를 사용할 수도 있습니다.

7. <xref:System.Drawing> 네임스페이스에서 제공하는 클래스를 사용하여 텍스트를 표시합니다.

8. 운영 체제 간에 일관성을 유지하려면 사용자 설정에 따라 <xref:System.Globalization.CultureInfo>가 재정의되지 않게 합니다. `CultureInfo` 매개 변수를 사용하는 `useUserOverride` 생성자를 사용하여 `false`로 설정합니다.

9. 국제 데이터를 사용하여 국제 운영 체제 버전에서 애플리케이션의 기능을 테스트합니다.

10. 문자열 비교 또는 대/소문자 변경 작업의 결과에 따라 보안을 결정하는 경우 문화권을 구분하지 않는 문자열 작업을 사용합니다. 이러한 구현 방법을 사용하면 결과가 `CultureInfo.CurrentCulture` 값의 영향을 받지 않습니다. 문화권을 구분하지 않는 문자열 비교로 인해 어떻게 일관되지 않은 결과가 나타날 수 있는지를 보여주는 예제는 [문자열 사용에 대한 모범 사례](../../../docs/standard/base-types/best-practices-strings.md)의 ["현재 문화권을 사용하는 문자열 비교"](../../../docs/standard/base-types/best-practices-strings.md#string-comparisons-that-use-the-current-culture) 섹션을 참조하세요.

## <a name="localization-best-practices"></a>지역화 모범 사례

1. 지역화할 수 있는 모든 리소스를 별도의 리소스 전용 DLL로 이동합니다. 지역화 가능한 리소스에는 문자열, 오류 메시지, 대화 상자, 메뉴 및 포함된 개체 리소스 등과 같은 사용자 인터페이스 요소가 포함됩니다.

2. 문자열이나 사용자 인터페이스 리소스를 하드 코드하지 마십시오.

3. 지역화할 수 없는 리소스를 리소스 전용 DLL에 두지 마십시오. 변환기에 혼동을 초래할 수 있습니다.

4. 연결된 구에서 런타임에 작성된 복합 문자열을 사용하지 마십시오. 복합 문자열은 일부 언어에만 적용되는 영문법 순서를 가정하는 경우가 많으므로 지역화하기가 어렵습니다.

5. "Empty Folder"와 같이 문자열이 문자열 구성 요소의 문법적 역할에 따라 다르게 변환될 수 있는 애매한 구문은 피합니다. 예를 들어, "empty"는 동사나 형용사로 사용할 수 있으므로 이탈리아어나 프랑스어와 같은 언어에서는 다르게 번역될 수 있습니다.

6. 애플리케이션에서 텍스트가 들어 있는 이미지나 아이콘은 사용하지 않도록 합니다. 이러한 경우에는 지역화 비용이 많이 듭니다.

7. 사용자 인터페이스에서 문자열 길이를 확장할 수 있도록 충분한 공간을 둡니다. 일부 언어에서는 다른 언어와 비교하여 구에 50-75%의 공간이 더 필요합니다.

8. <xref:System.Resources.ResourceManager?displayProperty=nameWithType> 클래스를 사용하여 문화권에 따라 리소스를 검색합니다.

9. [Windows Forms 리소스 편집기(Winres.exe)](../../../docs/framework/tools/winres-exe-windows-forms-resource-editor.md)를 사용하여 지역화할 수 있도록 [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)를 사용하여 Windows Forms 대화 상자를 만듭니다. Windows Forms 대화 상자는 직접 코딩하지 마십시오.

10. 전문적인 지역화(번역) 작업을 준비합니다.

11. 리소스 만들기 및 지역화에 대한 자세한 설명을 보려면 [애플리케이션의 리소스](../../../docs/framework/resources/index.md)를 참조하세요.

## <a name="globalization-best-practices-for-aspnet-applications"></a>ASP.NET 애플리케이션에 대한 세계화 모범 사례

1. 애플리케이션에서 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A> 및 <xref:System.Globalization.CultureInfo.CurrentCulture%2A> 속성을 명시적으로 설정합니다. 기본값을 사용하지 마십시오.

2. ASP.NET 애플리케이션은 관리되는 애플리케이션이므로 다른 애플리케이션의 경우와 같은 클래스를 사용하여 문화권 관련 정보를 검색, 표시 및 조작할 수 있습니다.

3. ASP.NET에 다음 세 가지 인코딩을 지정할 수 있습니다.

    - requestEncoding은 클라이언트 브라우저에서 받은 인코딩을 지정합니다.

    - responseEncoding은 클라이언트 브라우저로 보낼 인코딩을 지정합니다. 대부분의 경우 이 인코딩은 requestEncoding에 지정된 것과 같아야 합니다.

    - fileEncoding은 aspx, .asmx 및 .asax 파일 구문 분석의 기본 인코딩을 지정합니다.

4. ASP.NET 애플리케이션의 다음 세 위치에서 requestEncoding, responseEncoding, fileEncoding, culture 및 uiCulture 특성의 값을 지정합니다.

    - Web.config 파일의 전역화 섹션에서. 이 파일은 ASP.NET 애플리케이션에 대해 외부 파일입니다. 자세한 내용은 [\<globalization> 요소](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/hy4kkhe0(v=vs.100))를 참조하세요.

    - 페이지 지시문에서. 애플리케이션이 페이지에 있는 경우 파일이 이미 읽혀진 것입니다. 따라서 너무 늦었으므로 fileEncoding 및 requestEncoding을 지정할 수 없습니다. uiCulture, Culture 및 responseEncoding만 페이지 지시문에 지정할 수 있습니다.

    - 프로그램 방식으로 애플리케이션 코드에서. 이 설정은 요청마다 다를 수 있습니다. 페이지 지시문의 경우와 마찬가지로 해당 애플리케이션 코드에 도달되면 이미 너무 늦었으므로 fileEncoding 및 requestEncoding을 지정할 수 없습니다. uiCulture, Culture 및 responseEncoding만 애플리케이션 코드에 지정할 수 있습니다.

5. uiCulture 값은 브라우저 허용 언어로 설정될 수 있습니다.

## <a name="see-also"></a>참고 항목

- [전역화 및 지역화](../../../docs/standard/globalization-localization/index.md)
- [데스크톱 앱의 리소스](../../../docs/framework/resources/index.md)
