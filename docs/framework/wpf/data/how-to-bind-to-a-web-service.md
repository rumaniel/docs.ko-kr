---
title: '방법: 웹 서비스에 바인딩'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- binding data [WPF], Web service
- Web service binding [WPF]
- data binding [WPF], Web service
ms.assetid: 77e2d373-69ba-4cbd-b6f5-2c83c38fc98b
ms.openlocfilehash: 2c3bc1f2142f07aba3df2da6c46117d3907443a5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61954286"
---
# <a name="how-to-bind-to-a-web-service"></a>방법: 웹 서비스에 바인딩
이 예제에서는 웹 서비스 메서드 호출에서 반환 된 개체에 바인딩하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 합니다 [MSDN/TechNet 게시 시스템 (MTPS) 콘텐츠 서비스](https://go.microsoft.com/fwlink/?LinkId=95677) 지정된 된 문서를 지 원하는 언어의 목록을 검색 합니다.  
  
 웹 서비스를 호출 하기 전에에 대 한 참조 해야 합니다. 사용 하 여 MTPS 서비스 웹 참조를 만들려면 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)], 다음 단계를 수행 합니다.  
  
1. 프로젝트를 열고 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)]합니다.  
  
2. **프로젝트** 메뉴에서 클릭 **웹 참조 추가**합니다.  
  
3. 대화 상자에서 설정 합니다 **URL** 하 [ http://services.msdn.microsoft.com/contentservices/contentservice.asmx?wsdl ](https://services.msdn.microsoft.com/contentservices/contentservice.asmx?wsdl)합니다.  
  
4. 키를 눌러 **이동** 차례로 **참조 추가**합니다.  
  
 웹 서비스 메서드를 호출 하는 다음으로 설정 하 고는 <xref:System.Windows.FrameworkElement.DataContext%2A> 적절 한 컨트롤 또는 창의 반환 된 개체입니다. 합니다 **GetContent** MTPS 서비스의 메서드는에 대 한 참조를 사용 합니다 **getContentRequest** 개체입니다. 따라서 다음 예제에서는 먼저 요청 개체를 설정합니다.  
  
 [!code-csharp[BindToWebService#Namespace](~/samples/snippets/csharp/VS_Snippets_Wpf/BindToWebService/CSharp/Window1.xaml.cs#namespace)]
 [!code-vb[BindToWebService#Namespace](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BindToWebService/VisualBasic/Window1.xaml.vb#namespace)]  
[!code-csharp[BindToWebService#WebServiceCall](~/samples/snippets/csharp/VS_Snippets_Wpf/BindToWebService/CSharp/Window1.xaml.cs#webservicecall)]
[!code-vb[BindToWebService#WebServiceCall](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BindToWebService/VisualBasic/Window1.xaml.vb#webservicecall)]  
  
 후 합니다 <xref:System.Windows.FrameworkElement.DataContext%2A> 는 개체의 속성에 대 한 바인딩을 만들 수 있습니다가 설정 된는 <xref:System.Windows.FrameworkElement.DataContext%2A> 로 설정 되었습니다. 이 예제에서는 합니다 <xref:System.Windows.FrameworkElement.DataContext%2A> 로 설정 되어 합니다 **getContentResponse** 에서 반환 된 개체를 **GetContent** 메서드. 다음 예에서 합니다 <xref:System.Windows.Controls.ItemsControl> 에 바인딩하고 표시 합니다 **로캘** 값 **availableVersionsAndLocales** 의 **getContentResponse**.  
  
 [!code-xaml[BindToWebService#Binding](~/samples/snippets/csharp/VS_Snippets_Wpf/BindToWebService/CSharp/Window1.xaml#binding)]  
  
 구조에 대 한 자세한 **getContentResponse**를 참조 하십시오 [콘텐츠 서비스 설명서](https://services.msdn.microsoft.com/ContentServices/ContentService.asmx)합니다.  
  
## <a name="see-also"></a>참고자료

- [데이터 바인딩 개요](data-binding-overview.md)
- [바인딩 소스 개요](binding-sources-overview.md)
- [XAML의 바인딩에 사용할 수 있는 데이터 만들기](how-to-make-data-available-for-binding-in-xaml.md)
