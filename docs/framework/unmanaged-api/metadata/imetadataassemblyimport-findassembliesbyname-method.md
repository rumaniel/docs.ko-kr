---
title: IMetaDataAssemblyImport::FindAssembliesByName 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyImport.FindAssembliesByName
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyImport::FindAssembliesByName
helpviewer_keywords:
- FindAssembliesByName method [.NET Framework metadata]
- IMetaDataAssemblyImport::FindAssembliesByName method [.NET Framework metadata]
ms.assetid: 4db97cf9-e4c1-4233-8efa-cbdc0e14a8e4
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 315d9aa6f7db51342e71ba3f8fcdc091f7707743
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67777973"
---
# <a name="imetadataassemblyimportfindassembliesbyname-method"></a>IMetaDataAssemblyImport::FindAssembliesByName 메서드
지정 된 어셈블리의 배열을 가져옵니다 `szAssemblyName` 는 CLR (공용 언어 런타임) 참조를 확인 하 여는 표준 규칙을 사용 하 여 매개 변수입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT FindAssembliesByName (  
    [in]  LPCWSTR     szAppBase,   
    [in]  LPCWSTR     szPrivateBin,   
    [in]  LPCWSTR     szAssemblyName,   
    [out] IUnknown    *ppIUnk[],   
    [in]  ULONG       cMax,   
    [out] ULONG       *pcAssemblies  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `szAppBase`  
 [in] 지정된 된 어셈블리에 대 한 검색 하는 루트 디렉터리입니다. 이 값 설정 하는 경우 `null`, `FindAssembliesByName` 어셈블리에 대 한 전역 어셈블리 캐시에만 표시 됩니다.  
  
 `szPrivateBin`  
 [in] 목록 세미콜론으로 구분 된 하위 디렉터리 (예를 들어, "bin; bin2"), 어셈블리에 대 한 검색 하는 루트 디렉터리 아래입니다. 기본 검색 규칙에에서 지정 된 것 외에도 이러한 디렉터리가 검색 됩니다.  
  
 `szAssemblyName`  
 [in] 찾을 어셈블리의 이름입니다. 이 문자열의 형식은 클래스 참조 페이지에 대 한 정의 <xref:System.Reflection.AssemblyName>합니다.  
  
 `ppIUnk`  
 [in] 형식 배열의 [IUnknown](/cpp/atl/iunknown) 저장할는 `IMetadataAssemblyImport` 인터페이스 포인터입니다.  
  
 `cMax`  
 [out] 인터페이스 포인터에 배치할 수 있는 최대 `ppIUnk`합니다.  
  
 `pcAssemblies`  
 [out] 반환 된 인터페이스 포인터의 수입니다. 인터페이스 포인터의 개수에 실제로 배치, `ppIUnk`합니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|Description|  
|-------------|-----------------|  
|`S_OK`|`FindAssembliesByName` 성공적으로 반환 합니다.|  
|`S_FALSE`|어셈블리가 없는 경우|  
  
## <a name="remarks"></a>설명  
 지정 된 어셈블리 이름의 `FindAssembliesByName` 메서드 어셈블리 참조를 확인 하는 데 표준 규칙에 따라 어셈블리를 찾습니다. (자세한 내용은 [런타임 어셈블리를 찾는 방법](../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md).) `FindAssembliesByName` 호출자가 어셈블리 확인자 컨텍스트 응용 프로그램 기본 및 개인 검색 경로 등의 다양 한 측면을 구성할 수 있습니다.  
  
 `FindAssembliesByName` 메서드 어셈블리 해결 논리를 호출 하기 위해 초기화 프로세스에서 CLR이 있어야 합니다. 따라서 호출 해야 합니다 [CoInitializeEE](../../../../docs/framework/unmanaged-api/hosting/coinitializeee-function.md) (COINITEE_DEFAULT 전달) 호출 하기 전에 `FindAssembliesByName`를 호출 하 여 다음 [CoUninitializeCor](../../../../docs/framework/unmanaged-api/hosting/couninitializecor-function.md)합니다.  
  
 `FindAssembliesByName` 반환 된 [IMetaDataImport](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md) 전달 되는 어셈블리 이름에 대 한 어셈블리 매니페스트를 포함 하는 파일에 대 한 포인터입니다. 지정 된 어셈블리 이름 (예: 버전 포함 되어 있지 않으면) 완벽 하 게 지정 하지 않으면 여러 어셈블리 반환 될 수 있습니다.  
  
 `FindAssembliesByName` 컴파일 타임에 참조 된 어셈블리를 찾으려고 시도 하는 컴파일러에서 주로 사용 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [런타임에서 어셈블리를 찾는 방법](../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)
- [IMetaDataAssemblyImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyimport-interface.md)
