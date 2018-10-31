---
title: 어셈블리 특성 설정
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- assemblies [.NET Framework], attributes
- assembly binding, attributes
- assembly manifest, attributes
ms.assetid: 36a98a81-b5b5-4c19-912a-11f91eff7f4e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e1ed022193b4896f91f1096a0bb16c21f5374868
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50201428"
---
# <a name="setting-assembly-attributes"></a>어셈블리 특성 설정
어셈블리 특성은 어셈블리에 대한 정보를 제공하는 값입니다. 특성은 다음과 같은 정보 집합으로 나뉩니다.  
  
-   어셈블리 ID 특성  
  
-   정보 특성  
  
-   어셈블리 매니페스트 특성  
  
-   강력한 이름 특성  
  
## <a name="assembly-identity-attributes"></a>어셈블리 ID 특성  
 강력한 이름(해당하는 경우)과 더불어 name, version 및 culture의 세 가지 특성이 어셈블리의 ID를 결정합니다. 이러한 특성은 어셈블리의 전체 이름을 구성하며 코드에서 어셈블리를 참조할 때 필요합니다. 특성을 사용하여 어셈블리의 버전 및 문화권을 설정할 수 있습니다. 컴파일러 또는 [어셈블리 링커(Al.exe)](../../../docs/framework/tools/al-exe-assembly-linker.md) 는 어셈블리 매니페스트를 포함하는 파일에 따라 어셈블리가 만들어질 때 이름 값을 설정합니다.  
  
 다음 표에서는 version 및 culture 특성에 대해 설명합니다.  
  
|어셈블리 ID 특성|설명|  
|---------------------------------|-----------------|  
|<xref:System.Reflection.AssemblyCultureAttribute>|어셈블리에서 지원하는 문화권을 나타내는 열거형 필드입니다. 어셈블리는 기본 문화권에 대한 리소스가 포함되어 있음을 나타내는 문화권 독립성을 지정할 수도 있습니다. **참고:** 런타임은 culture 특성이 null로 설정되어 있지 않은 모든 어셈블리를 위성 어셈블리로 처리합니다. 이러한 어셈블리에는 위성 어셈블리 바인딩 규칙이 적용됩니다. 자세한 내용은 [런타임에서 어셈블리를 찾는 방법](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)을 참조하세요.|  
|<xref:System.Reflection.AssemblyFlagsAttribute>|어셈블리를 병렬로 실행할 수 있는지 여부와 같은 어셈블리 특성을 설정하는 값입니다.|  
|<xref:System.Reflection.AssemblyVersionAttribute>|*major*.*minor*.*build*.*revision* 형식의 숫자 값입니다(예: 2.4.0.0). 공용 언어 런타임은 이 값을 사용하여 강력한 이름의 어셈블리에서 바인딩 작업을 수행합니다. **참고:** <xref:System.Reflection.AssemblyInformationalVersionAttribute> 특성이 어셈블리에 적용되어 있지 않은 경우 <xref:System.Reflection.AssemblyVersionAttribute> 특성으로 지정된 버전 번호가 <xref:System.Windows.Forms.Application.ProductVersion%2A?displayProperty=nameWithType>, <xref:System.Windows.Forms.Application.UserAppDataPath%2A?displayProperty=nameWithType> 및 <xref:System.Windows.Forms.Application.UserAppDataRegistry%2A?displayProperty=nameWithType> 속성에서 사용됩니다.|  
  
 다음 코드 예제에서는 어셈블리에 version 및 culture 특성을 적용하는 방법을 보여 줍니다.  
  
 [!code-cpp[AssemblyDelaySignAttribute#3](../../../samples/snippets/cpp/VS_Snippets_CLR/AssemblyDelaySignAttribute/cpp/source2.cpp#3)]
 [!code-csharp[AssemblyDelaySignAttribute#3](../../../samples/snippets/csharp/VS_Snippets_CLR/AssemblyDelaySignAttribute/cs/source2.cs#3)]
 [!code-vb[AssemblyDelaySignAttribute#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AssemblyDelaySignAttribute/vb/source2.vb#3)]  
  
## <a name="informational-attributes"></a>정보 특성  
 정보 특성을 사용하여 어셈블리에 대한 추가 회사 또는 제품 정보를 제공할 수 있습니다. 다음 표에서는 어셈블리에 적용할 수 있는 정보 특성에 대해 설명합니다.  
  
|정보 특성|설명|  
|-----------------------------|-----------------|  
|<xref:System.Reflection.AssemblyCompanyAttribute>|회사 이름을 지정하는 문자열 값입니다.|  
|<xref:System.Reflection.AssemblyCopyrightAttribute>|저작권 정보를 지정하는 문자열 값입니다.|  
|<xref:System.Reflection.AssemblyFileVersionAttribute>|Win32 파일 버전 번호를 지정하는 문자열 값입니다. 기본값은 일반적으로 어셈블리 버전입니다.|  
|<xref:System.Reflection.AssemblyInformationalVersionAttribute>|전체 제품 버전 번호와 같이 공용 언어 런타임에서 사용되지 않는 버전 정보를 지정하는 문자열 값입니다. **참고:** 이 특성이 어셈블리에 적용된 경우 <xref:System.Windows.Forms.Application.ProductVersion%2A?displayProperty=nameWithType> 속성을 사용하여 런타임에 지정하는 문자열을 가져올 수 있습니다. 문자열은 <xref:System.Windows.Forms.Application.UserAppDataPath%2A?displayProperty=nameWithType> 및 <xref:System.Windows.Forms.Application.UserAppDataRegistry%2A?displayProperty=nameWithType> 속성이 제공하는 경로 및 레지스트리 키에서도 사용됩니다.|  
|<xref:System.Reflection.AssemblyProductAttribute>|제품 정보를 지정하는 문자열 값입니다.|  
|<xref:System.Reflection.AssemblyTrademarkAttribute>|상표 정보를 지정하는 문자열 값입니다.|  
  
 이러한 특성은 어셈블리의 Windows 속성 페이지에 표시될 수 있거나, **/win32res** 컴파일러 옵션을 통해 사용자 고유의 Win32 리소스 파일을 지정하여 재정의할 수 있습니다.  
  
## <a name="assembly-manifest-attributes"></a>어셈블리 매니페스트 특성  
 어셈블리 매니페스트 특성을 사용하여 제목, 설명, 기본 별칭 및 구성을 비롯한 어셈블리 매니페스트의 정보를 제공할 수 있습니다. 다음 표에서는 어셈블리 매니페스트 특성에 대해 설명합니다.  
  
|어셈블리 매니페스트 특성|설명|  
|---------------------------------|-----------------|  
|<xref:System.Reflection.AssemblyConfigurationAttribute>|일반 정품 또는 디버그와 같은 어셈블리 구성을 나타내는 문자열 값입니다. 런타임에서는 이 값을 사용하지 않습니다.|  
|<xref:System.Reflection.AssemblyDefaultAliasAttribute>|어셈블리를 참조하여 사용할 기본 별칭을 지정하는 문자열 값입니다. 이 값은 어셈블리 이름 자체가 친숙하지 않은 경우(예: GUID 값) 친숙한 이름을 제공합니다. 이 값을 전체 어셈블리 이름의 짧은 형태로 사용할 수도 있습니다.|  
|<xref:System.Reflection.AssemblyDescriptionAttribute>|어셈블리의 특성과 용도를 요약하는 간단한 설명을 지정하는 문자열 값입니다.|  
|<xref:System.Reflection.AssemblyTitleAttribute>|어셈블리에 대한 친숙한 이름을 지정하는 문자열 값입니다. 예를 들어 comdlg라는 어셈블리에 Microsoft 공용 대화 상자 컨트롤이라는 제목이 있을 수 있습니다.|  
  
## <a name="strong-name-attributes"></a>강력한 이름 특성  
 강력한 이름 특성을 사용하여 어셈블리에 대한 강력한 이름을 설정할 수 있습니다. 다음 표에서는 강력한 이름 특성에 대해 설명합니다.  
  
|강력한 이름 특성|설명|  
|----------------------------|-----------------|  
|<xref:System.Reflection.AssemblyDelaySignAttribute>|서명 연기가 사용되고 있음을 나타내는 부울 값입니다.|  
|<xref:System.Reflection.AssemblyKeyFileAttribute>|이 특성의 생성자에 매개 변수로 전달되는 공개 키(서명 연기를 사용하는 경우) 또는 공개 키와 개인 키 둘 다의 이름을 포함하는 파일의 이름을 나타내는 문자열 값입니다. 파일 이름은 원본 파일 경로가 아니라 출력 파일 경로(.exe 또는 .dll)를 기준으로 합니다.|  
|<xref:System.Reflection.AssemblyKeyNameAttribute>|이 특성의 생성자에 매개 변수로 전달되는 키 쌍을 포함하는 키 컨테이너를 나타냅니다.|  
  
 다음 코드 예제에서는 `myKey.snk`라는 공개 키 파일과 함께 서명 연기를 사용하여 강력한 이름의 어셈블리를 만들 때 적용할 특성을 보여 줍니다.  
  
 [!code-cpp[AssemblyDelaySignAttribute#4](../../../samples/snippets/cpp/VS_Snippets_CLR/AssemblyDelaySignAttribute/cpp/source2.cpp#4)]
 [!code-csharp[AssemblyDelaySignAttribute#4](../../../samples/snippets/csharp/VS_Snippets_CLR/AssemblyDelaySignAttribute/cs/source2.cs#4)]
 [!code-vb[AssemblyDelaySignAttribute#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AssemblyDelaySignAttribute/vb/source2.vb#4)]  
  
## <a name="see-also"></a>참고 항목  
- [어셈블리 만들기](../../../docs/framework/app-domains/create-assemblies.md)  
- [어셈블리를 사용한 프로그래밍](../../../docs/framework/app-domains/programming-with-assemblies.md)
