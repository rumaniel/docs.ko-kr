---
title: '방법: Windows Forms에서 컨트롤 잠금'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms controls, locking
- controls [Windows Forms], locking
ms.assetid: 94efe0d2-c14e-4d14-b903-63ea9b07e290
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f6dd079331c6c1883839efe5c6cb127044380fd2
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69987468"
---
# <a name="how-to-lock-controls-to-windows-forms"></a>방법: 컨트롤을 Windows Forms 잠금

Windows 응용 프로그램의 UI (사용자 인터페이스)를 디자인할 때 컨트롤이 제대로 배치 되 면 컨트롤을 잠가 다른 속성을 설정할 때 실수로 이동 하거나 크기를 조정할 수 없습니다.

또한 폼의 모든 컨트롤을 한 번에 잠그거나 잠금 해제할 수 있습니다 .이는 많은 컨트롤이 있는 폼에 유용 하거나 개별 컨트롤의 잠금을 해제할 수 있습니다. 폼에서 원하는 위치에 컨트롤을 모두 배치한 후에는 잘못 된 움직임을 방지 하기 위해 모든 컨트롤을 잠급니다.

## <a name="to-lock-a-control"></a>컨트롤을 잠그려면

Visual Studio의 **속성** 창에서 **Locked** 속성을 선택 하 고 **true**를 선택 합니다. (이름을 두 번 클릭 하면 속성 설정이 전환 됩니다.)

또는 컨트롤을 마우스 오른쪽 단추로 클릭 하 고 **컨트롤 잠금**을 선택 합니다.

> [!NOTE]
> 컨트롤을 잠그면 디자인 화면의 새 크기 또는 위치로 끌어 올 수 없습니다. 그러나 **속성** 창이 나 코드를 통해 컨트롤의 크기나 위치를 변경할 수 있습니다.

## <a name="to-lock-all-the-controls-on-a-form"></a>폼의 모든 컨트롤을 잠그려면

**서식** 메뉴에서 **컨트롤 잠금**을 선택 합니다.

> [!NOTE]
> 이 명령은 폼이 컨트롤 이기 때문에 폼의 크기도 잠급니다.

## <a name="to-unlock-all-locked-controls-on-a-form"></a>폼에서 잠긴 컨트롤의 잠금을 해제 하려면

**서식** 메뉴에서 **컨트롤 잠금**을 선택 합니다.

이제 폼에서 모든 이전에 잠긴 컨트롤의 잠금이 해제 됩니다.

## <a name="to-unlock-locked-controls-individually"></a>개별적으로 잠긴 컨트롤의 잠금을 해제 하려면

**속성** 창에서 **Locked** 속성을 선택 하 고 **false**를 선택 합니다. (이름을 두 번 클릭 하면 속성 설정이 전환 됩니다.)

## <a name="see-also"></a>참고자료

- [Windows Forms 컨트롤](index.md)
- [개별 Windows Forms 컨트롤 레이블 지정 및 바로 가기 제공](labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)
- [Windows Forms에 사용할 수 있는 컨트롤](controls-to-use-on-windows-forms.md)
- [기능별 Windows Forms 컨트롤](windows-forms-controls-by-function.md)
