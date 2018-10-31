---
title: '방법: Windows 서비스 계속(Visual Basic)'
ms.date: 03/30/2017
dev_langs:
- vb
f1_keywords:
- ServiceController.Continue
helpviewer_keywords:
- Windows Service applications, pausing
- pausing Windows Service applications
ms.assetid: e5d13760-4c83-4b0d-abef-39852677cd7a
author: ghogen
ms.openlocfilehash: 255dccfb74eced63ffbeff7ef567083a504cc6da
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48027288"
---
# <a name="how-to-continue-a-windows-service-visual-basic"></a>방법: Windows 서비스 계속(Visual Basic)
이 예제에서는 <xref:System.ServiceProcess.ServiceController> 구성 요소를 사용하여 로컬 컴퓨터에서 IIS 관리 서비스를 계속합니다.  
  
## <a name="example"></a>예  
 [!code-vb[VbRadconService#11](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#11)]  
[!code-vb[VbRadconService#13](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#13)]  
  
 이 코드 예제는 IntelliSense 코드 조각으로 사용할 수도 있습니다. 코드 조각 선택에서 **Windows 운영 체제 > Windows 서비스**에 있습니다. 자세한 내용은 [코드 조각](/visualstudio/ide/code-snippets)을 참조하세요.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
-   System.serviceprocess.dll에 대한 프로젝트 참조.  
  
-   <xref:System.ServiceProcess> 네임스페이스의 멤버에 대한 액세스 권한. 코드에서 멤버 이름을 정규화하지 않는 경우 `Imports` 문을 추가합니다. 자세한 내용은 [Imports 문(.NET 네임스페이스 및 형식)](~/docs/visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)을 참조하세요.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 <xref:System.ServiceProcess.ServiceController> 클래스의 <xref:System.ServiceProcess.ServiceController.MachineName%2A> 속성은 기본적으로 로컬 컴퓨터입니다. 다른 컴퓨터에서 Windows 서비스를 참조하려면 <xref:System.ServiceProcess.ServiceController.MachineName%2A> 속성을 해당 컴퓨터의 이름으로 변경합니다.  
  
 서비스 컨트롤러 상태가 <xref:System.ServiceProcess.ServiceControllerStatus.Paused>인 경우 서비스의 <xref:System.ServiceProcess.ServiceController.Continue%2A> 메서드를 호출할 수 없습니다.  
  
 다음 조건에서 예외가 발생합니다.  
  
-   서비스를 다시 시작할 수 없습니다. (<xref:System.InvalidOperationException>)  
  
-   시스템 API에 액세스할 때 오류가 발생했습니다. (<xref:System.ComponentModel.Win32Exception>)  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 <xref:System.ServiceProcess.ServiceControllerPermission> 클래스에서 <xref:System.ServiceProcess.ServiceControllerPermissionAccess> 열거형을 사용하여 권한을 설정하면 컴퓨터에서 서비스 제어가 제한될 수 있습니다.  
  
 <xref:System.Security.Permissions.PermissionState> 열거형을 사용하여 <xref:System.Security.Permissions.SecurityPermission> 클래스에서 권한을 설정하면 서비스 정보에 대한 액세스가 제한될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.ServiceProcess.ServiceController>  
 <xref:System.ServiceProcess.ServiceControllerStatus>  
 [방법: Windows 서비스 일시 중지(Visual Basic)](../../../docs/framework/windows-services/how-to-pause-a-windows-service-visual-basic.md)
