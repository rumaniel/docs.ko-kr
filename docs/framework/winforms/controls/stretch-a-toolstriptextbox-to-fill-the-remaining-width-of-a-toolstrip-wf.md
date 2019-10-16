---
title: '방법: Toolstriptextbox를 늘려 ToolStrip (Windows Forms)의 나머지 너비 채우기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text boxes [Windows Forms], stretching in ToolStrip control [Windows Forms]
- ToolStrip control [Windows Forms], stretching a text box
ms.assetid: 0e610fbf-85fe-414c-900c-9704a5dd5cc6
ms.openlocfilehash: 7a9fd703206caadf2d9c63d92567f8b1c3b51e61
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64751424"
---
# <a name="how-to-stretch-a-toolstriptextbox-to-fill-the-remaining-width-of-a-toolstrip-windows-forms"></a>방법: Toolstriptextbox를 늘려 ToolStrip (Windows Forms)의 나머지 너비 채우기
설정한 경우를 <xref:System.Windows.Forms.ToolStrip.Stretch%2A> 의 속성을 <xref:System.Windows.Forms.ToolStrip> 컨트롤을 `true`, 컨트롤이 해당 컨테이너 종단 간 채우고 해당 컨테이너의 크기를 조정 하는 경우 크기를 조정 합니다. 이 구성에서는 유용할 수 있습니다 것과 같은 컨트롤에서 항목을 확장 하는 <xref:System.Windows.Forms.ToolStripTextBox>, 사용 가능한 공간 및 크기를 조정 하는 경우 크기를 조정 합니다. 이 확장 유용 예를 들어, 모양 및 Microsoft® Internet Explorer의 주소 표시줄에 비슷한 동작을 수행 하려는 경우.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서 파생 된 클래스를 제공 <xref:System.Windows.Forms.ToolStripTextBox> 호출 `ToolStripSpringTextBox`합니다. 이 클래스에서 재정의 된 <xref:System.Windows.Forms.ToolStripTextBox.GetPreferredSize%2A> 부모 사용 가능한 너비를 계산 하는 방법 <xref:System.Windows.Forms.ToolStrip> 다른 모든 항목의 결합 된 너비를 뺀 후 제어 합니다. 이 코드 예제에서는 한 <xref:System.Windows.Forms.Form> 클래스 및 `Program` 클래스의 새 동작을 보여 줍니다.  
  
 [!code-csharp[ToolStripSpringTextBox#00](~/samples/snippets/csharp/VS_Snippets_Winforms/ToolStripSpringTextBox/cs/ToolStripSpringTextBox.cs#00)]
 [!code-vb[ToolStripSpringTextBox#00](~/samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripSpringTextBox/vb/ToolStripSpringTextBox.vb#00)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System, System.Drawing 및 System.Windows.Forms 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.ToolStrip.Stretch%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.ToolStripTextBox>
- <xref:System.Windows.Forms.ToolStripTextBox.GetPreferredSize%2A?displayProperty=nameWithType>
- [ToolStrip 컨트롤 아키텍처](toolstrip-control-architecture.md)
- [방법: StatusStrip에서 대화형으로 Spring 속성 사용](how-to-use-the-spring-property-interactively-in-a-statusstrip.md)
