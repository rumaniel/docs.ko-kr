---
title: '방법: Windows Forms NumericUpDown 컨트롤에 대한 형식 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- NumericUpDown control [Windows Forms], formatting values
- up-down controls [Windows Forms], formatting numeric values
ms.assetid: fa7c5557-6bfb-45b2-975d-8887b23b0ba0
ms.openlocfilehash: 6db7a1b2aeb7282c3ac827cb8319706ed348fc22
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69949159"
---
# <a name="how-to-set-the-format-for-the-windows-forms-numericupdown-control"></a>방법: Windows Forms NumericUpDown 컨트롤에 대한 형식 설정
Windows Forms <xref:System.Windows.Forms.NumericUpDown> 컨트롤에 값이 표시 되는 방법을 구성할 수 있습니다. 속성 <xref:System.Windows.Forms.NumericUpDown.DecimalPlaces%2A> 은 소수점 뒤에 표시 되는 숫자의 수를 결정 합니다. 기본값은 0입니다. 속성 <xref:System.Windows.Forms.NumericUpDown.ThousandsSeparator%2A> 은 소수점이 하 3 자리 마다 구분 기호를 삽입할지 여부를 결정 합니다. `false`기본값은입니다. 이 컨트롤은 <xref:System.Windows.Forms.NumericUpDown.Hexadecimal%2A> 속성이로 `true`설정 된 경우 decimal 형식 대신 16 진수 형식으로 값을 표시할 수 있습니다. 기본값 `false`은입니다.  
  
### <a name="to-format-the-numeric-value"></a>숫자 값의 형식을 지정 하려면  
  
- <xref:System.Windows.Forms.NumericUpDown.DecimalPlaces%2A> 속성을 정수로 설정 하 고 <xref:System.Windows.Forms.NumericUpDown.ThousandsSeparator%2A> 속성을 또는 `false`로 `true` 설정 하 여 10 진수 값을 표시 합니다.  
  
    ```vb  
    NumericUpDown1.DecimalPlaces = 2  
    NumericUpDown1.ThousandsSeparator = True  
    ```  
  
    ```csharp  
    numericUpDown1.DecimalPlaces = 2;  
    numericUpDown1.ThousandsSeparator = true;  
    ```  
  
    ```cpp  
    numericUpDown1->DecimalPlaces = 2;  
    numericUpDown1->ThousandsSeparator = true;  
    ```  
  
     또는  
  
- <xref:System.Windows.Forms.NumericUpDown.Hexadecimal%2A> 속성을로 `true`설정 하 여 16 진수 값을 표시 합니다.  
  
    ```vb  
    NumericUpDown1.Hexadecimal = True  
    ```  
  
    ```csharp  
    numericUpDown1.Hexadecimal = true;  
    ```  
  
    ```cpp  
    numericUpDown1->Hexadecimal = true;  
    ```  
  
    > [!NOTE]
    > 값이 폼에 16 진수로 표시 되는 경우에도 <xref:System.Windows.Forms.NumericUpDown.Value%2A> 속성에서 수행 하는 모든 테스트는 10 진수 값을 테스트 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.NumericUpDown>
- [NumericUpDown 컨트롤](numericupdown-control-windows-forms.md)
- [NumericUpDown 컨트롤 개요](numericupdown-control-overview-windows-forms.md)
