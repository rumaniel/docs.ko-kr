---
title: AssemblyOptions 열거형
ms.date: 03/30/2017
api_name:
- AssemblyOptions
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- AssemblyOptions
helpviewer_keywords:
- Alink API, AssemblyOptions enumeration
- AssemblyOptions enumeration
ms.assetid: 84f83921-64cb-49e3-ac8b-22a0b77b18a8
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 49e7b73559e8def890f8df8f596fbe8ad5bb5d3b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70777484"
---
# <a name="assemblyoptions-enumeration"></a>AssemblyOptions 열거형
어셈블리 옵션을 열거 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum _AssemblyOptions {  
    optAssemTitle = 0,  
    optAssemDescription,  
    optAssemConfig,  
    optAssemOS,  
    optAssemProcessor,  
    optAssemLocale,  
    optAssemVersion,  
    optAssemCompany,  
    optAssemProduct,  
    optAssemProductVersion,  
    optAssemCopyright,  
    optAssemTrademark,  
    optAssemKeyFile,  
    optAssemKeyName,  
    optAssemAlgID,  
    optAssemFlags,  
    optAssemHalfSign,  
    optAssemFileVersion,  
    optAssemSatelliteVer,  
    optLastAssemOption  
}   AssemblyOptions;  
```  
  
## <a name="fields"></a>필드  
  
|필드|Description|  
|-----------|-----------------|  
|optAssemTitle|String-어셈블리 제목을 나타냅니다.|  
|optAssemDescription|String-어셈블리 설명을 포함 합니다.|  
|optAssemConfig|String-어셈블리 구성을 포함 합니다.|  
|optAssemOS|문자열 인코딩: "dwOSPlatformId. DwosdwOSMinorVersion".|  
|optAssemProcessor|ULONG|  
|optAssemLocale|String-어셈블리 로캘을 포함 합니다.|  
|optAssemVersion|문자열 인코딩: "Major.Minor.Build.Revision".|  
|optAssemCompany|String-회사를 포함 합니다.|  
|optAssemProduct|String-제품 이름을 포함 합니다.|  
|optAssemProductVersion|문자열 (InformationalVersion이 라고도 함)|  
|optAssemCopyright|String-저작권 정보를 포함 합니다.|  
|optAssemTrademark|String-상표 정보를 포함 합니다.|  
|optAssemKeyFile|문자열 (파일 이름)입니다.|  
|optAssemKeyName|문자열 (키 이름)입니다.|  
|optAssemAlgID|ULONG|  
|optAssemFlags|ULONG|  
|optAssemHalfSign|Bool (DelaySign 라고도 함).|  
|optAssemFileVersion|"Major. ProductVersion"로 인코딩된 문자열입니다.|  
|optAssemSatelliteVer|"Major. 부. 빌드. 수정 버전"으로 문자열 인코딩됩니다.|  
|optLastAssemOption|요소 수의 카운터입니다.|  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** alink. h  
  
 **라이브러리**: alink .dll  
  
## <a name="see-also"></a>참고자료

- [Al.exe(어셈블리 링커)](../../tools/al-exe-assembly-linker.md)
