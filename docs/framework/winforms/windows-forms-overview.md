---
title: Windows Forms 개요
ms.date: 03/30/2017
helpviewer_keywords:
- smart clients
- Windows Forms, about Windows Forms
ms.assetid: 3a2b6284-c8d6-4e1c-8c69-0bed38f38cd4
ms.openlocfilehash: 71bf50bdcf058e94981dc5df4731b5d32dcc2069
ms.sourcegitcommit: 2d42b7ae4252cfe1232777f501ea9ac97df31b63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67487203"
---
# <a name="windows-forms-overview"></a>Windows Forms 개요

다음 개요에서는 스마트 클라이언트 애플리케이션의 이점, Windows Forms 프로그래밍의 주요 기능 및 Windows Forms를 사용하여 오늘날의 기업과 최종 사용자의 요구를 충족하는 스마트 클라이언트를 빌드하는 방법을 설명합니다.

## <a name="windows-forms-and-smart-client-apps"></a>Windows Forms 및 스마트 클라이언트 앱

 Windows Forms를 사용하여 스마트 클라이언트를 개발합니다. *스마트 클라이언트*는 쉽게 배포 및 업데이트되며, 인터넷에 연결되었거나 연결이 끊어졌을 때 작동할 수 있고, 기존의 Windows 기반 응용 프로그램보다 더 안전하게 로컬 컴퓨터의 리소스에 액세스할 수 있는 시각적으로 풍부한 응용 프로그램입니다.

### <a name="build-rich-interactive-user-interfaces"></a>다양 한 대화형 사용자 인터페이스 빌드

 Windows Forms는.NET Framework에서 읽기 및 쓰기 파일 시스템에 같은 일반적인 응용 프로그램 작업을 간소화 하는 관리 되는 라이브러리 집합에 대 한 스마트 클라이언트 기술입니다. Visual Studio와 같은 개발 환경에서 사용 하는 경우 네트워크를 통해 원격 컴퓨터와 정보를 표시 하 고 사용자 로부터 입력을 요청 하 고 전달 하는 Windows Forms 스마트 클라이언트 응용 프로그램을 만들 수 있습니다.

 Windows Forms에서 *폼*은 정보를 사용자에게 표시하는 비주얼 화면입니다. 일반적으로 폼에 컨트롤을 추가하고 마우스 클릭이나 키 누름과 같은 사용자 동작에 대한 응답을 개발하여 Windows Forms 애플리케이션을 빌드합니다. *컨트롤*은 데이터를 표시하거나 데이터 입력을 수락하는 고유한 UI(사용자 인터페이스) 요소입니다.

 사용자가 폼이나 컨트롤 중 하나에 작업을 수행하면 이벤트가 생성됩니다. 애플리케이션은 코드를 사용하여 이러한 이벤트에 대응하고, 발생 시 이벤트를 처리합니다. 자세한 내용은 [Windows Forms에서 이벤트 처리기 만들기](creating-event-handlers-in-windows-forms.md)를 참조하세요.

 Windows Forms에는 텍스트 상자, 단추, 드롭다운 상자, 라디오 단추 및 웹 페이지를 표시하는 컨트롤 등 폼에 추가할 수 있는 다양한 컨트롤이 포함되어 있습니다. 폼에서 사용할 수 있는 모든 컨트롤의 목록은 [Windows Forms에서 사용할 수 있는 컨트롤](./controls/controls-to-use-on-windows-forms.md)을 참조하세요. 기존 컨트롤이 요구를 충족하지 않는 경우 Windows Forms에서 <xref:System.Windows.Forms.UserControl> 클래스를 사용하여 고유한 사용자 지정 컨트롤을 만들 수도 있습니다.

 Windows Forms에는 Microsoft Office와 같은 고급 애플리케이션의 기능을 에뮬레이트하는 풍부한 UI 컨트롤이 있습니다. <xref:System.Windows.Forms.ToolStrip> 및 <xref:System.Windows.Forms.MenuStrip> 컨트롤을 사용하는 경우 텍스트와 이미지를 포함하고, 하위 메뉴를 표시하며, 텍스트 상자 및 콤보 상자와 같은 기타 컨트롤을 호스트하는 도구 모음과 메뉴를 만들 수 있습니다.

 끌어서 놓기를 사용 하 여 **Windows Forms 디자이너** Visual Studio에서 쉽게 만들 수 있습니다 Windows Forms 응용 프로그램입니다. 커서를 사용하여 컨트롤을 선택하고 폼에서 원하는 위치에 추가하면 됩니다. 디자이너는 컨트롤을 쉽게 배치하기 위한 모눈선 및 맞춤선과 같은 도구를 제공합니다. 사용할 수 있는지를 Visual Studio를 사용 하거나 명령줄에서 컴파일 및 합니다 <xref:System.Windows.Forms.FlowLayoutPanel>, <xref:System.Windows.Forms.TableLayoutPanel> 및 <xref:System.Windows.Forms.SplitContainer> 짧은 시간 내에 컨트롤을 만드는 고급 폼 레이아웃 합니다.

 끝으로, 고유한 사용자 지정 UI 요소를 만들어야 하는 경우 <xref:System.Drawing> 네임스페이스에는 선, 원 및 기타 도형을 폼에 직접 렌더링하는 다양한 클래스가 포함되어 있습니다.

> [!NOTE]
> Windows Forms 컨트롤은 애플리케이션 도메인 간에 마샬링되도록 설계되어 있지 않습니다. 이런 이유로 Microsoft는 <xref:System.MarshalByRefObject>의 <xref:System.Windows.Controls.Control> 기본 형식이 가능한 것처럼 표시해도 <xref:System.AppDomain> 경계를 넘어서 Windows Forms 컨트롤을 전달하는 기능을 지원하지 않습니다. 애플리케이션 도메인 경계를 넘어서 Windows Forms 컨트롤이 전달되지 않는 한 여러 개의 애플리케이션 도메인을 가진 Windows Forms 애플리케이션이 지원됩니다.

#### <a name="create-forms-and-controls"></a>폼 및 컨트롤 만들기

이러한 기능을 사용하는 방법에 대한 단계별 정보는 다음 도움말 항목을 참조하세요.

|설명|도움말 항목|
|-----------------|----------------|
|폼에서 컨트롤 사용|[방법: Windows Forms에 컨트롤 추가](./controls/how-to-add-controls-to-windows-forms.md)|
|<xref:System.Windows.Forms.ToolStrip> 컨트롤 사용|[방법: 디자이너를 사용 하 여 표준 항목을 포함 하는 기본 ToolStrip 만들기](./controls/create-a-basic-wf-toolstrip-with-standard-items-using-the-designer.md)|
|<xref:System.Drawing>을 사용하여 그래픽 만들기|[그래픽 프로그래밍 시작](./advanced/getting-started-with-graphics-programming.md)|
|사용자 지정 컨트롤 만들기|[방법: UserControl 클래스에서 상속](./controls/how-to-inherit-from-the-usercontrol-class.md)|

### <a name="display-and-manipulate-data"></a>표시 하 고 데이터를 조작
 많은 애플리케이션은 데이터베이스, XML 파일, XML Web services 또는 기타 데이터 소스의 데이터를 표시해야 합니다. Windows Forms는 각 데이터 조각이 해당 셀을 사용하도록 이러한 표 형식 데이터를 기존의 행과 열 형식으로 표시하기 위해 <xref:System.Windows.Forms.DataGridView> 컨트롤이라는 유연한 컨트롤을 제공합니다. <xref:System.Windows.Forms.DataGridView>를 사용하는 경우 다른 기능 중에서도 개별 셀의 모양을 사용자 지정하고, 임의의 행과 열을 제자리에 잠그고, 셀 안에 복잡한 컨트롤을 표시할 수 있습니다.

 네트워크를 통해 데이터 소스에 연결하는 것은 Windows Forms 스마트 클라이언트에서 간단한 작업입니다. <xref:System.Windows.Forms.BindingSource> 원래 소스에 다시 이전 및 다음 레코드로 이동, 레코드를 편집 및 변경 내용을 저장 하는 컨트롤에 바인딩 데이터에 대 한 메서드를 노출 및 구성 요소는 데이터 원본에 대 한 연결을 나타냅니다. <xref:System.Windows.Forms.BindingNavigator> 컨트롤은 <xref:System.Windows.Forms.BindingSource> 구성 요소를 통해 사용자가 레코드를 탐색하기 위한 간단한 인터페이스를 제공합니다.

 데이터 소스 창을 통해 데이터 바인딩된 컨트롤을 쉽게 만들 수 있습니다. 창에는 데이터베이스, 웹 서비스 및 개체와 같은 프로젝트의 데이터 소스가 표시됩니다. 이 창에서 프로젝트의 폼으로 항목을 끌어 데이터 바인딩된 컨트롤을 만들 수 있습니다. 데이터 소스 창에서 기존 컨트롤로 개체를 끌어 기존 컨트롤을 데이터에 바인딩할 수도 있습니다.

 Windows Forms에서 관리할 수 있는 다른 형식의 데이터 바인딩은 *설정*입니다. 대부분의 스마트 클라이언트 애플리케이션은 마지막으로 알려진 폼 크기와 같은 런타임 상태에 대한 일부 정보를 유지하고 저장된 파일의 기본 위치와 같은 사용자 기본 설정 데이터를 유지해야 합니다. 애플리케이션 설정 기능은 클라이언트 컴퓨터에 두 유형의 설정을 모두 쉽게 저장할 수 있는 방법을 제공하여 이러한 요구 사항을 충족합니다. Visual Studio 또는 코드 편집기를 사용 하 여 이러한 설정을 정의 하면 설정이 XML로 유지 하 고 런타임 시 자동으로 다시 메모리로 읽어옵니다.

#### <a name="display-and-manipulate-data"></a>표시 하 고 데이터를 조작

이러한 기능을 사용하는 방법에 대한 단계별 정보는 다음 도움말 항목을 참조하세요.

|설명|도움말 항목|
|-----------------|----------------|
|<xref:System.Windows.Forms.BindingSource> 구성 요소 사용|[방법: 디자이너를 사용 하는 BindingSource 구성 요소를 사용 하 여 Windows Forms 컨트롤 바인딩](./controls/bind-wf-controls-with-the-bindingsource.md)|
|ADO.NET 데이터 원본 작업|[방법: Forms BindingSource 구성 요소는 Windows 사용 하 여 ADO.NET 데이터 정렬 및 필터링](./controls/sort-and-filter-ado-net-data-with-wf-bindingsource-component.md)|
|데이터 소스 창 사용|[Visual Studio에서 데이터에 Windows Forms 컨트롤 바인딩](/visualstudio/data-tools/bind-windows-forms-controls-to-data-in-visual-studio)|
|애플리케이션 설정 사용|[방법: 응용 프로그램 설정 만들기](./advanced/how-to-create-application-settings.md)|

### <a name="deploy-apps-to-client-computers"></a>클라이언트 컴퓨터에 앱 배포

애플리케이션을 작성한 후 해당 클라이언트 컴퓨터에 설치하고 실행할 수 있도록 사용자에게 애플리케이션을 보내야 합니다. ClickOnce 기술을 사용 하면 몇 번의 클릭을 사용 하 여 Visual Studio 내에서 응용 프로그램을 배포 하 고 웹 응용 프로그램을 가리키는 URL을 사용 하 여 사용자를 제공할 수 있습니다. ClickOnce는 모든 요소와 응용 프로그램에서 종속성 관리 및 응용 프로그램이 클라이언트 컴퓨터에 올바르게 설치 되어 있는지 확인 합니다.

ClickOnce 응용 프로그램은 사용자가 네트워크에 연결 하는 경우에 실행 하거나 모두 실행 되도록 구성 된 오프 라인으로 사용할 수 있습니다. ClickOnce 응용 프로그램에 오프 라인 작업을 지원 해야 한다고 지정 하면 사용자의 응용 프로그램에 링크를 추가 **시작** 메뉴. 그러면 사용자가 URL을 사용하지 않고도 애플리케이션을 열 수 있습니다.

애플리케이션을 업데이트하는 경우 새 배포 매니페스트와 애플리케이션의 새 복사본을 웹 서버에 게시합니다. ClickOnce는 사용 가능한 업데이트에 대 한 사용자의 설치를 업그레이드를 검색합니다 사용자 지정 프로그래밍 없이 이전 어셈블리를 업데이트 해야 합니다.

#### <a name="deploy-clickonce-apps"></a>ClickOnce 앱 배포

ClickOnce에 대 한 전체 소개를 참조 하세요 [ClickOnce 보안 및 배포](/visualstudio/deployment/clickonce-security-and-deployment)합니다. 이러한 기능을 사용하는 방법에 대한 단계별 정보는 다음 도움말 항목을 참조하세요.

|설명|도움말 항목|
|-----------------|----------------|
|ClickOnce를 사용 하 여 응용 프로그램 배포|[방법: 게시 마법사를 사용하여 ClickOnce 애플리케이션 게시](/visualstudio/deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard)<br /><br /> [연습: 수동으로 ClickOnce 애플리케이션 배포](/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-application)|
|ClickOnce 배포를 업데이트 하는 중|[방법: ClickOnce 애플리케이션에 대한 업데이트 관리](/visualstudio/deployment/how-to-manage-updates-for-a-clickonce-application)|
|ClickOnce 사용 하 여 보안 관리|[방법: ClickOnce 보안 설정 사용](/visualstudio/deployment/how-to-enable-clickonce-security-settings)|

### <a name="other-controls-and-features"></a>기타 컨트롤 및 기능

Windows Forms에는 대화 상자 만들기, 인쇄, 도움말 및 설명서 추가 및 여러 언어로 애플리케이션 지역화 지원과 같이 일반적인 작업을 쉽고 빠르게 구현할 수 있게 해주는 다른 여러 기능이 있습니다. 또한 Windows Forms는.NET Framework의 강력한 보안 시스템에 의존합니다. 이 시스템을 통해 보다 안전한 애플리케이션을 고객에게 릴리스할 수 있습니다.

#### <a name="implement-other-controls-and-features"></a>기타 컨트롤 및 기능 구현

이러한 기능을 사용하는 방법에 대한 단계별 정보는 다음 도움말 항목을 참조하세요.

|설명|도움말 항목|
|-----------------|----------------|
|폼의 콘텐츠 인쇄|[방법: Windows Forms의 그래픽 인쇄](./advanced/how-to-print-graphics-in-windows-forms.md)<br /><br /> [방법: Windows Forms에서 다중 페이지 텍스트 파일 인쇄](./advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md)|
|Windows Forms 보안에 대한 자세한 정보|[Windows Forms의 보안 개요](security-in-windows-forms-overview.md)|

## <a name="see-also"></a>참고자료

- [Windows Forms 시작](getting-started-with-windows-forms.md)
- [새 Windows Form 만들기](creating-a-new-windows-form.md)
- [ToolStrip 컨트롤 개요](./controls/toolstrip-control-overview-windows-forms.md)
- [DataGridView 컨트롤 개요](./controls/datagridview-control-overview-windows-forms.md)
- [BindingSource 구성 요소 개요](./controls/bindingsource-component-overview.md)
- [응용 프로그램 설정 개요](./advanced/application-settings-overview.md)
- [ClickOnce 보안 및 배포](/visualstudio/deployment/clickonce-security-and-deployment)
