---
title: Fusion 전역 정적 함수
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged global static functions [.NET Framework], fusion
- fusion global static functions [.NET Framework]
- global static functions [.NET Framework fusion]
ms.assetid: 229b2188-9168-4b44-a987-e1f515494688
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6a8f15bc862c0486311960f7567c49424859846e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795321"
---
# <a name="fusion-global-static-functions"></a>Fusion 전역 정적 함수
이 섹션에서는 fusion API에서 사용 하는 관리 되지 않는 전역 정적 함수에 대해 설명 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [ClearDownloadCache 함수](cleardownloadcache-function.md)  
 다운로드 한 어셈블리의 전역 어셈블리 캐시를 지웁니다.  
  
 [CompareAssemblyIdentity 함수](compareassemblyidentity-function.md)  
 두 어셈블리 id를 비교 하 여 같은지 여부를 확인 합니다.  
  
 [CreateApplicationContext 함수](createapplicationcontext-function.md)  
 내부 전용입니다. 이 함수는 .NET Framework 인프라를 지원 하며 사용자 코드에서 직접 사용 하기 위한 것이 아닙니다.)  
  
 [CreateAssemblyCache 함수](createassemblycache-function.md)  
 전역 어셈블리 캐시를 나타내는 새 [Iassemblycache](iassemblycache-interface.md) 인스턴스에 대 한 포인터를 가져옵니다.  
  
 [CreateAssemblyEnum 함수](createassemblyenum-function.md)  
 지정 된 어셈블리에 존재 하는 개체의 목록을 나타내는 [Iassemblyenum](iassemblyenum-interface.md) 인스턴스에 대 한 포인터를 가져옵니다.  
  
 [CreateAssemblyNameObject 함수](createassemblynameobject-function.md)  
 지정 된 이름을 사용 하 여 어셈블리의 고유 id를 나타내는 [IAssemblyName](iassemblyname-interface.md) 인스턴스에 대 한 포인터를 가져옵니다.  
  
 [CreateHistoryReader 함수](createhistoryreader-function.md)  
 지정 된 파일에 대 한 기록 판독기를 만듭니다.  
  
 [CreateInstallReferenceEnum 함수](createinstallreferenceenum-function.md)  
 지정 된 어셈블리에 대 한 응용 프로그램 참조 목록을 나타내는 [Iinstallreferenceenum](iinstallreferenceenum-interface.md) 인스턴스에 대 한 포인터를 가져옵니다.  
  
 [GetAppIdAuthority 함수](getappidauthority-function.md)  
 응용 프로그램 id 및 참조에 대 한 키를 관리 하는 [Iappidauthority](iappidauthority-interface.md) 인스턴스에 대 한 포인터를 가져옵니다.  
  
 [GetAssemblyIdentityFromFile 함수](getassemblyidentityfromfile-function.md)  
 어셈블리에서 지정 된 파일 `IUnknown` 경로의 지정 `IID` 된을 사용 하 여 개체에 대 한 포인터를 가져옵니다.  
  
 [GetCachePath 함수](getcachepath-function.md)  
 지정 된 플래그를 사용 하 여 캐시 된 어셈블리에 대 한 경로를 가져옵니다.  
  
 [GetHistoryFileDirectory 함수](gethistoryfiledirectory-function.md)  
 응용 프로그램 기록 디렉터리의 경로를 검색 합니다.  
  
 [GetIdentityAuthority 함수](getidentityauthority-function.md)  
 코드 개체에 대 한 키를 관리 하는 [IIdentityAuthority](iidentityauthority-interface.md) 인스턴스에 대 한 포인터를 가져옵니다.  
  
 [IsFrameworkAssembly 함수](isframeworkassembly-function.md)  
 지정 된 어셈블리가 관리 되는지 여부를 나타내는 값을 가져옵니다.  
  
 [NukeDownloadedCache 함수](nukedownloadedcache-function.md)  
 공용 언어 런타임 다운로드 캐시를 삭제 합니다.  
  
 [PreBindAssemblyEx 함수](prebindassemblyex-function.md)  
 어셈블리의 정책 후 표시 이름을 가져옵니다.  
  
## <a name="related-sections"></a>관련 단원  
 [Fusion 인터페이스](fusion-interfaces.md)  
  
 [Fusion 열거형](fusion-enumerations.md)  
  
 [Fusion 구조체](fusion-structures.md)  
  
 [전역 어셈블리 캐시](../../app-domains/gac.md)
