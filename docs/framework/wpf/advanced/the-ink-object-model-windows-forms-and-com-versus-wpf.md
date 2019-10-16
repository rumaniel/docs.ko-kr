---
title: '잉크 개체 모델: Windows Forms/COM 및 WPF'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- enabling ink [WPF]
- InkCanvas control [WPF]
- ink object model [WPF]
- tablet pen [WPF], events [WPF]
- ink [WPF], enabling
- events [WPF], tablet pen
ms.assetid: 577835be-b145-4226-8570-1d309e9b3901
ms.openlocfilehash: 68003943041fe0ba405eff1236c43a8e7e9c2b71
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62051678"
---
# <a name="the-ink-object-model-windows-forms-and-com-versus-wpf"></a>잉크 개체 모델: Windows Forms/COM 및 WPF

디지털 잉크를 지 원하는 기본적으로 세 가지 플랫폼 가지: Tablet PC Windows Forms 플랫폼, Tablet PC COM 플랫폼 및 Windows Presentation Foundation (WPF) 플랫폼입니다.  Windows Forms 및 COM 플랫폼 공유에 대 한 유사한 개체 모델에 있지만 개체 모델을 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 플랫폼 크게 다릅니다.  이 항목에서는 개체 모델을 사용 하 여 작동 하는 개발자가 더 잘 이해할 수 다른 있도록 대략적으로 차이점을 설명 합니다.  
  
## <a name="enabling-ink-in-an-application"></a>응용 프로그램에서 잉크를 사용 하도록 설정  
 세 플랫폼 모두 개체 및 태블릿 펜에서 입력을 수신할 응용 프로그램을 사용 하는 컨트롤을 제공 합니다.  와 함께 제공 되는 Windows Forms 및 COM 플랫폼 [Microsoft.Ink.InkPicture](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583740(v=vs.90))를 [Microsoft.Ink.InkEdit](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552265(v=vs.90))하십시오 [Microsoft.Ink.InkOverlay](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552322(v=vs.90)) 및 [ Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90)) 클래스입니다.  [Microsoft.Ink.InkPicture](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583740(v=vs.90)) 하 고 [Microsoft.Ink.InkEdit](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552265(v=vs.90)) 추가할 수 있는 컨트롤은 잉크를 수집 하려면 응용 프로그램입니다.  합니다 [Microsoft.Ink.InkOverlay](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552322(v=vs.90)) 하 고 [Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90)) 기존 창 잉크 지원 창과 사용자 지정 컨트롤에 연결할 수 있습니다.  
  
 WPF 플랫폼에는 <xref:System.Windows.Controls.InkCanvas> 제어 합니다.  추가할 수 있습니다는 <xref:System.Windows.Controls.InkCanvas> 응용 프로그램에 잉크를 즉시 수집을 시작 합니다. 사용 하 여는 <xref:System.Windows.Controls.InkCanvas>, 사용자 수를 복사, 선택 및 잉크 크기를 조정 합니다.  다른 컨트롤을 추가할 수는 <xref:System.Windows.Controls.InkCanvas>, 한 사용자 수 해당 컨트롤에 비해 너무 합니다.  잉크 지원 사용자 지정 컨트롤을 추가 하 여 만들 수 있습니다는 <xref:System.Windows.Controls.InkPresenter> 하 고 해당 스타일러스 지점을 수집 합니다.  
  
 다음 표에서 응용 프로그램에서 잉크를 사용 하도록 설정 하는 방법에 대 한 자세한 내용을 보려면 위치를 나열 합니다.  
  
|이 작업을 수행 하는 중...|WPF 플랫폼...|Windows Forms/COM 플랫폼에서 하는 중...|  
|-----------------|--------------------------|------------------------------------------|  
|잉크 지원 컨트롤을 응용 프로그램 추가|참조 [잉크 시작](getting-started-with-ink.md)합니다.|참조 [자동 클레임 구성 샘플](/windows/desktop/tablet/auto-claims-form-sample)|  
|사용자 지정 컨트롤에서 잉크를 사용 하도록 설정|참조 [만드는 잉크 입력 컨트롤](creating-an-ink-input-control.md)합니다.|참조 [잉크 클립보드 샘플](/windows/desktop/tablet/ink-clipboard-sample)합니다.|  
  
## <a name="ink-data"></a>잉크 데이터  
 Windows Forms 및 COM 플랫폼에서 [Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90))를 [Microsoft.Ink.InkOverlay](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552322(v=vs.90))하십시오 [Microsoft.Ink.InkEdit](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552265(v=vs.90)), 및 [ Microsoft.Ink.InkPicture](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583740(v=vs.90)) 각 노출 된 [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) 개체입니다. 합니다 [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) 개체 하나 이상에 대 한 데이터가 [Microsoft.Ink.Stroke](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552692(v=vs.90)) 개체 및 공용 메서드와 해당 스트로크를 조작 하는 속성을 노출 합니다.  합니다 [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) 개체에 포함 된; 스트로크의 수명을 관리 합니다 [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) 개체를 만들고 소유 하는 스트로크를 삭제 합니다.  각 [Microsoft.Ink.Stroke](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552692(v=vs.90)) 부모 내에서 고유한 식별자 [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) 개체입니다.  
  
 WPF 플랫폼에는 <xref:System.Windows.Ink.Stroke?displayProperty=nameWithType> 소유 하 고 고유의 수명을 관리 하는 클래스입니다. 그룹 <xref:System.Windows.Ink.Stroke> 에서 개체를 함께 수집을 <xref:System.Windows.Ink.StrokeCollection>, 테스트, 지우기, 변환 및 잉크를 직렬화 하는 작업에 도달 하는 메서드를 제공 일반적인 잉크 데이터 관리 작업 등입니다. A <xref:System.Windows.Ink.Stroke> 0 개 이상의에 속할 수 있습니다 <xref:System.Windows.Ink.StrokeCollection> 개체에서 시간을 제공 합니다.  대신를 [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) 개체를 <xref:System.Windows.Controls.InkCanvas> 및 <xref:System.Windows.Controls.InkPresenter> 포함을 <xref:System.Windows.Ink.StrokeCollection?displayProperty=nameWithType>입니다.  
  
 다음 그림은 두 데이터 잉크 개체 모델을 비교합니다.  Windows Forms 및 COM 플랫폼에서의 [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) 개체의 수명을 제한 합니다 [Microsoft.Ink.Stroke](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552692(v=vs.90)) 개체 및 개별 스트로크 속한 스타일러스 패킷을 합니다.  동일한 두 개 이상의 스트로크 참조할 수 있습니다 [Microsoft.Ink.DrawingAttributes](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583636(v=vs.90)) 다음 그림에 나와 있는 것 처럼 개체입니다.  
  
 ![COM에 대 한 잉크 개체 모델의 다이어그램&#47;Winforms 합니다. ](./media/ink-inkownsstrokes.png "Ink_InkOwnsStrokes")  
  
 에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]각각 <xref:System.Windows.Ink.Stroke?displayProperty=nameWithType> 는 것이 있으면 해당 참조를으로 존재 하는 공용 언어 런타임 개체입니다.  각 <xref:System.Windows.Ink.Stroke> 참조를 <xref:System.Windows.Input.StylusPointCollection> 고 <xref:System.Windows.Ink.DrawingAttributes?displayProperty=nameWithType> 개체도 공용 언어 런타임 개체입니다.  
  
 ![WPF에 대 한 잉크 개체 모델의 다이어그램입니다. ](./media/ink-wpfinkobjectmodel.png "Ink_WPFInkObjectModel")  
  
 다음 표에서 비교에 몇 가지 일반적인 작업을 수행 하는 방법의 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 플랫폼 및 Windows Forms 및 COM 플랫폼입니다.  
  
|작업|Windows Presentation Foundation|Windows Forms 및 COM|  
|----------|-------------------------------------|---------------------------|  
|잉크 저장|<xref:System.Windows.Ink.StrokeCollection.Save%2A>|[Microsoft.Ink.Ink.Save](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms571335(v=vs.90))|  
|잉크를 로드 합니다.|만들기는 <xref:System.Windows.Ink.StrokeCollection> 사용 하 여는 <xref:System.Windows.Ink.StrokeCollection.%23ctor%2A> 생성자입니다.|[Microsoft.Ink.Ink.Load](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms569609(v=vs.90))|  
|적중 테스트|<xref:System.Windows.Ink.StrokeCollection.HitTest%2A>|[Microsoft.Ink.Ink.HitTest](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms571330(v=vs.90))|  
|잉크를 복사 합니다.|<xref:System.Windows.Controls.InkCanvas.CopySelection%2A>|[Microsoft.Ink.Ink.ClipboardCopy](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms571316(v=vs.90))|  
|잉크를 붙여 넣습니다.|<xref:System.Windows.Controls.InkCanvas.Paste%2A>|[Microsoft.Ink.Ink.ClipboardPaste](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms571318(v=vs.90))|  
|스트로크의 컬렉션에서 사용자 지정 속성에 액세스|<xref:System.Windows.Ink.StrokeCollection.AddPropertyData%2A> (속성 내부적으로 저장 되 고를 통해 액세스할 <xref:System.Windows.Ink.StrokeCollection.AddPropertyData%2A>하십시오 <xref:System.Windows.Ink.StrokeCollection.RemovePropertyData%2A>, 및 <xref:System.Windows.Ink.StrokeCollection.ContainsPropertyData%2A>)|사용 하 여 [Microsoft.Ink.Ink.ExtendedProperties](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms582214(v=vs.90))|  
  
### <a name="sharing-ink-between-platforms"></a>플랫폼 간 잉크를 공유합니다.  
 플랫폼 잉크 데이터에 대 한 다양 한 개체 모델을 갖지만 플랫폼 간의 데이터 공유는 매우 쉽습니다. 다음 예제에서는 Windows Forms 응용 프로그램에서 잉크를 저장 하 고 잉크를 Windows Presentation Foundation 응용 프로그램을 로드 합니다.  
  
 [!code-csharp[WinFormWPFInk#UsingWinforms](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwinforms)]
 [!code-vb[WinFormWPFInk#UsingWinforms](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwinforms)]  
[!code-csharp[WinFormWPFInk#SaveWinforms](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#savewinforms)]
[!code-vb[WinFormWPFInk#SaveWinforms](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#savewinforms)]  
  
 [!code-csharp[WinFormWPFInk#UsingWPF](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwpf)]
 [!code-vb[WinFormWPFInk#UsingWPF](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwpf)]  
[!code-csharp[WinFormWPFInk#LoadWPF](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#loadwpf)]
[!code-vb[WinFormWPFInk#LoadWPF](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#loadwpf)]  
  
 다음 예제에서는 Windows Presentation Foundation 응용 프로그램에서 잉크를 저장 하 고 잉크를 Windows Forms 응용 프로그램을 로드 합니다.  
  
 [!code-csharp[WinFormWPFInk#UsingWPF](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwpf)]
 [!code-vb[WinFormWPFInk#UsingWPF](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwpf)]  
[!code-csharp[WinFormWPFInk#SaveWPF](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#savewpf)]
[!code-vb[WinFormWPFInk#SaveWPF](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#savewpf)]  
  
 [!code-csharp[WinFormWPFInk#UsingWinforms](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwinforms)]
 [!code-vb[WinFormWPFInk#UsingWinforms](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwinforms)]  
[!code-csharp[WinFormWPFInk#LoadWinforms](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#loadwinforms)]
[!code-vb[WinFormWPFInk#LoadWinforms](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#loadwinforms)]
## <a name="events-from-the-tablet-pen"></a>태블릿 펜의 이벤트  

 합니다 [Microsoft.Ink.InkOverlay](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552322(v=vs.90)), [Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90)), 및 [Microsoft.Ink.InkPicture](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583740(v=vs.90)) 플랫폼을 Windows Forms 및 COM에서 이벤트를 받을 때 사용자 입력 데이터를 펜입니다. 합니다 [Microsoft.Ink.InkOverlay](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552322(v=vs.90)) 하거나 [Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90)) 창 또는 컨트롤을 연결 되어 있고 태블릿 입력된 데이터에서 발생 하는 이벤트를 구독할 수 있습니다. 이러한 이벤트가 발생 한 스레드 펜, 마우스를 사용 하 여 이러한 이벤트는 발생 하는 여부에 따라 달라 집니다 또는 프로그래밍 방식으로 합니다. 이러한 이벤트와 관련 하 여 스레딩에 대 한 자세한 내용은 참조 하세요. [일반적인 스레딩 고려 사항](/windows/desktop/tablet/general-threading-considerations) 하 고 [이벤트가 발생할 수 있는 스레드가](/windows/desktop/tablet/threads-on-which-an-event-can-fire)합니다.  
  
 Windows Presentation Foundation 플랫폼을 <xref:System.Windows.UIElement> 클래스에 펜 입력에 대 한 이벤트입니다. 이 스타일러스 이벤트의 전체 집합을 노출 하는 모든 컨트롤을 의미 합니다.  스타일러스 이벤트는 터널링/버블링 이벤트 쌍 및 항상 응용 프로그램 스레드에서 발생 합니다.  자세한 내용은 [라우트된 이벤트 개요](routed-events-overview.md)합니다.  
  
 다음 다이어그램은 스타일러스 이벤트를 발생 시키는 클래스에 대 한 개체 모델을 비교 합니다. Windows Presentation Foundation 개체 모델에만 버블링 이벤트를 터널링 이벤트 항목을 보여 줍니다.  
  
 ![WPF 및 Winforms의 스타일러스 이벤트 다이어그램입니다. ](./media/ink-stylusevents.png "Ink_StylusEvents")  
  
## <a name="pen-data"></a>펜 데이터  
 세 플랫폼 모두를 가로채 고 태블릿 펜의 제공 되는 데이터를 조작 하는 방법을 제공 합니다.  Windows Forms 및 COM 플랫폼에서 이렇게 만들어를 [Microsoft.StylusInput.RealTimeStylus](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms585724(v=vs.90))창 또는 컨트롤을 연결, 구현 하는 클래스를 생성 하는 [ Microsoft.StylusInput.IStylusSyncPlugin](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms575201(v=vs.90)) 나 [Microsoft.StylusInput.IStylusAsyncPlugin](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms575194(v=vs.90)) 인터페이스입니다. 사용자 지정 플러그 인은 플러그 인 컬렉션에 추가 합니다 [Microsoft.StylusInput.RealTimeStylus](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms585724(v=vs.90))합니다. 이 개체 모델에 대 한 자세한 내용은 참조 하세요. [StylusInput Api의 아키텍처](/windows/desktop/tablet/architecture-of-the-stylusinput-apis)합니다.  
  
 에 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 플랫폼을 <xref:System.Windows.UIElement> 플러그 인을 디자인이 비슷하며의 컬렉션을 노출 하는 클래스는 [Microsoft.StylusInput.RealTimeStylus](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms585724(v=vs.90))합니다.  데이터를 가로채도록 펜에서 상속 되는 클래스를 만듭니다 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 개체를 추가 하 고는 <xref:System.Windows.UIElement.StylusPlugIns%2A> 의 컬렉션을 <xref:System.Windows.UIElement>. 이 상호 작용에 대 한 자세한 내용은 참조 하세요. [스타일러스에서 입력 가로채기](intercepting-input-from-the-stylus.md)합니다.  
  
 모든 플랫폼에서 스레드 풀 스타일러스 이벤트를 통해 잉크 데이터를 수신 및 응용 프로그램 스레드에 보냅니다.  COM 및 Windows 플랫폼에서 스레딩에 대 한 자세한 내용은 참조 하세요. [StylusInput Api에 대 한 스레딩 고려 사항](/windows/desktop/tablet/threading-considerations-for-the-stylusinput-apis)합니다.  Windows 프레젠테이션 소프트웨어에서 스레딩에 대 한 자세한 내용은 참조 하세요. [잉크 스레딩 모델](the-ink-threading-model.md)합니다.  
  
 다음 그림에서는 펜 스레드 풀에서 펜 데이터를 수신 하는 클래스 개체 모델을 비교 합니다.  
  
 ![StylusPlugin 모델 WPF 및 Winforms의 다이어그램입니다. ](./media/ink-stylusplugins.png "Ink_StylusPlugins")
