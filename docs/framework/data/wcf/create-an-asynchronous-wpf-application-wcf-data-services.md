---
title: '방법: 비동기 Windows Presentation Framework 응용 프로그램 만들기 (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, asynchronous operations
ms.assetid: 834614df-1427-4839-b0be-90f68e5afffd
ms.openlocfilehash: 820cb4aa39b49d63cf1acc31e6eb5aa56fd1ba03
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790985"
---
# <a name="how-to-create-an-asynchronous-windows-presentation-framework-application-wcf-data-services"></a>방법: 비동기 Windows Presentation Framework 응용 프로그램 만들기 (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]를 사용하면 데이터 서비스에서 가져온 데이터를 WPF(Windows Presentation Framework) 애플리케이션의 UI 요소에 바인딩할 수 있습니다. 자세한 내용은 [컨트롤에 데이터 바인딩](binding-data-to-controls-wcf-data-services.md)을 참조 하세요. 비동기 방식으로 데이터 서비스에 대해 작업을 실행할 수도 있습니다 .이 경우 데이터 서비스 요청에 대 한 응답을 기다리는 동안 응용 프로그램이 계속 응답할 수 있습니다. 데이터 서비스에 비동기적으로 액세스하려면 Silverlight용 애플리케이션이 필요합니다. 자세한 내용은 [비동기 작업](asynchronous-operations-wcf-data-services.md)합니다.  
  
 이 항목에서는 데이터 서비스에 비동기적으로 액세스하고 그 결과를 WPF 애플리케이션의 요소에 바인딩하는 방법을 보여 줍니다. 이 항목의 예제에서는 Northwind 샘플 데이터 서비스 및 자동 생성된 클라이언트 데이터 서비스 클래스를 사용합니다. 이 서비스 및 클라이언트 데이터 클래스는 [WCF Data Services 빠른](quickstart-wcf-data-services.md)시작을 완료 하면 생성 됩니다.  
  
## <a name="example"></a>예제  
 다음 XAML에서는 WPF 애플리케이션의 창을 정의합니다.  
  
 [!code-xaml[Astoria Northwind Client#WpfDataBindingAsyncXaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerordersasync.xaml#wpfdatabindingasyncxaml)]  
  
## <a name="example"></a>예제  
 XAML 파일의 다음 코드 숨김 페이지에서는 데이터 서비스를 사용하여 비동기 쿼리를 실행하고 그 결과를 WPF 창의 요소에 바인딩합니다.  
  
 [!code-csharp[Astoria Northwind Client#WpfDataBindingAsync](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerordersasync.xaml.cs#wpfdatabindingasync)]
 [!code-vb[Astoria Northwind Client#WpfDataBindingAsync](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerordersasync.xaml.vb#wpfdatabindingasync)]  
  
## <a name="see-also"></a>참고자료

- [WCF Data Services 클라이언트 라이브러리](wcf-data-services-client-library.md)
