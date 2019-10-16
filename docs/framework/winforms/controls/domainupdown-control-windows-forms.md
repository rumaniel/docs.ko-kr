---
title: DomainUpDown 컨트롤(Windows Forms)
ms.date: 03/30/2017
helpviewer_keywords:
- DomainUpDown control [Windows Forms]
- spin button control [Windows Forms], up-down controls
- up-down controls
- spin button control
- up-down controls [Windows Forms], spin button controls
ms.assetid: fb7cf017-e931-4a95-9d21-8caee4ee122a
ms.openlocfilehash: 83d674e3fb7ff7e715b75c635b891cd4e9703a21
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61972057"
---
# <a name="domainupdown-control-windows-forms"></a>DomainUpDown 컨트롤(Windows Forms)
Windows Forms <xref:System.Windows.Forms.DomainUpDown> 컨트롤 같습니다 조합을 텍스트 상자 및 단추 쌍 목록을 통해 위로 또는 아래로 이동 합니다. 컨트롤이 표시 하 고 선택 목록에서 텍스트 문자열을 설정 합니다. 사용자 단추 목록에서 이동를 클릭 하 여, 위쪽 및 아래쪽 화살표 키를 눌러 또는 목록의 항목을 일치 하는 문자열을 입력 하 여 문자열을 선택할 수 있습니다. 이 컨트롤에 대 한 한 가지 가능한 용도 이름의 사전순으로 정렬된 된 목록에서 항목 선택입니다. (목록을 정렬 하려면 설정 합니다 <xref:System.Windows.Forms.DomainUpDown.Sorted%2A> 속성을 `true`.) 이 컨트롤의 기능 목록 상자 또는 콤보 상자에 매우 유사 하지만 매우 작은 공간을 차지 합니다.  
  
 컨트롤의 키 속성은 <xref:System.Windows.Forms.DomainUpDown.Items%2A>하십시오 <xref:System.Windows.Forms.UpDownBase.ReadOnly%2A>, 및 <xref:System.Windows.Forms.DomainUpDown.Wrap%2A>합니다. <xref:System.Windows.Forms.DomainUpDown.Items%2A> 속성 컨트롤의 텍스트 값을 표시 하는 개체의 목록을 포함 합니다. 하는 경우 <xref:System.Windows.Forms.UpDownBase.ReadOnly%2A> 로 설정 된 `false`, 사용자 형식과 값 목록에 일치 하는 텍스트를 자동으로 완성 하는 컨트롤입니다. 하는 경우 <xref:System.Windows.Forms.DomainUpDown.Wrap%2A> 로 설정 된 `true`, 마지막 항목을 지 나 스크롤 하면 첫 번째 항목 목록에서 이동 하 고 그 반대의 경우도 마찬가지입니다. 컨트롤의 주요 메서드는 <xref:System.Windows.Forms.DomainUpDown.UpButton%2A> 고 <xref:System.Windows.Forms.DomainUpDown.DownButton%2A>입니다.  
  
 이 컨트롤에는 텍스트 문자열만 표시 됩니다. 숫자 값을 표시 하는 컨트롤을 사용 합니다 <xref:System.Windows.Forms.NumericUpDown> 제어 합니다. 자세한 내용은 [NumericUpDown 컨트롤](numericupdown-control-windows-forms.md) 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [DomainUpDown 컨트롤 개요](domainupdown-control-overview-windows-forms.md)  
 일반적인 개념을 소개 합니다 <xref:System.Windows.Forms.DomainUpDown> 컨트롤을 탐색 하 고 텍스트 문자열의 목록에서 선택할 수 있습니다.  
  
 [방법: 프로그래밍 방식으로 Windows Forms DomainUpDown 컨트롤에 항목 추가](how-to-add-items-to-windows-forms-domainupdown-controls-programmatically.md)  
 텍스트 문자열을 지정 하는 방법에 설명 합니다 <xref:System.Windows.Forms.DomainUpDown> 컨트롤이 표시 해야 합니다.  
  
 [방법: Windows Forms DomainUpDown 컨트롤에서 항목을 제거 합니다.](how-to-remove-items-from-windows-forms-domainupdown-controls.md)  
 항목을 삭제 하는 방법에 설명 합니다 <xref:System.Windows.Forms.DomainUpDown> 코드에서 컨트롤입니다.  
  
## <a name="reference"></a>참조  
 <xref:System.Windows.Forms.DomainUpDown>  
 이 클래스를 설명하고 모든 해당 멤버의 링크를 포함합니다.  
  
 <xref:System.Windows.Forms.NumericUpDown>  
 이 클래스를 설명 하 고 모든 해당 멤버에 대 한 링크가 있습니다...  
  
## <a name="related-sections"></a>관련 단원  
 [Windows Forms에서 사용할 수 있는 컨트롤](controls-to-use-on-windows-forms.md)  
 사용 방법에 대한 정보 링크를 포함하는 Windows Forms 컨트롤의 전체 목록을 제공합니다.
