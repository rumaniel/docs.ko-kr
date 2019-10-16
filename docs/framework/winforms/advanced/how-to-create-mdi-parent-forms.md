---
title: '방법: MDI 부모 양식 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- parent forms
- MDI [Windows Forms], creating forms
ms.assetid: 12c71221-2377-4bb6-b10b-7b4b300fd462
ms.openlocfilehash: 2aa4261d6354f744f000f36a87e70a39f5c004ea
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211385"
---
# <a name="how-to-create-mdi-parent-forms"></a>방법: MDI 부모 양식 만들기

> [!IMPORTANT]
> 이 항목에서는 <xref:System.Windows.Forms.MainMenu> 컨트롤로 대체된 <xref:System.Windows.Forms.MenuStrip> 컨트롤을 사용합니다. <xref:System.Windows.Forms.MainMenu> 컨트롤은 이전 버전과의 호환성을 유지하고 원하는 경우 이후에 사용할 수 있도록 유지됩니다. 사용 하 여 부모 폼을 MDI 만들기에 대 한 자세한를 <xref:System.Windows.Forms.MenuStrip>를 참조 하세요 [방법: MenuStrip이 포함 된 MDI 창 목록 만들기](../controls/how-to-create-an-mdi-window-list-with-menustrip-windows-forms.md)합니다.

MDI(다중 문서 인터페이스) 부모 폼은 MDI(다중 문서 인터페이스) 애플리케이션의 기반이 되는 요소로, 사용자가 MDI 애플리케이션과 상호 작용하는 하위 창인 MDI 자식 창을 포함합니다. MDI 부모 폼은 Windows Forms 디자이너에서 그리고 프로그래밍 방식으로 쉽게 만들 수 있습니다.

## <a name="create-an-mdi-parent-form-at-design-time"></a>디자인 타임에 MDI 부모 폼 만들기

1. Visual Studio에서 Windows 응용 프로그램 프로젝트를 만듭니다.

2. 에 **속성** 창에서 설정 합니다 <xref:System.Windows.Forms.Form.IsMdiContainer%2A> 속성을 **true**합니다.

     그러면 폼이 자식 창의 MDI 컨테이너로 지정됩니다.

    > [!NOTE]
    > **속성** 창에서 속성을 설정하는 중에 원하는 경우 `WindowState` 속성을 **Maximized**(최대화)로 설정할 수도 있습니다. 부모 양식을 최대화하면 MDI 자식 창을 가장 쉽게 조작할 수 있기 때문입니다. 또한 MDI 부모 폼에는 <xref:System.Windows.Forms.Control.BackColor%2A?displayProperty=nameWithType> 속성을 사용하여 설정하는 배경색이 아니라 Windows 시스템 제어판에 설정된 시스템 색이 선택됩니다.

3. **도구 상자**에서 **MenuStrip** 컨트롤을 양식으로 끌어옵니다. **텍스트** 속성을 **새로 만들기(&N)** 및 **닫기(&C)** 라는 하위 항목이 있는 **파일(&F)** 로 설정하여 최상위 메뉴 항목을 만듭니다. **창(&W)** 이라는 최상위 메뉴 항목도 만듭니다.

     런타임에 첫 번째 메뉴가 작성되고 메뉴 항목은 숨겨지며 두 번째 메뉴는 열려 있는 MDI 자식 창을 추적합니다. 이제 MDI 부모 창이 만들어졌습니다.

4. **F5** 키를 눌러 응용 프로그램을 실행합니다. MDI 부모 폼 내에서 작동 하는 MDI 자식 창을 만드는 방법에 대 한 내용은 [방법: MDI 자식 폼 만들기](how-to-create-mdi-child-forms.md)합니다.

## <a name="see-also"></a>참고자료

- [MDI(다중 문서 인터페이스) 응용 프로그램](multiple-document-interface-mdi-applications.md)
- [방법: MDI 자식 폼 만들기](how-to-create-mdi-child-forms.md)
- [방법: 활성 MDI 자식 확인](how-to-determine-the-active-mdi-child.md)
- [방법: 활성 MDI 자식으로 데이터 전송](how-to-send-data-to-the-active-mdi-child.md)
- [방법: MDI 자식 폼 정렬](how-to-arrange-mdi-child-forms.md)
