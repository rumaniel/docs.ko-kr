---
title: '방법: 애플리케이션 리소스 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- application resources [WPF]
- resources [WPF], application resources
ms.assetid: 507ea937-5191-406b-8797-0a3d9f94156d
ms.openlocfilehash: 70dff8089c4da70fdc61247a0c604cf7ee85d02b
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59088205"
---
# <a name="how-to-use-application-resources"></a>방법: 애플리케이션 리소스 사용
이 예제에서는 애플리케이션 리소스를 사용하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 애플리케이션 정의 파일을 보여 줍니다. 리소스 섹션을 정의 하는 응용 프로그램 정의 파일 (에 대 한 값을 <xref:System.Windows.Application.Resources%2A> 속성). 애플리케이션 수준에 정의된 리소스는 애플리케이션의 일부인 다른 모든 페이지에 액세스할 수 있습니다. 이 경우 리소스는 선언된 스타일입니다. 이 예제에서는 내에 정의 된 컨트롤 템플릿을 생략 컨트롤 템플릿을 포함 하는 전체 스타일 일 수 있으므로 시간이 오래 걸리는 <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> 스타일의 속성 setter.  
  
 [!code-xaml[ResourcesApplication#PreTemplateResource](~/samples/snippets/csharp/VS_Snippets_Wpf/ResourcesApplication/CS/app.xaml#pretemplateresource)]  
[!code-xaml[ResourcesApplication#PostTemplateResource](~/samples/snippets/csharp/VS_Snippets_Wpf/ResourcesApplication/CS/app.xaml#posttemplateresource)]  
  
 다음 예제와 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 앞의 예제에서 정의한 응용 프로그램 수준 리소스를 참조 하는 페이지입니다. 리소스를 사용 하 여 참조 되는 [StaticResource 태그 확장](staticresource-markup-extension.md) 요청된 된 리소스에 대 한 고유한 리소스 키를 지정 하는 합니다. 현재 페이지에서 키가 “GelButton”인 리소스를 찾지 못했으므로 요청한 리소스에 대한 리소스 조회 범위가 현재 페이지 범위를 벗어나서 정의된 애플리케이션 수준 리소스로 이어집니다.  
  
 [!code-xaml[ResourcesApplication#ConsumingPage](~/samples/snippets/csharp/VS_Snippets_Wpf/ResourcesApplication/CS/page1.xaml#consumingpage)]  
  
## <a name="see-also"></a>참고자료

- [XAML 리소스](xaml-resources.md)
- [응용 프로그램 관리 개요](../app-development/application-management-overview.md)
- [방법 항목](resources-how-to-topics.md)
