---
title: '연습: 첫 번째 터치 애플리케이션 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- creating a touch-sensitive application [WPF]
- touchscreen applications [WPF], creating
- touch-sensitive applications [WPF], creating
- creating a touchscreen application [WPF]
ms.assetid: d69e602e-9a25-4e24-950b-e89eaa2a906b
ms.openlocfilehash: a915b8e238550eb3d9c1bcbe72d0d05a83a8312c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64605802"
---
# <a name="walkthrough-creating-your-first-touch-application"></a>연습: 첫 번째 터치 애플리케이션 만들기
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램이 터치에 응답할 수 있습니다. 예를 들어, 하나를 사용 하 여 응용 프로그램을 조작할 수 있습니다 또는이 연습에서는 사용자가 이동할 수 있는 응용 프로그램을 만듭니다 원하는 터치 스크린과 같은 터치 감지 장치에서 손가락을 크기를 조정 하거나 터치를 사용 하 여 단일 개체를 회전 합니다.  
  
## <a name="prerequisites"></a>전제 조건  
 이 연습을 완료하려면 다음 구성 요소가 필요합니다.  
  
- Visual Studio.  
  
- Windows Touch를 지 원하는 터치 스크린과 같은 터치식 입력을 허용 하는 장치입니다.  
  
 또한 응용 프로그램을 만드는 방법의 기본적인 이해를 해야 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], 특히 구독 하 고 이벤트를 처리 하는 방법입니다. 자세한 내용은 [연습: 내 첫 WPF 데스크톱 응용 프로그램](../getting-started/walkthrough-my-first-wpf-desktop-application.md)합니다.  
  
## <a name="creating-the-application"></a>애플리케이션 작성  
  
#### <a name="to-create-the-application"></a>애플리케이션을 만들려면  
  
1. Visual Basic 또는 Visual C#에서 `BasicManipulation`이라는 새 WPF 애플리케이션 프로젝트를 만듭니다. 자세한 내용은 [연습: 내 첫 WPF 데스크톱 응용 프로그램](../getting-started/walkthrough-my-first-wpf-desktop-application.md)합니다.  
  
2. MainWindow.xaml의 내용을 다음 XAML을 사용 하 여 대체 합니다.  
  
     이 태그는 빨간색을 포함 하는 간단한 응용 프로그램을 만듭니다 <xref:System.Windows.Shapes.Rectangle> 에 <xref:System.Windows.Controls.Canvas>합니다. 합니다 <xref:System.Windows.UIElement.IsManipulationEnabled%2A> 의 속성을 <xref:System.Windows.Shapes.Rectangle> 조작 이벤트를 받을 수 있도록 true로 설정 됩니다. 응용 프로그램을 등록 합니다 <xref:System.Windows.UIElement.ManipulationStarting>, <xref:System.Windows.UIElement.ManipulationDelta>, 및 <xref:System.Windows.UIElement.ManipulationInertiaStarting> 이벤트입니다. 이동 논리를 포함 하는 이러한 이벤트는 <xref:System.Windows.Shapes.Rectangle> 사용자 조작 경우.  
  
     [!code-xaml[BasicManipulation#UI](~/samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml#ui)]  
  
3. Visual Basic의 경우 MainWindow.xaml의 첫 번째 줄을 사용 하는 경우 대체 `x:Class="BasicManipulation.MainWindow"` 사용 하 여 `x:Class="MainWindow"`입니다.  
  
4. 에 `MainWindow` 클래스를 다음 추가 <xref:System.Windows.UIElement.ManipulationStarting> 이벤트 처리기입니다.  
  
     합니다 <xref:System.Windows.UIElement.ManipulationStarting> 이벤트가 발생할 때 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 터치 감지 입력 개체를 조작 하기 시작 합니다. 코드는 조작의 위치를 기준으로 하도록 지정 합니다 <xref:System.Windows.Window> 설정 하 여는 <xref:System.Windows.Input.ManipulationStartingEventArgs.ManipulationContainer%2A> 속성입니다.  
  
     [!code-csharp[BasicManipulation#ManipulationStarting](~/samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml.cs#manipulationstarting)]
     [!code-vb[BasicManipulation#ManipulationStarting](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicmanipulation/visualbasic/mainwindow.xaml.vb#manipulationstarting)]

5. 에 `MainWindow` 클래스를 다음 추가 <xref:System.Windows.Input.ManipulationDelta> 이벤트 처리기입니다.

     <xref:System.Windows.Input.ManipulationDelta> 이벤트 발생 터치 입력 위치를 변경 하 고 조작 하는 동안 여러 번 발생할 수 있습니다. 이벤트는 손가락 발생 한 후에 발생할 수 있습니다. 예를 들어, 사용자가 화면에서 손가락을 끌 경우는 <xref:System.Windows.Input.ManipulationDelta> 이벤트 손가락 이동으로 여러 번 발생 합니다. 화면에서 손가락을 움직일 때의 <xref:System.Windows.Input.ManipulationDelta> 관성을 시뮬레이션 하기 위해 이벤트가 계속 발생 합니다.

     적용 되는 코드를 <xref:System.Windows.Input.ManipulationDeltaEventArgs.DeltaManipulation%2A> 에 <xref:System.Windows.UIElement.RenderTransform%2A> 의 <xref:System.Windows.Shapes.Rectangle> 는 사용자가 터치 이동 하려면 다음을 입력 합니다. 또한 확인 여부를 <xref:System.Windows.Shapes.Rectangle> 의 범위를 벗어납니다를 <xref:System.Windows.Window> 관성 도중 이벤트가 발생 합니다. 따라서 응용 프로그램 호출 하는 경우는 <xref:System.Windows.Input.ManipulationDeltaEventArgs.Complete%2A?displayProperty=nameWithType> 조작을 종료 하는 방법입니다.

     [!code-csharp[BasicManipulation#ManipulationDelta](~/samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml.cs#manipulationdelta)]
     [!code-vb[BasicManipulation#ManipulationDelta](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicmanipulation/visualbasic/mainwindow.xaml.vb#manipulationdelta)]

6. 에 `MainWindow` 클래스를 다음 추가 <xref:System.Windows.UIElement.ManipulationInertiaStarting> 이벤트 처리기입니다.

     <xref:System.Windows.UIElement.ManipulationInertiaStarting> 사용자 화면에서 손가락을 모두 발생 하면 오류가 발생 합니다. 코드에는 초기 속도 및 이동, 확장 및 회전 사각형의 감속을 설정합니다.

     [!code-csharp[BasicManipulation#ManipulationInertiaStarting](~/samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml.cs#manipulationinertiastarting)]
     [!code-vb[BasicManipulation#ManipulationInertiaStarting](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicmanipulation/visualbasic/mainwindow.xaml.vb#manipulationinertiastarting)]

7. 프로젝트를 빌드하고 실행합니다.

     창에 나타나는 빨간색 사각형이 표시 됩니다.

## <a name="testing-the-application"></a>애플리케이션 테스트
 응용 프로그램을 테스트 하려면 다음 조작을 시도 합니다. 동시에 다음 중 하나 이상 수행할 수 있습니다 note 합니다.

- 이동 하는 <xref:System.Windows.Shapes.Rectangle>, 위에 손가락을 놓고는 <xref:System.Windows.Shapes.Rectangle> 화면에서 손가락을 이동 하 고 합니다.

- 크기를 조정 하려면 합니다 <xref:System.Windows.Shapes.Rectangle>에 두 손가락을 배치를 <xref:System.Windows.Shapes.Rectangle> 더 가깝게 또는 멀리 움직여 다른 손가락 이동 합니다.

- 회전 하는 <xref:System.Windows.Shapes.Rectangle>에 두 손가락을 배치 합니다 <xref:System.Windows.Shapes.Rectangle> 손가락을 서로 회전 및 합니다.

 관성 시킬 이전 조작을 수행 하면 화면에서 손가락을 발생 신속 하 게 합니다. <xref:System.Windows.Shapes.Rectangle> 이동, 크기 조정 또는 중지 하기 전에 몇 초간 회전 계속 됩니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.UIElement.ManipulationStarting?displayProperty=nameWithType>
- <xref:System.Windows.UIElement.ManipulationDelta?displayProperty=nameWithType>
- <xref:System.Windows.UIElement.ManipulationInertiaStarting?displayProperty=nameWithType>