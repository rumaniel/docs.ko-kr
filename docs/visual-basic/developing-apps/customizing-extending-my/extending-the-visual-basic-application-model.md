---
title: Visual Basic 애플리케이션 모델 확장
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic Application Model, extending
ms.assetid: e91d3bed-4c27-40e3-871d-2be17467c72c
ms.openlocfilehash: f4857d410b16c3bbcb2129cec0d753a1c3d7a726
ms.sourcegitcommit: 56ac30a336668124cb7d95d8ace16bd985875147
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65469491"
---
# <a name="extending-the-visual-basic-application-model"></a>Visual Basic 애플리케이션 모델 확장
재정의 하 여 응용 프로그램 모델 기능을 추가할 수 있습니다 합니다 `Overridable` 의 멤버는 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> 클래스입니다. 이 기술은 응용 프로그램 시작 및 종료 하는 대로 사용자 고유의 메서드 호출을 추가 및 응용 프로그램 모델의 동작을 사용자 지정할 수 있습니다.  
  
## <a name="visual-overview-of-the-application-model"></a>응용 프로그램 모델의 시각적 개요  
 이 섹션에서는 Visual Basic 응용 프로그램 모델에서 함수 호출 시퀀스를 시각적으로 표시합니다. 다음 섹션에서는 자세히 각 함수의 용도 설명합니다.  
  
 다음 그래픽 일반적인 Visual Basic Windows Forms 응용 프로그램에서 응용 프로그램 모델 호출 순서를 보여 줍니다. 시퀀스 될 때 시작 되는 `Sub Main` 프로시저 호출을 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A> 메서드.  
  
 ![응용 프로그램 모델 호출 순서를 보여 주는 다이어그램입니다.](./media/extending-the-visual-basic-application-model/application-model-call-sequence.gif)  
  
 Visual Basic 응용 프로그램 모델도 제공 합니다 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance> 및 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> 이벤트입니다. 다음 그래픽에는 이러한 이벤트를 발생 시키기 위한 메커니즘을 보여 줍니다.  
  
 ![StartupNextInstance 이벤트를 발생 시키는 OnStartupNextInstance 메서드를 보여 주는 다이어그램입니다.](./media/extending-the-visual-basic-application-model/raise-startupnextinstance-event.gif)  
  
 ![오류로 인해 UnhandledException 이벤트를 발생 시키는 OnUnhandledException 메서드를 보여 주는 다이어그램입니다.](./media/extending-the-visual-basic-application-model/raise-unhandledexception-event.gif)  
  
## <a name="overriding-the-base-methods"></a>기본 메서드를 재정의합니다.  
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A> 메서드는 순서를 정의 합니다 `Application` 메서드를 실행 합니다. 기본적으로 `Sub Main` 절차는 Windows Forms 응용 프로그램에 대 한 호출을 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A> 메서드.  
  
 응용 프로그램이 일반적인 응용 프로그램 (다중 인스턴스 응용 프로그램) 또는 단일 인스턴스 응용 프로그램을 첫 번째 인스턴스의 경우는 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A> 메서드가 실행 되는 `Overridable` 다음 순서 대로 메서드:  
  
1. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnInitialize%2A>. 기본적으로이 메서드 비주얼 스타일, 텍스트 표시 스타일 및 (애플리케이션에는 Windows 인증 사용) 하는 경우 기본 애플리케이션 스레드의 현재 보안 주체를 설정 및 호출 `ShowSplashScreen` 모두 `/nosplash` 도 `-nosplash` 로 사용 되는 명령줄 인수입니다.  
  
     이 함수에서 반환 하는 경우 응용 프로그램 시작 시퀀스 취소가 `False`합니다. 이 경우 응용 프로그램이 실행 되지 해야 하는 경우에 유용할 수 있습니다.  
  
     <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnInitialize%2A> 메서드는 다음 메서드를 호출 합니다.  
  
    1. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.ShowSplashScreen%2A>. 응용 프로그램 정의 시작 화면에 있는지 확인 하 고이 경우 별도 스레드에서 시작 화면을 표시 합니다.  
  
         <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.ShowSplashScreen%2A> 메서드는 시작을 표시 하는 코드를 포함 적어도 지정 된 밀리초 수에 대 한 화면을 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MinimumSplashScreenDisplayTime%2A> 속성입니다. 이 기능을 사용 하려면 사용 하 여 응용 프로그램 시작 화면 추가 해야 합니다는 **프로젝트 디자이너** (집합 합니다 `My.Application.MinimumSplashScreenDisplayTime` 속성을 2 초로), 설정 또는 `My.Application.MinimumSplashScreenDisplayTime` 를재정의하는메서드에서속성<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnInitialize%2A> 또는 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateSplashScreen%2A> 메서드. 자세한 내용은 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MinimumSplashScreenDisplayTime%2A>을 참조하세요.  
  
    2. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateSplashScreen%2A>. 디자이너를를 시작 화면을 초기화 하는 코드를 내보낼 수 있습니다.  
  
         기본적으로 이 메서드는 아무것도 수행하지 않습니다. Visual Basic에서 애플리케이션에 대 한 시작 화면을 선택 하면 **프로젝트 디자이너**, 디자이너 재정의 합니다 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateSplashScreen%2A> 설정 하는 메서드를 사용 하 여 메서드를 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SplashScreen%2A> 시작 화면 폼의 새 인스턴스 속성 .  
  
2. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartup%2A>. 발생 시키기 위한 확장성 지점을 제공 합니다 `Startup` 이벤트입니다. 이 함수에서 반환 하는 경우 응용 프로그램 시작 시퀀스 중지 `False`합니다.  
  
     기본적으로이 메서드는 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup> 이벤트입니다. 이벤트 처리기를 설정 하는 경우를 <xref:System.ComponentModel.CancelEventArgs.Cancel> 이벤트 인수의 속성 `True`, 메서드가 반환 `False` 응용 프로그램 시작을 취소 합니다.  
  
3. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnRun%2A>. 초기화가 완료된 후 기본 애플리케이션 실행을 시작할 준비가 되면 시작 지점을 제공합니다.  
  
     기본적으로 Windows Forms 메시지 루프에 들어가기 전에이 메서드를 호출 합니다 `OnCreateMainForm` (애플리케이션의 기본 폼 만들려면) 및 `HideSplashScreen` (시작 화면 닫기)를 메서드:  
  
    1. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A>. 기본 폼을 초기화 하는 코드를 내보내는 디자이너에 대 한 방법을 제공 합니다.  
  
         기본적으로 이 메서드는 아무것도 수행하지 않습니다. 그러나 선택 하면 기본 폼에서 Visual Basic 애플리케이션에 대 한 **프로젝트 디자이너**, 디자이너 재정의 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A> 설정 하는 메서드를 사용 하 여 메서드를 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MainForm%2A> 기본 폼의 새 인스턴스에 대 한 속성입니다.  
  
    2. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.HideSplashScreen%2A>. 응용 프로그램 정의 시작 화면에 열려 있는 경우이 메서드는 시작 화면을 닫습니다.  
  
         기본적으로이 메서드는 시작 화면을 닫습니다.  
  
4. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartupNextInstance%2A>. 응용 프로그램의 다른 인스턴스가 시작 되 면 단일 인스턴스 응용 프로그램을 작동 하는 방법을 사용자가 지정 하는 방법을 제공 합니다.  
  
     기본적으로이 메서드는 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance> 이벤트입니다.  
  
5. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnShutdown%2A>. 발생 시키기 위한 확장성 지점을 제공 합니다 `Shutdown` 이벤트입니다. 이 메서드는 기본 애플리케이션에서 처리 되지 않은 예외가 발생할 경우 실행 되지 않습니다.  
  
     기본적으로이 메서드는 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown> 이벤트입니다.  
  
6. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnUnhandledException%2A>. 위에 나열 된 방법 중 하나에서 처리 되지 않은 예외가 발생 하는 경우를 실행 합니다.  
  
     기본적으로이 메서드는 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> 디버거 연결 되지 않은 응용 프로그램을 처리 하는 동안 이벤트를 `UnhandledException` 이벤트입니다.  
  
 응용 프로그램은 단일 인스턴스 응용 프로그램을 이미 실행 중인 응용 프로그램을 응용 프로그램의 후속 인스턴스가 호출을 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartupNextInstance%2A> 메서드 원래 인스턴스의 응용 프로그램을 한 다음 종료 됩니다.  
 
 합니다 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartupNextInstance(Microsoft.VisualBasic.ApplicationServices.StartupNextInstanceEventArgs)> 생성자 호출을 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UseCompatibleTextRendering%2A> 응용 프로그램의 폼에 사용할 텍스트 렌더링 엔진을 결정 하는 속성입니다. 기본적으로 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UseCompatibleTextRendering%2A> 속성이 반환 `False`, GDI 텍스트 렌더링 엔진을 사용 하는 것을 나타내는, 기본값인 Visual Basic 2005 및 이후 버전입니다. 재정의할 수 있습니다는 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UseCompatibleTextRendering%2A> 반환할 속성 `True`, GDI + 텍스트 렌더링 엔진을 사용 함을 나타냅니다는 Visual Basic.NET 2002 및 Visual Basic.NET 2003 기본값.  
  
## <a name="configuring-the-application"></a>응용 프로그램 구성  
 Visual Basic 응용 프로그램 모델의 일부로 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> 클래스는 응용 프로그램을 구성 하는 보호 되는 속성을 제공 합니다. 이러한 속성을 구현 하는 클래스의 생성자에서 설정 되어야 합니다.  
  
 기본 Windows Forms 프로젝트에는 **프로젝트 디자이너** 디자이너 설정 사용 하 여 속성을 설정 하는 코드를 만듭니다. 속성은 응용 프로그램입니다; 시작 하는 경우에 사용 됩니다. 응용 프로그램이 시작 된 이후에 설정 해도 효과가 없습니다.  
  
|속성|결정|프로젝트 디자이너의 응용 프로그램 창에서 설정|  
|---|---|---|  
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.IsSingleInstance%2A>|여부 응용 프로그램이 단일 인스턴스 또는 다중 인스턴스 응용 프로그램으로 실행 합니다.|**단일 인스턴스 응용 프로그램** 확인란|  
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.EnableVisualStyles%2A>|Windows XP와 일치 하는 비주얼 스타일을 사용 하면 응용 프로그램입니다.|**XP 비주얼 스타일 사용** 확인란|  
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SaveMySettingsOnExit%2A>|응용 프로그램이 종료 될 때 응용 프로그램의 사용자 설정 변경 내용을 자동으로 저장 합니다.|**종료 시 종료할 때 My.Settings 저장** 확인란|  
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.ShutdownStyle%2A>|응용 프로그램이 시작 폼을 닫을 때 또는 마지막 폼을 닫을 때와 같은 종료 원인입니다.|**종료 모드** 목록|  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>
- [Visual Basic 응용 프로그램 모델 개요](../../../visual-basic/developing-apps/development-with-my/overview-of-the-visual-basic-application-model.md)
- [프로젝트 디자이너, 응용 프로그램 페이지(Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)
