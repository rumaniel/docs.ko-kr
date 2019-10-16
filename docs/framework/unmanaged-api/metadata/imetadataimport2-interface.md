---
title: IMetaDataImport2 인터페이스
ms.date: 03/30/2017
api_name:
- IMetaDataImport2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport2
helpviewer_keywords:
- IMetaDataImport2 interface [.NET Framework metadata]
ms.assetid: d39b2b87-ba53-4771-ae53-952a68452511
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6717c48fca14f2200f783a984594388ef3b29c15
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62042473"
---
# <a name="imetadataimport2-interface"></a>IMetaDataImport2 인터페이스
확장을 [IMetaDataImport](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md) 인터페이스의 제네릭 형식 작업 기능을 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[EnumGenericParamConstraints 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-enumgenericparamconstraints-method.md)|제네릭 매개 변수 제약 조건이 지정된 된 토큰을 나타내는 제네릭 매개 변수를 사용 하 여 연결의 배열에 대 한 열거자를 가져옵니다.|  
|[EnumGenericParams 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-enumgenericparams-method.md)|토큰 제네릭 매개 변수 토큰을 지정 된 형식 정의 또는 MethodDef 연결 된 배열에 대 한 열거자를 가져옵니다.|  
|[EnumMethodSpecs 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-enummethodspecs-method.md)|지정한 MethodDef 또는 MemberRef 연관 MethodSpec 토큰 배열의 토큰 열거자를 가져옵니다.|  
|[GetGenericParamConstraintProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-getgenericparamconstraintprops-method.md)|지정 된 제약 조건 토큰이 나타내는 제네릭 매개 변수 제약 조건이 있는 연결 된 메타 데이터를 가져옵니다.|  
|[GetGenericParamProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-getgenericparamprops-method.md)|지정된 된 토큰을 나타내는 제네릭 매개 변수를 사용 하 여 연결 된 메타 데이터를 가져옵니다.|  
|[GetMethodSpecProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-getmethodspecprops-method.md)|지정 된 MethodSpec에서 참조 하는 메서드 메타 데이터 서명의 토큰을 가져옵니다.|  
|[GetPEKind 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-getpekind-method.md)|가져옵니다는 pe (이식 가능)에서 코드의 특성을 식별 하는 값 파일을 일반적으로 DLL 또는 EXE 파일을 현재 메타 데이터 범위에서 정의|  
|[GetVersionString 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-getversionstring-method.md)|어셈블리를 빌드하는 런타임의 버전 번호를 가져옵니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Reflection.PortableExecutableKinds>
- [메타데이터 인터페이스](../../../../docs/framework/unmanaged-api/metadata/metadata-interfaces.md)
- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
