---
title: WPF 앱에서 잉크를 수집 합니다.
ms.date: 08/15/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ink [WPF], collecting
- InkCanvas element [WPF]
- properties [WPF], DrawingAttributes
- collecting digital ink [WPF]
- digital ink [WPF], collecting
- properties [WPF], DefaultDrawingAttributes
- DefaultDrawingAttributes property [WPF]
ms.assetid: 66a3129d-9577-43eb-acbd-56c147282016
ms.openlocfilehash: d2178a4cbf888baaf0ae84b03b3d463b0de658b1
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645724"
---
# <a name="collect-ink"></a>잉크 수집

[Windows Presentation Foundation](../index.md) 플랫폼은 기능의 핵심 요소로서 디지털 잉크를 수집합니다. 이 항목에서는 Windows Presentation Foundation (WPF)에서 잉크를 수집 하기 위한 메서드를 설명합니다.

## <a name="prerequisites"></a>전제 조건

다음 예제를 사용 하려면 먼저 설치 해야 Visual Studio 및 [!INCLUDE[TLA2#tla_winfxsdk](../../../../includes/tla2sharptla-winfxsdk-md.md)]합니다. WPF에 대 한 응용 프로그램을 작성 하는 방법을 이해 합니다. WPF를 사용 하 여 시작 하는 방법에 대 한 자세한 내용은 참조 하세요. [연습: 내 첫 WPF 데스크톱 응용 프로그램](../getting-started/walkthrough-my-first-wpf-desktop-application.md)합니다.

## <a name="use-the-inkcanvas-element"></a>InkCanvas 요소 사용

<xref:System.Windows.Controls.InkCanvas?displayProperty=fullName> WPF에서 잉크를 수집 하는 가장 쉬운 방법은 요소를 제공 합니다. 사용 하 여는 <xref:System.Windows.Controls.InkCanvas> 받고 잉크 입력을 표시 하는 요소입니다. 일반적으로 스타일러스를 사용하여 잉크를 입력합니다.이 스타일러스는 디지타이저와 상호 작용하여 잉크 스트로크를 생성합니다. 또한 스타일러스 대신 마우스를 사용할 수도 있습니다. 생성된 된 스트로크 표현 <xref:System.Windows.Ink.Stroke> , 이러한 개체를 프로그래밍 방식으로 및 사용자가 입력 조작할 수 있습니다. 합니다 <xref:System.Windows.Controls.InkCanvas> 선택, 수정 또는 기존 삭제 하면 <xref:System.Windows.Ink.Stroke>합니다.

XAML을 사용 하 여 설정할 수 있습니다 잉크 컬렉션을 추가 하는 것 처럼 쉽게를 **InkCanvas** 트리에 요소입니다. 다음 예제에서는 추가 <xref:System.Windows.Controls.InkCanvas> Visual Studio에서 만든 기본 WPF 프로젝트에:

[!code-xaml[DigitalInkTopics#6](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#6)]

합니다 **InkCanvas** 요소는 거의 모든 형식의 XAML 요소에 잉크 주석 기능을 추가할 수 있도록 자식 요소를 포함할 수도 있습니다. 예를 들어 텍스트 요소에 잉크 입력 기능을 추가 하려면 단순히 있도록 자식은 <xref:System.Windows.Controls.InkCanvas>:

[!code-xaml[DigitalInkTopics#5](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#5)]

잉크로 이미지를 표시 하기 위한 지원을 추가 하는 것은 쉽습니다.

[!code-xaml[DigitalInkTopics#7](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#7)]

### <a name="inkcollection-modes"></a>InkCollection 모드

합니다 <xref:System.Windows.Controls.InkCanvas> 모드를 통해 다양 한 입력에 대 한 지원을 제공 해당 <xref:System.Windows.Controls.InkCanvas.EditingMode%2A> 속성입니다.

### <a name="manipulate-ink"></a>잉크 조작

<xref:System.Windows.Controls.InkCanvas> 많은 잉크 편집 작업에 대 한 지원을 제공 합니다. 예를 들어 <xref:System.Windows.Controls.InkCanvas> 지원 펜 뒤쪽 지우기 및 요소에 기능을 추가 하려면 추가 코드 없이 필요 합니다.

#### <a name="selection"></a>선택

선택 모드 설정 간단 하 게 설정 합니다 <xref:System.Windows.Controls.InkCanvasEditingMode> 속성을 **선택**합니다.

값에 따라 편집 모드를 설정 하는 다음 코드는 <xref:System.Windows.Forms.CheckBox>:

[!code-csharp[DigitalInkTopics#8](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#8)]
[!code-vb[DigitalInkTopics#8](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#8)]

#### <a name="drawingattributes"></a>DrawingAttributes

사용 된 <xref:System.Windows.Ink.Stroke.DrawingAttributes%2A> 잉크 스트로크의 모양을 변경 하는 속성입니다. 예를 들어 합니다 <xref:System.Windows.Ink.DrawingAttributes.Color%2A> 소속 <xref:System.Windows.Ink.DrawingAttributes> 렌더링 된 색으로 설정 <xref:System.Windows.Ink.Stroke>합니다.

다음 예제에서는 빨간색 선택한 스트로크의 색을 변경합니다.

[!code-csharp[DigitalInkTopics#9](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#9)]
[!code-vb[DigitalInkTopics#9](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#9)]

### <a name="defaultdrawingattributes"></a>DefaultDrawingAttributes

합니다 <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> 높이, 너비 및에서 만들 스트로크의 색 같은 속성에 대 한 액세스를 제공 하는 속성을 <xref:System.Windows.Controls.InkCanvas>입니다. 변경 하면 합니다 <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>, 이후 모든 스트로크를 입력 합니다 <xref:System.Windows.Controls.InkCanvas> 새 속성 값을 사용 하 여 렌더링 됩니다.

수정 하는 것 외에도 합니다 <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> 코드 숨김 파일에 XAML 구문을 지정 하는 데 사용할 수 있습니다 <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> 속성입니다.

다음 예제에서는 설정 하는 방법에 설명 합니다 <xref:System.Windows.Ink.DrawingAttributes.Color%2A> 속성입니다. 이 코드를 사용 하려면 Visual Studio에서 "helloinkcanvas" 새 WPF 프로젝트를 만듭니다. 코드를 대체 합니다 *MainWindow.xaml* 를 다음 코드로 파일:

[!code-xaml[HelloInkCanvas#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HelloInkCanvas/CSharp/Window1.xaml#1)]

MainWindow 클래스 내에서 파일의 코드를 다음에 다음 단추 이벤트 처리기를 추가 합니다.

[!code-csharp[HelloInkCanvas#2](~/samples/snippets/csharp/VS_Snippets_Wpf/HelloInkCanvas/CSharp/Window1.xaml.cs#2)]

이 코드를 복사한 후 눌러 **F5** 디버거에서 프로그램을 실행 하려면 Visual Studio에서.

표시 하는 방법을 <xref:System.Windows.Controls.StackPanel> 위쪽에 단추를 배치 합니다 <xref:System.Windows.Controls.InkCanvas>합니다. 단추 위에 잉크로 채우려고 시도 합니다 <xref:System.Windows.Controls.InkCanvas> 수집 하 고 단추 뒤에서 잉크를 렌더링 합니다. 단추의 형제 이기 때문에 이것이 <xref:System.Windows.Controls.InkCanvas> 자식이 아니라 합니다. 또한 단추가 z 순서에서 더 앞서기 때문에 잉크가 단추 뒤에서 렌더링됩니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Ink.DrawingAttributes>
- <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>
- <xref:System.Windows.Ink>
