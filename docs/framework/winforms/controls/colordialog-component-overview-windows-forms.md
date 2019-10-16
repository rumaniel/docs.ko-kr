---
title: ColorDialog 구성 요소 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- ColorDialog
helpviewer_keywords:
- color dialog box [Windows Forms], about color dialog box
- ColorDialog component [Windows Forms], about ColorDialog
ms.assetid: 6dbdd8f0-f697-4728-bb09-7ea156f6d800
ms.openlocfilehash: 284d42218fb4fbce873325b1e45c883d51eefab8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61956340"
---
# <a name="colordialog-component-overview-windows-forms"></a>ColorDialog 구성 요소 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.ColorDialog> 구성 요소는 사용자 색상표에서 색을 선택 하 고 해당 색상표에 사용자 지정 색을 추가할 수 있도록 미리 구성 된 대화 상자. 이 구성 요소는 다른 Windows 기반 애플리케이션에서 색상 선택하는 데 사용하는 대화 상자와 동일합니다. 고유한 대화 상자를 구성하는 대신 Windows 기반 애플리케이션 내에서 간단한 솔루션으로 사용합니다.  
  
 대화 상자에서 선택한 색에 반환 되는 <xref:System.Windows.Forms.ColorDialog.Color%2A> 속성입니다. 경우는 <xref:System.Windows.Forms.ColorDialog.AllowFullOpen%2A> 속성이 `false`"사용자 지정 색" 단추가 비활성화 되 고 사용자가 미리 정의 된 색상표 색으로 제한 합니다. 경우는 <xref:System.Windows.Forms.ColorDialog.SolidColorOnly%2A> 속성이 `true`, 디더링된 색을 선택할 수 없습니다. 대화 상자를 표시 하려면 해당 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 메서드.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ColorDialog>
- [ColorDialog 구성 요소](colordialog-component-windows-forms.md)
- [대화 상자 컨트롤 및 구성 요소](dialog-box-controls-and-components-windows-forms.md)
- [방법: Windows Forms ColorDialog 구성 요소의 모양 변경](how-to-change-the-appearance-of-the-windows-forms-colordialog-component.md)
