---
title: '방법: Windows Forms에 사용자 인터페이스가 없는 컨트롤 추가'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- NonVisualSelection
helpviewer_keywords:
- invisible controls [Windows Forms]
- Windows Forms controls, adding to form
- controls [Windows Forms], nonvisual
- Windows Forms controls, nonvisual
- nonvisual controls [Windows Forms]
ms.assetid: 52134d9c-cff6-4eed-8e2b-3d5eb3bd494e
ms.openlocfilehash: bc1f844e5a2cf4d4f3b64ebf20e935f36ff85e12
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69987105"
---
# <a name="how-to-add-controls-without-a-user-interface-to-windows-forms"></a>방법: Windows Forms에 사용자 인터페이스가 없는 컨트롤 추가

비시각적 컨트롤 (또는 구성 요소)은 응용 프로그램에 기능을 제공 합니다. 다른 컨트롤과 달리 구성 요소는 사용자에 대 한 사용자 인터페이스를 제공 하지 않으므로 Windows Forms 디자이너 화면에 표시 하지 않아도 됩니다. 구성 요소가 폼에 추가 되 면 Windows Forms 디자이너 모든 구성 요소가 표시 되는 폼의 아래쪽에 크기 조정 가능한 트레이가 표시 됩니다. 구성 요소 트레이에 컨트롤이 추가 되 면 구성 요소를 선택 하 고 폼의 다른 컨트롤과 마찬가지로 해당 속성을 설정할 수 있습니다.

## <a name="add-a-component-to-a-windows-form"></a>Windows Form에 구성 요소 추가

1. Visual Studio에서 폼을 엽니다. 자세한 내용은 [방법: 디자이너](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/w5yd62ts(v=vs.100))에 Windows Forms를 표시 합니다.

2. **도구 상자**에서 구성 요소를 클릭 하 여 폼으로 끌어 옵니다.

     구성 요소가 구성 요소 트레이에 나타납니다.

또한 런타임에 구성 요소를 폼에 추가할 수 있습니다. 이는 특히 사용자 인터페이스가 있는 컨트롤과 달리 구성 요소에 시각적 식이 없기 때문에 일반적인 시나리오입니다. 아래 예제에서는 런타임에 <xref:System.Windows.Forms.Timer> 구성 요소가 추가 됩니다. Visual Studio에는 다양 한 타이머가 포함 되어 있습니다 .이 경우 Windows Forms <xref:System.Windows.Forms.Timer> 구성 요소를 사용 합니다. Visual Studio의 다양 한 타이머에 대 한 자세한 내용은 [서버 기반 타이머 소개](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/tb9yt5e6(v=vs.90))를 참조 하세요.

> [!CAUTION]
> 구성 요소에는 구성 요소가 효과적으로 작동 하기 위해 설정 해야 하는 컨트롤별 속성이 포함 되어 있는 경우가 많습니다. 아래 <xref:System.Windows.Forms.Timer> 구성 요소의 경우 `Interval` 속성을 설정 합니다. 프로젝트에 구성 요소를 추가 하는 경우 해당 구성 요소에 필요한 속성을 설정 해야 합니다.

## <a name="add-a-component-to-a-windows-form-programmatically"></a>프로그래밍 방식으로 Windows Form에 구성 요소 추가

1. 코드에서 <xref:System.Windows.Forms.Timer> 클래스의 인스턴스를 만듭니다.

2. 속성을 `Interval` 설정 하 여 타이머의 틱 간 시간을 결정 합니다.

3. 구성 요소에 필요한 다른 속성을 구성 합니다.

     다음 코드에서는 `Interval` 속성 집합을 사용 하 <xref:System.Windows.Forms.Timer> 여를 만드는 방법을 보여 줍니다.

    ```vb
    Public Sub CreateTimer()
       Dim timerKeepTrack As New System.Windows.Forms.Timer
       timerKeepTrack.Interval = 1000
    End Sub
    ```

    ```csharp
    public void createTimer()
    {
       System.Windows.Forms.Timer timerKeepTrack = new
           System.Windows.Forms.Timer();
       timerKeepTrack.Interval = 1000;
    }
    ```

    ```cpp
    public:
       void createTimer()
       {
          System::Windows::Forms::Timer^ timerKeepTrack = gcnew
             System::Windows::Forms::Timer();
          timerKeepTrack->Interval = 1000;
       }
    ```

    > [!IMPORTANT]
    > 악의적인 UserControl을 참조 하 여 네트워크를 통해 로컬 컴퓨터에 보안 위험을 노출할 수 있습니다. 악의적인 사용자가 손상 된 사용자 지정 컨트롤을 만든 다음 실수로 프로젝트에 추가 하는 경우에만이 문제가 발생 합니다.

## <a name="see-also"></a>참고자료

- [Windows Forms 컨트롤](index.md)
- [방법: Windows Forms에 컨트롤 추가](how-to-add-controls-to-windows-forms.md)
- [방법: ActiveX 컨트롤을 Windows Forms에 추가](how-to-add-activex-controls-to-windows-forms.md)
- [Windows Forms에 컨트롤 넣기](putting-controls-on-windows-forms.md)
- [개별 Windows Forms 컨트롤 레이블 지정 및 바로 가기 제공](labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)
- [Windows Forms에 사용할 수 있는 컨트롤](controls-to-use-on-windows-forms.md)
- [기능별 Windows Forms 컨트롤](windows-forms-controls-by-function.md)
