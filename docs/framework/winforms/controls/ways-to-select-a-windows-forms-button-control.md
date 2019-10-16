---
title: Windows Forms Button 컨트롤 선택 방법
ms.date: 03/30/2017
helpviewer_keywords:
- Button control [Windows Forms], selecting
ms.assetid: fe2fc058-5118-4f70-b264-6147d64a7a8d
ms.openlocfilehash: e511b0d7bcac725ed477678ab4c865f5337e658d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64584952"
---
# <a name="ways-to-select-a-windows-forms-button-control"></a>Windows Forms Button 컨트롤 선택 방법
다음과 같은 방법으로 Windows Forms 단추를 선택할 수 있습니다.  
  
- 마우스를 사용 하 여 단추를 클릭 합니다.  
  
- 단추의 호출 <xref:System.Windows.Forms.Control.Click> 코드의 이벤트입니다.  
  
- TAB 키를 눌러 단추에 포커스를 이동 하 고 스페이스바 또는 ENTER 키를 누르면 단추를 선택 합니다.  
  
- 단추에 대 한 액세스 키 (ALT + 밑줄이 그어진된 문자)를 누릅니다. 액세스 키에 대 한 자세한 내용은 참조 하세요. [방법: Windows Forms 컨트롤에 대 한 액세스 키를 만들](how-to-create-access-keys-for-windows-forms-controls.md)합니다.  
  
- 다른 컨트롤에 포커스가 있는 경우에 ENTER 키를 눌러 단추가 선택 단추를 폼의 "수락" 단추 이면-다른 단추, 여러 줄 텍스트 상자 또는 enter 키를 트래핑 하는 사용자 지정 컨트롤을 다른 제어 하는 경우를 제외 하 고 있습니다.  
  
- 단추를 폼의 "취소" 단추를 ESC 키를 눌러 선택 단추를 다른 컨트롤에 포커스가 있는 경우에 합니다.  
  
- 호출 된 <xref:System.Windows.Forms.Button.PerformClick%2A> 메서드를 프로그래밍 방식으로 단추를 선택 합니다.  
  
## <a name="see-also"></a>참고자료

- [Button 컨트롤 개요](button-control-overview-windows-forms.md)
- [방법: Windows Forms 단추 클릭에 응답](how-to-respond-to-windows-forms-button-clicks.md)
- [Button 컨트롤](button-control-windows-forms.md)
