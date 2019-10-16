---
title: '방법: UI인 추가 기능 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- creating an add-in that is a UI [WPF]
- add-ins [WPF], UI
- creating UI add-ins [WPF]
- UI add-ins [WPF], creating
- implementing UI add-ins [WPF]
- pipeline segments [WPF], creating add-ins
ms.assetid: 86375525-282b-4039-8352-8680051a10ea
ms.openlocfilehash: b0e847061a30e93d36997ab603c52715e2730765
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182644"
---
# <a name="how-to-create-an-add-in-that-is-a-ui"></a>방법: UI인 추가 기능 만들기
이 예제에서는 WPF 독립 실행형 응용 프로그램에서 호스팅하는 Windows Presentation Foundation (WPF) 인 추가 기능을 만드는 방법을 보여 줍니다.  
  
 추가 기능은 WPF 사용자 정의 컨트롤인 UI입니다. 이 사용자 정의 컨트롤의 콘텐츠는 클릭했을 때 메시지 상자를 표시하는 하나의 단추입니다. WPF 독립 실행형 응용 프로그램은 주 응용 프로그램 창의 콘텐츠로 추가 기능 UI를 호스팅합니다.  
  
 **필수 구성 요소**  
  
 이 예제에서는이 시나리오를 사용 하도록 설정 하는 .NET Framework 추가 기능 모델에 대 한 WPF 확장을 강조 표시 하 고 다음을 가정 합니다.  
  
- 파이프라인, 추가 기능 및 호스트 개발을 포함 하 여 .NET Framework 추가 기능 모델에 대 한 지식. 이러한 개념을 잘 모르는 경우 [추가 기능 및 확장성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))을 참조 하세요. 파이프라인, 추가 기능 및 호스트 응용 프로그램을 구현 하는 방법을 보여 주는 자습서를 보려면 [연습: 확장 가능한 응용 프로그램](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb788290(v%3dvs.100))만들기  
  
- .NET Framework 추가 기능 모델에 대 한 WPF 확장 정보 [WPF 추가 기능 개요](wpf-add-ins-overview.md)를 참조 하세요.  
  
## <a name="example"></a>예제  
 WPF UI 인 추가 기능을 만들려면 각 파이프라인 세그먼트, 추가 기능 및 호스트 응용 프로그램에 대 한 특정 코드가 필요 합니다.  

<a name="Contract"></a>   
## <a name="implementing-the-contract-pipeline-segment"></a>계약 파이프라인 세그먼트 구현

추가 기능이 UI 인 경우 추가 기능에 대 한 계약은를 구현 <xref:System.AddIn.Contract.INativeHandleContract>해야 합니다. 예제 `IWPFAddInContract` 에서는 다음 코드 <xref:System.AddIn.Contract.INativeHandleContract>와 같이을 구현 합니다.  
  
[!code-csharp[SimpleAddInIsAUISample#ContractCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInIsAUISample/CSharp/Contracts/IWPFAddInContract.cs#contractcode)]
[!code-vb[SimpleAddInIsAUISample#ContractCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInIsAUISample/VisualBasic/Contracts/IWPFAddInContract.vb#contractcode)]

<a name="AddInViewPipeline"></a>   
## <a name="implementing-the-add-in-view-pipeline-segment"></a>추가 기능 뷰 파이프라인 세그먼트 구현

추가 기능이 <xref:System.Windows.FrameworkElement> 형식의 하위 클래스로 구현 되기 때문에 추가 기능 뷰도 하위 클래스 <xref:System.Windows.FrameworkElement>여야 합니다. 다음 코드에서는 `WPFAddInView` 클래스로 구현 된 계약의 추가 기능 뷰를 보여 줍니다.  
  
[!code-csharp[SimpleAddInIsAUISample#AddInViewCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInIsAUISample/CSharp/AddInViews/WPFAddInView.cs#addinviewcode)]  
[!code-vb[SimpleAddInIsAUISample#AddInViewCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInIsAUISample/VisualBasic/AddInViews/WPFAddInView.vb#AddInViewCode)]  
  
여기서는 추가 기능 뷰가에서 <xref:System.Windows.Controls.UserControl>파생 됩니다. 따라서 추가 기능 UI는 에서도 파생 <xref:System.Windows.Controls.UserControl>되어야 합니다.  
  
<a name="AddInSideAdapter"></a>
## <a name="implementing-the-add-in-side-adapter-pipeline-segment"></a>추가 기능 쪽 어댑터 파이프라인 세그먼트 구현

계약은 <xref:System.AddIn.Contract.INativeHandleContract>인 반면 추가 기능은 추가 기능 뷰 파이프라인 세그먼트로 지정 <xref:System.Windows.FrameworkElement> 되는입니다. 따라서 격리 경계를 통과 <xref:System.AddIn.Contract.INativeHandleContract> 하기 전에를으로 변환 해야합니다.<xref:System.Windows.FrameworkElement> 이 작업은 다음 코드와 같이를 호출 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>하 여 추가 기능 측 어댑터에 의해 수행 됩니다.  
  
[!code-csharp[SimpleAddInIsAUISample#AddInSideAdapterCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInIsAUISample/CSharp/AddInSideAdapters/WPFAddIn_ViewToContractAddInSideAdapter.cs#addinsideadaptercode)]  
[!code-vb[SimpleAddInIsAUISample#AddInSideAdapterCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInIsAUISample/VisualBasic/AddInSideAdapters/WPFAddIn_ViewToContractAddInSideAdapter.vb#addinsideadaptercode)]

추가 기능이 ui를 반환 하는 추가 기능 모델에서 ( [ui를 반환 하는 추가 기능 만들기](how-to-create-an-add-in-that-returns-a-ui.md)참조) 추가 기능 어댑터는를 호출 <xref:System.Windows.FrameworkElement> <xref:System.AddIn.Contract.INativeHandleContract> <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>하 여를로 변환 합니다. <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>를 호출 하는 코드를 작성 하는 데 사용할 메서드를 구현 해야 하지만이 모델 에서도를 호출 해야 합니다. <xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> 호출 하는코드에가필요한경우를호출하는코드를재정의하고구현하여이작업을수행합니다.<xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> <xref:System.AddIn.Contract.INativeHandleContract> 이 경우 호출자가 호스트 쪽 어댑터가 됩니다. 이에 대해서는 이후의 하위 단원에서 설명합니다.  
  
> [!NOTE]
> 또한 호스트 응용 프로그램 ui <xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> 와 추가 기능 ui 사이에서 탭 이동을 사용 하려면이 모델에서를 재정의 해야 합니다. 자세한 내용은 [Wpf 추가 기능 개요](wpf-add-ins-overview.md)의 "wpf 추가 기능 제한 사항"을 참조 하세요.  
  
추가 기능 측 어댑터는에서 <xref:System.AddIn.Contract.INativeHandleContract>파생 되는 인터페이스를 구현 하므로를 재정의 <xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> 하더라도를 구현 <xref:System.AddIn.Contract.INativeHandleContract.GetHandle%2A>해야 합니다.  
  
<a name="HostViewPipeline"></a>   
## <a name="implementing-the-host-view-pipeline-segment"></a>호스트 뷰 파이프라인 세그먼트 구현

이 모델에서 호스트 응용 프로그램은 일반적으로 호스트 뷰가 <xref:System.Windows.FrameworkElement> 하위 클래스가 될 것으로 예상 합니다. 호스트 측 어댑터는가 격리 경계를 <xref:System.AddIn.Contract.INativeHandleContract> <xref:System.AddIn.Contract.INativeHandleContract> 교차할 때 <xref:System.Windows.FrameworkElement> 를로 변환 해야 합니다. 호스트 응용 프로그램에서 메서드를 호출 하 여를 가져오기 <xref:System.Windows.FrameworkElement>때문에 호스트 뷰는를 포함 하 여를 <xref:System.Windows.FrameworkElement> "반환" 해야 합니다. 따라서 호스트 뷰는와 <xref:System.Windows.FrameworkElement> <xref:System.Windows.Controls.UserControl>같은 다른 ui를 포함할 수 있는의 서브 클래스에서 파생 되어야 합니다. 다음 코드에서는 `WPFAddInHostView` 클래스로 구현 된 계약의 호스트 뷰를 보여 줍니다.  

[!code-csharp[WPFAddInHostView class](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInIsAUISample/CSharp/HostViews/WPFAddInHostView.cs#HostViewCode)]
[!code-vb[WPFAddInHostView class](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInIsAUISample/VisualBasic/HostViews/WPFAddInHostView.vb#HostViewCode)]

<a name="HostSideAdapter"></a>   
## <a name="implementing-the-host-side-adapter-pipeline-segment"></a>호스트 측 어댑터 파이프라인 세그먼트 구현

계약은 <xref:System.AddIn.Contract.INativeHandleContract>이지만 호스트 응용 프로그램에는 호스트 보기에 지정 <xref:System.Windows.Controls.UserControl> 된 대로가 필요 합니다. 따라서가 <xref:System.Windows.FrameworkElement> 에서 <xref:System.AddIn.Contract.INativeHandleContract> 파생되는호스트뷰의콘텐츠로설정되기전에격리경계를통과한후를로<xref:System.Windows.Controls.UserControl>변환 해야 합니다.  
  
다음 코드와 같이 이 작업은 호스트 쪽 어댑터로 수행됩니다.  

[!code-csharp[Host-side adapter](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInIsAUISample/CSharp/HostSideAdapters/WPFAddIn_ContractToViewHostSideAdapter.cs#HostSideAdapterCode)]
[!code-vb[Host-side adapter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInIsAUISample/VisualBasic/HostSideAdapters/WPFAddIn_ContractToViewHostSideAdapter.vb#HostSideAdapterCode)]

여기에서 볼 수 있듯이 호스트 측 어댑터는 추가 기능 측 <xref:System.AddIn.Contract.INativeHandleContract> 어댑터의 <xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> 메서드를 호출 하 여를 가져옵니다 ( <xref:System.AddIn.Contract.INativeHandleContract> 가 격리 경계를 교차 하는 지점).  
  
그런 다음 호스트 측 어댑터는를 호출 <xref:System.AddIn.Contract.INativeHandleContract> <xref:System.Windows.FrameworkElement> <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>하 여를로 변환 합니다. 마지막으로는 <xref:System.Windows.FrameworkElement> 호스트 뷰의 콘텐츠로 설정 됩니다.  
  
<a name="AddIn"></a>   
## <a name="implementing-the-add-in"></a>추가 기능 구현

추가 기능 쪽 어댑터와 추가 기능 뷰를 배치했으면 다음 코드와 같이 추가 기능 뷰에서 파생시켜 추가 기능을 구현할 수 있습니다.  

[!code-csharp[Add-in implementation](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInIsAUISample/CSharp/WPFAddIn1/AddInUI.xaml.cs#AddInCodeBehind)]
[!code-vb[Add-in implementation](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInIsAUISample/VisualBasic/WPFAddIn1/AddInUI.xaml.vb#AddInCodeBehind)]

이 예제에서이 모델의 흥미로운 장점 하나를 확인할 수 있습니다. 추가 기능 개발자가 추가 기능 클래스와 추가 기능 UI가 아니라 UI 뿐 이므로 추가 기능을 구현 하기만 하면 됩니다.  
  
<a name="HostApp"></a>
## <a name="implementing-the-host-application"></a>호스트 애플리케이션 구현

호스트 쪽 어댑터와 호스트 뷰를 만든 경우 호스트 응용 프로그램은 .NET Framework 추가 기능 모델을 사용 하 여 파이프라인을 열고 추가 기능에 대 한 호스트 뷰를 가져올 수 있습니다. 이러한 단계는 다음 코드에 나와 있습니다.  

[!code-csharp[Acquiring a host view of the add-in](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInIsAUISample/CSharp/Host/MainWindow.xaml.cs#GetUICode)]
[!code-vb[Acquiring a host view of the add-in](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInIsAUISample/VisualBasic/Host/MainWindow.xaml.vb#GetUICode)]

호스트 응용 프로그램은 일반적인 .NET Framework 추가 기능 모델 코드를 사용 하 여 추가 기능을 활성화 합니다 .이 경우 호스트 응용 프로그램에 호스트 뷰가 암시적으로 반환 됩니다. 그런 다음 호스트 응용 프로그램은 <xref:System.Windows.Controls.UserControl> <xref:System.Windows.Controls.Grid>에서 호스트 뷰 ()를 표시 합니다.  
  
 추가 기능 UI와의 상호 작용을 처리 하는 코드는 추가 기능의 응용 프로그램 도메인에서 실행 됩니다. 이러한 상호 작용에는 다음이 포함됩니다.  
  
- <xref:System.Windows.Controls.Button> 이벤트<xref:System.Windows.Controls.Primitives.ButtonBase.Click> 처리  
  
- 를 <xref:System.Windows.MessageBox>표시 합니다.  
  
 이 작업은 호스트 애플리케이션에서 완전히 격리됩니다.  
  
## <a name="see-also"></a>참고 항목

- [추가 기능 및 확장성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))
- [WPF 추가 기능 개요](wpf-add-ins-overview.md)
