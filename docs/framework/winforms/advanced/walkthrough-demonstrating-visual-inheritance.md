---
title: '연습: 시각적 상속 데모'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- form inheritance [Windows Forms], walkthroughs
- visual inheritance
- inheritance [Windows Forms], walkthroughs
- walkthroughs [Windows Forms], visual inheritance
- Windows Forms, inheritance
ms.assetid: 01966086-3142-450e-8210-3fd4cb33f591
ms.openlocfilehash: 32df98852b28963ffb748895156f7d9977c74b92
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046144"
---
# <a name="walkthrough-demonstrating-visual-inheritance"></a>연습: 시각적 상속 데모

시각적 상속을 통해 기본 폼의 컨트롤을 보고 새 컨트롤을 추가할 수 있습니다. 이 연습에서는 기본 폼을 만들고 클래스 라이브러리로 컴파일합니다. 이 클래스 라이브러리를 다른 프로젝트로 가져와 기본 폼에서 상속하는 새 양식을 만듭니다. 이 연습에서는 다음 작업을 수행하는 방법을 배웁니다.

- 기본 폼을 포함하는 클래스 라이브러리 프로젝트를 만듭니다.

- 기본 폼의 파생 클래스가 수정할 수 있는 속성을 가진 단추를 추가합니다.

- 기본 폼의 상속자가 수정할 수 없는 단추를 추가합니다.

- `BaseForm`에서 상속하는 폼을 포함하는 프로젝트를 만듭니다.

궁극적으로, 이 연습에서는 상속된 폼의 private 컨트롤과 protected 컨트롤 간의 차이점을 보여 줍니다.

> [!CAUTION]
> 일부 컨트롤은 기본 폼에서의 시각적 상속을 지원하지 않습니다. 다음 컨트롤은 이 연습에 설명된 시나리오를 지원하지 않습니다.
>
> - <xref:System.Windows.Forms.WebBrowser>
>
> - <xref:System.Windows.Forms.ToolStrip>
>
> - <xref:System.Windows.Forms.ToolStripPanel>
>
> - <xref:System.Windows.Forms.TableLayoutPanel>
>
> - <xref:System.Windows.Forms.FlowLayoutPanel>
>
> - <xref:System.Windows.Forms.DataGridView>
>
> 상속된 폼의 이러한 컨트롤은 사용하는 한정자(`private`, `protected` 또는 `public`)에 관계없이 항상 읽기 전용입니다.

## <a name="create-a-class-library-project-containing-a-base-form"></a>기본 폼을 포함 하는 클래스 라이브러리 프로젝트 만들기

1. Visual Studio의 **파일** 메뉴에서 **새** > **프로젝트** 를 선택 하 여 **새 프로젝트** 대화 상자를 엽니다.

2. 이라는 `BaseFormLibrary`Windows Forms 응용 프로그램을 만듭니다.

3. 표준 Windows Forms 응용 프로그램 대신 클래스 라이브러리를 만들려면 **솔루션 탐색기**에서 **baseformlibrary** 프로젝트 노드를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 선택 합니다.

4. 프로젝트에 대 한 속성에서 **출력 형식을** **Windows 응용 프로그램** 에서 **클래스 라이브러리로**변경 합니다.

5. **파일** 메뉴에서 **모두 저장** 을 선택 하 여 프로젝트 및 파일을 기본 위치에 저장 합니다.

다음 두 절차에서는 기본 폼에 단추를 추가합니다. 시각적 상속을 보여 주기 위해 단추의 `Modifiers` 속성을 설정하여 단추에 다양한 액세스 수준을 제공합니다.

## <a name="add-a-button-that-inheritors-of-the-base-form-can-modify"></a>기본 폼의 상속 자가 수정할 수 있는 단추를 추가 합니다.

1. 디자이너에서 **Form1**을 엽니다.

2. **도구 상자**의 **모두 Windows Forms** 탭에서 **단추** 를 두 번 클릭 하 여 단추를 폼에 추가 합니다. 마우스를 사용하여 단추를 배치하고 크기를 조정합니다.

3. 속성 창에서 단추의 다음 속성을 설정합니다.

    - **텍스트** 속성을 **Hello**로 설정 합니다.

    - **(Name)** 속성을 **btnProtected**로 설정 합니다.

    - **한정자** 속성을 **Protected**로 설정 합니다. 이렇게 하면 **Form1** 에서 상속 하는 폼이 **btnProtected**의 속성을 수정할 수 있습니다.

4. **Hello** 단추를 두 번 클릭 하 여 **click** 이벤트에 대 한 이벤트 처리기를 추가 합니다.

5. 다음 코드 줄을 이벤트 처리기에 추가합니다.

    ```vb
    MessageBox.Show("Hello, World!")
    ```

    ```csharp
    MessageBox.Show("Hello, World!");
    ```

## <a name="add-a-button-that-cannot-be-modified-by-inheritors-of-the-base-form"></a>기본 폼의 상속 자가 수정할 수 없는 단추를 추가 합니다.

1. 코드 편집기 위쪽의 form1.vb [ **design], Form1.cs [design] 또는 [design]** 탭을 클릭 하거나 F7 키를 눌러 디자인 뷰로 전환 합니다.

2. 두 번째 단추를 추가하고 해당 속성을 다음과 같이 설정합니다.

    - **텍스트** 속성을 **안녕히**로 설정 합니다.

    - **(Name)** 속성을 **btnPrivate**로 설정 합니다.

    - **한정자** 속성을 **Private**으로 설정 합니다. 이렇게 하면 **Form1** 에서 상속 하는 폼이 **btnPrivate**의 속성을 수정할 수 없습니다.

3. 예 단추를 두 번 클릭 하 여 **click** 이벤트에 대 한 이벤트 처리기를 추가 합니다. 다음 코드 줄을 이벤트 프로시저에 배치합니다.

    ```vb
    MessageBox.Show("Goodbye!")
    ```

    ```csharp
    MessageBox.Show("Goodbye!");
    ```

4. **빌드** 메뉴에서 **BaseForm library 빌드** 를 선택 하 여 클래스 라이브러리를 빌드합니다.

     라이브러리가 빌드되고 나면 방금 만든 폼에서 상속하는 새 프로젝트를 만들 수 있습니다.

## <a name="create-a-project-containing-a-form-that-inherits-from-the-base-form"></a>기본 폼에서 상속 되는 폼을 포함 하는 프로젝트 만들기

1. **파일** 메뉴에서 **추가** 를 선택 하 고 **새 프로젝트** 를 선택 하 여 **새 프로젝트 추가** 대화 상자를 엽니다.

2. 이라는 `InheritanceTest`Windows Forms 응용 프로그램을 만듭니다.

## <a name="add-an-inherited-form"></a>상속 된 폼 추가

1. **솔루션 탐색기**에서 **InheritanceTest** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **새 항목**을 선택 합니다.

2. **새 항목 추가** 대화 상자에서 범주 목록이 있는 경우 **Windows Forms** 범주를 선택 하 고 **상속 된 양식** 서식 파일을 선택 합니다.

3. 의 `Form2` 기본 이름을 그대로 두고 **추가**를 클릭 합니다.

4. **상속 선택** 대화 상자의 **baseformlibrary** 프로젝트에서 상속할 폼으로 **Form1** 을 선택 하 고 **확인**을 클릭 합니다.

     그러면 **Baseformlibrary**의 폼에서 파생 되는 **InheritanceTest** 프로젝트에 폼이 만들어집니다.

5. 디자이너에서 상속 된 폼 (**Form2**)을 두 번 클릭 하 여 엽니다 (아직 열려 있지 않은 경우).

    디자이너에서 상속 된 단추에는 기호 (![Visual Basic 상속 기호의 스크린샷](./media/walkthrough-demonstrating-visual-inheritance/visual-basic-inheritance-glyph.gif))를 위쪽 모퉁이에 표시 합니다.

6. **Hello** 단추를 선택 하 고 크기 조정 핸들을 관찰 합니다. 이 단추는 protected이므로 상속자가 이동하고, 크기를 조정하고, 캡션을 변경하고, 기타 수정 작업을 할 수 있습니다.

7. 비공개 **라고** 하는 단추를 선택 하 고 크기 조정 핸들이 없다는 것을 확인 합니다. 또한 **속성** 창에서이 단추의 속성은 수정할 수 없음을 나타내기 위해 회색으로 표시 됩니다.

8. 시각적 개체 C#를 사용 하는 경우:

    1. **솔루션 탐색기**에서 **InheritanceTest** 프로젝트의 **Form1** 을 마우스 오른쪽 단추로 클릭 한 다음 **삭제**를 선택 합니다. 표시 되는 메시지 상자에서 **확인** 을 클릭 하 여 삭제를 확인 합니다.

    2. Program.cs 파일을 열고 `Application.Run(new Form1());` 줄을 `Application.Run(new Form2());`으로 변경합니다.

9. **솔루션 탐색기**에서 **InheritanceTest** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **시작 프로젝트로 설정**을 선택 합니다.

10. **솔루션 탐색기**에서 **InheritanceTest** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.

11. **InheritanceTest** 속성 페이지에서 **시작 개체** 를 상속 된 폼 (**Form2**)으로 설정 합니다.

12. **F5** 키를 눌러 응용 프로그램을 실행 하 고 상속 된 폼의 동작을 관찰 합니다.

## <a name="next-steps"></a>다음 단계

사용자 정의 컨트롤의 상속도 거의 동일한 방식으로 작동합니다. 새 클래스 라이브러리 프로젝트를 열고 사용자 정의 컨트롤을 추가합니다. 구성 요소 컨트롤을 배치하고 프로젝트를 컴파일합니다. 다른 새 클래스 라이브러리 프로젝트를 열고 컴파일된 클래스 라이브러리에 대한 참조를 추가합니다. 또한 상속 **선택기**를 사용 하 여 **새 항목 추가** 대화 상자를 통해 상속 된 컨트롤을 프로젝트에 추가 해 봅니다. 사용자 정의 컨트롤을 추가 하 고 `Inherits` (`:` Visual C#) 문을 변경 합니다. 자세한 내용은 [방법: Windows Forms](how-to-inherit-windows-forms.md)를 상속 합니다.

## <a name="see-also"></a>참고자료

- [방법: Windows Forms 상속](how-to-inherit-windows-forms.md)
- [Windows Forms 시각적 개체 상속](windows-forms-visual-inheritance.md)
- [Windows Forms](../index.md)
