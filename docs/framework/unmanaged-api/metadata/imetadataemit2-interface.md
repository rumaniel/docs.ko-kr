---
title: IMetaDataEmit2 인터페이스
ms.date: 03/30/2017
api_name:
- IMetaDataEmit2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit2
helpviewer_keywords:
- IMetaDataEmit2 interface [.NET Framework metadata]
ms.assetid: 866dc96b-bbfc-4c0f-80c2-38ce93072106
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 87b5b60d75d5d28e100ec75192d0cacf51765927
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62042975"
---
# <a name="imetadataemit2-interface"></a>IMetaDataEmit2 인터페이스
확장 된 [IMetaDataEmit](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md) 주로 제네릭 형식을 사용 하는 기능을 제공 하는 인터페이스입니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[DefineGenericParam 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-definegenericparam-method.md)|제네릭 형식 매개 변수에 대 한 정의 만들고 제네릭 형식 매개 변수에 해당 토큰을 가져옵니다.|  
|[DefineMethodSpec 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-definemethodspec-method.md)|메서드의 제네릭 인스턴스를 만들고 정의 하는 토큰을 가져옵니다.|  
|[GetDeltaSaveSize 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-getdeltasavesize-method.md)|편집 하며 계속 하기는 현재 세션의 변경 내용을 나타내는 하는 데 필요한 데이터 크기의 차이 나타내는 값을 가져옵니다.|  
|[ResetENCLog 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-resetenclog-method.md)|편집 하며 계속 하기 로그를 다시 설정 하 고 새 세션을 시작 합니다.|  
|[SaveDelta 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-savedelta-method.md)|편집 하며 계속 하기는 현재 세션에서 지정된 된 파일 변경 내용을 저장 합니다.|  
|[SaveDeltaToMemory 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-savedeltatomemory-method.md)|메모리 편집 하며 계속 하기는 현재 세션에서 변경 내용을 저장 합니다.|  
|[SaveDeltaToStream 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-savedeltatostream-method.md)|편집 하며 계속 하기는 현재 세션에서 지정 된 스트림에 변경 내용을 저장 합니다.|  
|[SetGenericParamProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-setgenericparamprops-method.md)|지정 된 토큰에서 참조 하는 제네릭 매개 변수 정의 대 한 속성 값을 설정 합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 인터페이스](../../../../docs/framework/unmanaged-api/metadata/metadata-interfaces.md)
- [IMetaDataEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
