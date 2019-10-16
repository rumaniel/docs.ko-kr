---
title: TableLayoutPanel 컨트롤의 AutoSize 동작
ms.date: 03/30/2017
helpviewer_keywords:
- AutoSize property [Windows Forms], tableLayoutPanel control
- controls [Windows Forms], sizing
- localizing forms
- layout [Windows Forms], AutoSize
- sizing [Windows Forms], automatic
- TableLayoutPanel control [Windows Forms], AutoSize behavior
- automatic sizing
- AutoSizeMode property
ms.assetid: 9233e0c3-2fa6-405e-8701-959479b1250e
ms.openlocfilehash: 1f349981125097af4a3ca8a1950b820a0334bd11
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64621488"
---
# <a name="autosize-behavior-in-the-tablelayoutpanel-control"></a>TableLayoutPanel 컨트롤의 AutoSize 동작
## <a name="distinct-autosize-behaviors"></a>고유 AutoSize 동작  
 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤은 다음과 같은 방법으로 자동 크기 조정 동작을 지원 합니다.  
  
- 통해 여 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성  
  
- 통해 합니다 <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> 속성에는 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤의 열 및 행 스타일입니다.  
  
### <a name="the-autosize-property-with-row-and-column-styles"></a>행과 열 스타일을 사용 하 여 자동 크기 조정 속성  
 다음 표에서 간의 상호 작용 합니다 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성 및 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤의 열 및 행 스타일입니다.  
  
|자동 크기 조정 설정|스타일 상호 작용|  
|----------------------|-----------------------|  
|`false`|<xref:System.Windows.Forms.TableLayoutPanel> 컨트롤 왼쪽에서 오른쪽으로 진행 하 고 다음 순서 대로 또는 열 이나 행에 대 한 공간을 할당 합니다.<br /><br /> 1.  경우는 <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> 속성이 <xref:System.Windows.Forms.SizeType.Absolute>, 지정 된 픽셀 수 <xref:System.Windows.Forms.ColumnStyle.Width%2A> 또는 <xref:System.Windows.Forms.RowStyle.Height%2A> 할당 됩니다.<br />2.  경우는 <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> 속성이 <xref:System.Windows.Forms.SizeType.AutoSize>, 자식 컨트롤에 의해 반환 되는 픽셀 수가 <xref:System.Windows.Forms.Control.GetPreferredSize%2A> 메서드 할당 됩니다.<br />3.  모든 공백 뒤 <xref:System.Windows.Forms.SizeType.Absolute> 하 고 <xref:System.Windows.Forms.SizeType.AutoSize> 열 또는 행 할당 열 또는 행 <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> 로 <xref:System.Windows.Forms.SizeType.Percent> 남은 공간을 비례적으로 할당 하는 데 사용 됩니다|  
|`true`|예외를 사용 하 여 이전 상호 작용 비슷합니다는 <xref:System.Windows.Forms.SizeType.Percent> 열 또는 행 자동 크기 조정 aspect를 획득 합니다.<br /><br /> 합니다 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤이 확장 가능한 공간을 만들려면 행 이나 열의 있도록 없는 열 또는 행 <xref:System.Windows.Forms.SizeType.Percent> 스타일 해당 콘텐츠를 자릅니다. 합니다 <xref:System.Windows.Forms.TableLayoutPanel> 비율에 따라 새 공간을 할당 하는 컨트롤을 <xref:System.Windows.Forms.ColumnStyle.Width%2A> 또는 <xref:System.Windows.Forms.RowStyle.Height%2A> 속성입니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.TableLayoutPanel>
- [TableLayoutPanel 컨트롤 개요](tablelayoutpanel-control-overview.md)
