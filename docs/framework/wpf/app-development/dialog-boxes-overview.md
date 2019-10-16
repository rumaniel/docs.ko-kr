---
title: 대화 상자 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- modeless dialog boxes [WPF]
- dialog boxes [WPF]
- message boxes [WPF]
- modal dialog boxes [WPF]
ms.assetid: 0d23d544-a393-4a02-a3aa-d8cd5d3d6511
ms.openlocfilehash: bf4617d838ba7f02523d7bbdbb57932c033f4a9e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69958668"
---
# <a name="dialog-boxes-overview"></a>대화 상자 개요
독립 실행형 응용 프로그램에는 일반적으로 응용 프로그램이 작동 하는 기본 데이터를 표시 하 고 메뉴 모음, 도구 모음, 상태 표시줄 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 등의 메커니즘을 통해 해당 데이터를 처리 하는 기능을 노출 하는 주 창이 있습니다. 특수 애플리케이션에는 다음을 수행하는 추가 창이 표시될 수도 있습니다.  
  
- 사용자에게 특정 정보 표시.  
  
- 사용자로부터 정보 수집.  
  
- 정보 표시 및 수집.  
  
 이러한 형식의 창을 *대화 상자*라고 하며, 모달 및 모덜리스의 두 가지 형식이 있습니다.  
  
 *모달* 대화 상자는 함수가 사용자의 추가 데이터를 계속 사용 해야 하는 경우 함수에 의해 표시 됩니다. 함수가 작동하려면 모달 대화 상자를 통해 데이터를 수집해야 하기 때문에, 모달 대화 상자가 열려 있는 동안에는 사용자가 다른 창을 활성화할 수 없습니다. 대부분의 경우 모달 대화 상자에서 **확인** 또는 **취소** 단추를 눌러 모달 대화 상자를 완료 한 경우 사용자가 신호를 보낼 수 있습니다. **확인** 단추를 누르면 사용자가 데이터를 입력 하 고 함수를 통해 해당 데이터를 계속 처리 하려고 합니다. **취소** 단추를 누르면 사용자가 함수 실행을 완전히 중지 하는 것을 알 수 있습니다. 데이터를 열고, 저장하고, 인쇄하는 가장 일반적인 모달 대화 상자의 예가 나와 있습니다.  
  
 반면 *모덜리스* 대화 상자는 열려 있는 동안 사용자가 다른 창을 활성화할 수 없도록 합니다. 예를 들어, 사용자가 문서에서 특정 단어를 찾으려고 할 때 주 창에서 사용자가 찾으려는 단어를 입력할 대화 상자를 열 때가 많습니다. 단어를 찾는다고 해서 사용자가 문서를 편집하지 못하게 되는 것은 아니기 때문에 대화 상자를 모덜로 설정할 필요가 없습니다. 모덜리스 대화 상자는 최소한 대화 상자를 닫기 위한 **닫기** 단추를 제공 하 고, **다음 찾기** 단추와 같은 특정 함수를 실행 하는 추가 단추를 제공 하 여 단어 검색의 찾기 조건과 일치 하는 다음 단어를 찾을 수 있습니다.  
  
 WPF (Windows Presentation Foundation)를 사용 하면 메시지 상자, 일반 대화 상자 및 사용자 지정 대화 상자를 비롯 한 여러 가지 유형의 대화 상자를 만들 수 있습니다. 이 항목에서는 각에 대해 설명 하 고, [대화 상자 샘플](https://go.microsoft.com/fwlink/?LinkID=159984) 에서는 일치 하는 예제를 제공 합니다.  

<a name="Message_Boxes"></a>   
## <a name="message-boxes"></a>메시지 상자  
 *메시지 상자* 는 텍스트 정보를 표시 하 고 사용자가 단추를 사용 하 여 결정을 내릴 수 있도록 하는 대화 상자입니다. 다음 그림에는 텍스트 정보를 표시하고, 질문을 하고, 질문에 대답할 때 사용할 세 개의 단추를 사용자에게 제공하는 메시지 상자가 있습니다.  
  
 ![응용 프로그램을 닫기 전에 문서에 대 한 변경 내용을 저장할지 묻는 워드 프로세서 대화 상자입니다.](./media/dialog-boxes-overview/word-processor-dialog.png)  
  
 메시지 상자를 만들려면 <xref:System.Windows.MessageBox> 클래스를 사용 합니다. <xref:System.Windows.MessageBox>다음과 같은 코드를 사용 하 여 메시지 상자 텍스트, 제목, 아이콘 및 단추를 구성할 수 있습니다.  
  
 [!code-csharp[DialogBoxesOverviewSnippets#MsgBoxConfigureCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#msgboxconfigurecodebehind)]
 [!code-vb[DialogBoxesOverviewSnippets#MsgBoxConfigureCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#msgboxconfigurecodebehind)]  
  
 메시지 상자를 표시 하려면 다음 코드에서 보여 `static` 주는 것 처럼 <xref:System.Windows.MessageBox.Show%2A> 메서드를 호출 합니다.  
  
 [!code-csharp[DialogBoxesOverviewSnippets#MsgBoxShowCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#msgboxshowcodebehind)]
 [!code-vb[DialogBoxesOverviewSnippets#MsgBoxShowCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#msgboxshowcodebehind)]  
  
 메시지 상자를 표시하는 코드로 사용자의 결정을 감지하고 처리해야 할 경우는(단추 누름) 다음 코드에서와 같이 코드를 통해 메시지 상자 결과를 검사할 수 있습니다.  
  
 [!code-csharp[DialogBoxesOverviewSnippets#MsgBoxShowAndResultCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#msgboxshowandresultcodebehind1)]
 [!code-vb[DialogBoxesOverviewSnippets#MsgBoxShowAndResultCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#msgboxshowandresultcodebehind1)]  
  
 메시지 상자를 사용 하는 방법에 대 <xref:System.Windows.MessageBox>한 자세한 내용은 [MessageBox 샘플](https://go.microsoft.com/fwlink/?LinkID=160023)및 [대화 상자 샘플](https://go.microsoft.com/fwlink/?LinkID=159984)을 참조 하세요.  
  
 는 <xref:System.Windows.MessageBox> 간단한 대화 상자 사용자 환경을 제공할 수 있지만를 사용 하 <xref:System.Windows.MessageBox> 는 경우의 이점은 부분 신뢰 보안 샌드박스 내에서 실행 되는 응용 프로그램에서 표시할 수 있는 유일한 형식의 창입니다 ( [보안](../security-wpf.md)참조) [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)].  
  
 대부분의 대화 상자는 텍스트, 선택(확인란), 상호 배타적인 선택(라디오 단추), 목록 선택(목록 상자, 콤보 상자, 드롭다운 목록 상자)과 같이 메시지 상자의 결과보다 복잡한 데이터를 표시하고 수집합니다. 이러한 경우, Windows Presentation Foundation (WPF)는 여러 일반적인 대화 상자를 제공 하며,이 중 하나를 사용 하면 완전 신뢰로 실행 되는 응용 프로그램으로 제한 되지만 사용자 고유의 대화 상자를 만들 수 있습니다.  
  
<a name="Common_Dialogs"></a>   
## <a name="common-dialog-boxes"></a>일반 대화 상자  
 Windows는 파일을 열고, 파일을 저장 하 고, 인쇄 하는 대화 상자를 포함 하 여 모든 응용 프로그램에 공통적인 재사용 가능한 여러 대화 상자를 구현 합니다. 이러한 대화 상자는 운영 체제에서 구현되므로 운영 체제에서 실행되는 모든 애플리케이션에서 공유할 수 있어 사용자 경험의 일관성에 도움이 됩니다. 운영 체제에서 제공되는 대화 상자를 사용자가 한 애플리케이션에서 익히고 나면 다른 애플리케이션에서 대화 상자의 사용 방법을 다시 익힐 필요가 없습니다. 이러한 대화 상자는 모든 응용 프로그램에서 사용할 수 있으며 일관 된 사용자 환경을 제공 하는 데 도움이 되기 때문에 *일반 대화 상자*라고 합니다.  
  
 WPF (Windows Presentation Foundation)는 열려 있는 파일을 캡슐화 하 고, 파일을 저장 하 고, 일반 대화 상자를 인쇄 하 여 독립 실행형 응용 프로그램에서 사용할 수 있도록 관리 되는 클래스로 노출 합니다. 이 항목에서는 각각의 개요를 간략하게 제공합니다.  
  
<a name="Open_File_Dialog"></a>   
### <a name="open-file-dialog"></a>파일 열기 대화 상자  
 다음 그림에 표시된 파일 열기 대화 상자는 파일 열기 기능에서 열려는 파일의 이름을 검색할 때 사용됩니다.  
  
 ![파일을 검색할 위치를 보여 주는 열기 대화 상자입니다.](./media/dialog-boxes-overview/open-file-dialog-box.png)  
  
 일반 파일 열기 대화 상자는 <xref:Microsoft.Win32.OpenFileDialog> 클래스로 구현 되 고 <xref:Microsoft.Win32> 네임 스페이스에 있습니다. 다음 코드에서는 코드를 만들고 구성 및 표시하는 방법과 결과를 처리하는 방법을 보여 줍니다.  
  
 [!code-csharp[DialogBoxesOverviewSnippets#OpenFileDialogBoxCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#openfiledialogboxcodebehind)]
 [!code-vb[DialogBoxesOverviewSnippets#OpenFileDialogBoxCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#openfiledialogboxcodebehind)]  
  
 파일 열기 대화 상자에 대 한 자세한 내용은를 참조 <xref:Microsoft.Win32.OpenFileDialog?displayProperty=nameWithType>하십시오.  
  
> [!NOTE]
> <xref:Microsoft.Win32.OpenFileDialog>부분 신뢰로 실행 되는 응용 프로그램에서 파일 이름을 안전 하 게 검색 하는 데 사용할 수 있습니다 ( [보안](../security-wpf.md)참조).  
  
<a name="Save_File_Dialog"></a>   
### <a name="save-file-dialog-box"></a>파일 저장 대화 상자  
 다음 그림에 표시된 파일 저장 대화 상자는 파일 저장 기능에서 저장하려는 파일의 이름을 검색할 때 사용됩니다.  
  
 ![파일을 저장할 위치를 보여 주는 다른 이름으로 저장 대화 상자가 표시 됩니다.](./media/dialog-boxes-overview/save-file-dialog-box.png)  
  
 공용 파일 저장 대화 상자는 <xref:Microsoft.Win32.SaveFileDialog> 클래스로 구현 되 고 <xref:Microsoft.Win32> 네임 스페이스에 있습니다. 다음 코드에서는 코드를 만들고 구성 및 표시하는 방법과 결과를 처리하는 방법을 보여 줍니다.  
  
 [!code-csharp[DialogBoxesOverviewSnippets#SaveFileDialogBoxCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#savefiledialogboxcodebehind)]
 [!code-vb[DialogBoxesOverviewSnippets#SaveFileDialogBoxCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#savefiledialogboxcodebehind)]  
  
 파일 저장 대화 상자에 대 한 자세한 내용은을 참조 <xref:Microsoft.Win32.SaveFileDialog?displayProperty=nameWithType>하십시오.  
  
<a name="Print_Dialog"></a>   
### <a name="print-dialog-box"></a>인쇄 대화 상자

다음 그림에 표시된 인쇄 대화 상자는 인쇄 기능에서 사용자가 데이터를 인쇄할 프린터를 선택하고 구성할 때 사용됩니다.  
  
![인쇄 대화 상자를 표시 하는 스크린샷](./media/dialog-boxes-overview/print-data-dialog-box.png)  
  
일반 인쇄 대화 상자는 <xref:System.Windows.Controls.PrintDialog> 클래스로 구현 되 고 <xref:System.Windows.Controls> 네임 스페이스에 있습니다. 다음 코드에서는 만들고, 구성하고, 표시하는 방법을 보여 줍니다.  
  
 [!code-csharp[DialogBoxesOverviewSnippets#PrintDialogBoxCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#printdialogboxcodebehind)]
 [!code-vb[DialogBoxesOverviewSnippets#PrintDialogBoxCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#printdialogboxcodebehind)]  
  
 인쇄 대화 상자에 대 한 자세한 내용은를 참조 <xref:System.Windows.Controls.PrintDialog?displayProperty=nameWithType>하십시오. WPF의 인쇄에 대 한 자세한 내용은 [인쇄 개요](../advanced/printing-overview.md)를 참조 하세요.  
  
<a name="Custom_Dialog_Boxes"></a>   
## <a name="custom-dialog-boxes"></a>사용자 지정 대화 상자

일반 대화 상자는 유용하며 가능한 경우 사용하는 편이 좋지만, 도메인별 대화 상자의 요구 사항은 지원하지 않습니다. 이러한 경우 사용자가 직접 대화 상자를 만들어야 합니다. 살펴보겠지만, 대화 상자는 특별한 동작이 있는 창입니다. <xref:System.Windows.Window>는 이러한 동작을 구현 하므로를 사용 <xref:System.Windows.Window> 하 여 사용자 지정 모달 및 모덜리스 대화 상자를 만듭니다.  
  
<a name="Creating_a_Modal_Custom_Dialog_Box"></a>   
### <a name="creating-a-modal-custom-dialog-box"></a>모달 사용자 지정 대화 상자 만들기

이 항목에서는를 사용 <xref:System.Windows.Window> 하 여 `Margins` 대화 상자를 예로 사용 하 여 일반적인 모달 대화 상자 구현을 만드는 방법을 보여 줍니다 ( [대화 상자 샘플](https://go.microsoft.com/fwlink/?LinkID=159984)참조). 이 `Margins` 대화 상자는 다음 그림에 나와 있습니다.  
  
 ![왼쪽 여백, 위쪽 여백, 오른쪽 여백 및 아래쪽 여백을 정의 하는 필드를 포함 하는 여백 대화 상자입니다.](./media/dialog-boxes-overview/margin-size-dialog-box.png)  
  
#### <a name="configuring-a-modal-dialog-box"></a>모달 대화 상자 구성

일반 대화 상자의 사용자 인터페이스에는 다음이 포함됩니다.  
  
- 원하는 데이터를 수집하는 데 필요한 다양한 컨트롤.  
  
- 사용자가 클릭 하 여 대화 상자를 닫고 함수로 돌아가서 처리를 계속 하는 **확인** 단추입니다.  
  
- 사용자가 클릭 하 여 대화 상자를 닫고 추가 처리에서 함수를 중지 하는 **취소** 단추입니다.  
  
- 제목 표시줄에 **닫기** 단추가 있습니다.  
  
- 아이콘.  
  
- **최소화**, **최대화**및 **복원** 단추  
  
- 대화 상자를 최소화, 최대화, 복원 및 닫기 위한 **시스템** 메뉴입니다.  
  
- 대화 상자를 연 창의 가운데 및 위치입니다.  
  
- 가능 하면 크기를 조정 하 여 대화 상자가 너무 작지 않도록 하 고 사용자에 게 유용한 기본 크기를 제공 하는 기능입니다. 이렇게 하려면 기본값과 최소 차원을 모두 설정 해야 합니다.  
  
- **취소** 단추를 누르는 바로 가기 키인 ESC 키입니다. 이렇게 하려면 <xref:System.Windows.Controls.Button.IsCancel%2A> **취소** 단추의 속성을로 `true`설정 합니다.  
  
- **확인** 단추를 누르는 바로 가기 키 인 ENTER 또는 RETURN 키입니다. <xref:System.Windows.Controls.Button.IsDefault%2A> **확인** 단추의 속성`true`을 설정 하 여이 작업을 수행 합니다.  
  
다음 코드에서는 이 구성을 보여 줍니다.  
  
[!code-xaml[MarginsDialogBox XAML file](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml?range=1-16,106-112)]  

[!code-csharp[MarginsDialogBox C# code-behind](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml.cs?range=1-12,67-68)]
[!code-vb[MarginsDialogBox VB code-behind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MarginsDialogBox.xaml.vb?range=1-11,61-62)]  
  
대화 상자의 사용자 경험은 대화 상자를 여는 창의 메뉴 모음으로 확장됩니다. 메뉴 항목에서 함수를 계속하기 전에 대화 상자를 통한 사용자 상호 작용을 필요로 하는 함수를 실행하면, 함수의 메뉴 항목 헤더에 다음과 같이 줄임표가 표시됩니다.  
  
[!code-xaml[Menu bar of MainWindow.Xaml file](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml#L26-L27)]  
  
메뉴 항목에서 [정보] 대화 상자와 같이 사용자 상호 작용이 필요하지 않은 대화 상자를 표시하는 함수를 실행할 경우는 줄임표가 필요하지 않습니다.  
  
#### <a name="opening-a-modal-dialog-box"></a>모달 대화 상자 열기

대화 상자는 일반적으로 워드 프로세서에서 문서 여백을 설정하는 경우와 같이 사용자가 메뉴 항목을 선택하여 도메인 관련 함수를 수행할 때 표시됩니다. 추가 창을 대화 상자로 표시하는 것은 일반 창을 표시하는 것과 비슷하지만, 추가로 대화 상자 관련 구성이 필요합니다. 대화 상자를 인스턴스화하고, 구성하고, 여는 과정 전체가 다음 코드에 표시되어 있습니다.  
  
[!code-csharp[Opening a modal dialog box](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml.cs?range=1-11,78-88,193-195)]
[!code-vb[Opening a modal dialog box](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MainWindow.xaml.vb?range=1-9,58-67,130-132)]  

여기서 코드는 대화 상자에 기본 정보 (현재 여백)를 전달 합니다. 또한 대화 상자를 <xref:System.Windows.Window.Owner%2A?displayProperty=nameWithType> 표시 하는 창에 대 한 참조를 사용 하 여 속성을 설정 합니다. 일반적으로 모든 대화 상자에 공통적인 창 상태 관련 동작을 제공 하려면 항상 대화 상자 소유자를 설정 해야 합니다 (자세한 내용은 [WPF 창 개요](wpf-windows-overview.md) 참조).

> [!NOTE]
> 대화 상자에 대 한 UI (사용자 인터페이스) 자동화를 지원 하려면 소유자를 제공 해야 합니다 ( [Ui 자동화 개요](../../ui-automation/ui-automation-overview.md)참조).

대화 상자가 구성 된 후에는 메서드를 <xref:System.Windows.Window.ShowDialog%2A> 호출 하 여 모달로 표시 됩니다.  
  
#### <a name="validating-user-provided-data"></a>사용자 제공 데이터의 유효성 검사

대화 상자가 열리고 사용자가 필요한 데이터를 제공할 때, 다음과 같은 이유로 대화 상자에서 제공된 데이터가 유효한지 확인해야 합니다.  
  
- 보안 관점에서, 모든 입력이 유효해야 합니다.  
  
- 도메인 관련 관점에서, 데이터의 유효성을 검사하면 코드에서 잘못된 데이터를 처리하여 예외를 일으키는 것을 방지할 수 있습니다.  
  
- 사용자 경험 관점에서, 대화 상자는 사용자가 입력한 데이터 중에 어느 것이 유효한지 표시하여 사용자를 도울 수 있습니다.  
  
- 성능 관점에서, 다중 계층 애플리케이션의 데이터 유효성 검사를 수행하면 클라이언트와 애플리케이션 계층 사이의 왕복 횟수를 줄일 수 있으며 특히 애플리케이션이 웹 서비스나 서버 기반 데이터베이스로 구성된 경우에 효과가 좋습니다.  

WPF에서 바인딩된 컨트롤의 유효성을 검사 하려면 유효성 검사 규칙을 정의 하 고 바인딩과 연결 해야 합니다. 유효성 검사 규칙은에서 <xref:System.Windows.Controls.ValidationRule>파생 되는 사용자 지정 클래스입니다. 다음 예제에서는 바인딩된 값 `MarginValidationRule` <xref:System.Double> 이 이며 지정 된 범위 내에 있는지 확인 하는 유효성 검사 규칙을 보여 줍니다.  

[!code-csharp[Margin validation rules](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginValidationRule.cs)]
[!code-vb[Margin validation rules](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MarginValidationRule.vb)]  

이 코드에서 유효성 검사 규칙의 유효성 검사 논리는 데이터의 유효성을 검사 <xref:System.Windows.Controls.ValidationRule.Validate%2A> 하 고 적절 <xref:System.Windows.Controls.ValidationResult>한을 반환 하는 메서드를 재정의 하 여 구현 됩니다.  

유효성 검사 규칙을 바인딩 컨트롤과 연결하려면 다음과 같은 표시를 사용합니다.  
  
[!code-xaml[Associating a validation rule with a control](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml?range=1-16,57-68,111-112)]

유효성 검사 규칙이 연결 되 면 바인딩된 컨트롤에 데이터를 입력할 때 WPF가 자동으로 적용 합니다. 컨트롤에 잘못 된 데이터가 포함 되어 있는 경우 WPF는 다음 그림과 같이 잘못 된 컨트롤 주위에 빨간색 테두리를 표시 합니다.  
  
![잘못 된 왼쪽 여백 값 주위에 빨간색 테두리가 있는 여백 대화 상자입니다.](./media/dialog-boxes-overview/invalid-left-margin-dialog.png)  

WPF는 유효한 데이터를 입력할 때까지 사용자를 잘못 된 컨트롤로 제한 하지 않습니다. 대화 상자에서 좋은 동작입니다. 사용자는 데이터의 유효성에 관계없이 대화 상자에서 컨트롤을 자유롭게 탐색할 수 있어야 합니다. 그러나이는 사용자가 잘못 된 데이터를 입력 하 고 **확인** 단추를 누를 수 있음을 의미 합니다. 이러한 이유로 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트를 처리 하 여 **확인** 단추를 누르면 코드가 대화 상자에 있는 모든 컨트롤의 유효성을 검사 해야 합니다.  
  
[!code-csharp[Validating all controls in a dialog box](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml.cs?range=1-8,26-29,33-68)]
[!code-vb[Validating all controls in a dialog box](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MarginsDialogBox.xaml.vb?range=1-8,27-29,33-62)]  

이 코드는 창에 있는 모든 종속성 개체를 열거 하 고, 잘못 된 경우 (에 <xref:System.Windows.Controls.Validation.GetHasError%2A>의해 반환 됨), 잘못 된 컨트롤은 `IsValid` 포커스를 `false`가져오고, 메서드는를 반환 하며, 창은 잘못 된 것으로 간주 됩니다.  
  
대화 상자가 유효하면 안전하게 닫고 반환할 수 있습니다. 반환 과정의 일부로서 결과를 호출 함수에 반환해야 합니다.  
  
#### <a name="setting-the-modal-dialog-result"></a>모달 대화 상자 결과 설정

를 사용 하 <xref:System.Windows.Window.ShowDialog%2A> 여 대화 상자를 여는 것은 기본적으로 메서드를 호출 하는 것과 같습니다. <xref:System.Windows.Window.ShowDialog%2A> 를 사용 하 <xref:System.Windows.Window.ShowDialog%2A> 여 대화 상자를 연 코드는를 반환 합니다 가 <xref:System.Windows.Window.ShowDialog%2A> 반환 되 면 사용자가 **확인** 단추를 눌렀는지 아니면 **취소** 단추를 눌렀는지에 따라 호출 하는 코드에서 처리를 계속할지 아니면 처리를 중지할지를 결정 해야 합니다. 이 결정을 용이 하 게 하기 위해 대화 상자에서 사용자의 선택 항목을 <xref:System.Boolean> <xref:System.Windows.Window.ShowDialog%2A> 메서드에서 반환 되는 값으로 반환 해야 합니다.  

**확인** 단추를 클릭 하면에서을 <xref:System.Windows.Window.ShowDialog%2A> 반환 `true`해야 합니다. 확인 단추를 클릭 하면 대화 <xref:System.Windows.Window.DialogResult%2A> 상자의 속성을 설정 하 여이 를 달성할 수 있습니다.  

[!code-csharp[Responding to the OK button](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml.cs?range=1-8,25-27,32-33,67-68)]
[!code-vb[Responding to the OK button](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MarginsDialogBox.xaml.vb?range=1-8,27,31-33,61-62)]  

<xref:System.Windows.Window.DialogResult%2A> 속성을 설정 하면 창이 자동으로 닫히고 명시적으로를 호출할 <xref:System.Windows.Window.Close%2A>필요가 줄어듭니다.  
  
**취소** 단추를 클릭 하면에서 <xref:System.Windows.Window.ShowDialog%2A> <xref:System.Windows.Window.DialogResult%2A> 속성을 설정 `false`해야 하는도 반환 해야 합니다.  
  
[!code-csharp[Responding to the Cancel button](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml.cs?range=1-8,19-24,67-68)]
[!code-vb[Responding to the Cancel button](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MarginsDialogBox.xaml.vb?range=1-8,22-25,61-62)]  

단추의 <xref:System.Windows.Controls.Button.IsCancel%2A> 속성이로 `true` 설정 되 고 사용자가 **취소** 단추나 ESC 키 <xref:System.Windows.Window.DialogResult%2A> 를 누르면가 자동으로로 `false`설정 됩니다. 다음 태그는 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트를 처리할 필요 없이 이전 코드와 동일한 효과를 가집니다.  
  
[!code-xaml[Markup instead of handling the Click event](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml#L109-L109)]  

사용자가 제목 표시줄에서 `false` **닫기** 단추를 누르거나 **시스템** 메뉴에서 **닫기** 메뉴 항목을 선택 하면 대화 상자가 자동으로 반환 됩니다.  

#### <a name="processing-data-returned-from-a-modal-dialog-box"></a>모달 대화 상자에서 반환 된 데이터 처리  

대화 <xref:System.Windows.Window.DialogResult%2A> 상자에가 설정 된 경우이를 연 함수는가 반환 될 때 <xref:System.Windows.Window.ShowDialog%2A> 속성을 <xref:System.Windows.Window.DialogResult%2A> 검사 하 여 대화 상자 결과를 가져올 수 있습니다.  
  
[!code-csharp[Processing data returned from the modal dialog box](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml.cs?range=1-10,77-79,89-96,194-195)]
[!code-vb[Processing data returned from the modal dialog box](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MainWindow.xaml.vb?range=1-9,58,69-73,131-132)]

대화 상자 결과가 인 `true`경우 함수는 해당 사용자가 제공 하는 데이터를 검색 하 고 처리 하는 큐로이를 사용 합니다.  
  
> [!NOTE]
> 가 <xref:System.Windows.Window.ShowDialog%2A> 반환 된 후에는 대화 상자를 다시 열 수 없습니다. 대신 새 인스턴스를 만들어야 합니다.

대화 상자 결과가 `false`이면 함수에서 처리를 적절 하 게 종료 해야 합니다.  
  
<a name="Creating_a_Modeless_Custom_Dialog_Box"></a>   
### <a name="creating-a-modeless-custom-dialog-box"></a>모덜리스 사용자 지정 대화 상자 만들기

다음 그림의 찾기 대화 상자와 같은 모덜리스 대화 상자는 기본적인 모양이 모덜 대화 상자와 같습니다.  

![찾기 대화 상자를 표시 하는 스크린샷](./media/dialog-boxes-overview/find-modeless-dialog-box.png)  

그러나 다음 섹션에 설명된 것처럼 동작은 약간 다릅니다.  
  
#### <a name="opening-a-modeless-dialog-box"></a>모덜리스 대화 상자 열기

모덜리스 대화 상자는 메서드를 <xref:System.Windows.Window.Show%2A> 호출 하 여 열립니다.  

[!code-xaml[XAML to define a modeless dialog box](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml#L21-L22)]  
 
[!code-csharp[Opening a modeless dialog box](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml.cs?range=1-10,65-76,194-195)]
[!code-vb[Openng a modeless dialog box](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MainWindow.xaml.vb?range=1-9,18-23,131,132)]  

와 <xref:System.Windows.Window.ShowDialog%2A>달리 <xref:System.Windows.Window.Show%2A> 는 즉시 반환 됩니다. 따라서 호출하는 창에서는 모덜리스 대화 상자가 닫히는 시기를 알 수 없기 때문에 대화 상자의 결과를 검사하거나 대화 상자에서 더 처리할 데이터를 가져올 시기를 알 수가 없습니다. 대신, 대화 상자에서 호출한 창에 처리할 데이터를 반환할 다른 방법을 만들어야 합니다.  
  
#### <a name="processing-data-returned-from-a-modeless-dialog-box"></a>모덜리스 대화 상자에서 반환 된 데이터 처리  

이 예제에서는 `FindDialogBox` 특정 빈도를 제외 하 고 검색 되는 텍스트에 따라 주 창에 하나 이상의 찾기 결과를 반환할 수 있습니다. 모달 대화 상자와 마찬가지로, 모덜리스 대화 상자에서도 속성을 사용하여 결과를 반환할 수 있습니다. 그러나 대화 상자를 소유한 창에서 해당 속성을 검사할 시기를 알아야 합니다. 한 가지 방법은 대화 상자에서 텍스트를 찾을 때마다 발생하는 이벤트를 구현하는 것입니다. `FindDialogBox`는 `TextFoundEvent` 이 목적을 위해 먼저 대리자를 필요로 하는을 구현 합니다.  

[!code-csharp[The TextFoundEventHandler delegate](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/TextFoundEventHandler.cs)]
[!code-vb[The TextFoundEventHandler delegate](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/TextFoundEventHandler.vb)]  

대리자를 사용 하 `FindDialogBox` 여를 `TextFoundEvent`구현 합니다. `TextFoundEventHandler`
  
[!code-csharp[The TextFound event](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/FindDialogBox.xaml.cs?range=1-17,125-126)]
[!code-vb[The TextFound event](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/FindDialogBox.xaml.vb?range=1-15,102-103)]

따라서는 검색 결과가 발견 될 때 이벤트를 발생 시킬 수있습니다.`Find`  
  
[!code-csharp[Raising the TextFound event](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/FindDialogBox.xaml.cs?range=1-9,50-52,91-94,124-127)]
[!code-vb[Raising the TextFound event](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/FindDialogBox.xaml.vb?range=1-9,15,60-64,102-103)]  

소유자 창에서는 그 후에 이 이벤트를 등록하고 처리해야 합니다.

[!code-csharp[Registering and handling the event](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml.cs?range=1-10,184-195)]
[!code-vb[Registering and handling the event](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MainWindow.xaml.vb?range=1-9,126-132)]  

#### <a name="closing-a-modeless-dialog-box"></a>모덜리스 대화 상자 닫기

는 <xref:System.Windows.Window.DialogResult%2A> 설정할 필요가 없기 때문에 다음과 같은 시스템 제공 메커니즘을 사용 하 여 모덜리스 대화 상자를 닫을 수 있습니다.  
  
- 제목 표시줄에서 **닫기** 단추를 클릭 합니다.  
  
- ALT+F4 누르기.  
  
- **시스템** 메뉴에서 **닫기** 를 선택 합니다.  
  
또는 닫기 단추를 클릭할 때 <xref:System.Windows.Window.Close%2A> 코드에서 를 호출할 수 있습니다.  

[!code-csharp[Calling the Close method](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/FindDialogBox.xaml.cs?range=1-9,119-126)]
[!code-vb[Calling the Close method](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/FindDialogBox.xaml.vb?range=1-9,99-103)]  

## <a name="see-also"></a>참고자료

- [팝업 개요](../controls/popup-overview.md)
- [대화 상자 샘플](https://go.microsoft.com/fwlink/?LinkID=159984)
