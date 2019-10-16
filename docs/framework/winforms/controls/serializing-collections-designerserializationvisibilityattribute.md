---
title: '연습: DesignerSerializationVisibilityAttribute를 사용하여 표준 형식의 컬렉션 직렬화'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- serialization [Windows Forms], collections
- standard types [Windows Forms], collections
- collections [Windows Forms], serializing
- collections [Windows Forms], standard types
ms.assetid: 020c9df4-fdc5-4dae-815a-963ecae5668c
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f051d7a51a5f4ff8debf40fafbb8acfd8f7098f5
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182633"
---
# <a name="walkthrough-serialize-collections-of-standard-types"></a>연습: 표준 형식의 컬렉션 Serialize

사용자 지정 컨트롤은 컬렉션을 속성으로 노출 하는 경우도 있습니다. 이 연습에서는 <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute> 클래스를 사용 하 여 디자인 타임에 컬렉션이 serialize 되는 방법을 제어 하는 방법을 보여 줍니다. 컬렉션 속성에 값을 적용 하면 속성이 serialize 됩니다. <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute.Content>

이 항목의 코드를 단일 목록으로 복사하려면 [방법: DesignerSerializationVisibilityAttribute](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/ms171833(v=vs.120))를 사용 하 여 표준 형식의 컬렉션을 Serialize 합니다.

## <a name="prerequisites"></a>전제 조건

이 연습을 완료하려면 Visual Studio가 필요합니다.

## <a name="create-a-control-with-a-serializable-collection"></a>Serializable 컬렉션을 사용 하 여 컨트롤 만들기

첫 번째 단계는 serialize 할 수 있는 컬렉션을 속성으로 포함 하는 컨트롤을 만드는 것입니다. **속성** 창에서 액세스할 수 있는 **컬렉션 편집기**를 사용 하 여이 컬렉션의 콘텐츠를 편집할 수 있습니다.

1. Visual Studio에서 Windows 컨트롤 라이브러리 프로젝트를 만들고 이름을 **SerializationDemoControlLib**로 표시 합니다.

2. 이름을 `UserControl1` 로`SerializationDemoControl`바꿉니다. 자세한 내용은 [코드 기호 이름 바꾸기 리팩터링](/visualstudio/ide/reference/rename)을 참조 하세요.

3. **속성** 창에서 <xref:System.Windows.Forms.Padding.All%2A?displayProperty=nameWithType> 속성의 값을 **10**으로 설정 합니다.

4. 에 컨트롤 <xref:System.Windows.Forms.TextBox> 을 추가 합니다.`SerializationDemoControl`

5. <xref:System.Windows.Forms.TextBox> 컨트롤을 선택합니다. **속성** 창에서 다음 속성을 설정 합니다.

    |속성|다음으로 변경|
    |--------------|---------------|
    |**Multiline**|`true`|
    |**결합**|<xref:System.Windows.Forms.DockStyle.Fill>|
    |**ScrollBars**|<xref:System.Windows.Forms.ScrollBars.Vertical>|
    |**ReadOnly**|`true`|

6. **코드 편집기**에서 이름이 `stringsValue` `SerializationDemoControl`인 문자열 배열 필드를 선언 합니다.

     [!code-cpp[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/cpp/form1.cpp#4)]
     [!code-csharp[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/CS/form1.cs#4)]
     [!code-vb[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/VB/form1.vb#4)]

7. 에서 속성 `Strings` 을 정의 합니다. `SerializationDemoControl`

   > [!NOTE]
   > <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute.Content> 값은 컬렉션의 serialization을 활성화 하는 데 사용 됩니다.

   [!code-cpp[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/cpp/form1.cpp#5)]
   [!code-csharp[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/CS/form1.cs#5)]
   [!code-vb[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/VB/form1.vb#5)]

8. **F5** 키를 눌러 프로젝트를 빌드하고 **UserControl 테스트 컨테이너**에서 컨트롤을 실행 합니다.

9. <xref:System.Windows.Forms.PropertyGrid> **UserControl 테스트 컨테이너**의에서 **Strings** 속성을 찾습니다. **Strings** 속성을 선택한 다음 줄임표 (![Visual Studio](./media/visual-studio-ellipsis-button.png)속성 창의 줄임표 단추 (...)) 단추를 선택 하 여 **문자열 컬렉션 편집기**를 엽니다.

10. **문자열 컬렉션 편집기**에 여러 문자열을 입력 합니다. 각 문자열의 끝에서 **enter** 키를 눌러 각 문자열을 구분 합니다. 문자열 입력을 마치면 **확인을** 클릭 합니다.

   > [!NOTE]
   > 입력 한 문자열이의에 표시 <xref:System.Windows.Forms.TextBox> `SerializationDemoControl`됩니다.

## <a name="serialize-a-collection-property"></a>컬렉션 속성 직렬화

컨트롤의 serialization 동작을 테스트 하려면 폼에 추가 하 고 **컬렉션 편집기**를 사용 하 여 컬렉션의 내용을 변경 합니다. **Windows Forms 디자이너** 에서 코드를 내보내는 특수 한 디자이너 파일을 살펴보면 serialize 된 컬렉션 상태를 볼 수 있습니다.

1. Windows 응용 프로그램 프로젝트를 솔루션에 추가 합니다. 프로젝트 이름을 `SerializationDemoControlTest`로 지정합니다.

2. **도구 상자**에서 **SerializationDemoControlLib Components**라는 탭을 찾습니다. 이 탭에서을 찾을 `SerializationDemoControl`수 있습니다. 자세한 내용은 [연습: 도구 상자에 사용자 지정 구성 요소](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)를 자동으로 채웁니다.

3. 폼에 `SerializationDemoControl` 를 추가 합니다.

4. 속성 창 `Strings` 에서 속성을 찾습니다. 속성을 클릭 한 다음, Visual Studio](./media/visual-studio-ellipsis-button.png)의![속성 창에 있는 줄임표 단추 (...) 단추를 클릭 하 여 **문자열 컬렉션 편집기**를 엽니다. `Strings`

5. **문자열 컬렉션 편집기**에 여러 문자열을 입력 합니다. 각 문자열의 끝에서 **enter** 키를 눌러 구분 합니다. 문자열 입력을 마치면 **확인을** 클릭 합니다.

    > [!NOTE]
    > 입력 한 문자열이의에 표시 <xref:System.Windows.Forms.TextBox> `SerializationDemoControl`됩니다.

6. **솔루션 탐색기**에서 **모든 파일 표시** 단추를 클릭합니다.

7. **Form1** 노드를 엽니다. 아래에는 **Form1.Designer.cs 또는** 라는 파일이 **있습니다.** 이 파일은 **Windows Forms 디자이너** 폼과 해당 자식 컨트롤의 디자인 타임 상태를 나타내는 코드를 내보내는 파일입니다. **코드 편집기**에서 이 파일을 엽니다.

8. **Windows Form 디자이너에서 생성 한 코드** 라는 영역을 열고 **serializationDemoControl1**레이블이 지정 된 섹션을 찾습니다. 이 레이블 아래에는 컨트롤의 serialize 된 상태를 나타내는 코드가 있습니다. 5 단계에서 입력 한 문자열은 `Strings` 속성에 대 한 할당에 표시 됩니다. 및 Visual Basic의 C# 다음 코드 예제에서는 "red", "주황색" 및 "노란색" 문자열을 입력 했을 때 표시 되는 것과 유사한 코드를 보여 줍니다.

    ```csharp
    this.serializationDemoControl1.Strings = new string[] {
            "red",
            "orange",
            "yellow"};
    ```

    ```vb
    Me.serializationDemoControl1.Strings = New String() {"red", "orange", "yellow"}
    ```

9. **코드 편집기**에서 <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute> `Strings` 속성의 값을로 <xref:System.ComponentModel.DesignerSerializationVisibility.Hidden>변경 합니다.

    ```csharp
    [DesignerSerializationVisibility(DesignerSerializationVisibility.Hidden)]
    ```

    ```vb
    <DesignerSerializationVisibility(DesignerSerializationVisibility.Hidden)> _
    ```

10. 솔루션을 다시 빌드하고 3 단계와 4 단계를 반복 합니다.

> [!NOTE]
> 이 경우 **Windows Forms 디자이너** 는 `Strings` 속성에 대 한 할당을 내보냅니다.

## <a name="next-steps"></a>다음 단계

표준 형식의 컬렉션을 serialize 하는 방법을 알고 있으면 사용자 지정 컨트롤을 디자인 타임 환경에 더 많이 통합 하는 것이 좋습니다. 다음 항목에서는 사용자 지정 컨트롤의 디자인 타임 통합을 향상 시키는 방법에 대해 설명 합니다.

- [디자인 타임 아키텍처](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/c5z9s1h4(v=vs.120))

- [Windows Forms 컨트롤의 특성](attributes-in-windows-forms-controls.md)

- [디자이너 직렬화 개요](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/ms171834(v=vs.120))

- [연습: Visual Studio 디자인 타임 기능을 활용 하는 Windows Forms 컨트롤 만들기](creating-a-wf-control-design-time-features.md)

## <a name="see-also"></a>참고 항목

- <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute>
- [연습: 사용자 지정 구성 요소를 사용 하 여 도구 상자 자동 채우기](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)
