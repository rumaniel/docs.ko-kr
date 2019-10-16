---
title: '방법: 지역화 가능한 애플리케이션에서 리소스 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- applications [WPF], localizable
- localizable applications [WPF]
ms.assetid: 08539ad6-7fca-4f34-b82b-ff439e11dfa7
ms.openlocfilehash: 3634bb72cbacfb02b0a1230a47a1664cb8ce5009
ms.sourcegitcommit: 4d8efe00f2e5ab42e598aff298d13b8c052d9593
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68238457"
---
# <a name="how-to-use-resources-in-localizable-applications"></a>방법: 지역화 가능한 애플리케이션에서 리소스 사용
지역화에 맞게 의미를 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 를 다른 문화권입니다. 이렇게 하려면 제목, 캡션, 목록 상자 항목 등과 같은 텍스트를 번역해야 합니다. 번역을 쉽게 하기 위해 번역할 항목이 리소스 파일로 수집됩니다. 참조 [응용 프로그램 지역화](how-to-localize-an-application.md) 지역화에 리소스 파일을 만드는 방법에 대 한 정보에 대 한 합니다. 확인을 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램을 개발자가 지역화 가능한 리소스를 모두 리소스 어셈블리에 빌드해야 하는 데 필요한 지역화 합니다. 다른 언어로 지역화 된 리소스 어셈블리 및 코드 숨김 리소스 관리 API를 사용 하 여 로드를 합니다. 에 필요한 파일 중 하나는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램은 프로젝트 파일 (.proj)입니다. 애플리케이션에서 사용하는 모든 리소스는 프로젝트 파일에 포함되어야 합니다. 다음 코드 예제에서는 이를 보여 줍니다.  
  
## <a name="example"></a>예제  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]  
  
 `<Resource Include="data\picture1.jpg"/>`  
  
 `<EmbeddedResource Include="data\stringtable.en-US.restext"/>`  
  
 인스턴스화할 응용 프로그램에서 리소스를 사용 하려면 <xref:System.Resources.ResourceManager> 하 고 사용 하려는 리소스를 로드 합니다. 다음에서는 이 작업을 수행하는 방법에 대해 설명합니다.  
  
 [!code-csharp[LocalizationResources#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationResources/CSharp/page1.xaml.cs#2)]
