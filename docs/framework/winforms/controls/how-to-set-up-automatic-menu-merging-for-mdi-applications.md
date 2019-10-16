---
title: '방법: MDI 애플리케이션에 대한 자동 메뉴 병합 설정'
ms.date: 03/30/2017
helpviewer_keywords:
- MenuStrip [Windows Forms], merging
- Merging [Windows Forms], automatic menu
ms.assetid: 55e32cad-1141-4a56-aa33-d9543ca3d393
ms.openlocfilehash: 33e07bb655d81c6a802ebdce871a2fed845a5c96
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62013025"
---
# <a name="how-to-set-up-automatic-menu-merging-for-mdi-applications"></a>방법: MDI 애플리케이션에 대한 자동 메뉴 병합 설정
다음 절차 (MDI) 다중 문서 인터페이스 응용 프로그램에 자동 병합 설정에 대 한 기본 단계를 제공 <xref:System.Windows.Forms.MenuStrip>합니다.  
  
### <a name="to-set-up-automatic-menu-merging"></a>자동 메뉴 병합 설정 하려면  
  
1. 설정 하 여 MDI 부모 폼을 만드는 해당 <xref:System.Windows.Forms.Form.IsMdiContainer%2A> 속성을 `true`입니다.  
  
2. 추가 된 <xref:System.Windows.Forms.MenuStrip> 설정 MDI 부모에 해당 <xref:System.Windows.Forms.Form.MainMenuStrip%2A> 속성을 <xref:System.Windows.Forms.MenuStrip>.  
  
3. MDI 자식 폼을 만들고 설정 해당 <xref:System.Windows.Forms.Form.MdiParent%2A> 속성을 부모 폼의 이름입니다.  
  
4. 추가 된 <xref:System.Windows.Forms.MenuStrip> MDI 자식 폼입니다.  
  
5. 자식 폼을 설정 합니다 <xref:System.Windows.Forms.ToolStripItem.Visible%2A> 의 속성을 <xref:System.Windows.Forms.MenuStrip> 에 `false`.  
  
6. 자식 폼의 메뉴 항목을 추가할 <xref:System.Windows.Forms.MenuStrip> 부모 폼의 병합 하려는 <xref:System.Windows.Forms.MenuStrip> 자식 폼이 활성화 하는 경우.  
  
7. 사용 하 여는 <xref:System.Windows.Forms.ToolStripItem.MergeAction%2A> 자식 폼의 메뉴에서 속성 항목 <xref:System.Windows.Forms.MenuStrip> 부모 폼에 병합 되는 방식을 제어 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStripMenuItem>
- [MenuStrip 컨트롤 개요](menustrip-control-overview-windows-forms.md)
