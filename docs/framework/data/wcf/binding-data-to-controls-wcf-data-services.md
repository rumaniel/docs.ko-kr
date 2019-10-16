---
title: 컨트롤에 데이터 바인딩(WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- client applications, WCF Data Services
- WCF Data Services, client library
- data binding, WCF Data Services
ms.assetid: b32e1d49-c214-4cb1-867e-88fbb3d08c8d
ms.openlocfilehash: 3607b7e985bfaa081c003c1a7c59a26578156eb7
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780491"
---
# <a name="binding-data-to-controls-wcf-data-services"></a>컨트롤에 데이터 바인딩(WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]를 사용하면 `ComboBox`, `ListView` 등의 컨트롤을 <xref:System.Data.Services.Client.DataServiceCollection%601> 클래스 인스턴스에 바인딩할 수 있습니다. <xref:System.Collections.ObjectModel.ObservableCollection%601> 클래스에서 상속되는 이 컬렉션에는 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 피드의 데이터가 포함됩니다. 이 클래스는 항목이 추가 또는 제거될 때 알림을 제공하는 동적 데이터 컬렉션을 나타냅니다. 데이터 바인딩에 <xref:System.Data.Services.Client.DataServiceCollection%601> <xref:System.Data.Services.Client.DataServiceContext> 인스턴스를 사용 하는 경우 클라이언트라이브러리는이러한이벤트를처리하여에의해추적되는개체가바인딩된UI요소의데이터와동기화된상태를유지하는지확인합니다.[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]  
  
 <xref:System.Data.Services.Client.DataServiceCollection%601> 클래스는 <xref:System.Collections.Specialized.INotifyCollectionChanged> 인터페이스를 간접적으로 구현하여 개체가 컬렉션에 추가 또는 제거된 경우 컨텍스트에 알립니다. <xref:System.Data.Services.Client.DataServiceCollection%601>과 함께 사용된 데이터 서비스 형식 개체는 <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스도 구현하여 바인딩 컬렉션의 개체 속성이 변경된 경우 <xref:System.Data.Services.Client.DataServiceCollection%601>에 알려야 합니다.  
  
> [!NOTE]
> 클라이언트 데이터 서비스 클래스를 생성하는 `/dataservicecollection` 옵션과 함께 **서비스 참조 추가** 대화 상자 또는 [datasvcutil.exe](wcf-data-service-client-utility-datasvcutil-exe.md) 도구를 사용하는 경우 생성된 데이터 클래스는 <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스를 구현합니다. 자세한 내용은 [방법: 클라이언트 데이터 서비스 클래스](how-to-manually-generate-client-data-service-classes-wcf-data-services.md)를 수동으로 생성 합니다.  
  
## <a name="creating-the-binding-collection"></a>바인딩 컬렉션 만들기  
 제공된 <xref:System.Data.Services.Client.DataServiceCollection%601> 인스턴스와 선택적으로 실행 시 <xref:System.Data.Services.Client.DataServiceContext> 인스턴스를 반환하는 <xref:System.Data.Services.Client.DataServiceQuery%601> 또는 LINQ 쿼리를 통해 클래스 생성자 메서드 중 하나를 호출하여 <xref:System.Collections.Generic.IEnumerable%601> 클래스의 새 인스턴스를 만듭니다. 이 <xref:System.Collections.Generic.IEnumerable%601> 는 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 피드에서 구체화 되는 바인딩 컬렉션에 대 한 개체의 소스를 제공 합니다. 자세한 내용은 [개체 구체화](object-materialization-wcf-data-services.md)를 참조 하세요. 기본적으로 컬렉션에 삽입된 항목 및 바인딩된 개체의 변경 내용은 <xref:System.Data.Services.Client.DataServiceContext>에 의해 자동으로 추적됩니다. 이러한 변경 내용을 수동으로 추적 해야 하는 경우 매개 변수를 `trackingMode` 사용 하는 생성자 메서드 중 하나를 호출 하 고 <xref:System.Data.Services.Client.TrackingMode.None>값을 지정 합니다.  
  
 다음 예제에서는 제공된 <xref:System.Data.Services.Client.DataServiceCollection%601> 및 관련 주문과 함께 모든 고객을 반환하는 <xref:System.Data.Services.Client.DataServiceContext>를 기반으로 <xref:System.Data.Services.Client.DataServiceQuery%601> 인스턴스를 만드는 방법을 보여 줍니다.  
  
 [!code-csharp[Astoria Northwind Client#CustomersOrders2Binding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorders2.cs#customersorders2binding)]
 [!code-vb[Astoria Northwind Client#CustomersOrders2Binding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorders2.vb#customersorders2binding)]  
  
## <a name="binding-data-to-windows-presentation-foundation-elements"></a>Windows Presentation Foundation 요소에 데이터 바인딩  
 <xref:System.Data.Services.Client.DataServiceCollection%601> 클래스는 <xref:System.Collections.ObjectModel.ObservableCollection%601> 클래스에서 상속하기 때문에 바인딩에 <xref:System.Collections.ObjectModel.ObservableCollection%601> 클래스를 사용할 때처럼 WPF(Windows Presentation Foundation) 애플리케이션의 요소 또는 컨트롤에 개체를 바인딩할 수 있습니다. 자세한 내용은 [데이터 바인딩 (Windows Presentation Foundation)](../../wpf/data/data-binding-wpf.md)을 참조 하세요. 데이터 서비스 데이터를 WPF 컨트롤에 바인딩하는 한 가지 방법은 요소의 `DataContext` 속성을 쿼리 결과가 포함된 <xref:System.Data.Services.Client.DataServiceCollection%601> 클래스 인스턴스로 설정하는 것입니다. 이 경우 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 속성을 사용하여 컨트롤의 개체 소스를 설정합니다. <xref:System.Windows.Controls.ItemsControl.DisplayMemberPath%2A> 속성을 사용하면 표시할 바인딩된 개체의 속성을 지정할 수 있습니다. 탐색 속성에서 반환된 관련 개체에 요소를 바인딩하는 경우 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 속성의 정의된 바인딩에 경로를 포함합니다. 이 경로는 부모 컨트롤의 <xref:System.Windows.FrameworkElement.DataContext%2A> 속성에 설정된 루트 개체에 상대적입니다. 다음 예제에서는 <xref:System.Windows.FrameworkElement.DataContext%2A> 요소의 <xref:System.Windows.Controls.StackPanel> 속성을 설정하여 부모 컨트롤을 고객 개체의 <xref:System.Data.Services.Client.DataServiceCollection%601>에 바인딩합니다.  
  
 [!code-csharp[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderscustom.xaml.cs#masterdetailbinding)]
 [!code-csharp[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderswpf.xaml.cs#masterdetailbinding)]
 [!code-vb[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderscustom.xaml.vb#masterdetailbinding)]
 [!code-vb[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf.xaml.vb#masterdetailbinding)]
 [!code-vb[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderscustom2.xaml.vb#masterdetailbinding)]  
  
 다음 예제에서는 자식 <xref:System.Windows.Controls.DataGrid> 및 <xref:System.Windows.Controls.ComboBox> 컨트롤의 XAML 바인딩 정의를 보여 줍니다.  
  
 [!code-xaml[Astoria Northwind Client#MasterDetailXaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf.xaml#masterdetailxaml)]  
  
 자세한 내용은 [방법: 데이터를 Windows Presentation Foundation 요소](bind-data-to-wpf-elements-wcf-data-services.md)에 바인딩합니다.  
  
 엔터티가 일대다 또는 다대다 관계에 참여하는 경우 관계의 탐색 속성에서 관련 개체의 컬렉션을 반환합니다. **서비스 참조 추가** 대화 상자 또는 datasvcutil.exe 도구를 사용 하 여 클라이언트 데이터 서비스 클래스를 생성 하는 경우 탐색 속성은의 <xref:System.Data.Services.Client.DataServiceCollection%601>인스턴스를 반환 합니다. 이렇게 하면 관련 개체를 컨트롤에 바인딩하고 관련 엔터티에 대한 마스터-세부 정보 바인딩 패턴과 같은 일반적인 WPF 바인딩 시나리오를 지원할 수 있습니다. 위의 XAML 예제에 포함된 XAML 코드에서는 마스터 <xref:System.Data.Services.Client.DataServiceCollection%601>을 루트 데이터 요소에 바인딩합니다. 주문 <xref:System.Windows.Controls.DataGrid>는 선택한 고객 개체에서 반환된 주문 <xref:System.Data.Services.Client.DataServiceCollection%601>에 바인딩되고, 고객 개체는 <xref:System.Windows.Window>의 루트 데이터 요소에 바인딩됩니다.  
  
## <a name="binding-data-to-windows-forms-controls"></a>Windows Forms 컨트롤에 데이터 바인딩  
 개체를 Windows Form 컨트롤에 바인딩하려면 컨트롤의 `DataSource` 속성을 쿼리 결과가 포함된 <xref:System.Data.Services.Client.DataServiceCollection%601> 클래스 인스턴스로 설정합니다.  
  
> [!NOTE]
> 데이터 바인딩은 <xref:System.Collections.Specialized.INotifyCollectionChanged> 및 <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스를 구현하여 변경 이벤트를 수신 대기하는 컨트롤에만 지원됩니다. 컨트롤이 이러한 종류의 변경 알림을 지원하지 않으면 기본 <xref:System.Data.Services.Client.DataServiceCollection%601>에 대한 변경 내용이 바인딩된 컨트롤에 반영되지 않습니다.  
  
 다음 예제에서는 <xref:System.Data.Services.Client.DataServiceCollection%601>을 <xref:System.Windows.Forms.ComboBox> 컨트롤에 바인딩합니다.  
  
 [!code-csharp[Astoria Northwind Client#CustomersOrdersDataBindingSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorders.cs#customersordersdatabindingspecific)]
 [!code-vb[Astoria Northwind Client#CustomersOrdersDataBindingSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorders.vb#customersordersdatabindingspecific)]  
  
 **서비스 참조 추가** 대화 상자를 사용 하 여 클라이언트 데이터 서비스 클래스를 생성 하는 경우 생성 <xref:System.Data.Services.Client.DataServiceContext>된를 기반으로 하는 프로젝트 데이터 원본도 만들어집니다. 이 데이터 소스를 사용 하면 데이터 **소스** 창에서 디자이너로 항목을 끌어 데이터 서비스의 데이터를 표시 하는 UI 요소 또는 컨트롤을 만들 수 있습니다. 이러한 항목은 데이터 소스에 바인딩된 애플리케이션 UI의 요소가 됩니다. 자세한 내용은 [방법: 프로젝트 데이터 소스](how-to-bind-data-using-a-project-data-source-wcf-data-services.md)를 사용 하 여 데이터를 바인딩합니다.  
  
## <a name="binding-paged-data"></a>페이징 데이터 바인딩  
 단일 응답 메시지에 반환되는 쿼리된 데이터 양을 제한하도록 데이터 서비스를 구성할 수 있습니다. 자세한 내용은 [데이터 서비스 구성](configuring-the-data-service-wcf-data-services.md)합니다. 데이터 서비스에서 응답 데이터를 페이징하는 경우 각 응답에 다음 결과 페이지를 반환하는 데 사용되는 링크가 포함됩니다. 자세한 내용은 [지연 된 콘텐츠 로드](loading-deferred-content-wcf-data-services.md)를 참조 하세요. 이 경우 다음 예제와 같이 <xref:System.Data.Services.Client.DataServiceCollection%601.Load%2A> 속성에서 가져온 URI를 전달하여 <xref:System.Data.Services.Client.DataServiceCollection%601>의 <xref:System.Data.Services.Client.DataServiceQueryContinuation.NextLinkUri%2A> 메서드를 호출함으로써 명시적으로 페이지를 로드해야 합니다.  
  
 [!code-csharp[Astoria Northwind Client#BindPagedDataSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderswpf3.xaml.cs#bindpageddataspecific)]
 [!code-vb[Astoria Northwind Client#BindPagedDataSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf3.xaml.vb#bindpageddataspecific)]  
  
 관련 개체도 유사한 방식으로 로드됩니다. 자세한 내용은 [방법: 데이터를 Windows Presentation Foundation 요소](bind-data-to-wpf-elements-wcf-data-services.md)에 바인딩합니다.  
  
## <a name="customizing-data-binding-behaviors"></a>데이터 바인딩 동작 사용자 지정  
 <xref:System.Data.Services.Client.DataServiceCollection%601> 클래스를 사용하면 개체 추가 또는 제거와 같이 컬렉션이 변경될 때 및 컬렉션의 개체 속성이 변경될 때 발생하는 이벤트를 가로챌 수 있습니다. 데이터 바인딩 이벤트를 수정하여 다음 제약 조건이 포함된 기본 동작을 재정의할 수 있습니다.  
  
- 대리자 내에서는 유효성 검사가 수행되지 않습니다.  
  
- 엔터티를 추가하면 자동으로 관련 엔터티가 추가됩니다.  
  
- 엔터티를 삭제해도 관련 엔터티는 삭제되지 않습니다.  
  
 새 <xref:System.Data.Services.Client.DataServiceCollection%601> 인스턴스를 만드는 경우 바인딩된 개체가 변경될 때 발생하는 이벤트를 처리하는 메서드에 대리자를 정의하는 다음 매개 변수를 지정할 수 있습니다.  
  
- `entityChanged` - 바인딩된 개체의 속성이 변경될 때 호출되는 메서드입니다. 이 <xref:System.Func%602> 대리자는 <xref:System.Data.Services.Client.EntityChangedParams> 개체를 받아들이고 <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A>에서 <xref:System.Data.Services.Client.DataServiceContext>를 호출하는 기본 동작이 수행되어야 하는지 여부를 나타내는 부울 값을 반환합니다.  
  
- `entityCollectionChanged` - 개체가 바인딩 컬렉션에 추가 또는 제거될 때 호출되는 메서드입니다. 이 <xref:System.Func%602> 대리자는 <xref:System.Data.Services.Client.EntityCollectionChangedParams> 개체를 받아들이고 <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> 작업에 대해 <xref:System.Collections.Specialized.NotifyCollectionChangedAction.Add>를 호출하거나 <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A>에서 <xref:System.Collections.Specialized.NotifyCollectionChangedAction.Remove> 작업에 대해 <xref:System.Data.Services.Client.DataServiceContext>를 호출하는 기본 동작이 수행되어야 하는지 여부를 나타내는 부울 값을 반환합니다.  
  
> [!NOTE]
> [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]는 이러한 대리자에 구현한 사용자 지정 동작의 유효성 검사를 수행하지 않습니다.  
  
 다음 예제에서 <xref:System.Collections.Specialized.NotifyCollectionChangedAction.Remove> 작업은 <xref:System.Data.Services.Client.DataServiceContext.DeleteLink%2A> 및 <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A> 메서드를 호출하여 삭제된 `Orders_Details` 엔터티에 속하는 `Orders` 엔터티를 제거하도록 사용자 지정됩니다. 이 사용자 지정 작업은 부모 엔터티가 삭제될 때 종속 엔터티가 자동으로 삭제되지 않으므로 수행됩니다.  
  
 [!code-csharp[Astoria Northwind Client#CustomersOrdersDeleteRelated](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderscustom.xaml.cs#customersordersdeleterelated)]
 [!code-vb[Astoria Northwind Client#CustomersOrdersDeleteRelated](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderscustom.xaml.vb#customersordersdeleterelated)]
 [!code-vb[Astoria Northwind Client#CustomersOrdersDeleteRelated](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderscustom2.xaml.vb#customersordersdeleterelated)]  
  
 자세한 내용은 [방법: 데이터 바인딩 동작](how-to-customize-data-binding-behaviors-wcf-data-services.md)을 사용자 지정 합니다.  
  
 <xref:System.Data.Services.Client.DataServiceCollection%601> 메서드를 사용하여 <xref:System.Collections.ObjectModel.Collection%601.Remove%2A>에서 개체가 제거될 때의 기본 동작은 해당 개체가 <xref:System.Data.Services.Client.DataServiceContext>에서도 삭제된 것으로 표시되는 것입니다. 이 동작을 변경하려면 `entityCollectionChanged` 이벤트가 발생할 때 호출되는 <xref:System.Collections.Specialized.INotifyCollectionChanged.CollectionChanged> 매개 변수의 메서드로 대리자를 지정합니다.  
  
## <a name="data-binding-with-custom-client-data-classes"></a>사용자 지정 클라이언트 데이터 클래스를 사용하여 데이터 바인딩  
 개체를 <xref:System.Data.Services.Client.DataServiceCollection%601>으로 로드할 수 있으려면 개체 자체에서 <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스를 구현해야 합니다. **서비스 참조 추가** 대화 상자를 사용 하거나 [datasvcutil.exe](wcf-data-service-client-utility-datasvcutil-exe.md) 도구를 사용 하 여 생성 된 데이터 서비스 클라이언트 클래스는이 인터페이스를 구현할 수 있습니다. 고유한 클라이언트 데이터 클래스를 제공하는 경우 데이터 바인딩에 다른 컬렉션 형식을 사용해야 합니다. 개체가 변경되면 데이터 바인딩된 컨트롤에서 이벤트를 처리하여 <xref:System.Data.Services.Client.DataServiceContext> 클래스의 다음 메서드를 호출해야 합니다.  
  
- <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> - 새 개체가 컬렉션에 추가된 경우  
  
- <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A> - 개체가 컬렉션에서 제거된 경우  
  
- <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> - 컬렉션에 있는 개체의 속성이 변경된 경우  
  
- <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> - 개체가 관련 개체의 컬렉션에 추가된 경우  
  
- <xref:System.Data.Services.Client.DataServiceContext.SetLink%2A> - 개체가 관련 개체의 컬렉션에 추가된 경우  
  
 자세한 내용은 [데이터 서비스 업데이트](updating-the-data-service-wcf-data-services.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [방법: 수동으로 클라이언트 데이터 서비스 클래스 생성](how-to-manually-generate-client-data-service-classes-wcf-data-services.md)
- [방법: 데이터 서비스 참조 추가](how-to-add-a-data-service-reference-wcf-data-services.md)
