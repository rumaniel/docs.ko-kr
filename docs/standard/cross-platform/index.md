---
title: .NET Framework로 여러 플랫폼 개발
ms.date: 07/18/2018
ms.technology: dotnet-standard
ms.assetid: b153baaa-130c-4169-860b-e580591de91e
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c2167f74c5d1dd9f49995b6407e65feb474084dc
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65641435"
---
# <a name="developing-for-multiple-platforms-with-the-net-framework"></a>.NET Framework로 여러 플랫폼 개발

.NET Framework 및 Visual Studio를 사용하여 Microsoft 플랫폼과 Microsoft 이외의 플랫폼 둘 모두에서 사용할 수 있는 앱을 개발할 수 있습니다.
  
## <a name="options-for-cross-platform-development"></a>플랫폼 간 개발 옵션

[!INCLUDE[standard](../../../includes/pcl-to-standard.md)]
  
 여러 플랫폼용으로 개발하기 위해 소스 코드 또는 바이너리를 공유하고 .NET Framework 코드와 Windows 런타임 API 간에 호출할 수 있습니다.  
  
|다음을 원하는 경우...|다음을 사용...|  
|-----------------------|------------|  
|Windows Phone 8.1과 Windows 8.1 앱 간에 소스 코드 공유|**공유 프로젝트** (Visual Studio 2013 업데이트 2의에서 유니버설 앱 템플릿).<br /><br /> -현재 Visual Basic 지원이 없습니다.<br />#을 사용 하 여 플랫폼별 코드를 구분할 수-`if` 문입니다.<br /><br /> 자세한 내용은 다음 문서를 참조하세요.<br /><br /> -   [코딩 시작](/windows/uwp/get-started/create-uwp-apps)<br />-   [Visual Studio를 사용 하 여 유니버설 XAML 앱을 빌드할](https://devblogs.microsoft.com/visualstudio/using-visual-studio-to-build-universal-xaml-apps/) (블로그 게시물)<br />-   [Visual Studio의 XAML 수렴 형 앱 빌드를 사용 하 여](https://channel9.msdn.com/Events/Build/2014/3-591) (비디오)|  
|여러 플랫폼을 대상으로 하는 앱 간에 바이너리 공유|**이식 가능한 클래스 라이브러리 프로젝트** 플랫폼 제약 없는 코드에 대 한 합니다.<br /><br /> -이 방법은 비즈니스 논리를 구현 하는 코드에 대 한 일반적으로 사용 됩니다.<br />-Visual Basic 또는 C#을 사용할 수 있습니다.<br />API 지원은 플랫폼별으로 다릅니다.<br />-Windows 8.1 및 Windows Phone 8.1을 대상으로 하는 이식 가능한 클래스 라이브러리 프로젝트는 Windows 런타임 Api 및 XAML을 지원 합니다. 이러한 기능은 이식 가능한 클래스 라이브러리의 이전 버전에서는 사용할 수 없습니다.<br />-필요한 경우 인터페이스 또는 추상 클래스를 사용 하 여 플랫폼별 코드를 추출할 수 있습니다.<br /><br /> 자세한 내용은 다음 문서를 참조하세요.<br /><br /> -   [이식 가능한 클래스 라이브러리](cross-platform-development-with-the-portable-class-library.md)<br />-   [이식 가능한 클래스 라이브러리가 작동 확인 방법](https://blogs.msdn.microsoft.com/dsplaisted/2012/08/27/how-to-make-portable-class-libraries-work-for-you/) (블로그 게시물)<br />-   [MVVM과 함께 이식 가능한 클래스 라이브러리 사용](using-portable-class-library-with-model-view-view-model.md) <br />-   [여러 플랫폼을 대상으로 하는 라이브러리의 앱 리소스](app-resources-for-libraries-that-target-multiple-platforms.md) <br />-   [.NET 이식성 분석기](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) (Visual Studio 확장명)|  
|Windows 8.1 및 Windows Phone 8.1 이외 플랫폼용 앱 간에 소스 코드 공유|**링크로 추가** 기능입니다.<br /><br /> -이 방법은 어떤 이유로 두 앱 모두에 공통적으로 적용 되지만 식은 가능 하지 않은 앱 논리에 적합 합니다. 이 기능은 C# 또는 Visual Basic 코드에 사용할 수 있습니다.<br />     예를 들어, Windows Phone 8 및 Windows 8은 Windows 런타임 API를 공유하지만 이식 가능한 클래스 라이브러리는 이러한 플랫폼에 Windows 런타임을 지원하지 않습니다. `Add as link`를 사용하여 Windows Phone 8 앱과 Windows 8이 대상인 Windows 스토어 앱 간에 공통 Windows 런타임 코드를 공유할 수 있습니다.<br /><br /> 자세한 내용은 다음 문서를 참조하세요.<br /><br /> -   [링크로 추가 사용 하 여 코드 공유](https://docs.microsoft.com/previous-versions/windows/apps/jj714082(v=vs.105))<br />-   [방법: 프로젝트에 기존 항목 추가](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/9f4t9t92(v=vs.100))|  
|.NET Framework를 사용하여 Windows 스토어 앱 쓰기 또는 .NET Framework 코드에서 Windows 런타임 API 호출|**Windows 런타임 Api** .NET Framework C# 또는 Visual Basic 코드에서.NET Framework Windows 스토어 앱 만들기를 사용 합니다. 두 플랫폼 간의 API 차이점을 알고 있어야 합니다. 그러나 이러한 차이점을 처리하는 데 도움이 되는 클래스가 있습니다.<br /><br /> 자세한 내용은 다음 문서를 참조하세요.<br /><br /> -   [Windows 스토어 앱 및 Windows 런타임용.NET framework 지원](support-for-windows-store-apps-and-windows-runtime.md) <br />-   [Windows 런타임에 URI 전달](passing-a-uri-to-the-windows-runtime.md) <br />-   <xref:System.IO.WindowsRuntimeStreamExtensions><br />-    <xref:System.WindowsRuntimeSystemExtensions>|  
|Microsoft 이외의 플랫폼용 .NET Framework 앱 빌드|**이식 가능한 클래스 라이브러리 참조 어셈블리** .NET Framework 및 Xamarin과 같은 Visual Studio 확장 프로그램이 나 타사 도구입니다.<br /><br /> 자세한 내용은 다음 문서를 참조하세요.<br /><br /> -   [이식 가능한 클래스 라이브러리를 이제 모든 플랫폼에서 사용할 수 있습니다.](https://devblogs.microsoft.com/dotnet/portable-class-library-pcl-now-available-on-all-platforms/) (블로그 게시물)<br />-   [Xamarin 설명서](/xamarin)|  
|플랫폼 간 개발에 JavaScript 및 HTML 사용|**유니버설 앱 템플릿을** Visual Studio 2013 업데이트 2를 Windows 8.1 및 Windows Phone 8.1 용 Windows 런타임 Api에 대해 개발 합니다. 현재 플랫폼 간 앱을 개발하기 위해 .NET Framework API를 JavaScript 및 HTML과 함께 사용할 수 없습니다.<br /><br /> 자세한 내용은 다음 문서를 참조하세요.<br /><br /> -   [JavaScript 프로젝트 템플릿](https://docs.microsoft.com/previous-versions/windows/apps/hh758331%28v=win.10%29)<br />-   [Windows Phone는 JavaScript를 사용 하 여 Windows 런타임 앱에 이식](https://docs.microsoft.com/previous-versions/windows/apps/dn636144%28v=win.10%29)|
