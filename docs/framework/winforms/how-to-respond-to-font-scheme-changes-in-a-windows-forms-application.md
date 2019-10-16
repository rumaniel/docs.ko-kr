---
title: '방법: Windows Forms 애플리케이션에서 글꼴 구성표 변경 내용에 대응'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows Forms, font scheme changes
ms.assetid: 4db27702-22e7-43bf-a07d-9a004549853c
ms.openlocfilehash: 9fd7f99b35730cf867bfad5da24bc3f223e9a0f8
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425328"
---
# <a name="how-to-respond-to-font-scheme-changes-in-a-windows-forms-application"></a>방법: Windows Forms 애플리케이션에서 글꼴 구성표 변경 내용에 대응
Windows 운영 체제에서 사용자 크게 또는 작게 표시 기본 글꼴을 확인 하려면 시스템 글꼴 설정을 변경할 수 있습니다. 이러한 글꼴 설정을 변경 하는 것이 더 큰 형식 해당 화면에 텍스트를 읽이 필요는 시각 장애가 있는 사용자에 대 한 중요 합니다. 글꼴 구성표 변경 될 때마다 양식 및 포함 된 모든 텍스트의 크기를 늘리거나 줄여 이러한 변경에 반응 하는 Windows Forms 응용 프로그램을 조정할 수 있습니다. 동적으로 글꼴 크기의 변경 내용을 수용 하기 위해 폼을 하려는 경우에 폼에 코드를 추가할 수 있습니다.  
  
 일반적으로 Windows Forms에서 사용 된 기본 글꼴은 글꼴에서 반환 되는 <xref:Microsoft.Win32> 네임 스페이스 호출 `GetStockObject(DEFAULT_GUI_FONT)`합니다. 이 호출에서 반환 되는 글꼴 화면 해상도 변경 하는 경우에 변경 됩니다. 코드에서 기본 글꼴을 변경 해야 다음 절차 에서처럼 <xref:System.Drawing.SystemFonts.IconTitleFont%2A> 글꼴 크기의 변경 내용에 응답 합니다.  
  
### <a name="to-use-the-desktop-font-and-respond-to-font-scheme-changes"></a>데스크톱 글꼴을 사용 하 여 글꼴 구성표 변경에 응답  
  
1. 폼에 만들고에 원하는 컨트롤을 추가 합니다. 자세한 내용은 [방법: 명령줄에서 Windows Forms 응용 프로그램을 만듭니다](how-to-create-a-windows-forms-application-from-the-command-line.md) 하 고 [사용 하 여 Windows Forms에서 컨트롤](./controls/controls-to-use-on-windows-forms.md)합니다.  
  
2. 에 대 한 참조를 추가 합니다 <xref:Microsoft.Win32> 코드에 네임 스페이스입니다.  
  
     [!code-csharp[WinFormsAutoScaling#2](~/samples/snippets/csharp/VS_Snippets_Winforms/WinFormsAutoScaling/CS/Form1.cs#2)]
     [!code-vb[WinFormsAutoScaling#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/WinFormsAutoScaling/VB/Form1.vb#2)]  
  
3. 필요한 이벤트 처리기를 연결 하는 데 사용 하 여 폼의 기본 글꼴을 변경 하 여 폼의 생성자에 다음 코드를 추가 합니다.  
  
     [!code-csharp[WinFormsAutoScaling#3](~/samples/snippets/csharp/VS_Snippets_Winforms/WinFormsAutoScaling/CS/Form1.cs#3)]
     [!code-vb[WinFormsAutoScaling#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/WinFormsAutoScaling/VB/Form1.vb#3)]  
  
4. 에 대 한 처리기를 구현 합니다 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged> 하면 폼이 자동으로 크기를 조정 하는 이벤트 때는 <xref:Microsoft.Win32.UserPreferenceCategory.Window> 범주 변경 합니다.  
  
     [!code-csharp[WinFormsAutoScaling#4](~/samples/snippets/csharp/VS_Snippets_Winforms/WinFormsAutoScaling/CS/Form1.cs#4)]
     [!code-vb[WinFormsAutoScaling#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/WinFormsAutoScaling/VB/Form1.vb#4)]  
  
5. 마지막으로,에 대 한 처리기를 구현 합니다 <xref:System.Windows.Forms.Form.FormClosing> 분리 하는 이벤트를 <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged> 이벤트 처리기입니다.  
  
     > [!IMPORTANT]
     > 이 코드를 포함 하지 않으면 응용 프로그램에 메모리 누수가 발생 합니다.  
  
     [!code-csharp[WinFormsAutoScaling#5](~/samples/snippets/csharp/VS_Snippets_Winforms/WinFormsAutoScaling/CS/Form1.cs#5)]
     [!code-vb[WinFormsAutoScaling#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/WinFormsAutoScaling/VB/Form1.vb#5)]  
  
6. 코드를 컴파일하고 실행합니다.  
  
### <a name="to-manually-change-the-font-scheme-in-windows-xp"></a>수동으로 Windows XP에서 글꼴 구성표 변경  
  
1. Windows Forms 응용 프로그램 실행 되는 동안 Windows 바탕 화면을 마우스 오른쪽 단추로 클릭 하 고 선택 **속성** 바로 가기 메뉴에서.  
  
2. 에 **표시 속성** 대화 상자에서 클릭 합니다 **모양을** 탭 합니다.  
  
3. **글꼴 크기** 드롭다운 목록 상자에서 새 글꼴 크기를 선택 합니다.  
  
     폼이 데스크톱 글꼴 구성표의 런타임 변경 내용에 반응 이제 알 수 있습니다. 사용자 간에 변경 될 때 **정규**를 **큰 글꼴**, 및 **아주 큰 글꼴**, 폼 글꼴을 변경 하 고 크기가 올바르게 조정 합니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[WinFormsAutoScaling#1](~/samples/snippets/csharp/VS_Snippets_Winforms/WinFormsAutoScaling/CS/Form1.cs#1)]
 [!code-vb[WinFormsAutoScaling#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/WinFormsAutoScaling/VB/Form1.vb#1)]  
  
 이 코드 예제는 생성자 호출을 포함 `InitializeComponent`, Visual Studio에서 새 Windows Forms 프로젝트를 만들 때 정의 합니다. 명령줄에서 응용 프로그램을 작성 하는 경우이 코드 줄을 제거 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ContainerControl.PerformAutoScale%2A>
- [Windows Forms의 자동 크기 조정](automatic-scaling-in-windows-forms.md)
