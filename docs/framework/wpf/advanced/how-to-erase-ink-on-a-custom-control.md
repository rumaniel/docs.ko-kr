---
title: '방법: 사용자 지정 컨트롤에서 잉크 지우기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom controls [WPF], erasing ink on
- ink [WPF], erasing on custom control
ms.assetid: d88c50f9-b4d8-4962-a28b-67d6a15a5fe0
ms.openlocfilehash: 60e2af64cb0c5b313f4f1201cab70da6a88f61e7
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57365895"
---
# <a name="how-to-erase-ink-on-a-custom-control"></a>방법: 사용자 지정 컨트롤에서 잉크 지우기
<xref:System.Windows.Ink.IncrementalStrokeHitTester> 현재 그린된 스트로크에 다른 스트로크와 교차 하는지 여부를 결정 합니다.  일부 스트로크를 지울 사용자 수는 컨트롤 만들기에 대 한 유용, 서 사용자 수에 <xref:System.Windows.Controls.InkCanvas> 경우는 <xref:System.Windows.Controls.InkCanvas.EditingMode%2A> 로 설정 되어 <xref:System.Windows.Controls.InkCanvasEditingMode.EraseByPoint>입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 사용자가 일부 스트로크를 지울 수 있는 사용자 지정 컨트롤을 만듭니다.  이 예제에는 초기화 될 때 잉크를 포함 하는 컨트롤을 만듭니다.  잉크를 수집 하는 컨트롤을 만들려면 [잉크 입력 컨트롤 만들기](creating-an-ink-input-control.md).  
  
 [!code-csharp[HowToEraseInk#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToEraseInk/CSharp/InkEraser.cs#1)]
 [!code-vb[HowToEraseInk#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HowToEraseInk/VisualBasic/InkEraser.vb#1)]
