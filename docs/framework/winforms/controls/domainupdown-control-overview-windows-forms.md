---
title: DomainUpDown 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- DomainUpDown
helpviewer_keywords:
- spin button control [Windows Forms], about spin button
- DomainUpDown control [Windows Forms], about DomainUpDown control
ms.assetid: 3f40f9c1-20ad-4331-b9b5-b0127eb36eb3
ms.openlocfilehash: 6fda542204e2b41dd1d729d2b940c6f38a5812ad
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965309"
---
# <a name="domainupdown-control-overview-windows-forms"></a>DomainUpDown 컨트롤 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.DomainUpDown> 컨트롤은 기본적으로 텍스트 상자와 목록에서 위로 또는 아래로 이동 하는 단추 쌍의 조합입니다. 컨트롤은 선택 목록에서 텍스트 문자열을 표시 하 고 설정 합니다. 사용자는 위로 및 아래로 단추를 클릭 하 여 목록에서 이동 하거나, 위쪽 및 아래쪽 화살표 키를 누르거나, 목록의 항목과 일치 하는 문자열을 입력 하 여 문자열을 선택할 수 있습니다. 이 컨트롤의 한 가지 가능한 용도는 사전순으로 정렬 된 이름 목록에서 항목을 선택 하는 것입니다.  
  
> [!NOTE]
> 목록을 정렬 하려면 <xref:System.Windows.Forms.DomainUpDown.Sorted%2A> 속성을로 `true`설정 합니다.  
  
 이 컨트롤의 함수는 목록 상자나 콤보 상자와 매우 유사 하지만 공간을 거의 차지 하지 않습니다.  
  
## <a name="key-properties"></a>키 속성  
 컨트롤 <xref:System.Windows.Forms.DomainUpDown.Items%2A>의 키 속성은, <xref:System.Windows.Forms.UpDownBase.ReadOnly%2A>및 <xref:System.Windows.Forms.DomainUpDown.Wrap%2A>입니다. <xref:System.Windows.Forms.DomainUpDown.Items%2A> 속성에는 컨트롤에 표시 되는 텍스트 값이 있는 개체의 목록이 포함 되어 있습니다. 가 <xref:System.Windows.Forms.UpDownBase.ReadOnly%2A> 로`false`설정 된 경우 컨트롤은 사용자가 입력 하 고 목록의 값과 일치 하는 텍스트를 자동으로 완성 합니다. 가 <xref:System.Windows.Forms.DomainUpDown.Wrap%2A> 로`true`설정 된 경우 마지막 항목을 벗어나 스크롤하면 목록의 첫 번째 항목으로 이동 하 고 그 반대의 경우도 마찬가지입니다. 컨트롤 <xref:System.Windows.Forms.DomainUpDown.UpButton%2A> 의 주요 메서드는 및 <xref:System.Windows.Forms.DomainUpDown.DownButton%2A>입니다.  
  
 이 컨트롤은 텍스트 문자열만 표시 합니다. 숫자 값을 표시 하는 컨트롤을 사용 하려면 <xref:System.Windows.Forms.NumericUpDown> 컨트롤을 사용 합니다. 자세한 내용은 [NumericUpDown 컨트롤 개요](numericupdown-control-overview-windows-forms.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DomainUpDown>
- [DomainUpDown 컨트롤](domainupdown-control-windows-forms.md)
