---
title: '방법: Visual Basic에서 사용자 설정의 속성 표 만들기'
ms.date: 07/20/2015
helpviewer_keywords:
- My.Settings object [Visual Basic], creating property grids for user settings
- user settings [Visual Basic], creating property grids
- property grids [Visual Basic], creating for user settings
- property grids
ms.assetid: b0bc737e-50d1-43d1-a6df-268db6e6f91c
ms.openlocfilehash: 4a31b44cca61caea5fdf725405646f628b5430b7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968388"
---
# <a name="how-to-create-property-grids-for-user-settings-in-visual-basic"></a>방법: Visual Basic에서 사용자 설정의 속성 표 만들기
<xref:System.Windows.Forms.PropertyGrid> 컨트롤을 `My.Settings` 개체의 사용자 설정 속성으로 채워 사용자 설정에 대한 속성 표를 만들 수 있습니다.  
  
> [!NOTE]
> 이 예제가 작동하려면 애플리케이션에 해당 사용자 설정이 구성되어 있어야 합니다. 자세한 내용은 [애플리케이션 설정 관리(.NET)](/visualstudio/ide/managing-application-settings-dotnet)를 참조하세요.  
  
 `My.Settings` 개체는 각 설정을 속성으로 표시합니다. 속성 이름은 설정 이름과 같고 속성 형식은 설정 형식과 같습니다. 설정의 **범위**는 속성이 읽기 전용인지 여부를 결정합니다. **애플리케이션** 범위 설정의 속성은 읽기 전용이지만 **사용자** 범위 설정의 속성은 읽기-쓰기입니다. 자세한 내용은 [My.Settings 개체](../../../../visual-basic/language-reference/objects/my-settings-object.md)를 참조하세요.  
  
> [!NOTE]
> 런타임에 애플리케이션 범위 설정의 값을 변경하거나 저장할 수 없습니다. **프로젝트 디자이너**를 통해 또는 애플리케이션의 구성 파일을 편집하여 애플리케이션을 만들 때만 애플리케이션 범위 설정을 변경할 수 있습니다. 자세한 내용은 [애플리케이션 설정 관리(.NET)](/visualstudio/ide/managing-application-settings-dotnet)를 참조하세요.  
  
 이 예제에서는 <xref:System.Windows.Forms.PropertyGrid> 컨트롤을 사용하여 `My.Settings` 개체의 사용자 설정 속성에 액세스합니다. 기본적으로 <xref:System.Windows.Forms.PropertyGrid>는 `My.Settings` 개체의 모든 속성을 표시합니다. 하지만 사용자 설정 속성에는 <xref:System.Configuration.UserScopedSettingAttribute> 특성이 있습니다. 이 예제에서는 <xref:System.Windows.Forms.PropertyGrid>의 <xref:System.Windows.Forms.PropertyGrid.BrowsableAttributes%2A> 속성을 <xref:System.Configuration.UserScopedSettingAttribute>로 설정하여 사용자 설정 속성만 표시합니다.  
  
### <a name="to-add-a-user-setting-property-grid"></a>사용자 설정 속성 표를 추가하려면  
  
1. **도구 상자**에서 애플리케이션의 디자인 화면(여기서는 `Form1`)으로 **PropertyGrid** 컨트롤을 추가합니다.  
  
     속성 표 컨트롤의 기본 이름은 `PropertyGrid1`입니다.  
  
2. `Form1`의 디자인 화면을 두 번 클릭하여 양식 로드 이벤트 처리기에 대한 코드를 엽니다.  
  
3. `My.Settings` 개체를 속성 표에 대해 선택된 개체로 설정합니다.  
  
     [!code-vb[VbVbalrMyResources#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#11)]  
  
4. 사용자 설정만 표시하도록 속성 표를 구성합니다.  
  
     [!code-vb[VbVbalrMyResources#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#12)]  
  
    > [!NOTE]
    > 애플리케이션 범위 설정만 표시하려면 <xref:System.Configuration.UserScopedSettingAttribute> 대신 <xref:System.Configuration.ApplicationScopedSettingAttribute> 특성을 사용합니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 애플리케이션이 종료될 때 사용자 설정이 저장됩니다. 설정을 즉시 저장하려면 `My.Settings.Save` 메서드를 호출합니다. 자세한 내용은 [방법: Visual Basic에서 사용자 설정 유지](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [My.Settings 개체](../../../../visual-basic/language-reference/objects/my-settings-object.md)
- [방법: Visual Basic에서 애플리케이션 설정 읽기](../../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)
- [방법: Visual Basic에서 사용자 설정 변경](../../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)
- [방법: Visual Basic에서 사용자 설정 유지](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)
- [애플리케이션 설정 관리(.NET)](/visualstudio/ide/managing-application-settings-dotnet)
