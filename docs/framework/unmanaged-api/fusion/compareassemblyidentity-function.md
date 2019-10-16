---
title: CompareAssemblyIdentity 함수
ms.date: 03/30/2017
api_name:
- CompareAssemblyIdentity
api_location:
- fusion.dll
- clr.dll
api_type:
- COM
f1_keywords:
- CompareAssemblyIdentity
helpviewer_keywords:
- CompareAssemblyIdentity function [.NET Framework fusion]
ms.assetid: 8b364ae1-8efa-4744-a7da-81fd093d84d6
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b52d3af38bd09ce5864c25d27e148dbd7f4639b0
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795452"
---
# <a name="compareassemblyidentity-function"></a>CompareAssemblyIdentity 함수
두 어셈블리 id를 비교 하 여 같은지 여부를 확인 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
STDAPI CompareAssemblyIdentity (  
    [in]  LPCWSTR                  pwzAssemblyIdentity1,  
    [in]  BOOL                     fUnified1,  
    [in]  LPCWSTR                  pwzAssemblyIdentity2,  
    [in]  BOOL                     fUnified2,  
    [out] BOOL                     *pfEquivalent,  
    [out] AssemblyComparisonResult *pResult  
 );  
```  
  
## <a name="parameters"></a>매개 변수  
 `pwzAssemblyIdentity1`  
 진행 비교할 첫 번째 어셈블리의 텍스트 id입니다.  
  
 `fUnified1`  
 진행 에 대 한 `pwzAssemblyIdentity1`사용자 지정 통합을 나타내는 부울 플래그입니다.  
  
 `pwzAssemblyIdentity2`  
 진행 비교 하는 두 번째 어셈블리의 텍스트 id입니다.  
  
 `fUnified2`  
 진행 에 대 한 `pwzAssemblyIdentity2`사용자 지정 통합을 나타내는 부울 플래그입니다.  
  
 `pfEquivalent`  
 제한이 두 어셈블리가 동일한 지 여부를 나타내는 부울 플래그입니다.  
  
 `pResult`  
 제한이 비교에 대 한 자세한 정보를 포함 하는 [AssemblyComparisonResult](assemblycomparisonresult-enumeration.md) 열거형입니다.  
  
## <a name="return-value"></a>반환 값  
 `pfEquivalent`두 어셈블리가 동일한 지 여부를 나타내는 부울 값을 반환 합니다. `pResult`값 중 하나 `AssemblyComparisonResult` 를 반환 하 여 `pfEquivalent`값에 대 한 보다 자세한 원인을 제공 합니다.  
  
## <a name="remarks"></a>설명  
 `CompareAssemblyIdentity``pwzAssemblyIdentity1` 및`pwzAssemblyIdentity2` 가 동일한 지 여부를 확인 합니다. `pfEquivalent`는 다음 조건 `true` 중 하나 이상에서로 설정 됩니다.  
  
- 두 어셈블리 id는 동일 합니다. 강력한 이름의 어셈블리의 경우에는 어셈블리 이름, 버전, 공개 키 토큰 및 문화권이 동일 해야 합니다. 단순한 이름의 어셈블리의 경우에는 어셈블리 이름 및 문화권과 일치 해야 합니다.  
  
- 두 어셈블리 id는 모두 .NET Framework에서 실행 되는 어셈블리를 참조 합니다. 이 상태는 `true` 어셈블리 버전 번호가 일치 하지 않는 경우에도 반환 됩니다.  
  
- 두 어셈블리가 관리 되는 어셈블리가 아니지만 `fUnified1` 또는 `fUnified2` 로 `true`설정 된 경우  
  
 플래그 `fUnified` 는 강력한 이름의 어셈블리에 대 한 버전 번호 까지의 모든 버전 번호가 강력한 이름의 어셈블리와 동일한 것으로 간주 됨을 나타냅니다. 예를 들어 값 `pwzAssemblyIndentity1` 이 "MyAssembly, version = 3.0.0.0, culture = 중립, publicKeyToken = ..."이 고 `fUnified1` 값이 인 `true`경우에는 모든 버전의 MyAssembly를 버전 0.0.0.0에서 3.0.0.0로 지정 합니다. 동일 하 게 처리 됩니다. `pwzAssemblyIndentity2` 이 경우에서와 `pwzAssemblyIndentity1`동일한 어셈블리를 참조 하는 경우 `pfEquivalent` 는 더 낮은 버전 `true`번호가 있다는 점을 제외 하 고는로 설정 됩니다. `fUnified2` `pfEquivalent` `true` 가 더 높은 버전 번호를 `true`참조 하는 경우는의 값이 인 경우에만로 설정 됩니다. `pwzAssemblyIdentity2`  
  
 `pResult` 매개 변수에는 두 어셈블리가 동등 하거나 동일 하지 않은 것으로 간주 되는 이유에 대 한 특정 정보가 포함 되어 있습니다. 자세한 내용은 [AssemblyComparisonResult 열거형](assemblycomparisonresult-enumeration.md)을 참조 하세요.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Fusion. h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [Fusion 전역 정적 함수](fusion-global-static-functions.md)
- [AssemblyComparisonResult 열거형](assemblycomparisonresult-enumeration.md)
