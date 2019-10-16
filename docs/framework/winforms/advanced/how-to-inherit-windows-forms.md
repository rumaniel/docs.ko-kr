---
title: '방법: Windows Forms 상속'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- inherited forms [Windows Forms], creating at run-time
- inheritance [Windows Forms], forms
- Windows Forms, inheritance
ms.assetid: cb3e1c0f-3d2a-4cdc-b0d1-c92eae567ffb
ms.openlocfilehash: 402386e16687162e25e16e5c30c787f7e721fbba
ms.sourcegitcommit: 1e72e2990220b3635cebc39586828af9deb72d8c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71306369"
---
# <a name="how-to-inherit-windows-forms"></a>방법: Windows Forms 상속

기본 폼에서 상속해서 새 Windows Forms를 만드는 것은 필요할 때마다 폼을 전체적으로 다시 만드는 프로세스를 거치지 않고 최선의 노력을 되풀이하는 편리한 방법입니다.

디자인 타임에 **상속 선택** 대화 상자를 사용 하 여 폼을 상속 하는 방법과 상속 된 컨트롤 [의 보안 수준을 시각적으로 구분 하는 방법에 대 한 자세한 내용은 방법: 상속 선택 대화 상자](how-to-inherit-forms-using-the-inheritance-picker-dialog-box.md)를 사용 하 여 폼을 상속 합니다.

> [!NOTE]
> 폼에서 상속 하려면 해당 양식을 포함 하는 파일 또는 네임 스페이스가 실행 파일 또는 DLL에 내장 되어 있어야 합니다. 프로젝트를 빌드하려면 **빌드** 메뉴에서 **빌드**를 선택합니다. 또한 네임스페이스에 대한 참조는 폼을 상속하는 클래스에 추가되어야 합니다.

## <a name="inherit-a-form-programmatically"></a>프로그래밍 방식으로 양식 상속

1. 클래스에서 상속받을 폼이 포함된 네임스페이스에 대한 참조를 추가합니다.

2. 클래스 정의에서 상속받을 폼에 대한 참조를 추가합니다. 참조에는 폼이 들어 있는 네임스페이스, 마침표, 기본 폼 자체의 이름이 차례로 포함되어야 합니다.

    ```vb
    Public Class Form2
        Inherits Namespace1.Form1
    ```

    ```csharp
    public class Form2 : Namespace1.Form1
    ```

 폼을 상속할 때 이벤트 처리기가 기본 클래스와 상속된 클래스에서 두 번 호출되는 문제가 발생할 수 있다는 점을 염두에 두어야 합니다. 이 문제를 방지하는 방법에 대한 자세한 내용은 [Visual Basic에서 상속된 이벤트 처리기 관련 문제 해결](../../../visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)을 참조하세요.

## <a name="see-also"></a>참조

- [Inherits 문](../../../visual-basic/language-reference/statements/inherits-statement.md)
- [Imports 문(.NET 네임스페이스 및 형식)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
- [using](../../../csharp/language-reference/keywords/using.md)
- [기본 폼의 모양 수정 효과](effects-of-modifying-base-form-appearance.md)
- [Windows Forms 시각적 개체 상속](windows-forms-visual-inheritance.md)
