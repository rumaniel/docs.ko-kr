---
title: '방법: Windows Forms ErrorProvider 구성 요소를 사용하여 양식 유효성 오류 아이콘 표시'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- errors [Windows Forms], displaying to users
- error icons
- ErrorProvider component [Windows Forms], displaying error icons
- error messages [Windows Forms], displaying icons
ms.assetid: 3b681a32-9db4-497b-a34b-34980eabee46
ms.openlocfilehash: 2af8d3b9ea97b678c493de8a58d439b62f448387
ms.sourcegitcommit: 7e129d879ddb42a8b4334eee35727afe3d437952
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66053707"
---
# <a name="how-to-display-error-icons-for-form-validation-with-the-windows-forms-errorprovider-component"></a>방법: Windows Forms ErrorProvider 구성 요소를 사용하여 양식 유효성 오류 아이콘 표시
Windows Forms를 사용할 수 있습니다 <xref:System.Windows.Forms.ErrorProvider> 구성 요소에 잘못 된 데이터를 입력할 때 오류 아이콘을 표시 합니다. 두 개 이상의 폼의 컨트롤 간에 이동 하 여 유효성 검사 코드를 호출할 수 있어야 합니다.  
  
### <a name="to-display-an-error-icon-when-a-controls-value-is-invalid"></a>컨트롤의 값에 유효 하지 않을 때 오류 아이콘을 표시 하려면  
  
1. 두 개의 컨트롤 추가-예를 들어, 텍스트 상자-Windows 폼에 있습니다.  
  
2. 추가 <xref:System.Windows.Forms.ErrorProvider> 폼에 구성 요소입니다.  
  
3. 첫 번째 컨트롤을 선택 하 고 코드를 추가 하는 <xref:System.Windows.Forms.Control.Validating> 이벤트 처리기입니다. 이 코드를 제대로 실행 되려면, 절차 이벤트에 연결 되어야 합니다. 자세한 내용은 [방법: 런타임에 Windows Forms에 대 한 이벤트 처리기를 만들](../how-to-create-event-handlers-at-run-time-for-windows-forms.md)합니다.  
  
     다음 코드는 사용자가 입력 한; 데이터의 유효성을 테스트 데이터가 유효 하지 않은 경우는 <xref:System.Windows.Forms.ErrorProvider.SetError%2A> 메서드가 호출 됩니다. 첫 번째 인수는 <xref:System.Windows.Forms.ErrorProvider.SetError%2A> 메서드 아이콘 옆에 표시할 컨트롤을 지정 합니다. 두 번째 인수에 표시할 오류 텍스트입니다.  
  
    ```vb  
    Private Sub TextBox1_Validating(ByVal Sender As Object, _  
       ByVal e As System.ComponentModel.CancelEventArgs) Handles _  
       TextBox1.Validating  
          If Not IsNumeric(TextBox1.Text) Then  
             ErrorProvider1.SetError(TextBox1, "Not a numeric value.")  
          Else  
             ' Clear the error.  
             ErrorProvider1.SetError(TextBox1, "")  
          End If  
    End Sub  
    ```  
  
    ```csharp  
    protected void textBox1_Validating (object sender,  
       System.ComponentModel.CancelEventArgs e)  
    {  
       try  
       {  
          int x = Int32.Parse(textBox1.Text);  
          errorProvider1.SetError(textBox1, "");  
       }  
       catch (Exception ex)  
       {  
          errorProvider1.SetError(textBox1, "Not an integer value.");  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void textBox1_Validating(System::Object ^  sender,  
          System::ComponentModel::CancelEventArgs ^  e)  
       {  
          try  
          {  
             int x = Int32::Parse(textBox1->Text);  
             errorProvider1->SetError(textBox1, "");  
          }  
          catch (System::Exception ^ ex)  
          {  
             errorProvider1->SetError(textBox1, "Not an integer value.");  
          }  
       }  
    ```  
  
     (Visual C#, Visual C++) 이벤트 처리기를 등록 하려면 폼의 생성자에 다음 코드를 추가 합니다.  
  
    ```csharp  
    this.textBox1.Validating += new  
    System.ComponentModel.CancelEventHandler(this.textBox1_Validating);  
    ```  
  
    ```cpp  
    this->textBox1->Validating += gcnew  
       System::ComponentModel::CancelEventHandler  
       (this, &Form1::textBox1_Validating);  
    ```  
  
4. 프로젝트를 실행합니다. 그 다음으로 첫 번째 컨트롤을 두 번째 탭에 (이 예제에서는 숫자가 아닌)의 잘못 된 데이터를 입력 합니다. 오류 텍스트를 보려면 마우스 포인터를 사용 하 여 오류 아이콘이 표시 되 면 해당 가리킵니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ErrorProvider.SetError%2A>
- [ErrorProvider 구성 요소 개요](errorprovider-component-overview-windows-forms.md)
- [방법: Windows Forms ErrorProvider 구성 요소를 사용 하 여 데이터 집합에 있는 오류 보기](view-errors-within-a-dataset-with-wf-errorprovider-component.md)
