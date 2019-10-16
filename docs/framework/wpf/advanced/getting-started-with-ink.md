---
title: InkCanvas Visual Studio에서 WPF 앱에서 만들기
ms.date: 08/15/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- procedural code in lieu of XAML [WPF]
- XAML [WPF], procedural code in lieu of
- InkCanvas (WPF)
ms.assetid: 760332dd-594a-475d-865b-01659db8cab7
ms.openlocfilehash: d633111c5abc572b0fc27c1a5b32050681504073
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64753015"
---
# <a name="get-started-with-ink-in-wpf"></a>Wpf에서 잉크 시작

Windows Presentation Foundation (WPF)에 쉽게 앱에 디지털 잉크를 통합 하는 잉크 기능이 있습니다.

## <a name="prerequisites"></a>전제 조건

다음 예제를 사용 하려면 먼저 설치 [Microsoft Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)합니다. 또한 기본 WPF 앱을 작성 하는 방법을 알면 도움이 됩니다. WPF 시작 도움말을 참조 하세요. [연습: 내 첫 WPF 데스크톱 응용 프로그램](../getting-started/walkthrough-my-first-wpf-desktop-application.md)합니다.

## <a name="quick-start"></a>빠른 시작

이 섹션에서는 잉크를 수집 하는 간단한 WPF 응용 프로그램을 작성할 수 있습니다.

### <a name="got-ink"></a>잉크 사용

잉크를 지 원하는 WPF 앱을 만들려면:

1. Visual Studio를 엽니다.

2. 새 **WPF 앱**합니다.

   에 **새 프로젝트** 대화 상자에서 확장 된 **설치 됨** > **Visual C#** 또는 **Visual Basic**  >   **Windows 데스크톱** 범주입니다. 다음을 선택 합니다 **WPF 앱 (.NET Framework)** 앱 템플릿. 이름을 입력 하 고 선택한 **확인**합니다.

   Visual Studio는 프로젝트를 만듭니다. 및 *MainWindow.xaml* 디자이너에서 열립니다.

3. 형식 `<InkCanvas/>` 간에 `<Grid>` 태그입니다.

   ![InkCanvas 태그를 사용 하 여 XAML 디자이너](./media/getting-started-with-ink/inkcanvas-xaml.png)

4. 키를 눌러 **F5** 디버거에서 응용 프로그램을 시작 합니다.

5. 스타일러스 또는 마우스를 사용 하 여, 작성할 **hello world** 창의 합니다.

잉크에 해당 하는 12 키 입력을 사용 하 여 "hello world" 응용 프로그램을 작성 했습니다!

### <a name="spice-up-your-app"></a>앱 꾸미기

WPF의 일부 기능을 살펴보겠습니다. 열기 및 닫기 간의 대체 \<창 > 태그에 다음 태그를 사용 하 여:

```xaml
<Page>
  <InkCanvas Name="myInkCanvas" MouseRightButtonUp="RightMouseUpHandler">
    <InkCanvas.Background>
      <LinearGradientBrush>
        <GradientStop Color="Yellow" Offset="0.0" />
          <GradientStop Color="Blue" Offset="0.5" />
            <GradientStop Color="HotPink" Offset="1.0" />
              </LinearGradientBrush>
    </InkCanvas.Background>
  </InkCanvas>
</Page>
```

이 XAML에 잉크 입력 기능 화면에서 배경이 그라데이션 브러시를 만듭니다.

![WPF 앱에서 화면 잉크 입력에서 그라데이션 색](./media/getting-started-with-ink/gradient-colors.png)

### <a name="add-some-code-behind-the-xaml"></a>뒤에 XAML 코드를 추가 합니다.

XAML을 사용 하면 매우 쉽게 사용자 인터페이스를 디자인, 실제 응용 프로그램 이벤트를 처리 하는 코드를 추가 해야 합니다. 마우스의 응답을 마우스 오른쪽 단추로 클릭 하 여 잉크를 확대 하는 간단한 예는 다음과 같습니다.

1. 설정 된 `MouseRightButtonUp` 처리기에 XAML에서:

   [!code-xaml[DigitalInkTopics#3](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#3)]

1. **솔루션 탐색기**, MainWindow.xaml을 확장 하 고 (MainWindow.xaml.vb 또는 MainWindow.xaml.cs) 코드 숨김 파일을 엽니다. 다음 이벤트 처리기 코드를 추가 합니다.

   [!code-csharp[DigitalInkTopics#4](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml.cs#4)]
   [!code-vb[DigitalInkTopics#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window2.xaml.vb#4)]

1. 애플리케이션을 실행합니다. 에 잉크를 일부 추가 마우스 오른쪽 단추로 클릭 또는 스타일러스를 사용 하 여 해당 하는 키를 눌러-대기를 수행 합니다.

   마우스 오른쪽 단추로 클릭할 때마다 디스플레이 확대 합니다.

### <a name="use-procedural-code-instead-of-xaml"></a>XAML 대신 프로시저 코드 사용

프로시저 코드에서 모든 WPF 기능에 액세스할 수 있습니다. 모든 XAML을 전혀 사용 하지 않는 WPF에 대 한 "Hello 잉크 World" 응용 프로그램을 만들려면 다음이 단계를 수행 합니다.

1. Visual Studio에서 새 콘솔 응용 프로그램 프로젝트를 만듭니다.

   에 **새 프로젝트** 대화 상자에서 확장 된 **설치 됨** > **Visual C#** 또는 **Visual Basic**  >   **Windows 데스크톱** 범주입니다. 다음을 선택 합니다 **콘솔 앱 (.NET Framework)** 앱 템플릿. 이름을 입력 하 고 선택한 **확인**합니다.

1. Program.cs 또는 Program.vb 파일에 다음 코드를 붙여 넣습니다.

   [!code-csharp[InkCanvasConsoleApp#1](~/samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasConsoleApp/CSharp/Program.cs#1)]
   [!code-vb[InkCanvasConsoleApp#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/InkCanvasConsoleApp/VisualBasic/Module1.vb#1)]

1. 마우스 오른쪽 단추로 클릭 하 여 PresentationCore, PresentationFramework, 및 WindowsBase 어셈블리에 대 한 참조를 추가 **참조가** 에 **솔루션 탐색기** 선택 하 고 **참조추가**.

   ![참조 관리자 PresentationCore 및 PresentationFramework 표시](./media/getting-started-with-ink/reference-manager-presentationcore-presentationframework.png)

1. 키를 눌러 응용 프로그램을 빌드합니다 **F5**합니다.

## <a name="see-also"></a>참고자료

- [디지털 잉크](digital-ink.md)
- [잉크 수집](collecting-ink.md)
- [필기 인식](handwriting-recognition.md)
- [잉크 저장](storing-ink.md)
