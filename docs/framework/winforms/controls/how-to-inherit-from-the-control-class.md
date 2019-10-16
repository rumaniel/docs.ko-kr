---
title: '방법: Control 클래스에서 상속'
ms.date: 03/30/2017
helpviewer_keywords:
- inheritance [Windows Forms], Windows Forms custom controls
- Control class [Windows Forms], inheriting from
- custom controls [Windows Forms], inheritance
- OnPaint method [Windows Forms]
- custom controls [Windows Forms], creating
ms.assetid: 46ba0df3-5cf7-443c-a3b4-a72660172476
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 02c40e310778bd476742f62ee8b9d8598b084a53
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015847"
---
# <a name="how-to-inherit-from-the-control-class"></a>방법: Control 클래스에서 상속

Windows Form에서 사용할 완전히 사용자 지정 컨트롤을 만들려면 <xref:System.Windows.Forms.Control> 클래스에서 상속 해야 합니다. <xref:System.Windows.Forms.Control> 클래스에서 상속 하는 동안 추가 계획 및 구현을 수행 해야 하는 반면, 가장 큰 범위의 옵션도 제공 됩니다. 에서 <xref:System.Windows.Forms.Control>상속 하는 경우 컨트롤이 작동 하 게 하는 매우 기본적인 기능을 상속 합니다. <xref:System.Windows.Forms.Control> 클래스에 내재 된 기능은 키보드와 마우스를 통해 사용자 입력을 처리 하 고, 컨트롤의 범위와 크기를 정의 하 고, windows 핸들을 제공 하 고, 메시지 처리 및 보안을 제공 합니다. 이 경우에는 컨트롤의 그래픽 인터페이스의 실제 렌더링인 그리기를 통합하거나 특정 사용자 상호 작용 기능을 통합하지 않습니다. 사용자 지정 코드를 통해 이러한 모든 사항을 제공해야 합니다.

## <a name="to-create-a-custom-control"></a>사용자 지정 컨트롤을 만들려면

1. Visual Studio에서 새 **Windows 응용 프로그램** 또는 **windows 컨트롤 라이브러리** 프로젝트를 만듭니다.

2. **프로젝트** 메뉴에서 **클래스 추가**를 선택합니다.

3. **새 항목 추가** 대화 상자에서 **사용자 지정 컨트롤**을 클릭합니다.

   새 사용자 지정 컨트롤을 프로젝트에 추가합니다.

4. **F7** 키를 눌러 사용자 지정 컨트롤에 대 한 **코드 편집기** 를 엽니다.

5. 메서드를 찾습니다 .이 메서드는 기본 클래스의 <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드에 대 한 호출을 제외 하 고는 비어 있습니다. <xref:System.Windows.Forms.Control.OnPaint%2A>

6. 코드를 수정하여 컨트롤에 원하는 사용자 지정 그리기를 통합합니다.

   컨트롤의 그래픽을 렌더링하는 코드를 작성하는 방법에 대한 정보는 [사용자 지정 컨트롤 그리기 및 렌더링](custom-control-painting-and-rendering.md)을 참조하세요.

7. 컨트롤이 통합하는 사용자 지정 메서드, 속성 또는 이벤트를 구현합니다.

8. 컨트롤을 저장하고 테스트합니다.

## <a name="see-also"></a>참고자료

- [사용자 지정 컨트롤의 종류](varieties-of-custom-controls.md)
- [방법: UserControl 클래스에서 상속](how-to-inherit-from-the-usercontrol-class.md)
- [방법: 기존 Windows Forms 컨트롤에서 상속](how-to-inherit-from-existing-windows-forms-controls.md)
- [방법: Windows Forms에 대 한 Author 컨트롤](how-to-author-controls-for-windows-forms.md)
- [Visual Basic에서 상속된 이벤트 처리기 관련 문제 해결](../../../visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)
- [디자인 타임에 Windows Forms 컨트롤 개발](developing-windows-forms-controls-at-design-time.md)
