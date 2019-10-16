---
title: '방법: TableLayoutPanel 컨트롤에서 컨트롤 맞춤 및 늘이기'
ms.date: 03/30/2017
f1_keywords:
- net.ComponentModel.StyleCollectionEditor.TLP.AlignStretchCtrl
helpviewer_keywords:
- TableLayoutPanel control [Windows Forms], stretching controls
- controls [Windows Forms], stretching
- controls [Windows Forms], aligning
ms.assetid: 7dc1a157-6fee-4995-8ebc-b65bdc0909a8
ms.openlocfilehash: fd32593bcad9e3f3ef93edee8aa2659d423f9feb
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65210359"
---
# <a name="how-to-align-and-stretch-a-control-in-a-tablelayoutpanel-control"></a>방법: TableLayoutPanel 컨트롤에서 컨트롤 맞춤 및 늘이기

정렬 하는 컨트롤에서 stretch를 <xref:System.Windows.Forms.TableLayoutPanel> 사용 하 여를 <xref:System.Windows.Forms.Control.Anchor%2A> 및 <xref:System.Windows.Forms.Control.Dock%2A> 속성.

## <a name="align-and-stretch-a-control"></a>맞춤 및 늘이기 컨트롤

1. Visual Studio에서 끌어를 <xref:System.Windows.Forms.TableLayoutPanel> 에서 제어 합니다 **도구 상자** 폼입니다.

2. 끌어서를 <xref:System.Windows.Forms.Button> 에서 제어 합니다 **도구 상자** 의 왼쪽 위 셀에는 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤입니다. <xref:System.Windows.Forms.Button> 중앙 제어 셀에 배치 됩니다.

3. 값을 설정 합니다 <xref:System.Windows.Forms.Button> 컨트롤의 <xref:System.Windows.Forms.Control.Anchor%2A> 속성을 `Left,Right`입니다. <xref:System.Windows.Forms.Button> 컨트롤이 셀의 너비에 맞게 늘어납니다.

4. 값을 설정 합니다 <xref:System.Windows.Forms.Button> 컨트롤의 <xref:System.Windows.Forms.Control.Anchor%2A> 속성을 `Top,Bottom`입니다. <xref:System.Windows.Forms.Button> 컨트롤이 셀의 높이 맞게 늘어납니다.

5. 값을 설정 합니다 <xref:System.Windows.Forms.Button> 컨트롤의 <xref:System.Windows.Forms.Control.Dock%2A> 속성을 <xref:System.Windows.Forms.DockStyle.Fill>입니다. <xref:System.Windows.Forms.Button> 컨트롤이 확장 되어 셀을 채웁니다.

6. 값을 설정 합니다 <xref:System.Windows.Forms.Button> 컨트롤의 <xref:System.Windows.Forms.Control.Dock%2A> 속성을 <xref:System.Windows.Forms.DockStyle.None>입니다. <xref:System.Windows.Forms.Button> 컨트롤 원래 크기를 반환 하 고 셀의 왼쪽 위 모퉁이로 이동 합니다. **Windows Forms 디자이너** 가 설정 된 <xref:System.Windows.Forms.Control.Anchor%2A> 속성을 `Top, Left`입니다.

7. 값을 설정 합니다 <xref:System.Windows.Forms.Button> 컨트롤의 <xref:System.Windows.Forms.Control.Anchor%2A> 속성을 `Bottom,Right`입니다. <xref:System.Windows.Forms.Button> 셀의 오른쪽 아래 모퉁이에 컨트롤은 이동 합니다.

8. 값을 설정 합니다 <xref:System.Windows.Forms.Button> 컨트롤의 <xref:System.Windows.Forms.Control.Anchor%2A> 속성을 <xref:System.Windows.Forms.AnchorStyles.None>입니다. <xref:System.Windows.Forms.Button> 셀의 가운데에 컨트롤은 이동 합니다.

## <a name="see-also"></a>참고자료

- [TableLayoutPanel 컨트롤](tablelayoutpanel-control-windows-forms.md)
