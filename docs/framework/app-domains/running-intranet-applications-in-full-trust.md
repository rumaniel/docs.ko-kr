---
title: 완전 신뢰 모드에서 인트라넷 응용 프로그램 실행
ms.date: 03/30/2017
helpviewer_keywords:
- full trust, running intranet applications in
- intranet applications, running in full trust
- running intranet applications in full trust
ms.assetid: ee13c0a8-ab02-49f7-b8fb-9eab16c6c4f0
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8a40d77f58d6a614f874e12f118f89f25f149e55
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50180649"
---
# <a name="running-intranet-applications-in-full-trust"></a>완전 신뢰 모드에서 인트라넷 응용 프로그램 실행
.NET Framework 버전 3.5 SP1(서비스 팩 1)부터 응용 프로그램 및 해당 라이브러리 어셈블리를 네트워크 공유에서 완전 신뢰 어셈블리로 실행할 수 있습니다. <xref:System.Security.SecurityZone.MyComputer> 영역 증거가 인트라넷의 공유에서 로드된 어셈블리에 자동으로 추가됩니다. 이 증거는 컴퓨터에 있는 어셈블리와 동일한 권한 부여 집합(일반적으로 완전 신뢰)을 해당 어셈블리에 제공합니다. 이 기능은 호스트에서 실행되도록 설계된 응용 프로그램 또는 ClickOnce 응용 프로그램에는 적용되지 않습니다.  
  
## <a name="rules-for-library-assemblies"></a>라이브러리 어셈블리에 대한 규칙  
 다음 규칙은 네트워크 공유의 실행 파일에 의해 로드된 어셈블리에 적용됩니다.  
  
-   라이브러리 어셈블리는 실행 가능한 어셈블리와 동일한 폴더에 있어야 합니다. 하위 폴더에 있거나 다른 경로에서 참조된 어셈블리에는 완전 신뢰 권한 부여 집합이 제공되지 않습니다.  
  
-   실행 파일이 어셈블리를 지연 로드하는 경우 실행 파일을 시작하는 데 사용된 것과 동일한 경로를 사용해야 합니다. 예를 들어 \\\\*network-computer*\\*share*라는 공유를 드라이브 문자에 매핑한 경우 이 경로에서 실행 파일을 실행하면 실행 파일에서 네트워크 경로를 사용하여 로드한 어셈블리에 완전 신뢰가 부여되지 않습니다. <xref:System.Security.SecurityZone.MyComputer> 영역에서 어셈블리를 지연 로드하려면 실행 파일이 드라이브 문자 경로를 사용해야 합니다.  
  
## <a name="restoring-the-former-intranet-policy"></a>이전 인트라넷 정책 복원  
 이전 버전의 .NET Framework에서는 공유 어셈블리에 <xref:System.Security.SecurityZone.Intranet> 영역 증거가 부여되었습니다. 공유의 어셈블리에 완전 신뢰를 부여하려면 코드 액세스 보안 정책을 지정해야 했습니다.  
  
 이 새로운 동작은 인트라넷 어셈블리에 대한 기본값입니다. 컴퓨터의 모든 응용 프로그램에 적용되는 레지스트리 키를 설정하여 <xref:System.Security.SecurityZone.Intranet> 증거를 제공하는 이전 동작으로 되돌릴 수 있습니다. 이 프로세스는 32비트 컴퓨터와 64비트 컴퓨터에서 다릅니다.  
  
-   32비트 컴퓨터에서는 시스템 레지스트리의 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework 키 아래에 하위 키를 만듭니다. 키 이름 LegacyMyComputerZone, DWORD 값 1을 사용합니다.  
  
-   64비트 컴퓨터에서는 시스템 레지스트리의 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework 키 아래에 하위 키를 만듭니다. 키 이름 LegacyMyComputerZone, DWORD 값 1을 사용합니다. HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework 키 아래에 동일한 하위 키를 만듭니다.  
  
## <a name="see-also"></a>참고 항목  
- [어셈블리를 사용한 프로그래밍](../../../docs/framework/app-domains/programming-with-assemblies.md)
