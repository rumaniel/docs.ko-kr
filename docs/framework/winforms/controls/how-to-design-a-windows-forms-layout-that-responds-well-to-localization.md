---
title: '방법: 지역화에 효과적으로 대응하는 Windows Forms 레이아웃 디자인'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TableLayoutPanel control [Windows Forms]
- application design [Windows Forms], localization
- Windows Forms, localization
- localization [Windows Forms], Windows Forms layout
ms.assetid: d13eff2d-701c-4b6e-8838-3885cbfb7223
ms.openlocfilehash: c1aa62413e1c9cc29507b7b0ed5cbf1c5fcea26a
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928564"
---
# <a name="how-to-design-a-windows-forms-layout-that-responds-well-to-localization"></a>방법: 지역화에 효과적으로 대응하는 Windows Forms 레이아웃 디자인
지역화할 준비가 된 폼을 만들면 국제 시장에서 개발 속도를 크게 높일 수 있습니다. <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤을 사용하여 <xref:System.Windows.Forms.Control.Text%2A> 속성 값 변경 때문에 컨트롤 크기가 조정될 때 정상적으로 응답하는 레이아웃을 구현할 수 있습니다.  
  
## <a name="example"></a>예제  
 이 폼에서는 표시된 문자열 값을 다른 언어로 번역할 때 비례하여 조정되는 레이아웃을 만드는 방법을 보여 줍니다. 이 번역 프로세스를 *지역화*라고 합니다. 자세한 내용은 [지역화](../../../standard/globalization-localization/localization.md)를 참조하세요.  
  
 Visual Studio에서는 이 작업이 광범위하게 지원됩니다.  [연습: 지역화](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/7k9fa71y(v=vs.100))를 위해 비율을 조정 하는 레이아웃 만들기  
  
 [!code-csharp[System.Windows.Forms.TableLayoutPanel.LocalizableForm#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.TableLayoutPanel.LocalizableForm/CS/localizableform.cs#1)]
 [!code-vb[System.Windows.Forms.TableLayoutPanel.LocalizableForm#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.TableLayoutPanel.LocalizableForm/VB/localizableform.vb#1)]  
  
## <a name="additional-resources"></a>추가 자료

1. [방법: TableLayoutPanel 컨트롤의 컨트롤 맞춤 및 늘이기](how-to-align-and-stretch-a-control-in-a-tablelayoutpanel-control.md)  
  
2. [연습: FlowLayoutPanel를 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)  

3. [방법: TableLayoutPanel 컨트롤의 행 및 열 범위](how-to-span-rows-and-columns-in-a-tablelayoutpanel-control.md)  
  
4. [방법: TableLayoutPanel 컨트롤의 열 및 행 편집](how-to-edit-columns-and-rows-in-a-tablelayoutpanel-control.md)  
  
5. [연습: Windows Forms 컨트롤에서 스마트 태그를 사용 하 여 일반 작업 수행](performing-common-tasks-using-smart-tags-on-wf-controls.md)  
  
6. [연습: TableLayoutPanel를 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)  

7. [연습: 안쪽 여백, 여백 및 AutoSize 속성을 사용 하 여 Windows Forms 컨트롤 레이아웃](windows-forms-controls-padding-autosize.md)  
  
8. [방법: AutoSize 및 TableLayoutPanel 컨트롤을 사용 하 여 Windows Forms에 대 한 지역화 지원](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/1zkt8b33(v=vs.100))  
  
9. [연습: 데이터 입력을 위한 크기 조정 가능한 Windows Form 만들기](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/991eahec(v=vs.100))  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System, System.Data, System.Drawing 및 System.Windows.Forms 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.TableLayoutPanel>
- <xref:System.Windows.Forms.FlowLayoutPanel>
- [지역화](../../../standard/globalization-localization/localization.md)
