---
title: '문제 해결: 서비스 응용 프로그램이 설치되지 않음'
ms.date: 03/30/2017
helpviewer_keywords:
- troubleshooting service applications
- services, troubleshooting
- services, debugging
- Windows NT services, troubleshooting
- troubleshooting NT services
- Windows Service applications, troubleshooting
ms.assetid: 45c48e2e-b97d-44bc-8896-14f328e0ce33
author: ghogen
ms.openlocfilehash: 0912ff0909ffa5b22bed07543a2e514de4fb1ff5
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48035833"
---
# <a name="troubleshooting-service-application-won39t-install"></a>문제 해결: 서비스 응용 프로그램이 설치되지 않음
서비스 응용 프로그램이 올바로 설치되지 않으면 서비스 클래스의 <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> 속성이 해당 서비스의 설치 관리자에 표시된 값과 동일하게 설정되어 있는지 확인합니다. 서비스가 올바로 설치되려면 이 값이 두 인스턴스 모두에서 동일해야 합니다.  
  
> [!NOTE]
>  설치 로그를 확인하여 설치 프로세스에 대한 피드백을 얻을 수도 있습니다.  
  
 같은 이름의 다른 서비스가 이미 설치되어 있는지도 확인해야 합니다. 서비스 이름이 고유해야만 설치될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Windows 서비스 응용 프로그램 소개](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)
