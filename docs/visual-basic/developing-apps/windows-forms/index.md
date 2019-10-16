---
title: Windows Forms 애플리케이션 기초(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- Windows applications
- Windows Forms, Visual Basic
ms.assetid: 0b919d30-7fd6-42db-85c8-543d15312441
ms.openlocfilehash: dd3385d6459199d56f74abfb1b8e0e218a2adf78
ms.sourcegitcommit: 2d42b7ae4252cfe1232777f501ea9ac97df31b63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67487800"
---
# <a name="windows-forms-application-basics-visual-basic"></a>Windows Forms 애플리케이션 기초(Visual Basic)
사용자의 컴퓨터에서 로컬로 실행 되는 Windows Forms 응용 프로그램을 만드는 기능은 Visual Basic의 중요 한 부분입니다. Windows Forms를 사용 하 여 응용 프로그램 및 사용자 인터페이스를 만들려면 Visual Studio를 사용할 수 있습니다. Windows Forms 응용 프로그램의 클래스에 빌드되는 <xref:System.Windows.Forms> 네임 스페이스입니다.  
  
## <a name="designing-windows-forms-applications"></a>디자인 Windows Forms 응용 프로그램  
 Visual Studio를 사용 하 여 Windows Forms 및 Windows 서비스 응용 프로그램을 만들 수 있습니다. 자세한 내용은 다음 항목을 참조하세요.  
  
- [Windows Forms 시작](../../../framework/winforms/getting-started-with-windows-forms.md)합니다. 만들고 Windows Forms 프로그래밍 방법에 대 한 정보를 제공 합니다.  
   
- [Windows Forms 컨트롤](../../../framework/winforms/controls/index.md)합니다. Windows Forms 컨트롤의 사용을 자세히 설명 하는 항목의 컬렉션입니다.  
  
- [Windows 서비스 응용 프로그램](../../../framework/windows-services/index.md)합니다. Windows 서비스를 만드는 방법을 설명 하는 항목을 나열 합니다.  
  
## <a name="building-rich-interactive-user-interfaces"></a>풍부한 대화형 사용자 인터페이스 빌드  
 Windows Forms는.NET Framework에서 읽기 및 쓰기 파일 시스템에 같은 일반적인 응용 프로그램 작업을 사용 하도록 설정 하는 관리 되는 라이브러리 집합의 스마트 클라이언트 구성 요소입니다. Visual Studio와 같은 개발 환경을 사용 하 여, Windows Forms 응용 프로그램 정보를 표시 하 고 사용자 로부터 입력을 요청 하 고 전달 하는 원격 컴퓨터와 네트워크를 통해 만들 수 있습니다.  
  
 Windows Forms 폼의는 정보는 사용자를 표시 하는 비주얼 화면입니다. 일반적으로 폼에 컨트롤을 배치 하 고 마우스 클릭 이나 키 누름과 같은 사용자 작업에 대 한 응답을 개발 하 여 Windows Forms 응용 프로그램을 빌드합니다. *컨트롤*은 데이터를 표시하거나 데이터 입력을 수락하는 고유한 UI(사용자 인터페이스) 요소입니다.  
  
### <a name="events"></a>이벤트  
 사용자 폼 또는 컨트롤 중 하나에 작업 수행, 이벤트가 생성 됩니다. 애플리케이션은 코드를 사용하여 이러한 이벤트에 대응하고, 발생 시 이벤트를 처리합니다. 자세한 내용은 [Windows Forms에서 이벤트 처리기 만들기](../../../framework/winforms/creating-event-handlers-in-windows-forms.md)를 참조하세요.  
  
### <a name="controls"></a>컨트롤  
 다양 한 폼에 배치할 수 있는 컨트롤을 포함 하는 Windows Forms: 텍스트 상자, 단추, 드롭다운 목록 상자, 라디오 단추 및 심지어 웹 페이지를 표시 하는 컨트롤입니다. 폼에서 사용할 수 있는 모든 컨트롤의 목록은 [Windows Forms에서 사용할 수 있는 컨트롤](../../../framework/winforms/controls/controls-to-use-on-windows-forms.md)을 참조하세요. 기존 컨트롤이 요구를 충족하지 않는 경우 Windows Forms에서 <xref:System.Windows.Forms.UserControl> 클래스를 사용하여 고유한 사용자 지정 컨트롤을 만들 수도 있습니다.  
  
 Windows Forms에는 Microsoft Office와 같은 고급 애플리케이션의 기능을 에뮬레이트하는 풍부한 UI 컨트롤이 있습니다. 사용 하는 <xref:System.Windows.Forms.ToolStrip> 및 <xref:System.Windows.Forms.MenuStrip> 컨트롤 도구 모음 및 메뉴 텍스트와 이미지가 포함 될 하위 메뉴를 표시 하 고 텍스트 상자 및 콤보 상자와 같은 다른 컨트롤을 호스트를 만들 수 있습니다.  
  
 Visual Studio 끌어서 놓기 forms 디자이너를 사용 하 여 쉽게 만들 수 있습니다 Windows Forms 응용 프로그램: 커서를 사용 하 여 컨트롤을 선택 하 고 폼의 원하는 위치를 배치 합니다. 모눈선 및 "맞춤선"와 같은 도구를 제공 하는 디자이너 컨트롤을 쉽게 합니다. 사용할 수 있는지를 Visual Studio를 사용 하거나 명령줄에서 컴파일 및 합니다 <xref:System.Windows.Forms.FlowLayoutPanel>, <xref:System.Windows.Forms.TableLayoutPanel> 및 <xref:System.Windows.Forms.SplitContainer> 컨트롤을 만드는 고급 폼 레이아웃 최소한의 시간과 노력을 사용 하 여 합니다.  
  
### <a name="custom-ui-elements"></a>사용자 지정 UI 요소  
 마지막으로 사용자 고유의 사용자 지정 UI 요소를 만들어야 하는 경우는 <xref:System.Drawing> 선, 원 및 기타 도형을 폼에 직접 렌더링 해야 하는 클래스의 모든 네임 스페이스를 포함 합니다.  
  
 이러한 기능을 사용 하는 방법에 대 한 단계별 정보는 다음 도움말 항목을 참조 하세요.  
  
|대상|보기|  
|--------|---------|  
|Visual Studio를 사용 하 여 새 Windows Forms 응용 프로그램 만들기|[자습서 1: 사진 뷰어 만들기](/visualstudio/ide/tutorial-1-create-a-picture-viewer)|  
|폼에서 컨트롤 사용|[방법: Windows Forms에 컨트롤 추가](../../../framework/winforms/controls/how-to-add-controls-to-windows-forms.md)|   
|사용 하 여 그래픽 만들기 <xref:System.Drawing>|[그래픽 프로그래밍 시작](../../../framework/winforms/advanced/getting-started-with-graphics-programming.md)|  
|사용자 지정 컨트롤 만들기|[방법: UserControl 클래스에서 상속](../../../framework/winforms/controls/how-to-inherit-from-the-usercontrol-class.md)|  
  
## <a name="displaying-and-manipulating-data"></a>데이터 표시 및 조작  
 많은 애플리케이션은 데이터베이스, XML 파일, XML Web services 또는 기타 데이터 소스의 데이터를 표시해야 합니다. Windows Forms 이라는 유연한 컨트롤을 제공 합니다 <xref:System.Windows.Forms.DataGridView> 각 데이터 조각이 해당 셀 수 있도록 이러한 테이블 형식 데이터를 기존의 행 및 열 형식으로 렌더링 합니다. 사용 하 여 <xref:System.Windows.Forms.DataGridView> 개별 셀의 모양을 사용자 지정, 임의의 행 및 열 위치에 잠금 및 기타 기능 간에 셀 안에 복잡 한 컨트롤을 표시 합니다.  
  
 네트워크를 통해 데이터 소스에 연결하는 것은 Windows Forms 스마트 클라이언트에서 간단한 작업입니다. 합니다 <xref:System.Windows.Forms.BindingSource> Windows Forms에서 Visual Studio 2005 및.NET Framework 2.0에서 새로 추가 된 구성 요소를 데이터 원본에 대 한 연결을 나타내며 레코드를 편집 하는 이전 및 다음 레코드로 이동 하는 컨트롤에 데이터 바인딩 메서드를 노출 하 고 변경 내용을 다시 원래 소스에 저장 합니다. <xref:System.Windows.Forms.BindingNavigator> 컨트롤은 <xref:System.Windows.Forms.BindingSource> 구성 요소를 통해 사용자가 레코드를 탐색하기 위한 간단한 인터페이스를 제공합니다.  
  
### <a name="data-bound-controls"></a>데이터 바인딩된 컨트롤  
 프로젝트에서 데이터 원본 개체, 데이터베이스 및 웹 서비스 등을 표시 하는 데이터 소스 창를 사용 하 여 쉽게 데이터 바인딩된 컨트롤을 만들 수 있습니다. 이 창에서 프로젝트의 폼으로 항목을 끌어 데이터 바인딩된 컨트롤을 만들 수 있습니다. 데이터 소스 창에서 기존 컨트롤로 개체를 끌어 기존 컨트롤을 데이터에 바인딩할 수도 있습니다.  
  
### <a name="settings"></a>설정  
 다른 형식의 데이터 바인딩은 Windows Forms에서 관리할 수 있는 설정입니다. 대부분의 스마트 클라이언트 응용 프로그램을 마지막으로 알려진 폼 크기 등 해당 런타임 상태에 대 한 일부 정보를 유지 하 고 저장 된 파일에 대 한 기본 위치와 같은 사용자 기본 설정 데이터를 보존 해야 합니다. 응용 프로그램 설정 기능은 클라이언트 컴퓨터의 두 가지 유형의 설정 저장 하는 쉬운 방법을 제공 하 여 이러한 요구 사항을 해결 합니다. Visual Studio 또는 코드 편집기를 사용 하 여 정의 되 면 이러한 설정은 XML로 유지 되며 런타임에 자동으로 다시 메모리로 읽어옵니다 됩니다.  
  
 이러한 기능을 사용 하는 방법에 대 한 단계별 정보는 다음 도움말 항목을 참조 하세요.  
  
|대상|보기|  
|--------|---------|  
|사용 된 <xref:System.Windows.Forms.BindingSource> 구성 요소|[방법: 디자이너를 사용 하는 BindingSource 구성 요소를 사용 하 여 Windows Forms 컨트롤 바인딩](../../../framework/winforms/controls/bind-wf-controls-with-the-bindingsource.md)|  
|ADO.NET 데이터 원본 작업|[방법: Forms BindingSource 구성 요소는 Windows 사용 하 여 ADO.NET 데이터 정렬 및 필터링](../../../framework/winforms/controls/sort-and-filter-ado-net-data-with-wf-bindingsource-component.md)|
|데이터 소스 창 사용|[연습: Windows Form에 데이터 표시](/visualstudio/data-tools/accessing-data-in-visual-studio)|  
  
## <a name="deploying-applications-to-client-computers"></a>클라이언트 컴퓨터에 애플리케이션 배포  
 응용 프로그램을 작성 한 후 설치 하 고 자체 클라이언트 컴퓨터에서 실행할 수 있도록 사용자에 게 전송 해야 합니다. ClickOnce 기술을 사용 하 여, 몇 번의 클릭을 사용 하 여 Visual Studio 내에서 응용 프로그램을 배포 하 고 웹 응용 프로그램을 가리키는 URL을 사용 하 여 사용자를 제공할 수 있습니다. ClickOnce의 모든 요소 및 응용 프로그램에서 종속성 관리 및 응용 프로그램이 클라이언트 컴퓨터에 제대로 설치 되어 있는지 확인 합니다.  
  
 ClickOnce 응용 프로그램은 사용자가 네트워크에 연결 하는 경우에 실행 하거나 모두 실행 되도록 구성 된 오프 라인으로 사용할 수 있습니다. ClickOnce 응용 프로그램에 오프 라인 작업을 지원 해야 한다고 지정 하면 사용자의 응용 프로그램에 링크를 추가 **시작** 메뉴에서 사용자가 URL을 사용 하지 않고 열 수 있도록 합니다.  
  
 애플리케이션을 업데이트하는 경우 새 배포 매니페스트와 애플리케이션의 새 복사본을 웹 서버에 게시합니다. ClickOnce 사용 가능한 업데이트에 대 한 사용자의 설치를 업그레이드를 검색합니다 사용자 지정 프로그래밍 없이 이전 어셈블리를 업데이트 해야 합니다.  
  
 ClickOnce에 대 한 전체 소개를 참조 하세요 [ClickOnce 보안 및 배포](/visualstudio/deployment/clickonce-security-and-deployment)합니다. 이러한 기능을 사용 하는 방법에 대 한 단계별 정보를 다음 도움말 항목을 참조 하세요.  
  
|대상|참조|  
|--------|---------|  
|ClickOnce 사용 하 여 응용 프로그램 배포|[방법: 게시 마법사를 사용하여 ClickOnce 애플리케이션 게시](/visualstudio/deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard)<br /><br /> [연습: 수동으로 ClickOnce 애플리케이션 배포](/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-application)|  
|ClickOnce 배포를 업데이트 합니다.|[방법: ClickOnce 애플리케이션에 대한 업데이트 관리](/visualstudio/deployment/how-to-manage-updates-for-a-clickonce-application)|  
|ClickOnce 사용 하 여 보안 관리|[방법: ClickOnce 보안 설정 사용](/visualstudio/deployment/how-to-enable-clickonce-security-settings)|  
  
## <a name="other-controls-and-features"></a>기타 컨트롤 및 기능  
 Windows Forms에는 대화 상자 만들기, 인쇄, 도움말 및 설명서 추가 및 여러 언어로 애플리케이션 지역화 지원과 같이 일반적인 작업을 쉽고 빠르게 구현할 수 있게 해주는 다른 여러 기능이 있습니다. 또한 Windows Forms는 고객에 게 보다 안전한 응용 프로그램을 릴리스 하는 데 사용할.NET Framework의 강력한 보안 시스템에 의존 합니다.  
  
 이러한 기능을 사용 하는 방법에 대 한 단계별 정보를 다음 도움말 항목을 참조 하세요.  
  
|대상|보기|  
|--------|---------|  
|폼의 내용을 인쇄합니다|[방법: Windows Forms의 그래픽 인쇄](../../../framework/winforms/advanced/how-to-print-graphics-in-windows-forms.md)<br /><br /> [방법: Windows Forms에서 다중 페이지 텍스트 파일 인쇄](../../../framework/winforms/advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md)|   
|Windows Forms 보안에 대한 자세한 정보|[Windows Forms의 보안 개요](../../../framework/winforms/security-in-windows-forms-overview.md)|  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>
- [Windows Forms 개요](../../../framework/winforms/windows-forms-overview.md)
- [My.Forms 개체](../../../visual-basic/language-reference/objects/my-forms-object.md)
