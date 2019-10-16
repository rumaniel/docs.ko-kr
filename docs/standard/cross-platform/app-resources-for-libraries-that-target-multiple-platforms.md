---
title: 여러 플랫폼을 대상으로 하는 라이브러리의 앱 리소스
ms.date: 07/18/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- multiple platforms, resources for
- resources [.NET Framework]
- .NET Framework, resources when targeting multiple platforms
- resources, for multiple platforms
- targeting multiple platforms, resources for
ms.assetid: 72c76f0b-7255-4576-9261-3587f949669c
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e846f45b55ac09d6ce6af4f3223c3bdba1dc83ba
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67506017"
---
# <a name="app-resources-for-libraries-that-target-multiple-platforms"></a>여러 플랫폼을 대상으로 하는 라이브러리의 앱 리소스
.NET Framework를 사용 하 여 [이식 가능한 클래스 라이브러리](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md) 프로젝트 형식에 여러 플랫폼에서 클래스 라이브러리의 리소스에에서 액세스할 수 있는지 확인 합니다. 이 프로젝트 형식은 Visual Studio 2012에서 사용할 수 및.NET Framework 클래스 라이브러리의 이식 가능한 하위 집합을 대상으로 합니다. 이식 가능한 클래스 라이브러리를 사용 하 여 데스크톱 앱, Silverlight 앱, Windows Phone 앱에서 라이브러리에 액세스할 수 있는지 확인 하 고 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱.

[!INCLUDE[standard](../../../includes/pcl-to-standard.md)]

 이식 가능한 클래스 라이브러리 프로젝트에서 형식의 매우 제한 된 하위 집합만 사용 하면 합니다 <xref:System.Resources> 응용 프로그램을 사용할 수 있는 네임 스페이스 사용 할 수는 <xref:System.Resources.ResourceManager> 리소스를 검색 하는 클래스입니다. 그러나 Visual Studio를 사용하여 응용 프로그램을 만들려면 <xref:System.Resources.ResourceManager> 클래스를 직접 사용하는 대신에 Visual Studio가 생성한 강력한 형식의 래퍼를 사용하여야 합니다.

 Visual Studio를 강력한 형식의 래퍼를 만들려면 주 리소스 파일의 설정 **액세스 한정자** Visual Studio 리소스 디자이너에서 **공용**합니다. 이를 통해 강력한 형식의 ResourceManager 래퍼를 포함하는 [resourceFileName].designer.cs 또는 [resourceFileName].designer.vb 파일을 만듭니다. 강력한 형식의 리소스 래퍼를 사용 하는 방법에 대 한 자세한 내용은의 "강력한 형식의 리소스 클래스 생성" 섹션을 참조 합니다 [Resgen.exe (리소스 파일 생성기)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md) 항목입니다.

## <a name="resource-manager-in-the-portable-class-library"></a>이식 가능한 클래스 라이브러리의 리소스 관리자
 이식 가능한 클래스 라이브러리 프로젝트에서 리소스에 대 한 모든 액세스에서 처리 되는 <xref:System.Resources.ResourceManager> 클래스입니다. 때문에 형식 합니다 <xref:System.Resources> 네임 스페이스와 같은 <xref:System.Resources.ResourceReader> 및 <xref:System.Resources.ResourceSet>는 액세스할 수 없는 이식 가능한 클래스 라이브러리 프로젝트에서 사용할 수 없습니다 리소스에 액세스할 수 합니다.

 이식 가능한 클래스 라이브러리 프로젝트에 네 가지 <xref:System.Resources.ResourceManager> 다음 표에 나열 된 멤버입니다. 이러한 생성자와 메서드를 사용하여 <xref:System.Resources.ResourceManager> 개체를 인스턴스화하고 문자열 리소스를 검색할 수 있습니다.

|`ResourceManager` 멤버|설명|
|------------------------------|-----------------|
|<xref:System.Resources.ResourceManager.%23ctor%28System.String%2CSystem.Reflection.Assembly%29>|<xref:System.Resources.ResourceManager> 인스턴스를 만들어 지정한 어셈블리에서 발견되는 명명된 리소스 파일에 액세스합니다.|
|<xref:System.Resources.ResourceManager.%23ctor%28System.Type%29>|지정한 형식에 해당하는 <xref:System.Resources.ResourceManager> 인스턴스를 만듭니다.|
|<xref:System.Resources.ResourceManager.GetString%28System.String%29>|현재 문화권에 대해 명명된 리소스를 검색합니다.|
|<xref:System.Resources.ResourceManager.GetString%28System.String%2CSystem.Globalization.CultureInfo%29>|지정된 문화권에 속하는 명명된 리소스를 검색합니다.|

 다른 제외 <xref:System.Resources.ResourceManager> 리소스 파일에서 이식 가능한 클래스 라이브러리는 개체, 문자열이 아닌 데이터 및 이미지를 serialize 하는 수단에서 멤버를 검색할 수 없습니다. 이식 가능한 클래스 라이브러리에서 리소스를 사용 하려면 문자열 형식의 모든 개체 데이터를 저장 해야 합니다. 예를 들어, 이를 문자열로 변환하여 리소스 파일에 숫자 값을 저장할 수 있으며 숫자 데이터 형식의 `Parse` 또는 `TryParse` 메서드를 사용하여 다시 숫자로 변환할 수 있습니다. <xref:System.Convert.ToBase64String%2A?displayProperty=nameWithType> 메서드를 호출하여 이미지 또는 기타 이진 데이터를 문자열 표현으로 변환하고 <xref:System.Convert.FromBase64String%2A?displayProperty=nameWithType> 메서드를 호출하여 바이트 배열로 복원할 수 있습니다.

## <a name="the-portable-class-library-and-windows-store-apps"></a>이식 가능한 클래스 라이브러리 및 Windows 스토어 앱
 이식 가능한 클래스 라이브러리 프로젝트는 다음.resources 파일로 컴파일하고 컴파일 타임에 주 어셈블리 또는 위성 어셈블리를 포함 하는.resx 파일에 리소스를 저장 합니다. 반면에 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램은 리소스를 단일 패키지 리소스 인덱스(PRI) 파일로 컴파일되는 .resw 파일에 저장해야 합니다. 그러나 호환 되지 않는 파일 형식에도 불구 하 고 이식 가능한 클래스 라이브러리에서 작동 한 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱.

 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램에서 클래스 라이브러리를 사용하려면 Windows 스토어 앱 프로젝트에 이 라이브러리에 대한 참조를 추가합니다. Visual Studio.resw 파일로 어셈블리에서 리소스를 추출 하 고 Windows 런타임 리소스를 추출할 수 있는 PRI 파일을 생성 하는 데 사용할 투명 하 게 됩니다. 런타임 시 이식 가능한 클래스 라이브러리에 코드를 실행 하는 Windows 런타임 하지만 PRI 파일에서 이식 가능한 클래스 라이브러리의 리소스를 검색 합니다.

 이식 가능한 클래스 라이브러리 프로젝트에서 지역화 된 리소스를 포함 하는 경우 허브 및 스포크 모델을 사용 하 여 데스크톱 앱에서 라이브러리에 대 한 것 처럼 배포 합니다. [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램에서 주 리소스 파일과 지역화된 모든 리소스 파일을 사용하도록 주 어셈블리에 대한 참조를 추가합니다. 컴파일 타임에 Visual Studio는 주 리소스 파일 및 지역화된 리소스 파일에서 리소스를 추출하여 별도의 .resw 파일에 넣습니다. 그런 다음 실행 시 Windows 런타임에서 액세스 하는 단일 PRI 파일로.resw 파일을 컴파일합니다.

<a name="NonLoc"></a>
## <a name="example-non-localized-portable-class-library"></a>예제: 지역화 되지 않은 이식 가능한 클래스 라이브러리
 열의 이름을 저장 하 고 테이블 형식 데이터에 대 한 예약 문자 수를 확인 하려면 다음 간단 하 고 지역화 되지 않은 이식 가능한 클래스 라이브러리 예제에서는 리소스를 사용 합니다. 예제에서는 LibResources.resx라는 파일을 사용하여 다음 테이블에 나열된 문자열 리소스를 저장합니다.

|리소스 이름|리소스 값|
|-------------------|--------------------|
|Born|Birthdate|
|BornLength|12|
|Hired|Hire Date|
|HiredLength|12|
|ID|ID|
|ID.Length|12|
|이름|이름|
|NameLength|25|
|제목|직원 데이터베이스|

 다음 코드는 정의 `UILibrary` 라는 리소스 관리자 래퍼를 사용 하는 클래스 `resources` Visual Studio에서 생성 된 때를 **액세스 한정자** 파일에 변경 된 **공개** . UILibrary 클래스는 필요에 따라 문자열 데이터를 구문 분석합니다. . 클래스는 `MyCompany.Employees` 네임스페이스에 있습니다.

 [!code-csharp[Conceptual.Resources.Portable#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portable/cs/uilibrary.cs#1)]
 [!code-vb[Conceptual.Resources.Portable#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portable/vb/uilibrary.vb#1)]

 다음 코드는 `UILibrary` 클래스와 해당 리소스를 콘솔 모드 응용 프로그램에서 액세스하는 방법을 보여 줍니다. 콘솔 앱 프로젝트에 추가 하려면 uilibrary.dll 대 한 참조가 필요 합니다.

 [!code-csharp[Conceptual.Resources.Portable#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portable/cs/program.cs#2)]
 [!code-vb[Conceptual.Resources.Portable#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portable/vb/module1.vb#2)]

 다음 코드는 `UILibrary` 클래스와 해당 리소스를 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램에서 액세스하는 방법을 보여줍니다. Windows 스토어 앱 프로젝트에 추가 하려면 uilibrary.dll 대 한 참조가 필요 합니다.

 [!code-csharp[Conceptual.Resources.PortableMetro#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portablemetro/cs/blankpage.xaml.cs#1)]

## <a name="example-localized-portable-class-library"></a>예제: 지역화 된 이식 가능한 클래스 라이브러리
 다음 지역화 된 이식 가능한 클래스 라이브러리 예제에서는 프랑스어 (프랑스) 및 영어 (미국) 문화권에 대 한 리소스가 포함 됩니다. 영어 (미국) 문화권은 앱의 기본 문화권; 해당 리소스의 표에 표시 됩니다는 [이전 섹션](../../../docs/standard/cross-platform/app-resources-for-libraries-that-target-multiple-platforms.md#NonLoc)합니다. 프랑스어(프랑스) 문화권의 리소스 이름은 LibResources.fr-FR.resx라고 하며 다음 표에 나열된 문자열 리소스로 구성됩니다. `UILibrary` 클래스의 소스 코드는 이전 단원에 나와 있는 것과 동일합니다.

|리소스 이름|리소스 값|
|-------------------|--------------------|
|Born|Date de naissance|
|BornLength|20|
|Hired|Date embauché|
|HiredLength|16|
|ID|ID|
|이름|Nom|
|제목|Base de données des employés|

 다음 코드는 `UILibrary` 클래스와 해당 리소스를 콘솔 모드 응용 프로그램에서 액세스하는 방법을 보여 줍니다. 콘솔 앱 프로젝트에 추가 하려면 uilibrary.dll 대 한 참조가 필요 합니다.

 [!code-csharp[Conceptual.Resources.Portable#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portable/cs/program2.cs#3)]
 [!code-vb[Conceptual.Resources.Portable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portable/vb/module2.vb#3)]

 다음 코드는 `UILibrary` 클래스와 해당 리소스를 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램에서 액세스하는 방법을 보여줍니다. Windows 스토어 앱 프로젝트에 추가 하려면 uilibrary.dll 대 한 참조가 필요 합니다. 정적 `ApplicationLanguages.PrimaryLanguageOverride` 속성을 사용하여 응용 프로그램의 기본 설정 언어를 프랑스어로 설정합니다.

 [!code-csharp[Conceptual.Resources.PortableMetroLoc#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portablemetroloc/cs/blankpage.xaml.cs#1)]
 [!code-vb[Conceptual.Resources.PortableMetroLoc#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portablemetroloc/vb/blankpage.xaml.vb#1)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Resources.ResourceManager>
- [데스크톱 앱의 리소스](../../../docs/framework/resources/index.md)
- [리소스 패키징 및 배포](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)
