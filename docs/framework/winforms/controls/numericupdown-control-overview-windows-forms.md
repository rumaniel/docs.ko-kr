---
title: NumericUpDown 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- NumericUpDown
helpviewer_keywords:
- numeric spin button control [Windows Forms], Windows Forms
- NumericUpDown control [Windows Forms], about NumericUpDown control
- spin button control [Windows Forms], Windows Forms
ms.assetid: cff3cf30-4d46-4381-87df-37bfe83c71c5
ms.openlocfilehash: 218eb685e546acac76a18450612a1601ab87276b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61805764"
---
# <a name="numericupdown-control-overview-windows-forms"></a>NumericUpDown 컨트롤 개요(Windows Forms)
<xref:System.Windows.Forms.NumericUpDown> 컨트롤 사용자가 클릭 하 여 값을 조정할 수 있는 화살표 쌍 및 입력란의 조합을 다음과 같습니다. 컨트롤은 표시 하거나 고정 된 숫자 값 선택 목록에서 단일 숫자 값을 설정 합니다. 사용자는 증가 하 고 컨트롤의 텍스트 상자에에서 숫자를 입력 하거나 위쪽 및 아래쪽 화살표 키를 눌러 및 아래쪽 화살표, 화살표를 클릭 하 여 수를 줄일 수 있습니다. 최대 숫자는 이동 위쪽 화살표 키를 클릭 합니다. 아래쪽 화살표 키를 클릭 하면 번호를 최소값으로 이동 합니다.  
  
 여러 유용한 기능으로 인해이 제어는 것이 좋습니다, 예를 들어, 음악 플레이어 응용 프로그램에 대 한 볼륨 컨트롤을 만들려는 경우입니다. <xref:System.Windows.Forms.NumericUpDown> 많은 Windows 제어판 응용 프로그램에서 컨트롤을 사용 합니다.  
  
## <a name="key-properties-and-methods"></a>키 속성 및 메서드  
 컨트롤의 텍스트 상자에 표시 된 숫자 16 진수 다양 한 형식으로 포함 될 수 있습니다. 자세한 내용은 [방법: Windows Forms NumericUpDown 컨트롤의 형식 설정](how-to-set-the-format-for-the-windows-forms-numericupdown-control.md)합니다. 컨트롤의 키 속성은 <xref:System.Windows.Forms.NumericUpDown.Value%2A>, <xref:System.Windows.Forms.NumericUpDown.Maximum%2A> (기본값 100), <xref:System.Windows.Forms.NumericUpDown.Minimum%2A> (기본값 0), 및 <xref:System.Windows.Forms.NumericUpDown.Increment%2A> (기본값은 1). <xref:System.Windows.Forms.NumericUpDown.Value%2A> 속성 컨트롤에서 선택한 현재 수를 설정 합니다. <xref:System.Windows.Forms.NumericUpDown.Increment%2A> 속성 수를 위쪽 클릭 하면 / 아래쪽 화살표 조정 되는 크기를 설정 합니다. 포커스가 컨트롤 밖으로 이동, 입력 된 모든 최소 및 최대 숫자 값에 대해 유효성이 검사 됩니다. 지속적으로 누를 때 위쪽 또는 아래쪽 화살표, 컨트롤 번호를 통해 이동 하는 속도 높일 수 있습니다 사용 하 여는 <xref:System.Windows.Forms.NumericUpDown.Accelerations%2A> 속성입니다. 컨트롤의 주요 메서드는 <xref:System.Windows.Forms.NumericUpDown.UpButton%2A> 고 <xref:System.Windows.Forms.NumericUpDown.DownButton%2A>입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.NumericUpDown>
- [NumericUpDown 컨트롤](numericupdown-control-windows-forms.md)
- [방법: Windows Forms NumericUpDown 컨트롤에 대 한 형식을 설정합니다](how-to-set-the-format-for-the-windows-forms-numericupdown-control.md)
- [TextBox 컨트롤](textbox-control-windows-forms.md)
