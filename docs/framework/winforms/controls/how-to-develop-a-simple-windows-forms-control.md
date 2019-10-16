---
title: '방법: 간단한 Windows Forms 컨트롤 개발'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [Windows Forms]
- custom controls [Windows Forms], creating simple controls using code
- Control class [Windows Forms], Windows Forms
ms.assetid: 86cbe435-45b7-4cb4-9b5a-47418369758d
ms.openlocfilehash: a190d86f5ebe258427ac4a73c16c7f271462b69c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64753230"
---
# <a name="how-to-develop-a-simple-windows-forms-control"></a>방법: 간단한 Windows Forms 컨트롤 개발

이 섹션에서는 사용자 지정 Windows Forms 컨트롤을 작성하는 주요 단계를 설명합니다. 이 연습에서 개발한 간단한 컨트롤의 맞춤을 사용 하면 해당 <xref:System.Windows.Forms.Control.Text%2A> 변경할 속성입니다. 이벤트를 발생시키거나 처리하지 않습니다.

### <a name="to-create-a-simple-custom-control"></a>간단한 사용자 지정 컨트롤을 만들려면

1. <xref:System.Windows.Forms.Control?displayProperty=nameWithType>에서 파생된 클래스를 정의합니다.

    ```vb
    Public Class FirstControl
       Inherits Control

    End Class
    ```

    ```csharp
    public class FirstControl:Control {}
    ```

2. 속성을 정의합니다. (필요는 없습니다 속성을 정의 하는 컨트롤에서 여러 속성을 상속 하기 때문에 <xref:System.Windows.Forms.Control> 하지만 대부분의 사용자 지정 컨트롤이 일반적으로 추가 속성을 정의 합니다.) 라는 속성을 정의 하는 다음 코드 조각 `TextAlignment` 하는 `FirstControl` 사용 하 여의 표시 형식을 지정 하는 <xref:System.Windows.Forms.Control.Text%2A> 속성에서 상속 됩니다 <xref:System.Windows.Forms.Control>합니다. 속성을 정의하는 방법에 대한 자세한 내용은 [속성 개요](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v%3dvs.120))를 참조하세요.

     [!code-csharp[System.Windows.Forms.FirstControl#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/CS/FirstControl.cs#3)]
     [!code-vb[System.Windows.Forms.FirstControl#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/VB/FirstControl.vb#3)]

     컨트롤의 시각적 표시를 변경 하는 속성을 설정 하면 호출 해야 합니다는 <xref:System.Windows.Forms.Control.Invalidate%2A> 메서드 컨트롤을 다시 그리도록 합니다. <xref:System.Windows.Forms.Control.Invalidate%2A> 기본 클래스에 정의 된 <xref:System.Windows.Forms.Control>합니다.

3. 보호 된 재정의 <xref:System.Windows.Forms.Control.OnPaint%2A> 에서 상속 된 메서드 <xref:System.Windows.Forms.Control> 컨트롤에 렌더링 논리를 제공 합니다. 재정의 하지 않을 경우 <xref:System.Windows.Forms.Control.OnPaint%2A>, 컨트롤이 자신을 그릴 수 없습니다. 다음 코드 조각에서 합니다 <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드 표시 합니다 <xref:System.Windows.Forms.Control.Text%2A> 속성에서 상속 됩니다 <xref:System.Windows.Forms.Control> 에서 지정 된 맞춤을 사용 하 여는 `alignmentValue` 필드.

     [!code-csharp[System.Windows.Forms.FirstControl#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/CS/FirstControl.cs#4)]
     [!code-vb[System.Windows.Forms.FirstControl#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/VB/FirstControl.vb#4)]

4. 컨트롤의 특성을 제공합니다. 특성을 사용하면 시각적 디자이너가 디자인 타임에 컨트롤과 해당 속성 및 이벤트를 적절하게 표시할 수 있습니다. 다음 코드 조각은 `TextAlignment` 속성에 특성을 적용합니다. Visual Studio와 같은 디자이너는 <xref:System.ComponentModel.CategoryAttribute.Category%2A> (코드 조각에 표시 됨) 특성을 사용 하면 속성을 논리 범주 아래에 표시 합니다. <xref:System.ComponentModel.DescriptionAttribute.Description%2A> 특성을 사용 하면 설명이 포함 된 문자열의 맨 아래에 표시 되는 **속성** 창 때는 `TextAlignment` 속성을 선택 합니다. 특성에 대한 자세한 내용은 [구성 요소에 대한 디자인 타임 특성](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/tk67c2t8(v=vs.120))을 참조하세요.

     [!code-csharp[System.Windows.Forms.FirstControl#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/CS/FirstControl.cs#5)]
     [!code-vb[System.Windows.Forms.FirstControl#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/VB/FirstControl.vb#5)]

5. (선택 사항)컨트롤에 리소스를 제공합니다. 컨트롤과 함께 리소스를 패키징하는 컴파일러 옵션(C#의 경우 `/res`)을 사용하여 컨트롤에 비트맵과 같은 리소스를 제공할 수 있습니다. 런타임 시 리소스를 검색할 수의 메서드를 사용 하 여 <xref:System.Resources.ResourceManager> 클래스입니다. 리소스를 만들고 사용하는 방법에 대한 자세한 내용은 [데스크톱 앱의 리소스](../../resources/index.md)를 참조하세요.

6. 컨트롤을 컴파일하고 배포합니다. `FirstControl,`을 컴파일하고 배포하려면 다음 단계를 실행합니다.

    1. 다음 샘플의 코드를 소스 파일(예: FirstControl.cs 또는 FirstControl.vb)에 저장합니다.

    2. 소스 코드를 어셈블리로 컴파일하고 애플리케이션의 디렉터리에 저장합니다. 이를 수행하려면 소스 파일이 포함된 디렉터리에서 다음 명령을 실행합니다.

        ```console
        vbc -t:library -out:[path to your application's directory]/CustomWinControls.dll -r:System.dll -r:System.Windows.Forms.dll -r:System.Drawing.dll FirstControl.vb
        ```

        ```console
        csc -t:library -out:[path to your application's directory]/CustomWinControls.dll -r:System.dll -r:System.Windows.Forms.dll -r:System.Drawing.dll FirstControl.cs
        ```

         `/t:library` 컴파일러 옵션은 사용자가 만드는 어셈블리가 실행 파일이 아니라 라이브러리임을 컴파일러에 알립니다. `/out` 옵션은 어셈블리의 경로 및 이름을 지정합니다. `/r` 옵션은 코드에 의해 참조되는 어셈블리의 이름을 제공합니다. 이 예제에서는 애플리케이션에서만 사용할 수 있는 프라이빗 어셈블리를 만들 수 있습니다. 따라서 애플리케이션의 디렉터리에 저장해야 합니다. 배포하기 위한 컨트롤을 패키징하고 배포하는 방법에 대한 자세한 내용은 [배포](../../deployment/index.md)를 참조하세요.

다음 샘플은 `FirstControl`의 코드를 보여 줍니다. 컨트롤은 네임스페이스 `CustomWinControls`에서 따옴표로 묶입니다. 네임스페이스는 관련된 형식의 논리적 그룹화를 제공합니다. 새로운 또는 기존 네임스페이스에서 컨트롤을 만들 수 있습니다. C#에서 `using` 선언(Visual Basic의 경우 `Imports`)을 사용하면 형식의 정규화된 이름을 사용하지 않고 네임스페이스에서 형식에 액세스할 수 있습니다. 다음 예제에서는 `using` 선언을 클래스에 액세스 하는 코드를 사용 하면 <xref:System.Windows.Forms.Control> 에서 <xref:System.Windows.Forms?displayProperty=nameWithType> 간단 <xref:System.Windows.Forms.Control> 정규화 된 이름을 사용 하는 대신 <xref:System.Windows.Forms.Control?displayProperty=nameWithType>합니다.

[!code-csharp[System.Windows.Forms.FirstControl#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/CS/FirstControl.cs#1)]
[!code-vb[System.Windows.Forms.FirstControl#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/VB/FirstControl.vb#1)]

## <a name="using-the-custom-control-on-a-form"></a>양식에서 사용자 지정 컨트롤 사용

다음 예제에서는 `FirstControl`을 사용하는 간단한 양식을 보여 줍니다. `TextAlignment` 속성에 대해 각각 다른 값을 가진 세 개의 `FirstControl` 인스턴스를 만듭니다.

#### <a name="to-compile-and-run-this-sample"></a>이 샘플을 컴파일하고 실행하려면

1. 소스 파일(SimpleForm.cs 또는 SimpleForms.vb)에 다음 예제의 코드를 저장합니다.

2. 소스 파일을 포함하는 디렉터리에서 다음 명령을 실행하여 소스 코드를 실행 가능한 어셈블리로 컴파일합니다.

    ```console
    vbc -r:CustomWinControls.dll -r:System.dll -r:System.Windows.Forms.dll -r:System.Drawing.dll SimpleForm.vb
    ```

    ```console
    csc -r:CustomWinControls.dll -r:System.dll -r:System.Windows.Forms.dll -r:System.Drawing.dll SimpleForm.cs
    ```

     CustomWinControls.dll은 클래스를 포함 하는 어셈블리 `FirstControl`합니다. 이 어셈블리는 액세스하는 양식의 소스 파일과 동일한 디렉터리에 있어야 합니다(SimpleForm.cs 또는 SimpleForms.vb).

3. 다음 명령을 사용하여 SimpleForm.exe를 실행합니다.

    ```console
    SimpleForm
    ```

[!code-csharp[System.Windows.Forms.FirstControl#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/CS/SimpleForm.cs#10)]
[!code-vb[System.Windows.Forms.FirstControl#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/VB/SimpleForm.vb#10)]

## <a name="see-also"></a>참고자료

- [Windows Forms 컨트롤의 속성](properties-in-windows-forms-controls.md)
- [Windows Forms 컨트롤의 이벤트](events-in-windows-forms-controls.md)
