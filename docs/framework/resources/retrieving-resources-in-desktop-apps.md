---
title: 데스크톱 응용 프로그램의 리소스 검색
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- deploying applications [.NET Framework], resources
- resource files, deploying
- resource files, packaging
- application resources, packaging
- localization
- versioning satellite assemblies
- retrieving localized resources
- application resources, deploying
- packaging application resources
- versioning resources
- translating resources into languages
- localizing resources
ms.assetid: eca16922-1c46-4f68-aefe-e7a12283641f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f4c44bdb4be4c90c20cd6bdb56db6cd3380535c7
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045619"
---
# <a name="retrieving-resources-in-desktop-apps"></a>데스크톱 응용 프로그램의 리소스 검색
.NET Framework 데스크톱 앱의 지역화된 리소스로 작업할 경우에는 기본 또는 중립 문화권의 리소스를 주 어셈블리와 패키지하여 앱이 지원하는 각 언어 또는 문화권에 대해 별도의 위성 어셈블리를 만드는 것이 가장 바람직합니다. 그런 다음 <xref:System.Resources.ResourceManager> 클래스를 다음 섹션에 설명한 대로 사용하여 명명된 리소스에 액세스할 수 있습니다. 주 어셈블리와 위성 어셈블리에 리소스를 포함하지 않으려는 경우 이 문서의 뒷부분에 나오는 [.resources 파일에서 리소스 검색](#from_file) 섹션에서 설명한 것처럼, 이진 .resources 파일에 직접 액세스할 수도 있습니다.  [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱의 리소스 검색에 대한 자세한 내용은 Windows 개발자 센터의 [Windows 스토어 앱에서 리소스 만들기 및 검색](https://go.microsoft.com/fwlink/p/?LinkID=241674) 을 참조하세요.  
  
<a name="from_assembly"></a>   
## <a name="retrieving-resources-from-assemblies"></a>어셈블리에서 리소스 검색  
 <xref:System.Resources.ResourceManager> 클래스는 런타임에 리소스에 대한 액세스를 제공합니다. <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=nameWithType> 메서드를 사용하여 문자열 리소스를 검색하거나, <xref:System.Resources.ResourceManager.GetObject%2A?displayProperty=nameWithType> 또는 <xref:System.Resources.ResourceManager.GetStream%2A?displayProperty=nameWithType> 메서드를 사용하여 비문자열 리소스를 검색할 수 있습니다. 각 메서드에 두 개의 오버로드가 있습니다.  
  
- 단일 매개 변수가 리소스의 이름을 포함하는 문자열인 오버로드입니다. 메서드는 현재 스레드 문화권에 대한 해당 리소스를 검색하려고 시도합니다. 자세한 내용은 <xref:System.Resources.ResourceManager.GetString%28System.String%29>, <xref:System.Resources.ResourceManager.GetObject%28System.String%29>및 <xref:System.Resources.ResourceManager.GetStream%28System.String%29> 메서드를 참조하세요.  
  
- 리소스 이름을 포함하는 문자열, 리소스가 검색될 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 개체와 같은 두 개의 매개 변수가 있는 오버로드입니다. 해당 문화권에 대해 설정된 리소스를 찾을 수 없는 경우 리소스 관리자는 적절한 리소스를 검색하기 위해 대체(fallback) 규칙을 사용합니다. 자세한 내용은 <xref:System.Resources.ResourceManager.GetString%28System.String%2CSystem.Globalization.CultureInfo%29>, <xref:System.Resources.ResourceManager.GetObject%28System.String%2CSystem.Globalization.CultureInfo%29>및 <xref:System.Resources.ResourceManager.GetStream%28System.String%2CSystem.Globalization.CultureInfo%29> 메서드를 참조하세요.  
  
 리소스 관리자는 앱이 문화권 관련 리소스를 검색하는 방법을 제어하기 위해 리소스 대체 프로세스를 사용합니다. 자세한 내용은 [Packaging and Deploying Resources](packaging-and-deploying-resources-in-desktop-apps.md)의 "리소스 대체 프로세스" 섹션을 참조하세요. <xref:System.Resources.ResourceManager> 개체를 인스턴스화하는 방법에 대한 자세한 내용은 <xref:System.Resources.ResourceManager> 클래스 항목의 "ResourceManager 개체 인스턴스화" 섹션을 참조하세요.  
  
### <a name="retrieving-string-data-an-example"></a>문자열 데이터 검색: 예제  
 다음 예제는 현재 UI 문화권의 문자열 리소스를 검색하기 위해 <xref:System.Resources.ResourceManager.GetString%28System.String%29> 메서드를 호출합니다. 영어(미국) 문화권에 대해서는 중립 문자열 리소스를, 프랑스어(프랑스) 및 러시아어(러시아) 문화권에 대해서는 지역화된 리소스를 포함합니다. 다음 영어(미국) 리소스는 Strings.txt라는 파일에 있습니다.  
  
```text
TimeHeader=The current time is  
```  
  
 프랑스어(프랑스) 리소스 Strings.fr-FR.txt라는 파일에 있습니다.  
  
```text
TimeHeader=L'heure actuelle est  
```  
  
 러시아어(러시아) 리소스는 Strings.ru-RU.txt라는 파일에 있습니다.  
  
```text
TimeHeader=Текущее время —  
```  
  
 코드의 C# 버전에 대해서는 GetString.cs라는 이름의 파일에 있고 Visual Basic 버전에 대해서는 GetString.vb에 있는 이 예제의 소스 코드는 리소스를 사용할 수 있는 세 개의 문화권 및 스페인어(스페인) 문화권, 이렇게 네 개 문화권의 이름을 포함하는 문자열 배열을 정의합니다. 임의로 다섯 번 실행되는 루프는 이러한 문화권 중 하나를 선택하고 <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType> 및 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> 속성을 할당합니다. 그런 다음 <xref:System.Resources.ResourceManager.GetString%28System.String%29> 메서드를 호출하여 지역화된 문자열을 검색하고 하루 중 시간과 함께 표시합니다.  
  
 [!code-csharp[Conceptual.Resources.Retrieving#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.retrieving/cs/getstring.cs#3)]
 [!code-vb[Conceptual.Resources.Retrieving#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.retrieving/vb/getstring.vb#3)]  
  
 다음 배치(.bat) 파일은 예제를 컴파일하고 해당 디렉터리에 위성 어셈블리를 생성합니다. C# 언어 및 컴파일러에 대한 명령이 제공됩니다. Visual Basic의 경우 `csc` 를 `vbc`로, `GetString.cs` 를 `GetString.vb`로 변경합니다.  
  
```console
resgen strings.txt  
csc GetString.cs -resource:strings.resources  
  
resgen strings.fr-FR.txt  
md fr-FR  
al -embed:strings.fr-FR.resources -culture:fr-FR -out:fr-FR\GetString.resources.dll  
  
resgen strings.ru-RU.txt  
md ru-RU  
al -embed:strings.ru-RU.resources -culture:ru-RU -out:ru-RU\GetString.resources.dll  
```  
  
 현재 UI 문화권이 스페인어(스페인)인 경우 예제에서는 영어 리소스를 표시합니다. 스페인어 리소스를 사용할 수 없거나 영어가 예제의 기본 문화권이기 때문입니다.  
  
### <a name="retrieving-object-data-two-examples"></a>개체 데이터 검색: 두 가지 예제  
 개체 데이터를 검색하려면 <xref:System.Resources.ResourceManager.GetObject%2A> 및 <xref:System.Resources.ResourceManager.GetStream%2A> 메서드를 사용할 수 있습니다. 여기에는 기본 데이터 형식, 직렬화 가능 개체, 이진 형식으로 저장된 개체(예: 이미지)가 포함됩니다.  
  
 다음 예제에서는 <xref:System.Resources.ResourceManager.GetStream%28System.String%29> 메서드를 사용하여 앱의 열기 시작 창에 사용되는 비트맵을 검색합니다. CreateResources.cs(C#) 또는 CreateResources.vb(Visual Basic)라는 이름의 파일에 있는 다음 소스 코드는 serialize된 이미지를 포함하는 .resx 파일을 생성합니다. 이 경우 이미지는 SplashScreen.jpg라는 파일에서 로드됩니다. 이 파일 이름을 수정하여 자신의 고유한 이미지로 대체할 수 있습니다.  
  
 [!code-csharp[Conceptual.Resources.Retrieving#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.retrieving/cs/createresources.cs#4)]
 [!code-vb[Conceptual.Resources.Retrieving#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.retrieving/vb/createresources.vb#4)]  
  
 다음 코드는 리소스를 검색하고 <xref:System.Windows.Forms.PictureBox> 컨트롤에 이미지를 표시합니다.  
  
 [!code-csharp[Conceptual.Resources.Retrieving#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.retrieving/cs/getstream.cs#5)]
 [!code-vb[Conceptual.Resources.Retrieving#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.retrieving/vb/getstream.vb#5)]  
  
 C# 예제를 빌드하려면 다음 배치 파일을 사용할 수 있습니다. Visual Basic의 경우 `csc` 를 `vbc`로 변경하고, 소스 코드 파일의 확장을 `.cs` 에서 `.vb`로 변경합니다.  
  
```console
csc CreateResources.cs  
CreateResources  
  
resgen AppResources.resx  
  
csc GetStream.cs -resource:AppResources.resources  
```  
  
 다음 예제에서는 <xref:System.Resources.ResourceManager.GetObject%28System.String%29?displayProperty=nameWithType> 메서드를 사용하여 사용자 지정 개체를 deserialize합니다. 예제에는 `PersonTable`이라는 다음 구조를 정의하는 UIElements.cs(Visual Basic의 경우 UIElements.vb)라는 소스 코드 파일이 포함되어 있습니다. 이 구조는 테이블 열의 지역화된 이름을 표시하는 일반 테이블 표시 루틴에서 사용하기 위한 것입니다. `PersonTable` 구조체는 <xref:System.SerializableAttribute> 특성으로 표시됩니다.  
  
 [!code-csharp[Conceptual.Resources.Retrieving#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.retrieving/cs/example.cs#6)]
 [!code-vb[Conceptual.Resources.Retrieving#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.retrieving/vb/example.vb#6)]  
  
 CreateResources.cs(Visual Basic의 경우 CreateResources.vb)라는 파일에서 온 다음 코드는 테이블 제목 및 영어에 대해 지역화된 앱에 대한 정보를 포함하는 `PersonTable` 개체를 저장하는 UIResources.resx라는 XML 리소스 파일을 만듭니다.  
  
 [!code-csharp[Conceptual.Resources.Retrieving#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.retrieving/cs/example1.cs#7)]
 [!code-vb[Conceptual.Resources.Retrieving#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.retrieving/vb/example.vb#7)]  
  
 그런 다음 GetObject.cs(GetObject.vb)라는 소스 코드 파일의 다음 코드가 리소스를 검색하여 콘솔에 표시합니다.  
  
 [!code-csharp[Conceptual.Resources.Retrieving#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.retrieving/cs/example2.cs#8)]
 [!code-vb[Conceptual.Resources.Retrieving#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.retrieving/vb/example2.vb#8)]  
  
 필요한 리소스 파일 및 어셈블리를 빌드하고 다음 배치 파일을 실행하여 앱을 실행할 수 있습니다. `/r` 옵션을 사용하여 UIElements.dll에 대한 참조와 함께 Resgen.exe를 제공해야 합니다. 이렇게 해야 `PersonTable` 구조에 대한 정보에 액세스할 수 있습니다. C#을 사용하는 경우 `vbc` 컴파일러 이름을 `csc`로 바꾸고, `.vb` 확장을 `.cs`로 바꿉니다.  
  
```console
vbc -t:library UIElements.vb  
vbc CreateResources.vb -r:UIElements.dll  
CreateResources  
  
resgen UIResources.resx  -r:UIElements.dll  
vbc GetObject.vb -r:UIElements.dll -resource:UIResources.resources  
  
GetObject.exe  
```  
  
## <a name="versioning-support-for-satellite-assemblies"></a>위성 어셈블리에 대한 버전 관리 지원  
 기본적으로 <xref:System.Resources.ResourceManager> 개체는 요청된 리소스를 검색할 때 주 어셈블리의 버전 번호와 일치하는 버전 번호를 가지고 있는 위성 어셈블리를 찾습니다. 앱을 배포한 후 주 어셈블리 또는 특정 리소스 위성 어셈블리를 업데이트할 수 있습니다. .NET Framework는 주 어셈블리와 위성 어셈블리 버전 관리에 대한 지원을 제공합니다.  
  
 <xref:System.Resources.SatelliteContractVersionAttribute> 특성은 주 어셈블리에 대한 버전 관리 지원을 제공합니다. 앱의 주 어셈블리에 대해 이 특성을 지정하면 위성 어셈블리를 업데이트하지 않은 채 주 어셈블리를 업데이트 및 재배포할 수 있습니다. 주 어셈블리를 업데이트한 후, 주 어셈블리의 버전 번호는 높이되 위성 계약 버전 번호는 변경하지 않고 그대로 둡니다. 리소스 관리자는 요청된 리소스를 검색할 때 이 특성에 의해 지정된 위성 어셈블리 버전을 로드합니다.  
  
 게시자 정책 어셈블리는 위성 어셈블리 버전 관리에 대한 지원을 제공합니다. 주 어셈블리를 업데이트하지 않은 채 위성 어셈블리를 업데이트 및 재배포할 수 있습니다. 위성 어셈블리를 업데이트한 후, 버전 번호를 높이고 게시자 정책 어셈블리와 함께 제공합니다. 게시자 정책 어셈블리에서 새 위성 어셈블리가 이전 버전과 호환됨을 지정합니다. 리소스 관리자는 <xref:System.Resources.SatelliteContractVersionAttribute> 특성을 사용하여 위성 어셈블리의 버전을 확인하지만, 어셈블리 로더는 게시자 정책에서 지정한 위성 어셈블리 버전에 바인딩됩니다. 게시자 정책 어셈블리에 대한 자세한 내용은 [게시자 정책 파일 만들기](../configure-apps/how-to-create-a-publisher-policy.md)를 참조하세요.  
  
 전체 어셈블리 버전 관리 지원을 사용하려면 강력한 이름의 어셈블리는 [전역 어셈블리 캐시](../app-domains/gac.md) 에 배포하고, 강력한 이름을 가지고 있지 않은 어셈블리는 애플리케이션 디렉터리에 배포하는 것이 좋습니다. 애플리케이션 디렉터리에 강력한 이름의 어셈블리를 배포하려는 경우 어셈블리를 업데이트할 때 위성 어셈블리의 버전 번호를 높일 수 없습니다. 대신, 기존 코드를 업데이트된 코드로 바꾸고 동일한 버전 번호를 유지 관리하는 내부 업데이트를 수행해야 합니다. 예를 들어, 위성 어셈블리의 버전 1.0.0.0을 완전히 지정된 어셈블리 이름 "myApp.resources, Version=1.0.0.0, Culture=de, PublicKeyToken=b03f5f11d50a3a"로 업데이트하려는 경우, 완전히 지정된 동일한 어셈블리 이름 "myApp.resources, Version=1.0.0.0, Culture=de, PublicKeyToken=b03f5f11d50a3a"로 컴파일된 업데이트된 myApp.resources.dll로 이를 덮어씁니다. 위성 어셈블리 파일에서 내부 업데이트를 사용하면 앱이 위성 어셈블리의 버전을 정확히 확인하기가 어려워집니다.  
  
 어셈블리 버전 관리에 대한 자세한 내용은 [어셈블리 버전 관리](../../standard/assembly/versioning.md) 및 [런타임에서 어셈블리를 찾는 방법](../deployment/how-the-runtime-locates-assemblies.md)을 참조하세요.  
  
<a name="from_file"></a>   
## <a name="retrieving-resources-from-resources-files"></a>.resources 파일에서 리소스 검색  
 위성 어셈블리에서 리소스를 배포하지 않더라도 <xref:System.Resources.ResourceManager> 개체를 사용하여 .resources 파일에서 직접 리소스에 액세스할 수 있습니다. 이렇게 하려면 .resources 파일을 올바르게 배포해야 합니다. 그런 다음 <xref:System.Resources.ResourceManager.CreateFileBasedResourceManager%2A?displayProperty=nameWithType> 메서드를 사용하여 <xref:System.Resources.ResourceManager> 개체를 인스턴스화하고 독립형 .resources 파일을 포함하는 디렉터리를 지정합니다.  
  
### <a name="deploying-resources-files"></a>.resources 파일 배포  
 애플리케이션 어셈블리 및 위성 어셈블리에 .resources 파일을 포함하는 경우, 각 위성 어셈블리는 같은 파일 이름을 갖지만 위성 어셈블리의 문화권을 반영하는 하위 디렉터리에 배치됩니다. 반면, .resources 파일에서 직접 리소스에 액세스할 경우에는 일반적으로 애플리케이션 디렉터리의 하위 디렉터리인 단일 디렉터리에 모든 .resources 파일을 배치할 수 있습니다. 앱의 기본 .resources 파일의 이름은 문화권에 대한 암시 없이 루트 이름으로만 구성됩니다(예: strings.resources). 지역화된 각 문화권에 대한 리소스는 이름이 루트 이름과 문화권(예: strings.ja.resources 또는 strings.de-DE.resources)으로 구성된 파일에 저장됩니다. 
 
 다음 그림은 리소스 파일을 디렉터리 구조에서 어디에 배치해야 하는지를 보여 줍니다. 또한 .resource 파일에 대한 명명 규칙을 제공합니다.  

 ![애플리케이션의 주 디렉터리를 보여주는 그림.](./media/retrieving-resources-in-desktop-apps/resource-application-directory.gif)  
  
### <a name="using-the-resource-manager"></a>리소스 관리자 사용  
 리소스를 만들어서 적절한 디렉터리에 배치했으면, <xref:System.Resources.ResourceManager> 메서드를 호출하여 리소스를 사용할 수 있도록 <xref:System.Resources.ResourceManager.CreateFileBasedResourceManager%28System.String%2CSystem.String%2CSystem.Type%29> 개체를 만듭니다. 첫 번째 매개 변수는 앱의 기본 .resources 파일의 루트 이름을 지정합니다(이전 섹션의 예제에서는 "strings"). 두 번째 매개 변수는 리소스의 위치를 지정합니다(이전 예제에서는 "Resources"). 세 번째 매개 변수는 사용할 <xref:System.Resources.ResourceSet> 구현을 지정합니다. 세 번째 매개 변수가 `null`인 경우 기본 런타임 <xref:System.Resources.ResourceSet> 가 사용됩니다.  
  
> [!NOTE]
> 독립 실행형 .resources 파일을 사용하여 ASP.NET 앱을 배포해서는 안 됩니다. 그렇게 할 경우 잠금 문제가 발생할 수 있으며 XCOPY 배포가 중단됩니다. ASP.NET 리소스를 위성 어셈블리에 배포하는 것이 좋습니다. 자세한 내용은 [ASP.NET Web Page Resources Overview](https://docs.microsoft.com/previous-versions/aspnet/ms227427(v=vs.100))을 참조하세요.  
  
 <xref:System.Resources.ResourceManager> 개체를 인스턴스화한 후에는 앞서 설명한 대로 <xref:System.Resources.ResourceManager.GetString%2A>, <xref:System.Resources.ResourceManager.GetObject%2A>및 <xref:System.Resources.ResourceManager.GetStream%2A> 메서드를 사용하여 리소스를 검색합니다. 그러나 .resources 파일에서 직접 리소스를 검색하는 것은 어셈블리에서 포함된 리소스를 검색하는 것과 다릅니다. .resources 파일에서 리소스를 검색할 경우 <xref:System.Resources.ResourceManager.GetString%28System.String%29>, <xref:System.Resources.ResourceManager.GetObject%28System.String%29>및 <xref:System.Resources.ResourceManager.GetStream%28System.String%29> 메서드는 항상 현재 문화권과 관계없이 기본 문화권의 리소스를 검색합니다. 앱의 현재 문화권 또는 특정 문화권의 리소스를 검색하려면 <xref:System.Resources.ResourceManager.GetString%28System.String%2CSystem.Globalization.CultureInfo%29>, <xref:System.Resources.ResourceManager.GetObject%28System.String%2CSystem.Globalization.CultureInfo%29>또는 <xref:System.Resources.ResourceManager.GetStream%28System.String%2CSystem.Globalization.CultureInfo%29> 메서드를 호출하고 리소스를 검색할 문화권을 지정해야 합니다. 현재 문화권의 리소스를 검색하려면 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> 속성의 값을 `culture` 인수로서 지정합니다. 리소스 관리자는 `culture`의 리소스를 검색할 수 없는 경우 표준 리소스 대체 규칙을 사용하여 적절한 리소스를 검색할 수 있습니다.  
  
### <a name="an-example"></a>예제  
 다음 예제에서는 리소스 관리자가 .resources 파일에서 직접 리소스를 검색하는 방법을 보여 줍니다. 예제는 영어(미국), 프랑스어(프랑스) 및 러시아어(러시아) 문화권에 대한 세 가지 텍스트 기반 리소스 파일로 구성됩니다. 영어(미국)가 예제의 기본 문화권입니다. 해당 리소스는 Strings.txt라는 다음 파일에 저장됩니다.  
  
```text
Greeting=Hello  
Prompt=What is your name?  
```  
  
 프랑스어(프랑스) 문화권에 대한 리소스는 Strings.fr-FR.txt라는 다음 파일에 저장 됩니다.  
  
```text 
Greeting=Bon jour  
Prompt=Comment vous appelez-vous?  
```  
  
 러시아어(러시아) 문화권에 대한 리소스는 Strings.ru-RU.txt라는 다음 파일에 저장됩니다.  
  
```text
Greeting=Здравствуйте  
Prompt=Как вас зовут?  
```  
  
 다음은 예제의 소스 코드입니다. 이 예제에서는 영어(미국), 영어(캐나다), 프랑스어(프랑스) 및 러시아어(러시아) 문화권에 대한 <xref:System.Globalization.CultureInfo> 개체를 인스턴스화하고 각각을 현재 문화권으로 설정합니다. 그런 다음 <xref:System.Resources.ResourceManager.GetString%28System.String%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType> 메서드는 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> 속성의 값을 `culture` 인수로 제공하여 적절한 문화권 관련 리소스를 검색합니다.  
  
 [!code-csharp[Conceptual.Resources.Retrieving#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.retrieving/cs/example3.cs#9)]
 [!code-vb[Conceptual.Resources.Retrieving#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.retrieving/vb/example3.vb#9)]  
  
 다음 배치 파일을 실행하여 예제의 C# 버전을 컴파일할 수 있습니다. Visual Basic을 사용하는 경우 `csc`를 `vbc`로 바꾸고 `.cs` 확장을 `.vb`로 바꿉니다.  
  
```console
Md Resources  
Resgen Strings.txt Resources\Strings.resources  
Resgen Strings.fr-FR.txt Resources\Strings.fr-FR.resources  
Resgen Strings.ru-RU.txt Resources\Strings.ru-RU.resources  
  
csc Example.cs  
```  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Resources.ResourceManager>
- [데스크톱 앱의 리소스](index.md)
- [리소스 패키징 및 배포](packaging-and-deploying-resources-in-desktop-apps.md)
- [런타임에서 어셈블리를 찾는 방법](../deployment/how-the-runtime-locates-assemblies.md)
- [Windows 스토어 앱에서 리소스 만들기 및 검색](https://go.microsoft.com/fwlink/p/?LinkID=241674)
