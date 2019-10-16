---
title: 설치 문제 해결
ms.date: 03/30/2017
ms.assetid: 1644f885-c408-4d5f-a5c7-a1a907bc8acd
ms.openlocfilehash: 326daab1f7df5f8a4ea4f74fd8890031f243f7f5
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291522"
---
# <a name="troubleshooting-setup-issues"></a>설치 문제 해결
이 항목에서는 WCF (Windows Communication Foundation) 설정 문제를 해결 하는 방법에 대해 설명 합니다.  
  
## <a name="some-windows-communication-foundation-registry-keys-are-not-repaired-by-performing-an-msi-repair-operation-on-the-net-framework-30"></a>일부 Windows Communication Foundation 레지스트리 키를 .NET Framework 3.0에서 MSI 복구 작업을 수행하여 복구할 수 없음  
 다음과 같은 레지스트리 키를 삭제한 경우 이 문제가 발생합니다.  
  
- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ServiceModelService 3.0.0.0  
  
- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ServiceModelOperation 3.0.0.0  
  
- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ServiceModelEndpoint 3.0.0.0  
  
- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\SMSvcHost 3.0.0.0  
  
- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSDTC Bridge 3.0.0.0  
  
 제어판의 [ **프로그램 추가/제거** **]** 에서 시작 된 .NET Framework 3.0 설치 관리자를 사용 하 여 복구를 실행 하는 경우 키가 다시 생성 되지 않습니다. 해당 키를 다시 만들려면 .NET Framework 3.0을 제거하고 다시 설치해야 합니다.  
  
## <a name="wmi-service-corruption-blocks-installation-of-the-windows-communication-foundation-wmi-provider-during-installation-of-net-framework-30-package"></a>.NET Framework 3.0 패키지 설치 시 WMI 서비스 손상으로 인해 Windows Communication Foundation WMI 공급자가 설치되지 않음  
 WMI 서비스 손상으로 인해 Windows Communication Foundation WMI 공급자가 설치되지 않을 수 있습니다. 설치 시 Windows Communication Foundation 설치 관리자가 mofcomp.exe 구성 요소를 사용하여 WCF .mof 파일을 등록할 수 없습니다. 다음과 같은 증상이 있습니다.  
  
1. .NET Framework 3.0 설치를 완료했지만 WCF WMI 공급자가 등록되지 않습니다.  
  
2. 오류 이벤트가 WCF의 WMI 공급자 등록이나 mofcomp.exe 실행에 관련된 문제를 참조하는 애플리케이션 이벤트 로그에 표시됩니다.  
  
3. 사용자의 %temp% 디렉터리에 있는 이름이 dd_wcf_retCA*인 설치 로그 파일에 WCF WMI 공급자 등록 실패에 대한 참조가 있습니다.  
  
4. 다음과 같은 예외가 이벤트 로그나 설치 추적 로그 파일에 표시됩니다.  
  
     ServiceModelReg [11:09:59:046]: System.ApplicationException: "E:\WINDOWS\Microsoft.NET\Framework\v3.0\Windows Communication Foundation\ServiceModel.mof"를 사용 하 여 E:\WINDOWS\system32\wbem\mofcomp.exe를 실행 하는 예기치 않은 결과 3  
  
     또는  
  
     ServiceModelReg [07:19:33:843]: System.TypeInitializationException: ' System.object. ManagementPath '의 형식 이니셜라이저가 예외를 throw 했습니다. >---T e m. COMException (0x80040154): 다음 오류로 인해 CLSID {CF4CC405-E2C5-4DDD-B3CE-5E7582D8C9FA}가 포함 된 구성 요소에 대 한 COM 클래스 팩터리를 검색 하지 못했습니다. 80040154.  
  
     또는  
  
     ServiceModelReg [07:19:32:750]: System.IO.FileNotFoundException: 파일이 나 어셈블리 ' C:\WINDOWS\system32\wbem\mofcomp.exe ' 또는 해당 종속성 중 하나를 로드할 수 없습니다. 시스템에서 지정한 파일을 찾을 수 없습니다.  
  
     파일 이름 'C:\WINDOWS\system32\wbem\mofcomp.exe  
  
 위에 설명한 문제를 해결하려면 다음 단계를 수행해야 합니다.  
  
1. [WMI Diagnosis Utility 버전 2.0을](https://go.microsoft.com/fwlink/?LinkId=94685) 실행 하 여 WMI 서비스를 복구 합니다. 이 도구를 사용 하는 방법에 대 한 자세한 내용은 [WMI Diagnosis Utility](https://go.microsoft.com/fwlink/?LinkId=94686) 항목을 참조 하세요.  
  
 **제어판**에 있는 **프로그램 추가/제거** 애플릿을 사용 하 여 .NET Framework 3.0 설치를 복구 하거나 .NET Framework 3.0를 제거/다시 설치 합니다.  
  
## <a name="repairing-net-framework-30-after-net-framework-35-installation-removes-configuration-elements-introduced-by-net-framework-35-in-machineconfig"></a>.NET Framework 3.5 설치 후 .NET Framework 3.0을 복구하면 machine.config에서 .NET Framework 3.5에 의해 추가된 구성 요소가 제거됨  
 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]를 설치한 후 .NET Framework 3.0을 복구하면 machine.config에서 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]에 의해 추가된 구성 요소가 제거됩니다. 그러나 web.config는 그대로 유지됩니다. 해결 방법은 ARP를 통해이 후에 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]을 복구 하거나 `/c` 스위치와 [워크플로 서비스 등록 도구 (wfservicesreg.exe)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md) 를 사용 하는 것입니다.  
  
 [워크플로 서비스 등록 도구 (wfservicesreg.exe)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md) 는 \Framework\v3.5\ 또는%windir%\Microsoft.NET\framework64\v3.5\에서 찾을 수 있습니다.  
  
## <a name="configure-iis-properly-for-wcfwf-webhost-after-installing-net-framework-35"></a>.NET Framework 3.5 설치 후 WCF/WF Webhost에 대해 IIS를 올바로 구성  
 @No__t-0 설치는 추가 WCF 관련 IIS 구성 설정을 구성 하지 못할 경우 설치 로그에 오류를 기록 하 고 계속 합니다. 필요한 구성 설정이 없기 때문에 WorkflowServices 애플리케이션을 실행할 수 없습니다. 예를 들어 xoml 또는 규칙 서비스를 로드하지 못할 수 있습니다.  
  
 이 문제를 해결 하려면 `/c` 스위치와 [워크플로 서비스 등록 도구 (wfservicesreg.exe)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md) 를 사용 하 여 컴퓨터에서 IIS 스크립트 맵을 제대로 구성 합니다. [워크플로 서비스 등록 도구 (wfservicesreg.exe)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md) 는 \Framework\v3.5\ 또는%windir%\Microsoft.NET\framework64\v3.5\에서 찾을 수 있습니다.  
  
## <a name="could-not-load-type-systemservicemodelactivationhttpmodule-from-assembly-systemservicemodel-version-3000-cultureneutral-publickeytokenb77a5c561934e089"></a>‘System.ServiceModel, Version 3.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089’ 어셈블리에서 ‘System.ServiceModel.Activation.HttpModule’ 형식을 로드할 수 없습니다.  
 이 오류는 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]이 설치 되어 있고 WCF HTTP 활성화가 사용 하도록 설정 된 경우에 발생 합니다. 이 문제를 해결 하려면 Visual Studio 용 개발자 명령 프롬프트 내에서 다음 명령줄을 실행 합니다.  
  
```console
aspnet_regiis.exe -i -enable  
```  
  
## <a name="see-also"></a>참조

- [설치 지침](../../../docs/framework/wcf/samples/set-up-instructions.md)
