---
title: '방법: Windows 서비스 일시 중지(Visual Basic)'
ms.date: 03/30/2017
dev_langs:
- vb
f1_keywords:
- ServiceController.Pause
helpviewer_keywords:
- Windows Service applications, pausing
- pausing Windows Service applications
ms.assetid: eddb9409-942b-46b6-a2ce-fbd4c65f2790
author: ghogen
ms.openlocfilehash: c62de97439ecf90ebfcc14d9fea4c5ab52f6ef73
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48035125"
---
# <a name="how-to-pause-a-windows-service-visual-basic"></a>방법: Windows 서비스 일시 중지(Visual Basic)
이 예제에서는 <xref:System.ServiceProcess.ServiceController> 구성 요소를 사용하여 로컬 컴퓨터에서 IIS 관리 서비스를 일시 중지합니다.  
  
## <a name="example"></a>예  
 [!code-vb[VbRadconService#11](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#11)]  
[!code-vb[VbRadconService#12](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#12)]  
  
 이 코드 예제는 IntelliSense 코드 조각으로 사용할 수도 있습니다. 코드 조각 선택에서 **Windows 운영 체제 > Windows 서비스**에 있습니다. 자세한 내용은 [코드 조각](/visualstudio/ide/code-snippets)을 참조하세요.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
-   System.serviceprocess.dll에 대한 프로젝트 참조.  
  
-   <xref:System.ServiceProcess> 네임스페이스의 멤버에 대한 액세스 권한. 코드에서 멤버 이름을 정규화하지 않는 경우 `Imports` 문을 추가합니다. 자세한 내용은 [Imports 문(.NET 네임스페이스 및 형식)](~/docs/visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)을 참조하세요.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 <xref:System.ServiceProcess.ServiceController> 클래스의 <xref:System.ServiceProcess.ServiceController.MachineName%2A> 속성은 기본적으로 로컬 컴퓨터입니다. 다른 컴퓨터에서 Windows 서비스를 참조하려면 <xref:System.ServiceProcess.ServiceController.MachineName%2A> 속성을 해당 컴퓨터의 이름으로 변경합니다.  
  
 다음 조건에서 예외가 발생합니다.  
  
-   서비스를 일시 중지할 수 없습니다. (<xref:System.InvalidOperationException>)  
  
-   시스템 API에 액세스할 때 오류가 발생했습니다. (<xref:System.ComponentModel.Win32Exception>)  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 <xref:System.ServiceProcess.ServiceControllerPermission>에서 <xref:System.ServiceProcess.ServiceControllerPermissionAccess>를 사용하여 권한을 설정하면 컴퓨터에서 서비스 제어가 제한될 수 있습니다.  
  
 <xref:System.Security.Permissions.PermissionState>를 사용하여 <xref:System.Security.Permissions.SecurityPermission>에서 권한을 설정하면 서비스 정보에 대한 액세스가 제한될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.ServiceProcess.ServiceController>  
 <xref:System.ServiceProcess.ServiceControllerStatus>  
 <xref:System.ServiceProcess.ServiceController.WaitForStatus%2A>  
 [방법: Windows 서비스 계속(Visual Basic)](../../../docs/framework/windows-services/how-to-continue-a-windows-service-visual-basic.md)
