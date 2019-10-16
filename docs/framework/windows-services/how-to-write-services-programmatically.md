---
title: '방법: 프로그래밍 방식으로 서비스 작성'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- services, creating
- Windows Service applications, creating
ms.assetid: 3abbb2ec-78d2-41e6-b9f9-6662d4e2cdc7
author: ghogen
ms.openlocfilehash: 5637d569ad5261bff6865af4ab2ed8b7631d2d38
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053554"
---
# <a name="how-to-write-services-programmatically"></a>방법: 프로그래밍 방식으로 서비스 작성
Windows 서비스 프로젝트 템플릿을 사용하지 않으려는 경우 상속 및 기타 인프라 요소를 직접 설정하여 고유한 서비스를 작성할 수 있습니다. 서비스를 프로그래밍 방식으로 만드는 경우 템플릿을 사용할 경우 자동으로 처리되는 다음과 같은 여러 단계를 직접 수행해야 합니다.  
  
- <xref:System.ServiceProcess.ServiceBase> 클래스에서 상속하도록 서비스 클래스를 설정해야 합니다.  
  
- 서비스 프로젝트에 대한 `Main` 메서드를 만들어야 합니다. 이 메서드는 실행할 서비스를 정의하고 해당 서비스에 대해 <xref:System.ServiceProcess.ServiceBase.Run%2A> 메서드를 호출합니다.  
  
- <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 및 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 프로시저를 재정의하고 이들 프로시저에서 실행할 코드를 입력해야 합니다.  
  
### <a name="to-write-a-service-programmatically"></a>서비스를 프로그래밍 방식으로 작성하려면  
  
1. 빈 프로젝트를 만들고 다음 단계에 따라 필요한 네임스페이스에 대한 참조를 만듭니다.  
  
    1. **솔루션 탐색기**에서 **참조** 노드를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 클릭합니다.  
  
    2. **.NET Framework** 탭에서 **System.dll**로 스크롤하고 **선택**을 클릭합니다.  
  
    3. **System.ServiceProcess.dll**로 스크롤하고 **선택**을 클릭합니다.  
  
    4. **확인**을 클릭합니다.  
  
2. 클래스를 추가하고 <xref:System.ServiceProcess.ServiceBase>에서 상속하도록 클래스를 구성합니다.  
  
     [!code-csharp[VbRadconService#7](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#7)]
     [!code-vb[VbRadconService#7](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#7)]  
  
3. 다음 코드를 추가하여 서비스 클래스를 구성합니다.  
  
     [!code-csharp[VbRadconService#8](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#8)]
     [!code-vb[VbRadconService#8](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#8)]  
  
4. 클래스에 대한 `Main` 메서드를 만들고 이 메서드를 사용하여 클래스에 포함할 서비스를 정의합니다. 여기서 `userService1`은 클래스 이름입니다.  
  
     [!code-csharp[VbRadconService#9](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#9)]
     [!code-vb[VbRadconService#9](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#9)]  
  
5. <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 메서드를 재정의하고 서비스가 시작될 때 수행할 처리를 정의합니다.  
  
     [!code-csharp[VbRadconService#10](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#10)]
     [!code-vb[VbRadconService#10](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#10)]  
  
6. 사용자 지정 처리를 정의할 다른 메서드를 재정의하고 각 경우에 서비스가 수행할 작업을 결정하는 코드를 작성합니다.  
  
7. 서비스 애플리케이션에 필요한 설치 관리자를 추가합니다. 자세한 내용은 [방법: 서비스 애플리케이션에 설치 관리자 추가](how-to-add-installers-to-your-service-application.md)를 참조하세요.  
  
8. **빌드** 메뉴에서 **솔루션 빌드**를 선택하여 프로젝트를 빌드합니다.  
  
    > [!NOTE]
    > F5 키를 눌러 프로젝트를 실행하지 마세요. 서비스 프로젝트는 이러한 방식으로 실행할 수 없습니다.  
  
9. 설치 프로젝트와 서비스를 설치하는 사용자 지정 작업을 만듭니다. 예제를 보려면 [연습: 구성 요소 디자이너에서 Windows 서비스 애플리케이션 만들기](walkthrough-creating-a-windows-service-application-in-the-component-designer.md).  
  
10. 서비스를 설치합니다. 자세한 내용은 [방법: 서비스 설치 및 제거](how-to-install-and-uninstall-services.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [Windows 서비스 애플리케이션 소개](introduction-to-windows-service-applications.md)
- [방법: Windows 서비스 만들기](how-to-create-windows-services.md)
- [방법: 서비스 애플리케이션에 설치 관리자 추가](how-to-add-installers-to-your-service-application.md)
- [방법: 서비스에 대한 정보 로깅](how-to-log-information-about-services.md)
- [연습: 구성 요소 디자이너에서 Windows 서비스 애플리케이션 만들기](walkthrough-creating-a-windows-service-application-in-the-component-designer.md)
