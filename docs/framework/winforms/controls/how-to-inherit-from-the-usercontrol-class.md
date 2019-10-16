---
title: '방법: UserControl 클래스에서 상속'
ms.date: 03/30/2017
helpviewer_keywords:
- inheritance [Windows Forms], Windows Forms custom controls
- UserControl class [Windows Forms], inheriting from
- user controls [Windows Forms], creating
- composite controls [Windows Forms], creating
ms.assetid: 67713625-e2e4-4f6a-bce7-0855ee5043d9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7f4055c2374103b7df941d9a9bef24ed5e6cb27c
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015836"
---
# <a name="how-to-inherit-from-the-usercontrol-class"></a>방법: UserControl 클래스에서 상속

사용자 지정 코드를 사용하여 하나 이상의 Windows Forms 컨트롤의 기능을 결합하려면 *사용자 정의 컨트롤*을 만들면 됩니다. 사용자 정의 컨트롤은 빠른 컨트롤 개발, 표준 Windows Forms 컨트롤 기능 및 사용자 지정 속성 및 메서드의 다양성을 모두 제공합니다. 사용자 정의 컨트롤을 만들기 시작하면 표준 Windows Forms 컨트롤을 배치할 수 있는 시각적인 디자이너로 표시됩니다. 이러한 컨트롤은 표준 컨트롤의 모양 및 동작(모양 및 느낌)뿐만 아니라 고유 기능을 모두 유지합니다. 그러나 이러한 컨트롤이 사용자 정의 컨트롤에 기본 제공되지 않으면 더 이상 코드를 통해 사용할 수 없습니다. 사용자 정의 컨트롤은 고유한 그리기를 수행하고 컨트롤과 관련된 모든 기본 기능을 처리합니다.

## <a name="to-create-a-user-control"></a>사용자 정의 컨트롤을 만들려면

1. Visual Studio에서 새 **Windows 컨트롤 라이브러리** 프로젝트를 만듭니다.

   새 프로젝트는 빈 사용자 정의 컨트롤을 사용하여 생성됩니다.

2. 디자이너의 **도구 상자**에 있는 **Windows Forms** 탭에서 컨트롤을 끌어 놓습니다.

3. 최종 사용자 정의 컨트롤에 표시하려는 대로 이러한 컨트롤을 배치하고 디자인해야 합니다. 개발자가 구성 요소 컨트롤에 액세스할 수 있도록 하려는 경우 공용으로 선언하거나 선택적으로 구성 요소 컨트롤의 속성을 노출해야 합니다. 자세한 내용은 [방법: 구성 요소 컨트롤](how-to-expose-properties-of-constituent-controls.md)의 속성을 노출 합니다.

4. 컨트롤이 통합하는 사용자 지정 메서드 또는 속성을 구현합니다.

5. **F5** 키를 눌러 프로젝트를 빌드하고 **UserControl 테스트 컨테이너**에서 컨트롤을 실행 합니다. 자세한 내용은 [방법: UserControl](how-to-test-the-run-time-behavior-of-a-usercontrol.md)의 런타임 동작을 테스트 합니다.

## <a name="see-also"></a>참고자료

- [사용자 지정 컨트롤의 종류](varieties-of-custom-controls.md)
- [방법: Control 클래스에서 상속](how-to-inherit-from-the-control-class.md)
- [방법: 기존 Windows Forms 컨트롤에서 상속](how-to-inherit-from-existing-windows-forms-controls.md)
- [방법: Windows Forms에 대 한 Author 컨트롤](how-to-author-controls-for-windows-forms.md)
- [Visual Basic의 상속 된 이벤트 처리기 문제 해결](~/docs/visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)
- [방법: UserControl의 런타임 동작 테스트](how-to-test-the-run-time-behavior-of-a-usercontrol.md)
