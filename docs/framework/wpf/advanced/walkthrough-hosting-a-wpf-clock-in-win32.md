---
title: '연습: Win32에서 WPF 시계 호스팅'
ms.date: 03/30/2017
helpviewer_keywords:
- interoperability [WPF], tutorials
- Win32 code [WPF], WPF interoperation
- interoperability [WPF], Win32
ms.assetid: 555e55a7-0851-4ec8-b1c6-0acba7e9b648
ms.openlocfilehash: 27e1a2e88beeacf8c2cd98f61b11542ee2341e8f
ms.sourcegitcommit: 1e7ac70be1b4d89708c0d9552897515f2cbf52c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433972"
---
# <a name="walkthrough-hosting-a-wpf-clock-in-win32"></a>연습: Win32에서 WPF 시계 호스팅

응용 프로그램 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 내 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 에 배치 하려면 <xref:System.Windows.Interop.HwndSource> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠를 포함 하는 HWND를 제공 하는를 사용 합니다. 먼저를 만들어 <xref:System.Windows.Interop.HwndSource>CreateWindow와 유사한 매개 변수를 제공 합니다. 그런 다음, 내부 <xref:System.Windows.Interop.HwndSource> 에서 원하는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠에 대 한 정보를 알려 줍니다. 마지막으로에서 <xref:System.Windows.Interop.HwndSource>HWND를 가져옵니다. 이 연습에서는 운영 체제 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] **날짜 및 시간 속성** 대화 상자를 다시 구현 하는 혼합 내부 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 응용 프로그램을 만드는 방법을 보여 줍니다.

## <a name="prerequisites"></a>전제 조건

[WPF 및 Win32 상호 운용성을](wpf-and-win32-interoperation.md)참조 하세요.

## <a name="how-to-use-this-tutorial"></a>이 자습서를 사용하는 방법

이 자습서는 상호 운용 애플리케이션을 생성하는 중요한 단계에 대해 중점적으로 설명합니다. 이 자습서는 [Win32 클록 상호 운용성 샘플](https://go.microsoft.com/fwlink/?LinkID=160051)샘플에서 지원 되지만이 샘플은 최종 제품을 반영 합니다. 이 자습서에서는 기존 프로젝트와 같은 기존 프로젝트를 사용 하 여 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 시작 하 고 응용 프로그램에 호스팅된 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 를 추가 하는 것 처럼 단계를 문서화 합니다. 최종 제품을 [Win32 클록 상호 운용 샘플과](https://go.microsoft.com/fwlink/?LinkID=160051)비교할 수 있습니다.

## <a name="a-walkthrough-of-windows-presentation-framework-inside-win32-hwndsource"></a>Win32 내에서 Windows Presentation Framework의 연습(HwndSource)

다음 그래픽에서는 이 자습서의 의도된 최종 제품을 보여 줍니다.

![날짜 및 시간 속성 대화 상자를 보여 주는 스크린샷](./media/walkthrough-hosting-a-wpf-clock-in-win32/date-time-properties-dialog.png)

Visual Studio에서 C++ Win32 프로젝트를 만들고 대화 상자 편집기를 사용 하 여 다음을 만드는 방법으로이 대화 상자를 다시 만들 수 있습니다.

![다시 생성 한 날짜 및 시간 속성 대화 상자](./media/walkthrough-hosting-a-wpf-clock-in-win32/recreated-date-time-properties-dialog.png)

를 사용 하 여를 사용할 필요는 없으며 프로그램을 작성 C++ [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 하는 데를 사용할 필요는 없지만,이 작업을 수행 하는 일반적인 방법은 물론 단계별 자습서 설명에 적합 합니다. [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] <xref:System.Windows.Interop.HwndSource>

대화 상자에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 시계를 추가 하려면 5 개의 특정 하위 단계를 수행 해야 합니다.

1. [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 에서 프로젝트[!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)]설정을 변경 하 여 프로젝트에서 관리 코드 ( **/clr**)를 호출할 수 있도록 합니다.

2. 별도의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] DLL에를 <xref:System.Windows.Controls.Page> 만듭니다.

3. 내 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.Page>에를 넣습니다 .<xref:System.Windows.Interop.HwndSource>

4. 속성<xref:System.Windows.Interop.HwndSource.Handle%2A> 을 사용 하 여 <xref:System.Windows.Controls.Page> 해당에 대 한 HWND를 가져옵니다.

5. [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 큰[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 응용 프로그램 내에서 HWND를 넣을 위치를 결정 하는 데 사용

## <a name="clr"></a>/clr

첫 번째 단계는 관리 코드를 호출할 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 수 있는 프로젝트로이 관리 되지 않는 프로젝트를 설정 하는 것입니다. /Clr 컴파일러 옵션을 사용 합니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].이 옵션을 사용 하 여 필요한 dll에 연결 하 고에 사용할 Main 메서드를 조정 합니다.

C++ 프로젝트 내에서 관리 코드를 사용 하도록 설정 하려면 다음을 수행 합니다. Win32clock 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다. **일반** 속성 페이지 (기본값)에서 공용 언어 런타임 지원을로 `/clr`변경 합니다.

다음으로에 필요한 Dll에 대 한 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]참조를 추가 합니다. PresentationCore, PresentationFramework, Uiautomationprovider.dll 및 Uiautomationtypes.dll와 같은 경우에는이를 기반으로 합니다. 다음 지침에서는 운영 체제가 C: 드라이브에 설치되어 있다고 가정합니다.

1. Win32clock 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **참조 ...** 를 선택 하 고 해당 대화 상자 내에서 다음을 선택 합니다.

2. Win32clock 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **참조 ...** 를 선택 합니다.

3. **새 참조 추가**를 클릭 하 고 찾아보기 탭을 클릭 한 다음 C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationCore.dll을 입력 하 고 확인을 클릭 합니다.

4. PresentationFramework에 대해 반복 합니다. C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationFramework.dll.

5. WindowsBase .dll에 대해 반복 합니다. C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\WindowsBase.dll.

6. Uiautomationtypes.dll에 대해 반복 합니다. C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\UIAutomationTypes.dll.

7. Uiautomationprovider.dll에 대해 반복 합니다. C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\UIAutomationProvider.dll.

8. **새 참조 추가**를 클릭 하 고, 시스템 .dll을 선택 하 고, **확인**을 클릭 합니다.

9. **확인** 을 클릭 하 여 참조 추가에 대 한 Win32clock 속성 페이지를 종료 합니다.

 마지막으로에를 `STAThreadAttribute` 사용 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]하기 `_tWinMain` 위해를 메서드에 추가 합니다.

```cpp
[System::STAThreadAttribute]
int APIENTRY _tWinMain(HINSTANCE hInstance,
                     HINSTANCE hPrevInstance,
                     LPTSTR    lpCmdLine,
                     int       nCmdShow)
```

이 특성은 COM (구성 요소 개체 모델)을 초기화할 때 (및 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)])에 필요한 STA (단일 스레드 아파트 모델)를 사용 해야 하는 CLR (공용 언어 런타임)에 지시 합니다.

## <a name="create-a-windows-presentation-framework-page"></a>Windows Presentation Framework 페이지 만들기

다음으로를 정의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.Page>하는 DLL을 만듭니다. 을 독립 실행형 응용 프로그램 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.Page> 으로 만들고이 방식으로 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 부분을 작성 하 고 디버그 하는 것이 가장 쉬운 경우가 많습니다. 완료 되 면 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 한 다음 응용 프로그램으로 이동 하 고 출력 형식을 Windows 클래스 라이브러리로 변경 하 여 해당 프로젝트를 DLL로 변환할 수 있습니다.

그런 다음 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] dll 프로젝트를 프로젝트 (두 프로젝트를 포함 하는 솔루션 하나)와 결합할 수 있습니다. 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **Add\Existing project**를 선택 합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]

프로젝트에서 해당 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dll을 사용 하려면 참조를 추가 해야 합니다. [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]

1. Win32clock 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **참조 ...** 를 선택 합니다.

2. **새 참조 추가**를 클릭 합니다.

3. **프로젝트** 탭을 클릭합니다. WPFClock을 선택하고 [확인]을 클릭합니다.

4. **확인** 을 클릭 하 여 참조 추가에 대 한 Win32clock 속성 페이지를 종료 합니다.

## <a name="hwndsource"></a>HwndSource

다음에는 <xref:System.Windows.Interop.HwndSource> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 를사용하여HWND와같이표시됩니다.<xref:System.Windows.Controls.Page> 다음 코드 블록을 C++ 파일에 추가합니다.

```cpp
namespace ManagedCode
{
    using namespace System;
    using namespace System::Windows;
    using namespace System::Windows::Interop;
    using namespace System::Windows::Media;

    HWND GetHwnd(HWND parent, int x, int y, int width, int height) {
        HwndSource^ source = gcnew HwndSource(
            0, // class style
            WS_VISIBLE | WS_CHILD, // style
            0, // exstyle
            x, y, width, height,
            "hi", // NAME
            IntPtr(parent)        // parent window
            );

        UIElement^ page = gcnew WPFClock::Clock();
        source->RootVisual = page;
        return (HWND) source->Handle.ToPointer();
    }
}
}
```

 다음은 약간의 설명이 필요할 수 있는 긴 코드 조각입니다. 첫 번째 부분은 다양한 절이어서 모든 호출을 정규화할 필요가 없습니다.

```cpp
namespace ManagedCode
{
    using namespace System;
    using namespace System::Windows;
    using namespace System::Windows::Interop;
    using namespace System::Windows::Media;
```

 그런 다음 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠 <xref:System.Windows.Interop.HwndSource> 를 만들고이를 둘러싼 다음 HWND를 반환 하는 함수를 정의 합니다.

```cpp
HWND GetHwnd(HWND parent, int x, int y, int width, int height) {
```

먼저 매개 변수가 CreateWindow <xref:System.Windows.Interop.HwndSource>와 유사한을 만듭니다.

```cpp
HwndSource^ source = gcnew HwndSource(
    0, // class style
    WS_VISIBLE | WS_CHILD, // style
    0, // exstyle
    x, y, width, height,
    "hi", // NAME
    IntPtr(parent) // parent window
);
```

그런 다음 해당 생성자 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 를 호출 하 여 콘텐츠 클래스를 만듭니다.

```cpp
UIElement^ page = gcnew WPFClock::Clock();
```

그런 다음 페이지를에 연결 합니다 <xref:System.Windows.Interop.HwndSource>.

```cpp
source->RootVisual = page;
```

 마지막 줄에서의 HWND <xref:System.Windows.Interop.HwndSource>를 반환 합니다.

```cpp
return (HWND) source->Handle.ToPointer();
```

## <a name="positioning-the-hwnd"></a>Hwnd 위치 지정

이제 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] clock을 포함 하는 hwnd가 있으므로 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 대화 상자 내에 해당 hwnd를 넣어야 합니다. HWND를 배치할 위치를 알고 있다면 앞에서 정의한 `GetHwnd` 함수에 해당 크기와 위치를 전달 하면 됩니다. 그러나 리소스 파일을 사용하여 대화 상자를 정의했으므로 HWND를 배치할 위치를 정확하게 알 수 없습니다. [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 대화 상자 편집기를 사용 하 여 clock을 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 이동할 위치 ("여기에 클록 삽입")을 입력 하 고이를 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 사용 하 여 clock을 배치할 수 있습니다.

WM_INITDIALOG를 처리 하는 경우를 `GetDlgItem` 사용 하 여 자리 표시자 정적의 HWND를 검색 합니다.

```cpp
HWND placeholder = GetDlgItem(hDlg, IDC_CLOCK);
```

그런 다음 해당 자리 표시자 정적의 크기와 위치를 계산 하 여 해당 위치에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 시계를 배치할 수 있습니다.

RECT 사각형의 경우입니다.

```cpp
GetWindowRect(placeholder, &rectangle);
int width = rectangle.right - rectangle.left;
int height = rectangle.bottom - rectangle.top;
POINT point;
point.x = rectangle.left;
point.y = rectangle.top;
result = MapWindowPoints(NULL, hDlg, &point, 1);
```

그런 다음 자리 표시자 STATIC을 숨깁니다.

```cpp
ShowWindow(placeholder, SW_HIDE);
```

그런 다음 해당 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 위치에 클록 HWND를 만듭니다.

```cpp
HWND clock = ManagedCode::GetHwnd(hDlg, point.x, point.y, width, height);
```

자습서를 흥미 있게 만들고 실제 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 시계를 생성 하려면이 시점에서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] clock 컨트롤을 만들어야 합니다. 코드 숨김에서 몇 개의 이벤트 처리기만 사용하여 태그에서 거의 모든 작업을 수행할 수 있습니다. 이 자습서는 컨트롤 디자인에 대 한 것이 아니라 상호 운용성에 대 한 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 것 이기 때문에이에 대 한 전체 코드는 여기에서 코드 블록으로 제공 됩니다. 이 코드를 자유롭게 사용하여 컨트롤의 모양과 느낌 또는 기능을 변경해 보세요.

다음은 태그입니다.

[!code-xaml[Win32Clock#AllClockXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/Win32Clock/CS/Clock.xaml#allclockxaml)]

다음은 함께 제공되는 코드 숨김입니다.

[!code-csharp[Win32Clock#AllClockCS](~/samples/snippets/csharp/VS_Snippets_Wpf/Win32Clock/CS/Clock.xaml.cs#allclockcs)]

최종 결과는 다음과 같습니다.

![최종 결과 날짜 및 시간 속성 대화 상자](./media/walkthrough-hosting-a-wpf-clock-in-win32/final-result-date-time-properties-dialog.png)

최종 결과를이 스크린샷을 생성 한 코드와 비교 하려면 [Win32 클록 상호 운용성 샘플](https://go.microsoft.com/fwlink/?LinkID=160051)을 참조 하세요.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Interop.HwndSource>
- [WPF 및 Win32 상호 운용성](wpf-and-win32-interoperation.md)
- [Win32 시계 상호 운용 샘플](https://go.microsoft.com/fwlink/?LinkID=160051)
