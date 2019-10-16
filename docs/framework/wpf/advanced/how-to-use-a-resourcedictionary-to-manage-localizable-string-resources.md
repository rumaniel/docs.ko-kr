---
title: '방법: ResourceDictionary를 사용하여 지역화 가능한 문자열 리소스 관리'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- resources [WPF], packaging string resources
- packaging string resources [WPF]
- ResourceDictionary [WPF]
- localization [WPF], packaging string resources
ms.assetid: 19e7d9a5-20df-4ad3-b157-fe6515902e5e
ms.openlocfilehash: b56a307ed31fc8f7573215eac70350ac5e4b9de1
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59772117"
---
# <a name="how-to-use-a-resourcedictionary-to-manage-localizable-string-resources"></a>방법: ResourceDictionary를 사용하여 지역화 가능한 문자열 리소스 관리
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.ResourceDictionary> 패키지 지역화 가능한 문자열 리소스 Windows Presentation Foundation (WPF) 응용 프로그램에 대 한 합니다.  
  
### <a name="to-use-a-resourcedictionary-to-manage-localizable-string-resources"></a>ResourceDictionary를 사용하여 지역화 가능한 문자열 리소스를 관리하려면  
  
1. 만들기는 <xref:System.Windows.ResourceDictionary> 지역화 하려는 문자열을 포함 하는 합니다. 다음 코드는 예제를 보여 줍니다.  
  
     [!code-xaml[StringLocalizationSample#StringResourceDictionary](~/samples/snippets/csharp/VS_Snippets_Wpf/StringLocalizationSample/CSharp/StringResources.xaml#stringresourcedictionary)]  
  
     이 코드에서는 문자열 리소스를 정의 `localizedMessage`, 형식 <xref:System.String>에서 <xref:System> mscorlib.dll의 네임 스페이스입니다.  
  
2. 추가 된 <xref:System.Windows.ResourceDictionary> 응용 프로그램에 다음 코드를 사용 합니다.  
  
     [!code-xaml[StringLocalizationSample#ReferencingStringResourceDictionary](~/samples/snippets/csharp/VS_Snippets_Wpf/StringLocalizationSample/CSharp/App.xaml#referencingstringresourcedictionary)]  
  
3. 태그에서 문자열 리소스를 사용 하 여 사용 하 여 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 다음과 같이 합니다.  
  
     [!code-xaml[StringLocalizationSample#GetLocalizedResourceFromMarkup](~/samples/snippets/csharp/VS_Snippets_Wpf/StringLocalizationSample/CSharp/MainWindow.xaml#getlocalizedresourcefrommarkup)]  
  
4. 코드 숨김에서 다음과 같은 코드를 사용하여 문자열 리소스를 사용합니다.  
  
     [!code-csharp[StringLocalizationSample#GetLocalizedResourceFromCode](~/samples/snippets/csharp/VS_Snippets_Wpf/StringLocalizationSample/CSharp/MainWindow.xaml.cs#getlocalizedresourcefromcode)]
     [!code-vb[StringLocalizationSample#GetLocalizedResourceFromCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StringLocalizationSample/VisualBasic/MainWindow.xaml.vb#getlocalizedresourcefromcode)]  
  
5. 애플리케이션을 지역화합니다. 자세한 내용은 [응용 프로그램 지역화](how-to-localize-an-application.md)합니다.
