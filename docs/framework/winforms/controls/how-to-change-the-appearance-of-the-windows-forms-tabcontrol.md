---
title: '방법: Windows Forms TabControl의 모양 변경'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- icons [Windows Forms], displaying on tabs
- TabControl control [Windows Forms], changing page appearance
- tabs [Windows Forms], controlling appearance
- buttons [Windows Forms], displaying tabs as
ms.assetid: 7c6cc443-ed62-4d26-b94d-b8913b44f773
ms.openlocfilehash: e8ab97c545577dd393fd7d9844b396973621e6a7
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64650865"
---
# <a name="how-to-change-the-appearance-of-the-windows-forms-tabcontrol"></a>방법: Windows Forms TabControl의 모양 변경
속성을 사용 하 여 Windows Forms에서 탭의 모양을 변경할 수 있습니다 합니다 <xref:System.Windows.Forms.TabControl> 하며 <xref:System.Windows.Forms.TabPage> 컨트롤에서 개별 탭에 구성 하는 개체입니다. 이러한 속성을 설정 하면 수 탭에서 이미지를 표시, 가로로 대신 세로 탭이 표시, 탭의 여러 행을 표시 및 사용 하도록 설정 또는 탭을 프로그래밍 방식으로 사용 하지 않도록 설정 합니다.  
  
### <a name="to-display-an-icon-on-the-label-part-of-a-tab"></a>탭 레이블 부분 아이콘을 표시 하려면  
  
1. 추가 <xref:System.Windows.Forms.ImageList> 컨트롤을 폼입니다.  
  
2. 이미지 목록에 이미지를 추가 합니다.  
  
     이미지 목록에 대 한 자세한 내용은 참조 하세요. [ImageList 구성 요소](imagelist-component-windows-forms.md) 고 [방법: 제거 이미지는 Windows Forms ImageList 구성 요소 추가 또는](how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md)합니다.  
  
3. 설정를 <xref:System.Windows.Forms.TabControl.ImageList%2A> 의 속성을 <xref:System.Windows.Forms.TabControl> 에 <xref:System.Windows.Forms.ImageList> 컨트롤.  
  
4. 설정 합니다 <xref:System.Windows.Forms.TabPage.ImageIndex%2A> 의 속성은 <xref:System.Windows.Forms.TabPage> 목록에서 적절 한 이미지의 인덱스입니다.  
  
### <a name="to-create-multiple-rows-of-tabs"></a>여러 행의 탭을 만들려면  
  
1. 탭 페이지 수를 추가 합니다.  
  
2. 설정 합니다 <xref:System.Windows.Forms.TabControl.Multiline%2A> 의 속성을 <xref:System.Windows.Forms.TabControl> 에 `true`.  
  
3. 탭 여러 행에 표시 되지 않는 경우 설정 합니다 <xref:System.Windows.Forms.Control.Width%2A> 의 속성을 <xref:System.Windows.Forms.TabControl> 모든 탭 보다 더 작게 할 합니다.  
  
### <a name="to-arrange-tabs-on-the-side-of-the-control"></a>탭 컨트롤의 측면을 정렬 하려면  
  
- 설정 합니다 <xref:System.Windows.Forms.TabControl.Alignment%2A> 의 속성을 <xref:System.Windows.Forms.TabControl> 에 <xref:System.Windows.Forms.TabAlignment.Left> 또는 <xref:System.Windows.Forms.TabAlignment.Right>.  
  
### <a name="to-programmatically-enable-or-disable-all-controls-on-a-tab"></a>프로그래밍 방식으로 사용 하도록 설정 또는 탭의 모든 컨트롤을 사용 하지 않도록 설정 하려면  
  
1. 설정 합니다 <xref:System.Windows.Forms.TabPage.Enabled%2A> 의 속성을 <xref:System.Windows.Forms.TabPage> 에 `true` 또는 `false`.  
  
    ```vb  
    TabPage1.Enabled = False  
    ```  
  
    ```csharp  
    tabPage1.Enabled = false;  
    ```  
  
    ```cpp  
    tabPage1->Enabled = false;  
    ```  
  
### <a name="to-display-tabs-as-buttons"></a>단추와 탭을 표시 하려면  
  
- 설정 합니다 <xref:System.Windows.Forms.TabControl.Appearance%2A> 의 속성을 <xref:System.Windows.Forms.TabControl> 에 <xref:System.Windows.Forms.TabAppearance.Buttons> 또는 <xref:System.Windows.Forms.TabAppearance.FlatButtons>.  
  
## <a name="see-also"></a>참고자료

- [TabControl 컨트롤](tabcontrol-control-windows-forms.md)
- [TabControl 컨트롤 개요](tabcontrol-control-overview-windows-forms.md)
- [방법: 탭 페이지에 컨트롤 추가](how-to-add-a-control-to-a-tab-page.md)
- [방법: 탭 페이지를 사용 하지 않도록 설정](how-to-disable-tab-pages.md)
- [방법: Windows Forms TabControl 사용 하 여 탭 추가 및 제거](how-to-add-and-remove-tabs-with-the-windows-forms-tabcontrol.md)
