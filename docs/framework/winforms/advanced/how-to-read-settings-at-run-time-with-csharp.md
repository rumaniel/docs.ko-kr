---
title: '방법: C#을 사용하여 런타임에 설정 읽기'
ms.date: 03/30/2017
helpviewer_keywords:
- application settings [Windows Forms], reading
- application settings [Windows Forms], run time
- application settings [Windows Forms], C#
ms.assetid: dbe8bf09-5e1c-49da-9192-154033d7240b
ms.openlocfilehash: 6a40718d57fad4041eeea2fded03b7256abbe8d1
ms.sourcegitcommit: eb9ff6f364cde6f11322e03800d8f5ce302f3c73
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68710220"
---
# <a name="how-to-read-settings-at-run-time-with-c"></a>방법: C를 사용 하 여 런타임에 설정 읽기\#

속성 개체를 통해 런타임에 애플리케이션 범위 및 사용자 범위 설정을 둘 다 읽을 수 있습니다. Properties 개체는 속성을 정의 하는 프로젝트의 기본 네임 스페이스에 있는 기본 네임 스페이스의 기본 네임 스페이스에 있는 속성을 통해 프로젝트의 모든 기본 설정을 노출 합니다.  
  
## <a name="to-read-settings-at-run-time-with-c"></a>런타임에 C를 사용 하 여 설정을 읽으려면\#
  
Properties.Settings.Default 멤버를 통해 적절한 설정에 액세스합니다. 다음 예제에서는 `myColor` 설정을 BackColor 속성에 할당하는 방법을 보여 줍니다. `System.Drawing.Color` 형식의 `myColor` 설정이 포함된 설정 파일을 미리 만들어야 합니다. 설정 파일 [을 만드는 방법에 대 한 자세한 내용은 방법: 디자인 타임](how-to-create-a-new-setting-at-design-time.md)에 새 설정을 만듭니다.  
  
```csharp
this.BackColor = Properties.Settings.Default.myColor;  
```  
  
## <a name="see-also"></a>참고자료

- [응용 프로그램 설정 및 사용자 설정 사용](using-application-settings-and-user-settings.md)
- [방법: 런타임에 사용자 설정 쓰기C#](how-to-write-user-settings-at-run-time-with-csharp.md)
- [응용 프로그램 설정 개요](application-settings-overview.md)
