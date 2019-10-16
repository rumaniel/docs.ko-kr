---
title: Windows Forms에서 사용자 입력 유효성 검사
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, validating user input
- validation [Windows Forms], Windows Forms user input
- user input [Windows Forms], validating in Windows Forms
- validating user input [Windows Forms], Windows Forms
ms.assetid: 4ec07681-1dee-4bf9-be5e-718f635a33a1
ms.openlocfilehash: 7ee99d1b264f508882418c83da8e82759b0d95fa
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70206129"
---
# <a name="user-input-validation-in-windows-forms"></a>Windows Forms에서 사용자 입력 유효성 검사
사용자가 응용 프로그램에 데이터를 입력 하는 경우 응용 프로그램에서 사용 하기 전에 데이터가 유효한 지 확인 해야 할 수 있습니다. 특정 텍스트 필드의 길이는 0이 아니어야 하 고, 필드는 전화 번호 또는 형식이 올바른 형식의 데이터로 포맷 되거나, 데이터베이스의 보안을 손상 시키는 데 사용할 수 있는 안전 하지 않은 문자를 포함 하지 않을 수 있습니다. Windows Forms는 응용 프로그램에서 입력의 유효성을 검사 하는 여러 가지 방법을 제공 합니다.  
  
## <a name="validation-with-the-maskedtextbox-control"></a>MaskedTextBox 컨트롤을 사용 하 여 유효성 검사  
 사용자가 전화 번호 또는 부품 번호와 같은 잘 정의 된 형식으로 데이터를 입력 해야 하는 경우 컨트롤을 <xref:System.Windows.Forms.MaskedTextBox> 사용 하 여 코드를 최소한으로 빠르게 수행할 수 있습니다. *마스크* 는 텍스트 상자의 지정 된 위치에 입력할 수 있는 문자를 지정 하는 마스킹 언어의 문자로 구성 된 문자열입니다. 컨트롤은 사용자에 게 프롬프트 집합을 표시 합니다. 사용자가 잘못 된 항목을 입력 하는 경우, 예를 들어 숫자가 필요할 때 문자를 입력 하면 컨트롤에서 자동으로 입력을 거부 합니다.  
  
 에서 <xref:System.Windows.Forms.MaskedTextBox> 사용 하는 마스킹 언어는 매우 유연 합니다. 이 기능을 사용 하면 필요한 문자, 선택적 문자, 문자 (예: 하이픈 및 괄호, 통화 문자 및 날짜 구분 기호)를 지정할 수 있습니다. 컨트롤은 데이터 소스에 바인딩된 경우에도 잘 작동 합니다. 데이터 바인딩의 <xref:System.Windows.Forms.Binding.Parse> 이벤트를 사용 하 여 마스크를 따르도록 들어오는 데이터의 서식을 다시 지정 하 고, 이벤트를 사용 하 여 데이터 필드의 사양을 따르도록 보내는 데이터의 서식을 다시 지정할 수 있습니다. <xref:System.Windows.Forms.Binding.Format>  
  
 자세한 내용은 [MaskedTextBox Control](./controls/maskedtextbox-control-windows-forms.md)을 참조 하세요.  
  
## <a name="event-driven-validation"></a>이벤트 기반 유효성 검사  
 유효성 검사를 완전히 프로그래밍 방식으로 제어 하거나 복잡 한 유효성 검사를 수행 해야 하는 경우 대부분의 Windows Forms 컨트롤에 기본 제공 되는 유효성 검사 이벤트를 사용 해야 합니다. 자유 형식 사용자 입력을 허용 하는 각 컨트롤에 <xref:System.Windows.Forms.Control.Validating> 는 컨트롤에 데이터 유효성 검사가 필요할 때마다 발생 하는 이벤트가 있습니다. 이벤트 처리 <xref:System.Windows.Forms.Control.Validating> 메서드에서는 여러 가지 방법으로 사용자 입력의 유효성을 검사할 수 있습니다. 예를 들어 우편 번호를 포함 해야 하는 텍스트 상자가 있는 경우 다음과 같은 방법으로 유효성 검사를 수행할 수 있습니다.  
  
- 우편 번호가 특정 우편 번호 그룹에 속해야 하는 경우 입력에 대해 문자열 비교를 수행 하 여 사용자가 입력 한 데이터의 유효성을 검사할 수 있습니다. 예를 들어 우편 번호가 {10001, 10002, 10003} 집합에 있어야 하는 경우 문자열 비교를 사용 하 여 데이터의 유효성을 검사할 수 있습니다.  
  
- 우편 번호가 특정 폼에 있어야 하는 경우 정규식을 사용 하 여 사용자가 입력 한 데이터의 유효성을 검사할 수 있습니다. 예를 들어 또는 `#####` `#####-####`폼의 유효성을 검사 하기 위해 정규식을 사용할 `^(\d{5})(-\d{4})?$`수 있습니다. 양식의 `A#A #A#`유효성을 검사 하기 위해 `[A-Z]\d[A-Z] \d[A-Z]\d`정규식을 사용할 수 있습니다. 정규식에 대 한 자세한 내용은 정규식 및 [정규식 예제](../../standard/base-types/regular-expression-examples.md) [.NET Framework](../../standard/base-types/regular-expressions.md) 를 참조 하세요.  
  
- 우편 번호가 유효한 미국 우편 번호 여야 하는 경우 우편 번호 웹 서비스를 호출 하 여 사용자가 입력 한 데이터의 유효성을 검사할 수 있습니다.  
  
 이벤트 <xref:System.Windows.Forms.Control.Validating> 는 형식의 <xref:System.ComponentModel.CancelEventArgs>개체를 제공 합니다. 컨트롤의 데이터가 유효 하지 않은 것으로 확인 되 면이 개체의 <xref:System.Windows.Forms.Control.Validating> <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 속성을로 `true`설정 하 여 이벤트를 취소할 수 있습니다. <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 속성을 설정 하지 않으면 Windows Forms에서 해당 컨트롤에 대 한 유효성 검사를 완료 한 것으로 가정 하 <xref:System.Windows.Forms.Control.Validated> 고 이벤트를 발생 시킵니다.  
  
 에서 <xref:System.Windows.Controls.TextBox>전자 메일 주소의 유효성을 검사 하는 코드 예제는를 <xref:System.Windows.Forms.Control.Validating>참조 하십시오.  
  
### <a name="data-binding-and-event-driven-validation"></a>데이터 바인딩 및 이벤트 구동 유효성 검사  
 유효성 검사는 데이터 원본 (예: 데이터베이스 테이블)에 컨트롤을 바인딩한 경우 매우 유용 합니다. 유효성 검사를 사용 하 여 컨트롤의 데이터가 데이터 소스에 필요한 형식을 충족 하는지, 안전 하지 않을 수 있는 따옴표 및 백슬래시와 같은 특수 문자를 포함 하 고 있지 않은지 확인할 수 있습니다.  
  
 데이터 바인딩을 사용 하는 경우 <xref:System.Windows.Forms.Control.Validating> 이벤트를 실행 하는 동안 컨트롤의 데이터가 데이터 원본과 동기화 됩니다. <xref:System.Windows.Forms.Control.Validating> 이벤트를 취소 하면 데이터가 데이터 원본과 동기화 되지 않습니다.  
  
> [!IMPORTANT]
> <xref:System.Windows.Forms.Control.Validating> 이벤트 후에 발생 하는 사용자 지정 유효성 검사를 수행 하는 경우 데이터 바인딩에 영향을 주지 않습니다. 예를 들어 <xref:System.Windows.Forms.Control.Validated> 이벤트에 데이터 바인딩을 취소 하려고 하는 코드가 있는 경우 데이터 바인딩이 계속 발생 합니다. 이 경우 <xref:System.Windows.Forms.Control.Validated> 이벤트에서 유효성 검사를 수행 하려면 컨트롤의 **데이터 원본 업데이트 모드** 속성 ( **(데이터 바인딩)** \\ **(고급)** )을 **onvalidation** 에서 **Never**로 변경 하 고를 추가 *합니다.* `.DataBindings["`유효성 검사 코드에 *\<>* 필드를제어합니다.`"].WriteValue()`  
  
### <a name="implicit-and-explicit-validation"></a>암시적 및 명시적 유효성 검사  
 그렇다면 컨트롤의 데이터 유효성을 검사할 때 개발자에 게는 사용자가 있습니다. 응용 프로그램의 요구 사항에 따라 암시적 또는 명시적 유효성 검사 중 하나를 사용할 수 있습니다.  
  
#### <a name="implicit-validation"></a>암시적 유효성 검사  
 암시적 유효성 검사 방법은 사용자가 입력 한 데이터의 유효성을 검사 합니다. 키를 눌렀을 때 키를 읽어 컨트롤에 데이터를 입력 하거나 사용자가 한 컨트롤에서 입력 포커스를 벗어나 다음으로 이동할 때마다 데이터의 유효성을 검사할 수 있습니다. 이 방법은 사용자가 작업할 때 데이터에 대 한 즉각적인 피드백을 제공 하려는 경우에 유용 합니다.  
  
 컨트롤에 대해 암시적 유효성 검사를 사용 하려면 해당 컨트롤의 <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A> 속성을로 `true`설정 해야 합니다. <xref:System.Windows.Forms.Control.Validating> 이벤트를 취소 하는 경우 컨트롤의 동작은에 <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A>할당 한 값에 따라 결정 됩니다. 를 할당 <xref:System.Windows.Forms.AutoValidate.EnablePreventFocusChange>하면 이벤트 <xref:System.Windows.Forms.Control.Validated> 를 취소 하면 이벤트가 발생 하지 않습니다. 입력 포커스는 사용자가 데이터를 유효한 입력으로 변경할 때까지 현재 컨트롤에 그대로 남아 있습니다. <xref:System.Windows.Forms.AutoValidate.EnableAllowFocusChange> 할당<xref:System.Windows.Forms.Control.Validated> 한 경우 이벤트를 취소 해도 이벤트가 발생 하지 않지만 포커스는 다음 컨트롤로 계속 변경 됩니다.  
  
 속성에를 할당 <xref:System.Windows.Forms.AutoValidate.Disable> 하면 암시적 유효성 검사가 수행 되지 않습니다. <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A> 컨트롤의 유효성을 검사 하려면 명시적 유효성 검사를 사용 해야 합니다.  
  
#### <a name="explicit-validation"></a>명시적 유효성 검사  
 명시적 유효성 검사 접근 방식은 한 번에 데이터의 유효성을 검사 합니다. 저장 단추 또는 다음 링크를 클릭 하는 것과 같은 사용자 동작에 대 한 응답으로 데이터의 유효성을 검사할 수 있습니다. 사용자 작업이 발생 하면 다음 방법 중 하나를 사용 하 여 명시적 유효성 검사를 트리거할 수 있습니다.  
  
- 을 <xref:System.Windows.Forms.ContainerControl.Validate%2A> 호출 하 여 포커스가 손실 될 마지막 컨트롤의 유효성을 검사 합니다.  
  
- 을 <xref:System.Windows.Forms.ContainerControl.ValidateChildren%2A> 호출 하 여 폼 또는 컨테이너 컨트롤의 모든 자식 컨트롤의 유효성을 검사 합니다.  
  
- 사용자 지정 메서드를 호출 하 여 컨트롤의 데이터를 수동으로 유효성 검사 합니다.  
  
#### <a name="default-implicit-validation-behavior-for-windows-forms-controls"></a>Windows Forms 컨트롤에 대 한 기본 암시적 유효성 검사 동작  
 Windows Forms 컨트롤 마다 <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A> 속성의 기본값이 다릅니다. 다음 표에서는 가장 일반적인 컨트롤과 기본값을 보여 줍니다.  
  
|컨트롤|기본 유효성 검사 동작|  
|-------------|---------------------------------|  
|<xref:System.Windows.Forms.ContainerControl>|<xref:System.Windows.Forms.AutoValidate.Inherit>|  
|<xref:System.Windows.Forms.Form>|<xref:System.Windows.Forms.AutoValidate.EnableAllowFocusChange>|  
|<xref:System.Windows.Forms.PropertyGrid>|속성이 Visual Studio에서 노출 되지 않음|  
|<xref:System.Windows.Forms.ToolStripContainer>|속성이 Visual Studio에서 노출 되지 않음|  
|<xref:System.Windows.Forms.SplitContainer>|<xref:System.Windows.Forms.AutoValidate.Inherit>|  
|<xref:System.Windows.Forms.UserControl>|<xref:System.Windows.Forms.AutoValidate.EnableAllowFocusChange>|  
  
## <a name="closing-the-form-and-overriding-validation"></a>폼 닫기 및 유효성 검사 재정의  
 컨트롤에 포함 된 데이터가 잘못 되어 컨트롤에서 포커스를 유지 하는 경우 일반적인 방법 중 하나로 부모 폼을 닫을 수 없습니다.  
  
- **닫기** 단추를 클릭 합니다.  
  
- **시스템** 메뉴에서 **닫기** 를 선택 합니다.  
  
- 메서드를 <xref:System.Windows.Forms.Form.Close%2A> 프로그래밍 방식으로 호출 합니다.  
  
 그러나 경우에 따라 컨트롤의 값이 유효한 지 여부에 관계 없이 사용자가 폼을 닫을 수 있습니다. 폼의 <xref:System.Windows.Forms.Form.FormClosing> 이벤트에 대 한 처리기를 만들어 유효성 검사를 재정의 하 고 잘못 된 데이터가 여전히 포함 된 폼을 닫을 수 있습니다. 이벤트에서 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 속성을로 `false`설정 합니다. 이렇게 하면 폼이 강제로 닫힙니다. 자세한 내용과 예제는 <xref:System.Windows.Forms.Form.FormClosing?displayProperty=nameWithType>를 참조하세요.  
  
> [!NOTE]
> 이러한 방식으로 폼을 강제로 닫으려면 폼의 컨트롤에서 아직 저장 되지 않은 데이터는 모두 손실 됩니다. 또한 모달 폼은 컨트롤을 닫을 때 컨트롤 내용의 유효성을 검사 하지 않습니다. 컨트롤 유효성 검사를 사용 하 여 포커스를 컨트롤에 잠글 수 있지만 폼 닫기와 관련 된 동작에 대해 걱정 하지 않아도 됩니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Control.Validating?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Form.FormClosing?displayProperty=nameWithType>
- <xref:System.Windows.Forms.FormClosingEventArgs?displayProperty=nameWithType>
- [MaskedTextBox 컨트롤](./controls/maskedtextbox-control-windows-forms.md)
- [정규식 예제](../../standard/base-types/regular-expression-examples.md)
