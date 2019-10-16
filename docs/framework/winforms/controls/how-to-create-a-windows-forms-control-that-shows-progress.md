---
title: '방법: 진행률을 보여 주는 Windows Forms 컨트롤 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [Windows Forms], progress tracking
- controls [Windows Forms], creating
- progress [Windows Forms], reporting [Windows Forms]
- FlashTrackBar custom control
ms.assetid: 24c5a2e3-058c-4b8d-a217-c06e6a130c2f
ms.openlocfilehash: 84f0caace70f9877e84fdd01dc69216dc10fe485
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950570"
---
# <a name="how-to-create-a-windows-forms-control-that-shows-progress"></a>방법: 진행률을 보여 주는 Windows Forms 컨트롤 만들기
다음 코드 예제에서는 사용자에게 수준 또는 애플리케이션의 진행률을 표시하는 데 사용할 수 있는 `FlashTrackBar`이라는 사용자 지정 컨트롤을 보여 줍니다. 그라데이션을 사용하여 진행률을 시각적으로 나타냅니다.  
  
 `FlashTrackBar` 컨트롤에서는 다음과 같은 개념을 보여 줍니다.  
  
- 사용자 지정 속성 정의  
  
- 사용자 지정 이벤트 정의 `FlashTrackBar`은 `ValueChanged` 이벤트를 정의합니다.  
  
- <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드를 재정의 하 여 컨트롤을 그리는 논리를 제공 합니다.  
  
- <xref:System.Windows.Forms.Control.ClientRectangle%2A> 속성을 사용 하 여 컨트롤을 그리는 데 사용할 수 있는 영역을 계산 합니다. `FlashTrackBar`은 해당 `OptimizedInvalidate` 메서드에서 이를 수행합니다.  
  
- Windows Forms 디자이너에서 변경되는 경우 속성의 serialization 또는 지속성을 구현합니다. `FlashTrackBar`은 `StartColor` 및 `EndColor` 속성을 직렬화하는 `ShouldSerializeStartColor` 및 `ShouldSerializeEndColor` 메서드를 정의합니다.  
  
 다음 테이블에서는 `FlashTrackBar`에서 정의된 사용자 지정 속성을 보여 줍니다.  
  
|속성|설명|  
|--------------|-----------------|  
|`AllowUserEdit`|사용자가 플래시 트랙 표시줄의 값을 클릭하고 끌어와서 변경할 수 있는지 여부를 나타냅니다.|  
|`EndColor`|트랙 표시줄의 끝 색을 지정합니다.|  
|`DarkenBy`|전경 그라데이션과 관련하여 배경 밝기의 정도를 지정합니다.|  
|`Max`|트랙 표시줄의 최대값을 지정합니다.|  
|`Min`|트랙 표시줄의 최소값을 지정합니다.|  
|`StartColor`|그라데이션의 시작 색을 지정합니다.|  
|`ShowPercentage`|그라데이션의 백분율을 표시할지 여부를 나타냅니다.|  
|`ShowValue`|그라데이션의 현재 값을 표시할지 여부를 나타냅니다.|  
|`ShowGradient`|트랙 표시줄에서 현재 값을 나타내는 색 그라데이션을 표시해야 할지 여부를 나타냅니다.|  
|-   `Value`|트랙 표시줄의 현재 값을 지정합니다.|  
  
 다음 테이블에서는 `FlashTrackBar:` 속성 변경 이벤트 및 이벤트를 발생시키는 메서드에 의해 정의된 추가 구성원을 보여 줍니다.  
  
|멤버|설명|  
|------------|-----------------|  
|`ValueChanged`|트랙 표시줄의 `Value` 속성이 변경되면 발생하는 이벤트입니다.|  
|`OnValueChanged`|메서드는 `ValueChanged` 이벤트를 발생시킵니다.|  
  
> [!NOTE]
> `FlashTrackBar`이벤트 데이터 <xref:System.EventArgs> 및 <xref:System.EventHandler> 이벤트 대리자에 대해 클래스를 사용 합니다.  
  
 해당 *EventName* 이벤트 `FlashTrackBar` 를 처리 하기 위해은에서 <xref:System.Windows.Forms.Control?displayProperty=nameWithType>상속 되는 다음 메서드를 재정의 합니다.  
  
- <xref:System.Windows.Forms.Control.OnPaint%2A>  
  
- <xref:System.Windows.Forms.Control.OnMouseDown%2A>  
  
- <xref:System.Windows.Forms.Control.OnMouseMove%2A>  
  
- <xref:System.Windows.Forms.Control.OnMouseUp%2A>  
  
- <xref:System.Windows.Forms.Control.OnResize%2A>  
  
 해당 속성 변경 이벤트 `FlashTrackBar` 를 처리 하기 위해은에서 <xref:System.Windows.Forms.Control?displayProperty=nameWithType>상속 되는 다음 메서드를 재정의 합니다.  
  
- <xref:System.Windows.Forms.Control.OnBackColorChanged%2A>  
  
- <xref:System.Windows.Forms.Control.OnBackgroundImageChanged%2A>  
  
- <xref:System.Windows.Forms.Control.OnTextChanged%2A>  
  
## <a name="example"></a>예제  
 `FlashTrackBar` 컨트롤은 `FlashTrackBarValueEditor` 및 `FlashTrackBarDarkenByEditor`이라는 두 개의 UI 형식 편집기를 정의하며 이는 다음 코드 목록에 표시됩니다. `HostApp` 클래스는 Windows Form에소 `FlashTrackBar` 컨트롤을 사용합니다.  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#1)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#1)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBarDarkenByEditor.cs#10)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBarDarkenByEditor.vb#10)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#20](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBarValueEditor.cs#20)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#20](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBarValueEditor.vb#20)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#30](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/HostApp.cs#30)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#30](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/HostApp.vb#30)]  
  
## <a name="see-also"></a>참고자료

- [디자인 타임 지원 확장](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/37899azc(v=vs.120))
- [Windows Forms 컨트롤 개발 기본 사항](windows-forms-control-development-basics.md)
