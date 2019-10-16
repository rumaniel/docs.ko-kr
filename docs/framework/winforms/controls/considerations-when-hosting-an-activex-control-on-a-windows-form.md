---
title: Windows Form에서 ActiveX 컨트롤을 호스팅할 때의 고려 사항
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms controls, ActiveX controls
- ActiveX controls [Windows Forms], hosting
- Windows Forms, ActiveX controls
- Windows Forms, hosting ActiveX controls
- ActiveX controls [Windows Forms], adding
ms.assetid: 2509302d-a74e-484f-9890-2acdbfa67a68
ms.openlocfilehash: 0b95bab20299b966b9f3c6e6ce089a641670f974
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69933419"
---
# <a name="considerations-when-hosting-an-activex-control-on-a-windows-form"></a>Windows Form에서 ActiveX 컨트롤을 호스팅할 때의 고려 사항
Windows Forms는 Windows Forms 컨트롤을 호스팅하도록 최적화되어 있지만 ActiveX 컨트롤을 사용할 수도 있습니다. ActiveX 컨트롤을 사용하는 애플리케이션을 계획할 때 다음 사항을 고려하세요.  
  
- **보안** 공용 언어 런타임이 코드 액세스 보안과 관련하여 향상되었습니다. Windows Forms 기능이 있는 애플리케이션은 완전히 신뢰할 수 있는 환경에서 문제 없이 실행할 수 있으며, 대부분의 기능에 액세스할 수 있지만 부분적으로 신뢰할 수 있는 환경에서도 실행할 수 있습니다. Windows Forms 컨트롤은 브라우저에서 별다른 어려움 없이 간단하게 호스팅될 수 있지만, Windows Forms의 ActiveX 컨트롤은 향상된 보안 기능을 사용할 수 없습니다. ActiveX 컨트롤을 실행 하려면 <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A?displayProperty=nameWithType> 속성으로 설정 된 비관리 코드 권한이 필요 합니다. 보안 및 비관리 코드 권한에 대 한 자세한 내용은을 참조 <xref:System.Security.Permissions.SecurityPermissionAttribute>하십시오.  
  
- **TCO(총 소유 비용)** Windows Form에 추가된 ActiveX 컨트롤은 해당 Windows Form과 함께 전부 배포되므로 만들어지는 파일의 크기가 상당히 커질 수 있습니다. 또한 Windows Forms에서 ActiveX 컨트롤을 사용하려면 레지스트리에 기록해야 합니다. 이 작업은 레지스트리에 기록할 필요가 없는 Windows Forms 컨트롤에 비해 사용자의 컴퓨터를 간섭할 여지가 많습니다.  
  
    > [!NOTE]
    > ActiveX 컨트롤을 사용하려면 COM interop 래퍼를 사용해야 합니다. 자세한 내용은 [Visual Basic 및 Visual C#의 COM 상호 운용성](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)을 참조하세요.  
  
    > [!NOTE]
    > Activex 컨트롤의 멤버 이름이 .NET Framework에 정의 된 이름과 일치 하는 경우에는 activex 컨트롤 가져오기에서 파생 클래스를 <xref:System.Windows.Forms.AxHost> 만들 때 해당 멤버 이름에 **Ctl** 을 접두사로 사용 합니다. 예를 들어, ActiveX 컨트롤에 이름이 **layout**인 멤버가 있는 경우 **layout** 이벤트가 .NET Framework 내에 정의 되어 있으므로 Axhost 파생 클래스에서 **CtlLayout** 로 이름이 변경 됩니다.  
  
## <a name="see-also"></a>참고자료

- [방법: ActiveX 컨트롤을 Windows Forms에 추가](how-to-add-activex-controls-to-windows-forms.md)
- [코드 액세스 보안](../../misc/code-access-security.md)
- [여러 언어 및 라이브러리에서 사용되는 컨트롤 및 프로그래밍 가능한 개체 비교](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/0061wezk(v=vs.100))
- [Windows Forms에 컨트롤 넣기](putting-controls-on-windows-forms.md)
- [Windows Forms 컨트롤](index.md)
