---
title: '방법: Visual Basic에서 사용자 설정 유지'
ms.date: 07/20/2015
helpviewer_keywords:
- My.Settings object [Visual Basic], persisting user settings
- persistence [Visual Basic], persisting user settings [Visual Basic]
- user settings [Visual Basic], persisting
ms.assetid: 0e5e6415-b6e2-4602-9be0-a65fa167d007
ms.openlocfilehash: 0683a5c359da1c4d082f7312c1ed8f43e1c151f3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968384"
---
# <a name="how-to-persist-user-settings-in-visual-basic"></a>방법: Visual Basic에서 사용자 설정 유지
`My.Settings.Save` 메서드를 사용하여 사용자 설정에 대한 변경 내용을 유지할 수 있습니다.  
  
 일반적으로 애플리케이션은 해당 애플리케이션이 종료될 때 사용자 설정에 대한 변경 내용을 유지하도록 설계되었습니다. 이는 여러 가지 요인에 따라 몇 초마다 설정이 저장될 수 있기 때문입니다.  
  
 자세한 내용은 [My.Settings 개체](../../../../visual-basic/language-reference/objects/my-settings-object.md)를 참조하세요.  
  
> [!NOTE]
> 런타임에 사용자 범위의 값을 변경하고 저장할 수 있지만 애플리케이션 범위 설정은 읽기 전용이고 프로그래밍 방식으로 변경할 수 없습니다. **프로젝트 디자이너**를 통해 또는 애플리케이션의 구성 파일을 편집하여 애플리케이션을 만들 때 애플리케이션 범위 설정을 변경할 수 있습니다. 자세한 내용은 [애플리케이션 설정 관리(.NET)](/visualstudio/ide/managing-application-settings-dotnet)를 참조하세요.  
  
## <a name="example"></a>예  
 이 예제에서는 `LastChanged` 사용자 설정의 값을 변경하고 `My.Settings.Save` 메서드를 호출하여 해당 변경 내용을 저장합니다.  
  
 [!code-vb[VbVbalrMyResources#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#5)]  
  
 이 예제가 작동하려면 애플리케이션에 `Date` 형식의 `LastChanged` 사용자 설정이 있어야 합니다. 자세한 내용은 [애플리케이션 설정 관리(.NET)](/visualstudio/ide/managing-application-settings-dotnet)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [My.Settings 개체](../../../../visual-basic/language-reference/objects/my-settings-object.md)
- [방법: Visual Basic에서 애플리케이션 설정 읽기](../../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)
- [방법: Visual Basic에서 사용자 설정 변경](../../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)
- [방법: Visual Basic에서 사용자 설정의 속성 표 만들기](../../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)
- [애플리케이션 설정 관리(.NET)](/visualstudio/ide/managing-application-settings-dotnet)
