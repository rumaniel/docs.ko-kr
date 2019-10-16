---
title: (WPF) 스타일에서 애니메이션을 적용 하는 방법
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], properties [WPF], within styles
- styles [WPF], animating properties within
ms.assetid: 6a791f3d-6b1f-4972-a2f9-35880bcfd954
ms.openlocfilehash: 5fb18a2d927746c3437ec01d2a19327be373cae3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61789287"
---
# <a name="how-to-animate-in-a-style"></a>스타일에서 애니메이션을 적용 하는 방법

이 예에서는 스타일 내에서 속성에 애니메이션을 적용 하는 방법을 보여 줍니다. 스타일 내에서 애니메이션, 스타일 정의 되는 프레임 워크 요소만 직접 지정할 수 있습니다. Freezable 개체를 대상으로 하면 해야 "dot 아래로" 스타일의 요소 속성에서.

다음 예제에서는 여러 애니메이션 스타일 내에서 정의 되 고 적용을 <xref:System.Windows.Controls.Button>입니다. 불투명에서 부분적으로 투명 하 고 백을 사라지기 단추 위로 마우스를 이동할 때 반복적으로, 다시 합니다. 사용자가 단추 밖으로 마우스를 움직이면 완전히 불투명 하 게 됩니다. 단추를 클릭 하면 해당 배경색이 흰색으로 다시 주황색에서 변경 합니다. 때문에 합니다 <xref:System.Windows.Media.SolidColorBrush> 그리는 데 단추는 직접 대상이 될 수 없습니다, 아래쪽 단추에서 연결 하는지 확인 하 여 액세스할 수 <xref:System.Windows.Controls.Control.Background%2A> 속성입니다.

## <a name="example"></a>예제

[!code-xaml[timingbehaviors_snip#21](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/StyleStoryboardsExample.xaml#21)]

스타일 내에서 애니메이션을 적용할 때는 수 있다는 것 존재 하지 않는 대상 개체에 note 합니다. 예를 들어, 다음을 사용 하 여 스타일을 <xref:System.Windows.Media.SolidColorBrush> 단추의 배경 속성을 설정 하지만 특정 시점에 스타일을 재정의 되 고 단추의 배경을 사용 하 여 설정 됩니다는 <xref:System.Windows.Media.LinearGradientBrush>합니다.  애니메이션을 적용 하는 동안는 <xref:System.Windows.Media.SolidColorBrush> ; 예외를 throw 하지 않습니다만 애니메이션 자동으로 실패 합니다.

스토리 보드 대상 지정 구문에 대 한 자세한 내용은 참조는 [스토리 보드 개요](storyboards-overview.md)합니다. 애니메이션에 대 한 자세한 내용은 참조는 [애니메이션 개요](animation-overview.md)합니다. 스타일에 대 한 자세한 내용은 참조는 [스타일 및 템플릿](../controls/styling-and-templating.md)합니다.
