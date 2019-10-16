---
title: .NET Framework 4 및 4.5에 추가된 CLR 호스팅 인터페이스
ms.date: 03/30/2017
helpviewer_keywords:
- hosting interfaces [.NET Framework], version 4
- .NET Framework 4, hosting interfaces
- interfaces [.NET Framework hosting], version 4
ms.assetid: f6af6116-f5b0-4bda-a276-fffdba70893d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ea95789ea1623985a6a53fcf923b70d7df2ad460
ms.sourcegitcommit: a8d3504f0eae1a40bda2b06bd441ba01f1631ef0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67170433"
---
# <a name="clr-hosting-interfaces-added-in-the-net-framework-4-and-45"></a>.NET Framework 4 및 4.5에 추가된 CLR 호스팅 인터페이스
관리 되지 않는 인터페이스를 설명 하는이 섹션에서는 호스트 응용 프로그램에.NET Framework 4,.NET Framework 4.5 및 이후 버전에는 CLR (공용 언어 런타임) 통합을 사용할 수 있습니다. 이러한 인터페이스는 구성 프로세스에 런타임을 로드 하는 호스트에 대 한 메서드를 제공 합니다.  
  
 .NET Framework 4 부터는 모든 호스팅 인터페이스는 다음과 같은 특징이 있습니다.  
  
- 수명 관리 사용 (`AddRef` 하 고 `Release`)를 캡슐화 (암시적 컨텍스트) 및 `QueryInterface` com  
  
- COM 형식이 현재 형식과 같은 사용 하지 `BSTR`하십시오 `SAFEARRAY`, 또는 `VARIANT`합니다.  
  
- 아파트 모델, 집계 또는 없습니다 레지스트리 정품 인증을 사용 하는 합니다 [CoCreateInstance 함수](https://go.microsoft.com/fwlink/?LinkId=142894)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [ICLRAppDomainResourceMonitor 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-interface.md)  
 응용 프로그램 도메인의 메모리 및 CPU 사용량을 검사 하는 방법을 제공 합니다.  
  
 [ICLRDomainManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrdomainmanager-interface.md)  
 호스트를에서 기본 응용 프로그램 도메인을 초기화 하 고 초기화 속성을 지정 하는 응용 프로그램 도메인 관리자를 지정할 수 있습니다.  
  
 [ICLRGCManager2 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrgcmanager2-interface.md)  
 제공 된 [SetGCStartupLimitsEx](../../../../docs/framework/unmanaged-api/hosting/iclrgcmanager2-setgcstartuplimitsex-method.md) 메서드를 사용 하면 가비지 수집 세그먼트의 크기 및 가비지 컬렉션 시스템의 0 세대의 최대 크기 이상으로 설정 값을 호스트 하는 `DWORD`합니다.  
  
 [ICLRMetaHost 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrmetahost-interface.md)  
 CLR의 특정 버전을 반환, 모든 설치 된 Clr 목록, 모든 프로세스에서 런타임을 나열, 정품 인증 인터페이스를 반환 되며 어셈블리로 컴파일하는 데 사용 되는 CLR 버전을 검색 하는 방법을 제공 합니다.  
  
 [ICLRMetaHostPolicy 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrmetahostpolicy-interface.md)  
 제공 된 [GetRequestedRuntime](../../../../docs/framework/unmanaged-api/hosting/iclrmetahostpolicy-getrequestedruntime-method.md) 정책 기준, 관리 되는 어셈블리, 버전 및 구성 파일을 기반으로 CLR 인터페이스를 제공 하는 방법입니다.  
  
 [ICLRRuntimeInfo 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md)  
 특정 런타임 버전, 디렉터리 및 부하 상태를 포함 하 여에 대 한 정보를 반환 하는 메서드를 제공 합니다.  
  
 [ICLRStrongName 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)  
 강력한 이름의 어셈블리를 서명 하는 기본 전역 정적 함수를 제공 합니다. 모든 합니다 [ICLRStrongName](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md) 메서드는 표준 COM HRESULTs를 반환 합니다.  
  
 [ICLRStrongName2 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname2-interface.md)  
 보안 해시 알고리즘 (SHA-256, SHA-384 및 SHA-512)의 sha-2 그룹을 사용 하 여 강력한 이름을 만드는 기능을 제공 합니다.  
  
 [ICLRTask2 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtask2-interface.md)  
 모든 기능을 제공 합니다 [ICLRTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)를 현재 스레드에서 지연 될 스레드 중단을 허용 하는 메서드를 제공 합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [사용되지 않는 CLR 호스팅 인터페이스 및 Coclass](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-interfaces-and-coclasses.md)  
 .NET Framework 버전 1.0 및 1.1을 사용 하 여 제공 하는 호스팅 인터페이스를 설명 합니다.  
  
 [CLR 호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/clr-hosting-interfaces.md)  
 .NET Framework 버전 2.0, 3.0 및 3.5를 사용 하 여 제공 하는 호스팅 인터페이스를 설명 합니다.  
  
 [호스팅](../../../../docs/framework/unmanaged-api/hosting/index.md)  
 .NET Framework에서 호스팅 소개 합니다.
