---
title: '방법: Windows Forms ColorDialog 구성 요소의 모양 변경'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- ColorDialog component [Windows Forms], examples
- ColorDialog component [Windows Forms], formatting appearance
- color dialog box [Windows Forms], configuring appearance
ms.assetid: bba4e262-1cd7-4f63-89cf-330a36f7b539
ms.openlocfilehash: d2bb9e06d9d84a9b61c67510e9c012066f69d55e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61595455"
---
# <a name="how-to-change-the-appearance-of-the-windows-forms-colordialog-component"></a>방법: Windows Forms ColorDialog 구성 요소의 모양 변경
Windows Forms의 모양에 구성한 <xref:System.Windows.Forms.ColorDialog> 다양 한 해당 속성을 사용 하 여 구성 요소입니다. 대화 상자에는 두 섹션이 있습니다.-기본 색을 사용자 지정 색을 정의할 수 있도록 표시 하는 것입니다.  
  
 대부분의 속성 대화 상자에서 선택할 수 있는 색을 제한 합니다. 경우는 <xref:System.Windows.Forms.ColorDialog.AllowFullOpen%2A> 속성 `true`는 사용자가 사용자 지정 색을 정의할 수 있습니다. 합니다 <xref:System.Windows.Forms.ColorDialog.FullOpen%2A> 속성은 `true` ; 사용자 지정 색을 정의 하는 대화 상자 확장 되 면 그렇지 않은 경우 사용자를 클릭 해야 "사용자 지정 색 만들기" 단추입니다. 경우는 <xref:System.Windows.Forms.ColorDialog.AnyColor%2A> 속성이 `true`, 대화 상자 기본 색 집합에서 사용 가능한 모든 색을 표시 합니다. 경우는 <xref:System.Windows.Forms.ColorDialog.SolidColorOnly%2A> 속성이 `true`, 디더링된 색을 선택할 수 없습니다. 사용자는 단색만 선택할 수 있습니다.  
  
 경우는 <xref:System.Windows.Forms.ColorDialog.ShowHelp%2A> 속성이 `true`, 대화 상자에 도움말 단추가 표시 됩니다. 사용자가 도움말 단추를 클릭 합니다 <xref:System.Windows.Forms.ColorDialog> 구성 요소의 <xref:System.Windows.Forms.CommonDialog.HelpRequest> 이벤트가 발생 합니다.  
  
### <a name="to-configure-the-appearance-of-the-color-dialog-box"></a>모양의 색 대화 상자를 구성 하려면  
  
1. 설정 합니다 <xref:System.Windows.Forms.ColorDialog.AllowFullOpen%2A>, <xref:System.Windows.Forms.ColorDialog.AnyColor%2A>를 <xref:System.Windows.Forms.ColorDialog.SolidColorOnly%2A>, 및 <xref:System.Windows.Forms.ColorDialog.ShowHelp%2A> 속성을 원하는 값입니다.  
  
    ```vb  
    ColorDialog1.AllowFullOpen = True  
    ColorDialog1.AnyColor = True  
    ColorDialog1.SolidColorOnly = False  
    ColorDialog1.ShowHelp = True  
    ```  
  
    ```csharp  
    colorDialog1.AllowFullOpen = true;  
    colorDialog1.AnyColor = true;  
    colorDialog1.SolidColorOnly = false;  
    colorDialog1.ShowHelp = true;  
    ```  
  
    ```cpp  
    colorDialog1->AllowFullOpen = true;  
    colorDialog1->AnyColor = true;  
    colorDialog1->SolidColorOnly = false;  
    colorDialog1->ShowHelp = true;  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ColorDialog>
- [ColorDialog 구성 요소](colordialog-component-windows-forms.md)
- [ColorDialog 구성 요소 개요](colordialog-component-overview-windows-forms.md)
