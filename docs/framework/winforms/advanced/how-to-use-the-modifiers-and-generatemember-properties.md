---
title: '방법: Modifiers 및 GenerateMember 속성 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
f1_keywords:
- Designer_GenerateMember
- Designer_Modifiers
helpviewer_keywords:
- base forms
- inheritance [Windows Forms], forms
- inherited forms [Windows Forms], Windows Forms
- inherited forms
- form inheritance
- Windows Forms, inheritance
ms.assetid: 3381a5e4-e1a3-44e2-a765-a0b758937b85
ms.openlocfilehash: 3fbaaae53aa60f6356c3a8daa0513de86ef2dacb
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211288"
---
# <a name="how-to-use-the-modifiers-and-generatemember-properties"></a>방법: Modifiers 및 GenerateMember 속성 사용

디자인 환경에서 두 개의 속성을 제공 구성 요소를 Windows Form에 넣을 때: `GenerateMember` 고 `Modifiers`입니다. `GenerateMember` 속성 Windows Forms 디자이너 구성 요소에 대 한 멤버 변수를 생성 하는 경우를 지정 합니다. `Modifiers` 속성은 해당 멤버 변수에 할당 하는 액세스 한정자입니다. 경우의 값을 `GenerateMember` 속성은 `false`의 값은 `Modifiers` 속성이 적용 되지 않습니다.

## <a name="specify-whether-a-component-is-a-member-of-the-form"></a>구성 요소 폼의 멤버 인지 여부를 지정 합니다.

1. Visual Studio Windows Forms 디자이너에서에서 폼을 엽니다.

2. 엽니다는 **도구 상자**, 양식에서 세 가지를 배치 하 고 <xref:System.Windows.Forms.Button> 컨트롤입니다.

3. 설정 합니다 `GenerateMember` 하 고 `Modifiers` 각각에 대 한 속성 <xref:System.Windows.Forms.Button> 컨트롤은 다음 표에 따라 합니다.

    |단추 이름|GenerateMember 값|한정자 값|
    |-----------------|--------------------------|---------------------|
    |`button1`|`true`|`private`|
    |`button2`|`true`|`protected`|
    |`button3`|`false`|변경 안 함|

4. 솔루션을 빌드합니다.

5. **솔루션 탐색기**에서 **모든 파일 표시** 단추를 클릭합니다.

6. 엽니다는 **Form1** 노드를 고를 **코드 편집기**을 엽니다는 **Form1.Designer.vb** 또는 **Form1.Designer.cs** 파일. 이 파일은 Windows Forms 디자이너에서 생성 된 코드를 포함 합니다.

7. 세 개의 단추에 대 한 선언을 찾습니다. 다음 코드 예제에서는 지정 된 차이점을 보여 줍니다.는 `GenerateMember` 고 `Modifiers` 속성입니다.

     [!code-csharp[System.Windows.Forms.GenerateMember#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.GenerateMember#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/VB/Form1.vb#3)]

     [!code-csharp[System.Windows.Forms.GenerateMember#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.GenerateMember#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/VB/Form1.vb#2)]

> [!NOTE]
> 기본적으로 Windows Forms 디자이너를 할당 합니다 `private` (`Friend` Visual Basic의) 처럼 컨테이너 컨트롤에는 한정자 <xref:System.Windows.Forms.Panel>합니다. 경우 베이스가 <xref:System.Windows.Forms.UserControl> 또는 <xref:System.Windows.Forms.Form> 컨테이너 컨트롤에 상속 된 컨트롤 및 폼에 새 자식 항목을 허용 하지 것입니다. 솔루션은 기본 컨테이너 컨트롤의 한정자를 변경할 `protected` 또는 `public`합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Button>
- [Windows Forms 시각적 개체 상속](windows-forms-visual-inheritance.md)
- [연습: 시각적 상속 설명](walkthrough-demonstrating-visual-inheritance.md)
- [방법: Windows Forms 상속](how-to-inherit-windows-forms.md)
