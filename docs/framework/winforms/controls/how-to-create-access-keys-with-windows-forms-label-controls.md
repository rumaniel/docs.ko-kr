---
title: '방법: Windows Forms Label 컨트롤을 사용하여 선택키 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- controls [Windows Forms], access keys
- dialog box controls [Windows Forms], mnemonics
- access keys [Windows Forms], creating for controls
- Label control [Windows Forms], creating access keys
- mnemonics [Windows Forms], adding to dialog box controls
- mnemonics
- Windows Forms controls, access keys
- UseMnemonic property [Windows Forms], Label control
- keyboard shortcuts [Windows Forms], creating for controls
- access keys [Windows Forms], Windows Forms
ms.assetid: 5ee8f823-80be-4a4f-96a4-412671e2e306
ms.openlocfilehash: dd7f238f8c20ba990158f23344e36376d3b1cb7a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950532"
---
# <a name="how-to-create-access-keys-with-windows-forms-label-controls"></a>방법: Windows Forms Label 컨트롤을 사용하여 선택키 만들기
Windows Forms <xref:System.Windows.Forms.Label> 컨트롤은 다른 컨트롤에 대 한 선택 키를 정의 하는 데 사용할 수 있습니다. 레이블 컨트롤에서 선택 키를 정의 하는 경우 사용자는 ALT 키와 지정한 문자를 눌러 탭 순서에서 뒤에 오는 컨트롤로 포커스를 이동할 수 있습니다. 레이블은 포커스를 받을 수 없기 때문에 포커스가 탭 순서의 다음 컨트롤로 자동 이동 합니다. 이 방법을 사용 하 여 텍스트 상자, 콤보 상자, 목록 상자 및 데이터 표에 액세스 키를 할당할 수 있습니다.  
  
### <a name="to-assign-an-access-key-to-a-control-with-a-label"></a>레이블이 있는 컨트롤에 액세스 키를 할당 하려면  
  
1. 먼저 레이블을 그린 다음 다른 컨트롤을 그립니다.  
  
     또는  
  
     컨트롤을 임의의 순서로 그리고 레이블의 <xref:System.Windows.Forms.Control.TabIndex%2A> 속성을 다른 컨트롤 보다 하나 작은 값으로 설정 합니다.  
  
2. 레이블의 <xref:System.Windows.Forms.Label.UseMnemonic%2A> 속성을로 `true`설정 합니다.  
  
3. 레이블의 <xref:System.Windows.Forms.Label.Text%2A> 속성에 앰퍼샌드 (&)를 사용 하 여 레이블에 대 한 액세스 키를 할당 합니다. 자세한 내용은 [Windows Forms 컨트롤에 대 한 선택 키 만들기](how-to-create-access-keys-for-windows-forms-controls.md)를 참조 하세요.  
  
    > [!NOTE]
    > 앰퍼샌드를 사용 하 여 액세스 키를 만드는 대신 앰퍼샌드를 레이블 컨트롤에 표시 하는 것이 좋습니다. 이 문제는 데이터에 앰퍼샌드가 포함 된 레코드 집합의 필드에 레이블 컨트롤을 바인딩하는 경우에 발생할 수 있습니다. 레이블 컨트롤에 앰퍼샌드를 표시 하려면 <xref:System.Windows.Forms.Label.UseMnemonic%2A> 속성을로 `false`설정 합니다. 앰퍼샌드를 표시 하 고 액세스 키를 포함 하려는 경우 <xref:System.Windows.Forms.Label.UseMnemonic%2A> 속성을로 `true` 설정 하 고 앰퍼샌드 (&) 하나를 포함 하는 선택 키와 두 개의 앰퍼샌드를 표시 하는 앰퍼샌드를 나타냅니다.  
  
    ```vb  
    Label1.UseMnemonic = True  
    Label1.Text = "&Print"  
    Label2.UseMnemonic = True  
    Label2.Text = "&Copy && Paste"  
    ```  
  
    ```csharp  
    label1.UseMnemonic = true;  
    label1.Text = "&Print";  
    label2.UseMnemonic = true;  
    label2.Text = "&Copy && Paste";  
    ```  
  
    ```cpp  
    label1->UseMnemonic = true;  
    label1->Text = "&Print";  
    label2->UseMnemonic = true;  
    label2->Text = "&Copy && Paste";  
    ```  
  
## <a name="see-also"></a>참고자료

- [방법: 내용에 맞게 Windows Forms 레이블 컨트롤 크기 조정](how-to-size-a-windows-forms-label-control-to-fit-its-contents.md)
- [Label 컨트롤 개요](label-control-overview-windows-forms.md)
- [레이블 컨트롤](label-control-windows-forms.md)
