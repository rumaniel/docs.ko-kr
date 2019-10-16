---
title: '방법: UI를 반환하는 추가 기능 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- creating an add-in that returns a UI [WPF]
- implementing add-in pipeline segments [WPF]
- add-in [WPF], returns a UI
ms.assetid: 57f274b7-4c66-4b72-92eb-81939a393776
ms.openlocfilehash: e32987355a6c7ad32b5e0e8522dc4daa63783fdd
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291250"
---
# <a name="how-to-create-an-add-in-that-returns-a-ui"></a>방법: UI를 반환하는 추가 기능 만들기
이 예제에서는 Windows Presentation Foundation (WPF)를 호스트 WPF 독립 실행형 응용 프로그램에 반환 하는 추가 기능을 만드는 방법을 보여 줍니다.  
  
 추가 기능은 WPF 사용자 정의 컨트롤인 UI를 반환 합니다. 이 사용자 정의 컨트롤의 콘텐츠는 클릭했을 때 메시지 상자를 표시하는 하나의 단추입니다. WPF 독립 실행형 응용 프로그램은 추가 기능을 호스팅하고 추가 기능에서 반환 하는 사용자 정의 컨트롤을 주 응용 프로그램 창의 콘텐츠로 표시 합니다.  
  
 **필수 구성 요소**  
  
 이 예제에서는이 시나리오를 사용 하도록 설정 하는 .NET Framework 추가 기능 모델에 대 한 WPF 확장을 강조 표시 하 고 다음을 가정 합니다.  
  
- 파이프라인, 추가 기능 및 호스트 개발을 포함 하 여 .NET Framework 추가 기능 모델에 대 한 지식. 이러한 개념을 잘 모르는 경우 [추가 기능 및 확장성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))을 참조 하세요. 파이프라인, 추가 기능 및 호스트 응용 프로그램을 구현 하는 방법을 보여 주는 자습서를 보려면 [ 연습: 확장 가능한 응용 프로그램 @ no__t-0을 만듭니다.  
  
- 다음 위치에서 찾을 수 있는 .NET Framework 추가 기능 모델에 대 한 WPF 확장 정보 [WPF 추가 기능 개요](wpf-add-ins-overview.md).  
  
## <a name="example"></a>예제  
 WPF UI를 반환 하는 추가 기능을 만들려면 각 파이프라인 세그먼트, 추가 기능 및 호스트 응용 프로그램에 대 한 특정 코드가 필요 합니다.  

<a name="Contract"></a>   
## <a name="implementing-the-contract-pipeline-segment"></a>계약 파이프라인 세그먼트 구현  
 계약에서 UI를 반환 하기 위해 메서드를 정의 해야 하며, 반환 값은 <xref:System.AddIn.Contract.INativeHandleContract> 형식 이어야 합니다. 이는 다음 코드에서 `IWPFAddInContract` 계약의 `GetAddInUI` 메서드에서 보여 줍니다.  
  
 [!code-csharp[SimpleAddInReturnsAUISample#ContractCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/Contracts/IWPFAddInContract.cs#contractcode)]
 [!code-vb[SimpleAddInReturnsAUISample#ContractCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/Contracts/IWPFAddInContract.vb#contractcode)]  
  
<a name="AddInView"></a>   
## <a name="implementing-the-add-in-view-pipeline-segment"></a>추가 기능 뷰 파이프라인 세그먼트 구현  
 추가 기능은에서 제공 하는 Ui를 <xref:System.Windows.FrameworkElement>의 서브 클래스로 구현 하기 때문에 `IWPFAddInView.GetAddInUI`과 상관 관계가 있는 추가 기능 뷰의 메서드는 <xref:System.Windows.FrameworkElement> 형식의 값을 반환 해야 합니다. 다음 코드에서는 인터페이스로 구현된 계약의 추가 기능 뷰를 보여 줍니다.  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInViewCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/AddInViews/IWPFAddInView.cs#addinviewcode)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInViewCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/AddInViews/IWPFAddInView.vb#addinviewcode)]  
  
<a name="AddInSideAdapter"></a>   
## <a name="implementing-the-add-in-side-adapter-pipeline-segment"></a>추가 기능 쪽 어댑터 파이프라인 세그먼트 구현  
 계약 메서드는 <xref:System.AddIn.Contract.INativeHandleContract>을 반환 하지만 추가 기능에서 <xref:System.Windows.FrameworkElement>을 반환 합니다 (추가 기능 뷰에서 지정). 따라서 <xref:System.Windows.FrameworkElement>은 격리 경계를 통과 하기 전에 <xref:System.AddIn.Contract.INativeHandleContract>로 변환 되어야 합니다. 이 작업은 다음 코드와 같이 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>을 호출 하 여 추가 기능 측 어댑터에 의해 수행 됩니다.  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInSideAdapterCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/AddInSideAdapters/WPFAddIn_ViewToContractAddInSideAdapter.cs#addinsideadaptercode)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInSideAdapterCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/AddInSideAdapters/WPFAddIn_ViewToContractAddInSideAdapter.vb#addinsideadaptercode)]  
  
<a name="HostView"></a>   
## <a name="implementing-the-host-view-pipeline-segment"></a>호스트 뷰 파이프라인 세그먼트 구현  
 호스트 응용 프로그램에 <xref:System.Windows.FrameworkElement>이 표시 되기 때문에 `IWPFAddInHostView.GetAddInUI`과 상관 관계가 있는 호스트 뷰의 메서드는 <xref:System.Windows.FrameworkElement> 형식의 값을 반환 해야 합니다. 다음 코드에서는 인터페이스로 구현된 계약의 호스트 뷰를 보여 줍니다.  
  
 [!code-csharp[SimpleAddInReturnsAUISample#HostViewCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/HostViews/IWPFAddInHostView.cs#hostviewcode)]
 [!code-vb[SimpleAddInReturnsAUISample#HostViewCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/HostViews/IWPFAddInHostView.vb#hostviewcode)]  
  
<a name="HostSideAdapter"></a>   
## <a name="implementing-the-host-side-adapter-pipeline-segment"></a>호스트 측 어댑터 파이프라인 세그먼트 구현  
 계약 메서드는 <xref:System.AddIn.Contract.INativeHandleContract>을 반환 하지만 호스트 응용 프로그램에는 호스트 보기에 지정 된 대로 <xref:System.Windows.FrameworkElement>이 필요 합니다. 따라서 <xref:System.AddIn.Contract.INativeHandleContract>은 격리 경계를 넘는 후 <xref:System.Windows.FrameworkElement>로 변환 되어야 합니다. 이 작업은 다음 코드에 표시 된 것 처럼 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>을 호출 하 여 호스트 측 어댑터에 의해 수행 됩니다.  
  
 [!code-csharp[SimpleAddInReturnsAUISample#HostSideAdapterCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/HostSideAdapters/WPFAddIn_ContractToViewHostSideAdapter.cs#hostsideadaptercode)]
 [!code-vb[SimpleAddInReturnsAUISample#HostSideAdapterCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/HostSideAdapters/WPFAddIn_ContractToViewHostSideAdapter.vb#hostsideadaptercode)]  
  
<a name="AddIn"></a>   
## <a name="implementing-the-add-in"></a>추가 기능 구현  
 추가 기능 쪽 어댑터와 추가 기능 뷰를 만든 후 추가 기능 (`WPFAddIn1.AddIn`)은 <xref:System.Windows.FrameworkElement> 개체를 반환 하는 `IWPFAddInView.GetAddInUI` 메서드를 구현 해야 합니다 (이 예제에서는 <xref:System.Windows.Controls.UserControl>). @No__t-0 `AddInUI`의 구현은 다음 코드에 나와 있습니다.  
  
 [!code-xaml[SimpleAddInReturnsAUISample#AddInUIMarkup](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/WPFAddIn1/AddInUI.xaml#addinuimarkup)]  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInUICodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/WPFAddIn1/AddInUI.xaml.cs#addinuicodebehind)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInUICodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/WPFAddIn1/AddInUI.xaml.vb#addinuicodebehind)]  
  
 추가 기능에의 한 `IWPFAddInView.GetAddInUI` 구현은 다음 코드와 같이 `AddInUI`의 새 인스턴스를 반환 하기만 하면 됩니다.  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/WPFAddIn1/AddIn.cs#addincode)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/WPFAddIn1/AddIn.vb#addincode)]  
  
<a name="App"></a>   
## <a name="implementing-the-host-application"></a>호스트 애플리케이션 구현  
 호스트 쪽 어댑터와 호스트 뷰를 만든 상태에서 호스트 응용 프로그램은 .NET Framework 추가 기능 모델을 사용 하 여 파이프라인을 열고, 추가 기능에 대 한 호스트 뷰를 가져오고, `IWPFAddInHostView.GetAddInUI` 메서드를 호출할 수 있습니다. 이러한 단계는 다음 코드에 나와 있습니다.  
  
 [!code-csharp[SimpleAddInReturnsAUISample#GetUICode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/Host/MainWindow.xaml.cs#getuicode)]
 [!code-vb[SimpleAddInReturnsAUISample#GetUICode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/Host/MainWindow.xaml.vb#getuicode)]  
  
## <a name="see-also"></a>참조

- [추가 기능 및 확장성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))
- [WPF 추가 기능 개요](wpf-add-ins-overview.md)
