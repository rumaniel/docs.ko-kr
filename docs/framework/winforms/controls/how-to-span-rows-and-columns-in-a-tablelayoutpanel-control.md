---
title: '방법: TableLayoutPanel 컨트롤에서 행 및 열 확장'
ms.date: 03/30/2017
f1_keywords:
- net.ComponentModel.StyleCollectionEditor.TLP.SpanRowsColumns
helpviewer_keywords:
- columns [Windows Forms], spanning
- merging cells
- TableLayoutPanel control [Windows Forms], spanning rows and columns
- rows [Windows Forms], spanning
- cells [Windows Forms], merging
ms.assetid: a8a2fdd3-a848-48b0-a4cd-4e85ebded87e
ms.openlocfilehash: a215b2b4e05bab5c81d2779d4b67d5b9d57b6ba5
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69039694"
---
# <a name="how-to-span-rows-and-columns-in-a-tablelayoutpanel-control"></a>방법: TableLayoutPanel 컨트롤에서 행 및 열 확장
<xref:System.Windows.Forms.TableLayoutPanel> 컨트롤의 컨트롤은 인접 한 행과 열에 걸쳐 있을 수 있습니다.

## <a name="to-span-columns-and-rows"></a>열 및 행을 확장 하려면

1. <xref:System.Windows.Forms.TableLayoutPanel> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다.

2. <xref:System.Windows.Forms.Button> **도구 상자** 에서 컨트롤의 <xref:System.Windows.Forms.TableLayoutPanel> 왼쪽 위 셀로 컨트롤을 끌어 옵니다.

3. 컨트롤의 **columnspan** 속성을 2로 설정 합니다. <xref:System.Windows.Forms.Button> 컨트롤은 <xref:System.Windows.Forms.Button> 첫 번째 및 두 번째 열로 확장 됩니다.

4. 컨트롤의 RowSpan 속성을 **2**로 설정 합니다. <xref:System.Windows.Forms.Button> 이 컨트롤은 <xref:System.Windows.Forms.Button> 첫 번째 및 두 번째 행으로 확장 됩니다.

5. 컨트롤의 **columnspan** 속성을 1로 설정 합니다. <xref:System.Windows.Forms.Button> <xref:System.Windows.Forms.Button> 컨트롤이 첫 번째 열로 이동 하 고 첫 번째 행과 두 번째 행으로 확장 됩니다.

## <a name="see-also"></a>참고자료

- [TableLayoutPanel 컨트롤](tablelayoutpanel-control-windows-forms.md)
