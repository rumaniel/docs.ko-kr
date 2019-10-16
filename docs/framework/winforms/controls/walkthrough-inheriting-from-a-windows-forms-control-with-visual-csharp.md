---
title: '연습: Visual C#을 사용하여 Windows Forms 컨트롤에서 상속'
ms.date: 03/30/2017
helpviewer_keywords:
- inheritance [Windows Forms], custom controls
- inheritance [Windows Forms], control
- Windows Forms controls, inheritance
- inheritance [Windows Forms], walkthroughs
- custom controls [Windows Forms], inheritance
ms.assetid: 09476da0-8d4c-4a4c-b969-649519dfb438
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 4a9a4b9bc15d2579837c3f4969a8d85293f10967
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015676"
---
# <a name="walkthrough-inherit-from-a-windows-forms-control-with-c"></a>연습: C를 사용 하 여 Windows Forms 컨트롤에서 상속\#

시각적 개체 C#를 사용 하면 *상속*을 통해 강력한 사용자 지정 컨트롤을 만들 수 있습니다. 상속을 통해 표준 Windows Forms 컨트롤의 모든 고유 기능을 유지하면서 사용자 지정 기능을 통합하는 컨트롤을 만들 수 있습니다. 이 연습에서는 `ValueButton`이라는 간단한 상속된 컨트롤을 만듭니다. 이 단추는 표준 Windows Forms <xref:System.Windows.Forms.Button> 컨트롤에서 기능을 상속 하 고 라는 `ButtonValue`사용자 지정 속성을 노출 합니다.

## <a name="create-the-project"></a>프로젝트 만들기

새 프로젝트를 만들 때는 루트 네임스페이스, 어셈블리 이름 및 프로젝트 이름을 설정하기 위해 이름을 지정하고 기본 구성 요소가 올바른 네임스페이스에 있는지 확인합니다.

### <a name="to-create-the-valuebuttonlib-control-library-and-the-valuebutton-control"></a>ValueButtonLib 컨트롤 라이브러리 및 ValueButton 컨트롤을 만들려면

1. Visual Studio에서 새 **Windows Forms 컨트롤 라이브러리** 프로젝트를 만들고 이름을 **Valuebuttonlib**로 표시 합니다.

     프로젝트 이름, `ValueButtonLib`는 기본적으로 루트 네임스페이스에도 할당됩니다. 루트 네임스페이스는 어셈블리에서 구성 요소의 이름을 정규화하는 데 사용됩니다. 예를 들어 두 어셈블리에서 `ValueButton`이라는 구성 요소를 제공하면 `ValueButtonLib.ValueButton`을 사용하여 `ValueButton` 구성 요소를 지정할 수 있습니다. 자세한 내용은 [네임스페이스](../../../csharp/programming-guide/namespaces/index.md)를 참조하세요.

2. **솔루션 탐색기**에서 **UserControl1.cs**를 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **이름 바꾸기**를 선택합니다. 파일 이름을 **ValueButton.cs**로 변경 합니다. 코드 요소 '`UserControl1`'에 대한 모든 참조 이름을 변경할지 묻는 메시지가 표시되면 **예** 단추를 클릭합니다.

3. **솔루션 탐색기**에서 **ValueButton.cs**를 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 선택합니다.

4. 문 줄을 `public partial class ValueButton`찾아이 컨트롤이 상속 <xref:System.Windows.Forms.UserControl> 되는 형식을로 <xref:System.Windows.Forms.Button>변경 합니다. `class` 이렇게 하면 상속 된 컨트롤이 <xref:System.Windows.Forms.Button> 컨트롤의 모든 기능을 상속할 수 있습니다.

5. **솔루션 탐색기**에서 **ValueButton.cs** 노드를 열어 디자이너에서 생성한 코드 파일인 **ValueButton.Designer.cs**를 표시합니다. **코드 편집기**에서 이 파일을 엽니다.

6. 메서드를 `InitializeComponent` 찾아 <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A> 속성을 할당 하는 줄을 제거 합니다. 이 속성은 <xref:System.Windows.Forms.Button> 컨트롤에 없습니다.

7. **파일** 메뉴에서 **모두 저장**을 선택하여 프로젝트를 저장합니다.

    > [!NOTE]
    > 비주얼 디자이너는 더 이상 사용할 수 없습니다. 컨트롤은 <xref:System.Windows.Forms.Button> 자체적으로 그리기를 수행 하므로 디자이너에서 모양을 수정할 수 없습니다. 시각적 표시는 코드에서 수정 되지 않는 한, 상속 된 클래스 (즉, <xref:System.Windows.Forms.Button>)와 정확히 동일 합니다. UI 요소가 없는 구성 요소를 디자인 화면에 계속 추가할 수 있습니다.

## <a name="add-a-property-to-your-inherited-control"></a>상속 된 컨트롤에 속성 추가

상속된 Windows Forms 컨트롤의 한 가지 가능한 용도는 표준 Windows Forms 컨트롤과 모양 및 느낌이 동일하지만 사용자 지정 속성을 노출하는 컨트롤을 만드는 것입니다. 이 섹션에서는 `ButtonValue`라는 속성을 컨트롤에 추가합니다.

### <a name="to-add-the-value-property"></a>Value 속성을 추가하려면

1. **솔루션 탐색기**에서 **ValueButton.cs**를 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **코드 보기**를 클릭합니다.

2. `class` 문을 찾습니다. `{` 바로 뒤에 다음 코드를 입력합니다.

    ```csharp
    // Creates the private variable that will store the value of your
    // property.
    private int varValue;
    // Declares the property.
    public int ButtonValue
    {
       // Sets the method for retrieving the value of your property.
       get
       {
          return varValue;
       }
       // Sets the method for setting the value of your property.
       set
       {
          varValue = value;
       }
    }
    ```

     이 코드는 `ButtonValue` 속성을 저장 및 검색할 메서드를 설정합니다. `get` 문은 반환된 값을 private 변수 `varValue`에 저장된 값으로 설정하고 `set` 문은 `value` 키워드를 사용하여 private 변수의 값을 설정합니다.

3. **파일** 메뉴에서 **모두 저장**을 선택하여 프로젝트를 저장합니다.

## <a name="test-the-control"></a>컨트롤 테스트

컨트롤은 독립 실행형 프로젝트가 아니며 컨테이너에서 호스팅해야 합니다. 컨트롤을 테스트하려면 컨트롤을 실행할 테스트 프로젝트를 제공해야 합니다. 또한 컨트롤을 빌드(컴파일)하여 컨트롤에서 테스트 프로젝트에 액세스할 수 있도록 해야 합니다. 이 섹션에서는 컨트롤을 테스트하고 Windows Form에서 테스트합니다.

### <a name="to-build-your-control"></a>컨트롤을 빌드하려면

**빌드** 메뉴에서 **솔루션 빌드**를 클릭합니다. 컴파일러 오류 또는 경고 없이 빌드에 성공해야 합니다.

### <a name="to-create-a-test-project"></a>테스트 프로젝트를 만들려면

1. **파일** 메뉴에서 **추가**를 가리킨 후 **새 프로젝트**를 클릭하여 **새 프로젝트 추가** 대화 상자를 엽니다.

2. **Windows** 노드를 선택하고 **Visual C#** 노드 아래에서 **Windows Forms 애플리케이션**을 클릭합니다.

3. **이름** 상자에 **Test**를 입력 합니다.

4. **솔루션 탐색기**에서 테스트 프로젝트에 대한 **참조** 노드를 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **참조 추가**를 선택하면 **참조 추가** 대화 상자가 표시됩니다.

5. **프로젝트**로 레이블이 지정된 탭을 클릭합니다. ValueButtonLib 프로젝트가 **프로젝트 이름**아래에 나열 됩니다. 프로젝트를 두 번 클릭하여 테스트 프로젝트에 참조를 추가합니다.

6. **솔루션 탐색기**에서 **Test**를 마우스 오른쪽 단추로 클릭한 후 **빌드**를 선택합니다.

### <a name="to-add-your-control-to-the-form"></a>폼에 컨트롤을 추가하려면

1. **솔루션 탐색기**에서 **Form1.cs**를 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **뷰 디자이너**를 선택합니다.

2. **도구 상자**에서 **Valuebuttonlib 구성 요소**를 선택 합니다. **ValueButton**을 두 번 클릭합니다.

     **ValueButton**이 폼에 나타납니다.

3. **ValueButton**을 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **속성**을 선택합니다.

4. **속성** 창에서 이 컨트롤의 속성을 점검합니다. 추가 속성인 ButtonValue를 제외 하 고는 표준 단추에 의해 노출 되는 속성과 동일 합니다.

5. **Buttonvalue** 속성을 **5**로 설정 합니다.

6. **도구 상자**의 **모두 Windows Forms** 탭에서 <xref:System.Windows.Forms.Label> **레이블** 을 두 번 클릭 하 여 컨트롤을 폼에 추가 합니다.

7. 폼 가운데에 레이블을 다시 배치합니다.

8. `valueButton1`을 두 번 클릭합니다.

     **코드 편집기**에 `valueButton1_Click` 이벤트가 열립니다.

9. 다음 코드 행을 삽입합니다.

    ```csharp
    label1.Text = valueButton1.ButtonValue.ToString();
    ```

10. **솔루션 탐색기**에서 **Test**를 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **시작 프로젝트로 설정**을 선택합니다.

11. **디버그** 메뉴에서 **디버깅 시작**을 선택합니다.

     `Form1`이 나타납니다.

12. `valueButton1`을 클릭합니다.

     숫자 '5'가 `label1`에 표시되며 상속된 컨트롤의 `ButtonValue` 속성이 `valueButton1_Click` 메서드를 통해 `label1`에 전달되었음을 보여 줍니다. 따라서 `ValueButton` 컨트롤은 표준 Windows Forms 단추의 모든 기능을 상속하지만 추가 사용자 지정 속성을 노출합니다.

## <a name="see-also"></a>참고자료

- [방법: 도구 상자 항목 선택 대화 상자에 컨트롤 표시](how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)
- [연습: 시각적 개체를 사용 하 여 복합 컨트롤 작성C#](walkthrough-authoring-a-composite-control-with-visual-csharp.md)
