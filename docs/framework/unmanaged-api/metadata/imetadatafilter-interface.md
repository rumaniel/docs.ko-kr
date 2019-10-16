---
title: IMetaDataFilter 인터페이스
ms.date: 03/30/2017
api_name:
- IMetaDataFilter
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataFilter
helpviewer_keywords:
- IMetaDataFilter interface [.NET Framework metadata]
ms.assetid: ec0856ef-8c56-40ba-bf60-86e0ce8b337f
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4196ff2cb2d4ebc401076f603a8a7fdc9b9c76ea
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62049962"
---
# <a name="imetadatafilter-interface"></a>IMetaDataFilter 인터페이스
이미 수행된 반복 작업을 방지하려고 메타데이터 토큰을 표시 및 필터링하는 메서드를 제공합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[IsTokenMarked 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadatafilter-istokenmarked-method.md)|지정 된 메타 데이터 토큰 처리 되었는지 여부를 나타내는 값을 가져옵니다.|  
|[MarkToken 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadatafilter-marktoken-method.md)|지정 된 메타 데이터 토큰을 처리 했는지를 나타내는 값을 설정 합니다.|  
|[UnmarkAll 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadatafilter-unmarkall-method.md)|현재 메타 데이터 범위에서 모든 토큰에서 처리 표시를 제거합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 인터페이스](../../../../docs/framework/unmanaged-api/metadata/metadata-interfaces.md)
