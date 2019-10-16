---
title: '연습: Win32에서 WPF 콘텐츠 호스팅'
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- hosting WPF content in Win32 window [WPF]
ms.assetid: 38ce284a-4303-46dd-b699-c9365b22a7dc
ms.openlocfilehash: 3433819761c19b616a7c9c19fe52e250b0f028dc
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929184"
---
# <a name="walkthrough-hosting-wpf-content-in-win32"></a>연습: Win32에서 WPF 콘텐츠 호스팅
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에서는 응용 프로그램을 만들기 위한 다양한 환경을 제공합니다. 그러나 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 코드에 상당한 투자를 한 경우 원본 코드를 다시 작성하는 대신 응용 프로그램에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 기능을 추가하는 것이 더 효과적일 수 있습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]창에서 콘텐츠를 호스트 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 하기 위한 간단한 메커니즘을 제공 합니다. [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]  
  
 이 자습서에서는 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창에서 콘텐츠를 호스트 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 하는 샘플 응용 프로그램 ( [Win32 창에서 WPF 콘텐츠 호스팅 샘플](https://go.microsoft.com/fwlink/?LinkID=160004))을 작성 하는 방법을 설명 합니다. [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창을 호스트하도록 이 샘플을 확장할 수 있습니다. 관리 코드와 비관리 코드를 혼합 하 여 포함 하기 때문에 응용 C++프로그램은/cli로 작성 됩니다.  

<a name="requirements"></a>   
## <a name="requirements"></a>요구 사항  
 이 자습서에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 및 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 프로그래밍에 대한 기본 지식이 있다고 가정합니다. 프로그래밍에 대 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 한 기본적인 소개는 [시작](../getting-started/index.md)을 참조 하세요. 프로그래밍에 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 대 한 소개를 보려면 특히 Charles Petzold의 *프로그래밍 창* 에서 주제에 대 한 다양 한 책을 참조 해야 합니다.  
  
 이 자습서와 함께 제공 되는 샘플은/Cli C++에서 구현 되었으므로이 자습서에서는를 사용 C++ 하 여 Windows API를 프로그래밍 하는 방법과 관리 코드 프로그래밍에 대해 잘 알고 있다고 가정 합니다. /Cli를 C++사용 하는 데 도움이 되지만 반드시 필요한 것은 아닙니다.  
  
> [!NOTE]
> 이 자습서에는 관련 샘플의 많은 코드 예제가 포함되어 있습니다. 그러나 가독성을 위해 전체 샘플 코드를 포함하지는 않습니다. 전체 샘플 코드는 [Win32 창에서 WPF 콘텐츠 호스팅 샘플](https://go.microsoft.com/fwlink/?LinkID=160004)을 참조 하세요.  
  
<a name="basic_procedure"></a>   
## <a name="the-basic-procedure"></a>기본 절차  
 이 섹션에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창에서 콘텐츠를 호스트 하는 데 사용 하는 기본 절차를 간략하게 설명 합니다. 나머지 섹션에서는 각 단계를 자세히 설명합니다.  
  
 창 에서콘텐츠[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 를 호스트 하는 열쇠는 클래스입니다.<xref:System.Windows.Interop.HwndSource> [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 이 클래스는 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 에서 콘텐츠를 래핑하여에 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 자식 창으로 통합 될 수 있도록 합니다. 다음 접근 방식은 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 및 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]를 단일 애플리케이션에 결합합니다.  
  
1. 콘텐츠를 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 관리 되는 클래스로 구현 합니다.  
  
2. /Cli를 사용 하 여 C++Windows 응용 프로그램 구현 기존 응용 프로그램과 비관리 C++ 코드로 시작 하는 경우 일반적으로 `/clr` 컴파일러 플래그를 포함 하도록 프로젝트 설정을 변경 하 여 관리 코드를 호출할 수 있도록 설정할 수 있습니다.  
  
3. 스레딩 모델을 STA(단일 스레드 아파트)로 설정합니다.  
  
4. 창 프로시저에서 [WM_CREATE](/windows/desktop/winmsg/wm-create)알림을 처리 하 고 다음을 수행 합니다.  
  
    1. 부모 창을 해당 <xref:System.Windows.Interop.HwndSource> 매개 변수로 사용하여 새 `parent` 개체를 만듭니다.  
  
    2. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠 클래스의 인스턴스를 만듭니다.  
  
    3. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠 개체에 대 한 참조를의 <xref:System.Windows.Interop.HwndSource.RootVisual%2A> <xref:System.Windows.Interop.HwndSource>속성에 할당 합니다.  
  
    4. 콘텐츠에 대한 HWND를 가져옵니다. <xref:System.Windows.Interop.HwndSource.Handle%2A> 개체의 <xref:System.Windows.Interop.HwndSource> 속성에는 창 핸들(HWND)이 포함됩니다. 애플리케이션의 관리되지 않는 부분에서 사용할 수 있는 HWND를 가져오려면 `Handle.ToPointer()`를 HWND로 캐스팅합니다.  
  
5. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠에 대한 참조를 보유할 정적 필드가 포함된 관리되는 클래스를 구현합니다. 이 클래스를 통해 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 코드에서 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 콘텐츠에 대한 참조를 가져올 수 있습니다.  
  
6. 정적 필드에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠를 할당합니다.  
  
7. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 하나[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 이상의 이벤트에 처리기를 연결 하 여 콘텐츠에서 알림을 받습니다.  
  
8. 정적 필드에 저장된 참조를 통해 속성 등을 설정하여 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠와 통신합니다.  
  
> [!NOTE]
> 를 사용 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 하 여 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠를 구현할 수도 있습니다. 그러나 dll (동적 연결 라이브러리)로 별도로 컴파일하고 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 응용 프로그램에서 해당 dll을 참조 해야 합니다. 프로시저의 나머지 부분은 위에서 설명한 것과 비슷합니다.

<a name="implementing_the_application"></a>
## <a name="implementing-the-host-application"></a>호스트 애플리케이션 구현
 이 섹션에서는 기본 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 응용 프로그램에서 콘텐츠를 호스트 하는 방법을 설명 합니다. 콘텐츠 자체는/Cli에서 C++관리 되는 클래스로 구현 됩니다. 대부분의 경우 간단한 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 프로그래밍입니다. 콘텐츠 구현의 주요 측면은 [WPF 콘텐츠 구현](#implementing_the_wpf_page)에서 설명 합니다.

- [기본 응용 프로그램](#the_basic_application)

- [WPF 콘텐츠 호스트](#hosting_the_wpf_page)

- [WPF 콘텐츠에 대한 참조 보유](#holding_a_reference)

- [WPF 콘텐츠와 통신](#communicating_with_the_page)

<a name="the_basic_application"></a>
### <a name="the-basic-application"></a>기본 애플리케이션
 호스트 응용 프로그램의 시작점은 Visual Studio 2005 템플릿을 만드는 것 이었습니다.

1. Visual Studio 2005을 열고 **파일** 메뉴에서 **새 프로젝트** 를 선택 합니다.

2. [!INCLUDE[TLA2#tla_visualcpp](../../../../includes/tla2sharptla-visualcpp-md.md)] 프로젝트 형식 목록에서 **Win32** 를 선택 합니다. 기본 언어가가 아닌 C++경우 이러한 프로젝트 형식은 **다른 언어**아래에 있습니다.

3. **Win32 프로젝트** 템플릿을 선택 하 고 프로젝트에 이름을 할당 한 다음 **확인** 을 클릭 하 여 **win32 응용 프로그램 마법사**를 시작 합니다.

4. 마법사의 기본 설정을 그대로 적용 하 고 **마침** 을 클릭 하 여 프로젝트를 시작 합니다.

 템플릿은 다음을 포함하여 기본 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 응용 프로그램을 만듭니다.

- 애플리케이션에 대한 진입점

- 연결된 창 프로시저(WndProc)가 있는 창

- **파일** 및 **도움말** 머리글이 있는 메뉴입니다. **파일** 메뉴에는 응용 프로그램을 닫는 **끝내기** 항목이 있습니다. **도움말** 메뉴에는 간단한 대화 상자를 시작 하는 **About** 항목이 있습니다.

 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠를 호스트할 코드 작성을 시작 하기 전에 기본 템플릿을 두 번 수정 해야 합니다.

 첫 번째는 프로젝트를 관리 코드로 컴파일하는 것입니다. 기본적으로 프로젝트는 비관리 코드로 컴파일됩니다. 그러나 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]가 관리 코드에서 구현되었으므로 프로젝트도 그에 따라 컴파일해야 합니다.

1. **솔루션 탐색기** 에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 **속성** 을 선택 하 여 **속성 페이지** 대화 상자를 시작 합니다.

2. 왼쪽 창의 트리 뷰에서 **구성 속성** 을 선택 합니다.

3. 오른쪽 창의 **프로젝트 기본값** 목록에서 **공용 언어 런타임** 지원을 선택 합니다.

4. 드롭다운 목록 상자에서 **공용 언어 런타임 지원 (/clr)** 을 선택 합니다.

> [!NOTE]
> 이 컴파일러 플래그를 통해 애플리케이션에서 관리 코드를 사용할 수 있지만 비관리 코드는 계속 이전처럼 컴파일됩니다.

 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 STA(단일 스레드 아파트) 스레딩 모델을 사용합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠 코드에서 제대로 작동 하려면 진입점에 특성을 적용 하 여 응용 프로그램의 스레딩 모델을 STA로 설정 해야 합니다.

 [!code-cpp[Win32HostingWPFPage#WinMain](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#winmain)]

<a name="hosting_the_wpf_page"></a>
### <a name="hosting-the-wpf-content"></a>WPF 콘텐츠 호스트
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠는 간단한 주소 입력 응용 프로그램입니다. 사용자 이름, 주소 등을 가져오는 여러 개의 <xref:System.Windows.Controls.TextBox> 컨트롤로 구성됩니다. 두 개의 <xref:System.Windows.Controls.Button> 컨트롤인 **확인** 과 **취소**도 있습니다. 사용자가 **확인**을 클릭 하면 단추의 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트 처리기가 <xref:System.Windows.Controls.TextBox> 컨트롤에서 데이터를 수집 하 고 해당 속성에 할당 한 다음 사용자 지정 이벤트를 `OnButtonClicked`발생 시킵니다. 사용자가 **취소**를 클릭 하면 처리기가 발생 `OnButtonClicked`합니다. `OnButtonClicked`에 대한 이벤트 인수 개체에는 클릭된 단추를 나타내는 부울 필드가 포함됩니다.

 콘텐츠를 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 호스트 하는 코드는 호스트 창의 [WM_CREATE](/windows/desktop/winmsg/wm-create) 알림에 대 한 처리기에서 구현 됩니다.

 [!code-cpp[Win32HostingWPFPage#WMCreate](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#wmcreate)]

 메서드 `GetHwnd` 는 크기 및 위치 정보와 부모 창 핸들을 사용 하 고 호스트 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 된 콘텐츠의 창 핸들을 반환 합니다.

> [!NOTE]
> `#using` 네임스페이스에는 `System::Windows::Interop` 지시문을 사용할 수 없습니다. 사용할 경우 해당 네임스페이스의 <xref:System.Windows.Interop.MSG> 구조와 winuser.h에 선언된 MSG 구조 간에 이름 충돌이 생깁니다. 대신 정규화된 이름을 사용하여 해당 네임스페이스의 내용에 액세스해야 합니다.

 [!code-cpp[Win32HostingWPFPage#GetHwnd](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#gethwnd)]

 응용 프로그램 창에서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 직접 콘텐츠를 호스트할 수는 없습니다. <xref:System.Windows.Interop.HwndSource> 콘텐츠를 래핑할 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 개체를 먼저 만듭니다. 이 개체는 기본적으로 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠를 호스트 하도록 설계 된 창입니다. 응용 프로그램의 <xref:System.Windows.Interop.HwndSource> 일부인 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창의 자식으로 만들어 부모 창에서 개체를 호스트 합니다. <xref:System.Windows.Interop.HwndSource> 생성자 매개 변수에는 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 자식 창을 만들 때 CreateWindow에 전달하는 것과 동일한 정보가 포함됩니다.

 다음에는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠 개체의 인스턴스를 만듭니다. 이 경우 콘텐츠는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] /cli를 사용 하 여 `WPFPage` C++별도 클래스로 구현 됩니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]을 통해 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 콘텐츠를 구현할 수도 있습니다. 그러나 이렇게 하려면 별도 프로젝트를 설정 하 고 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠를 DLL로 빌드해야 합니다. 해당 DLL에 대 한 참조를 프로젝트에 추가 하 고 해당 참조를 사용 하 여 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠의 인스턴스를 만들 수 있습니다.

 콘텐츠에 대 한 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Interop.HwndSource.RootVisual%2A> 참조를의 속성 <xref:System.Windows.Interop.HwndSource>에 할당 하 여 자식 창에 콘텐츠를 표시 합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]

 코드의 다음 줄에서는 이벤트 처리기 `WPFButtonClicked`를 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠 `OnButtonClicked` 이벤트에 연결합니다. 이 처리기는 사용자가 **확인** 또는 **취소** 단추를 클릭할 때 호출 됩니다. 이 이벤트 처리기에 대 한 자세한 내용은 [communicating_with_the_WPF 콘텐츠](#communicating_with_the_page) 를 참조 하세요.

 표시된 코드의 마지막 줄에서는 <xref:System.Windows.Interop.HwndSource> 개체와 연결된 창 핸들(HWND)을 반환합니다. 샘플에서는 수행하지 않지만 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 코드에서 이 핸들을 사용하여 호스트된 창에 메시지를 보낼 수 있습니다. <xref:System.Windows.Interop.HwndSource> 개체는 메시지를 받을 때마다 이벤트를 발생시킵니다. 메시지를 처리하려면 <xref:System.Windows.Interop.HwndSource.AddHook%2A> 메서드를 호출하여 메시지 처리기를 연결한 다음 해당 처리기에서 메시지를 처리합니다.

<a name="holding_a_reference"></a>
### <a name="holding-a-reference-to-the-wpf-content"></a>WPF 콘텐츠에 대한 참조 보유
 대부분의 응용 프로그램에서는 나중에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠와 통신하려고 합니다. 예를 들어 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠 속성을 수정하거나 <xref:System.Windows.Interop.HwndSource> 개체가 다른 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠를 호스트하게 할 수 있습니다. 이렇게 하려면 <xref:System.Windows.Interop.HwndSource> 개체 또는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠에 대한 참조가 필요합니다. <xref:System.Windows.Interop.HwndSource> 개체 및 연결된 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠는 창 핸들을 삭제할 때까지 메모리에 남아 있습니다. 그러나 <xref:System.Windows.Interop.HwndSource> 개체에 할당하는 변수는 창 프로시저에서 반환되는 즉시 범위를 벗어납니다. [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 응용 프로그램에서 이 문제를 처리하는 일반적인 방법은 정적 변수나 전역 변수를 사용하는 것입니다. 이러한 유형의 변수에는 관리되는 개체를 할당할 수 없습니다. <xref:System.Windows.Interop.HwndSource> 개체와 연결된 창 핸들을 전역 변수나 정적 변수에 할당할 수 있지만 개체 자체에 대한 액세스는 제공되지 않습니다.

 이 문제에 대한 가장 간단한 해결 방법은 액세스해야 하는 관리되는 개체에 대한 참조를 보유할 정적 필드 집합이 포함된 관리되는 클래스를 구현하는 것입니다. 샘플에서는 `WPFPageHost` 클래스를 사용하여 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠에 대한 참조 및 나중에 사용자가 변경할 수 있는 여러 해당 속성의 초기 값을 보유합니다. 이는 헤더에서 정의됩니다.

 [!code-cpp[Win32HostingWPFPage#WPFPageHost](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.h#wpfpagehost)]

 `GetHwnd` 함수의 뒷부분에서는 나중에 `myPage`가 범위 내에 있는 동안 사용하기 위해 해당 필드에 값을 할당합니다.

<a name="communicating_with_the_page"></a>
### <a name="communicating-with-the-wpf-content"></a>WPF 콘텐츠와 통신
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠와의 통신에는 두 가지 유형이 있습니다. 응용 프로그램은 사용자가 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] **확인** 또는 **취소** 단추를 클릭할 때 콘텐츠에서 정보를 받습니다. 응용 프로그램에는 사용자가 배경색 또는 기본 글꼴 크기와 같은 다양한 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 콘텐츠 속성을 변경할 수 있게 해주는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]도 있습니다.

 위에서 설명했듯이 사용자가 단추 중 하나를 클릭하면 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠에서 `OnButtonClicked` 이벤트를 발생시킵니다. 애플리케이션은 이 이벤트에 처리기를 연결하여 이러한 알림을 수신합니다. **확인** 단추를 클릭 한 경우 처리기는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠에서 사용자 정보를 가져오고 정적 컨트롤 집합에 표시 합니다.

 [!code-cpp[Win32HostingWPFPage#WPFButtonClicked](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#wpfbuttonclicked)]

 처리기는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠로부터 사용자 지정 이벤트 인수 개체 `MyPageEventArgs`를 받습니다. 확인 단추를 `IsOK` 클릭 한 경우 개체 `true` 의 속성이 로 설정 되 고, `false` **취소** 단추를 클릭 한 경우로 설정 됩니다.

 **확인** 단추를 클릭 한 경우 처리기는 컨테이너 클래스에서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠에 대 한 참조를 가져옵니다. 그런 다음 연결된 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 속성에 보유된 사용자 정보를 수집하고 정적 컨트롤을 사용하여 부모 창에 정보를 표시합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠 데이터는 관리되는 문자열 형식이므로 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 컨트롤에서 사용하기 위해 마샬링해야 합니다. **취소** 단추를 클릭 한 경우 처리기는 정적 컨트롤에서 데이터를 지웁니다.

 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 응용 프로그램은 사용자가 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠의 배경색 및 여러 글꼴 관련 속성을 수정할 수 있게 해주는 라디오 단추 집합을 제공합니다. 다음 예제는 애플리케이션의 창 프로시저(WndProc) 및 각 메시지에서 배경색을 비롯한 다양한 속성을 설정하는 해당 메시지 처리에서 발췌한 내용입니다. 다른 예제도 비슷하며 표시되지는 않습니다. 자세한 내용과 컨텍스트는 전체 샘플을 참조하세요.

 [!code-cpp[Win32HostingWPFPage#WMCommandToBG](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#wmcommandtobg)]

 배경색을 설정하려면 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 `hostedPage` 콘텐츠(`WPFPageHost`)에 대한 참조를 가져오고 배경색 속성을 적절한 색으로 설정합니다. 샘플에서는 세 가지 색 옵션(원래 색, 연한 녹색 또는 연한 연어살색)을 사용합니다. 원래 배경색은 `WPFPageHost` 클래스에 정적 필드로 저장되어 있습니다. 다른 두 색을 설정하기 위해 <xref:System.Windows.Media.SolidColorBrush> 개체를 새로 만들고 생성자에 <xref:System.Windows.Media.Colors> 개체의 정적 색 값을 전달합니다.

<a name="implementing_the_wpf_page"></a>
## <a name="implementing-the-wpf-page"></a>WPF 페이지 구현
 실제 구현에 대 한 지식 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 없이 콘텐츠를 호스트 하 고 사용할 수 있습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠가 별도의 DLL에 패키지 된 경우 CLR (공용 언어 런타임) 언어로 빌드된 것일 수 있습니다. 다음은 샘플에서 사용 되는 C++/cli 구현에 대 한 간단한 연습입니다. 이 섹션에는 다음 하위 섹션이 포함되어 있습니다.

- [레이아웃](#page_layout)

- [호스트 창에 데이터 반환](#returning_data_to_window)

- [WPF 속성 설정](#set_page_properties)

<a name="page_layout"></a>
### <a name="layout"></a>레이아웃
 콘텐츠의 요소 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]는연결 <xref:System.Windows.Controls.TextBox> 된<xref:System.Windows.Controls.Label> 컨트롤을 포함 하는 5 개의 컨트롤로 구성 됩니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 이름, 주소, 구/군/시, 시/도 및 우편 번호입니다. 두 개의 <xref:System.Windows.Controls.Button> 컨트롤인 **확인** 과 **취소** 도 있습니다.

 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠는 `WPFPage` 클래스에서 구현됩니다. 레이아웃은 <xref:System.Windows.Controls.Grid> 레이아웃 요소에서 처리됩니다. 클래스는 <xref:System.Windows.Controls.Grid>에서 상속되며 효과적으로 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠 루트 요소로 설정됩니다.

 콘텐츠 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 생성자는 필요한 너비와 높이를 사용 하 고 <xref:System.Windows.Controls.Grid> 크기를 적절히 조정 합니다. <xref:System.Windows.Controls.ColumnDefinition> 그런 다음 <xref:System.Windows.Controls.Grid.RowDefinitions%2A> 및 <xref:System.Windows.Controls.RowDefinition> 개체 집합을 만들어 각각 <xref:System.Windows.Controls.Grid> 개체 기본 <xref:System.Windows.Controls.Grid.ColumnDefinitions%2A> 및 컬렉션에 추가 하 여 기본 레이아웃을 정의 합니다. 그러면 크기가 셀의 내용에 따라 결정되는 5개의 행과 7개의 열로 구성된 표가 정의됩니다.

 [!code-cpp[Win32HostingWPFPage#WPFPageCtorToGridDef](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectortogriddef)]

 다음에는 생성자가 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]에 <xref:System.Windows.Controls.Grid> 요소를 추가합니다. 첫 번째 요소는 표의 첫 번째 행 가운데에 표시되는 <xref:System.Windows.Controls.Label> 컨트롤인 제목 텍스트입니다.

 [!code-cpp[Win32HostingWPFPage#WPFPageCtorTitle](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectortitle)]

 다음 행에는 Name <xref:System.Windows.Controls.Label> 컨트롤 및 연결된 <xref:System.Windows.Controls.TextBox> 컨트롤이 포함됩니다. 동일한 코드가 각 레이블/텍스트 상자 쌍에 사용되므로 private 메서드 쌍에 배치되고 레이블/텍스트 상자 쌍 5개에 모두 사용됩니다. 메서드는 적절한 컨트롤을 만들고 <xref:System.Windows.Controls.Grid> 클래스의 정적 <xref:System.Windows.Controls.Grid.SetColumn%2A> 및 <xref:System.Windows.Controls.Grid.SetRow%2A> 메서드를 호출하여 컨트롤을 적절한 셀에 배치합니다. 컨트롤이 만들어진 후 샘플에서는 <xref:System.Windows.Controls.UIElementCollection.Add%2A>의 <xref:System.Windows.Controls.Panel.Children%2A> 속성에 대해 <xref:System.Windows.Controls.Grid> 메서드를 호출하여 표에 컨트롤을 추가합니다. 나머지 레이블/텍스트 상자 쌍을 추가하는 코드도 비슷합니다. 자세한 내용은 샘플 코드를 참조하세요.

 [!code-cpp[Win32HostingWPFPage#WPFPageCtorName](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectorname)]

 두 메서드의 구현은 다음과 같습니다.

 [!code-cpp[Win32HostingWPFPage#WPFPageCreateHelpers](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagecreatehelpers)]

 마지막으로이 샘플에서는 **확인** 및 **취소** 단추를 추가 하 고 이벤트 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 처리기를 이벤트에 연결 합니다.

 [!code-cpp[Win32HostingWPFPage#WPFPageCtorButtonsEvents](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectorbuttonsevents)]

<a name="returning_data_to_window"></a>
### <a name="returning-the-data-to-the-host-window"></a>호스트 창에 데이터 반환
 단추 중 하나를 클릭하면 해당 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트가 발생합니다. 호스트 창은 단순히 이러한 이벤트에 처리기를 연결하고 <xref:System.Windows.Controls.TextBox> 컨트롤에서 직접 데이터를 가져올 수 있습니다. 샘플에서는 상대적으로 덜 직접적인 접근 방식을 사용합니다. 콘텐츠 내에서 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 를 처리 한 다음 사용자 지정 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 이벤트 `OnButtonClicked`를 발생 시켜 콘텐츠에 알립니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 이렇게 하면 호스트 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 에 알리기 전에 콘텐츠에서 일부 매개 변수 유효성 검사를 수행할 수 있습니다. 처리기는 <xref:System.Windows.Controls.TextBox> 컨트롤에서 텍스트를 가져와 호스트가 정보를 검색할 수 있는 public 속성에 할당합니다.

 WPFPage.h의 이벤트 선언:

 [!code-cpp[Win32HostingWPFPage#WPFPageEventDecl](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.h#wpfpageeventdecl)]

 WPFPage.cpp의 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트 처리기:

 [!code-cpp[Win32HostingWPFPage#WPFPageButtonClicked](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagebuttonclicked)]

<a name="set_page_properties"></a>
### <a name="setting-the-wpf-properties"></a>WPF 속성 설정
 호스트를 통해 사용자는 여러 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠 속성을 변경할 수 있습니다. [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 쪽에서는 단순히 속성을 변경하면 됩니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠 클래스의 구현은 모든 컨트롤의 글꼴을 제어하는 단일 전역 속성이 없기 때문에 다소 복잡합니다. 대신, 각 컨트롤에 적절한 속성이 속성의 set 접근자에서 변경됩니다. 다음 예제에서는 `DefaultFontFamily` 속성에 대 한 코드를 보여 줍니다. 속성을 설정하면 private 메서드가 호출되고, 다시 다양한 컨트롤에 대한 <xref:System.Windows.Controls.Control.FontFamily%2A> 속성이 설정됩니다.

 WPFPage.h에서:

 [!code-cpp[Win32HostingWPFPage#WPFPageFontFamilyProperty](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.h#wpfpagefontfamilyproperty)]

 WPFPage.cpp에서:

 [!code-cpp[Win32HostingWPFPage#WPFPageSetFontFamily](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagesetfontfamily)]

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Interop.HwndSource>
- [WPF 및 Win32 상호 운용성](wpf-and-win32-interoperation.md)
