---
title: ICeeGen 인터페이스
ms.date: 03/30/2017
api_name:
- ICeeGen
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICeeGen
helpviewer_keywords:
- ICeeGen interface [.NET Framework metadata]
ms.assetid: 383d20b0-efe9-4e71-8fb8-1186b2e7d0c0
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6fb081c48abf899b44da1c1351efa3f6036f1c8d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62050209"
---
# <a name="iceegen-interface"></a>ICeeGen 인터페이스
동적 코드 컴파일에 대한 메서드를 제공합니다.  
  
 이 인터페이스는 사용 되지 않습니다 및 사용할 수 없습니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[AddSectionReloc 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-addsectionreloc-method.md)|사용되지 않습니다. 코드 베이스.reloc 명령을 추가합니다.|  
|[AllocateMethodBuffer 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-allocatemethodbuffer-method.md)|사용되지 않습니다. 메서드의 경우 지정된 된 크기의 버퍼를 만들고 메서드의 상대 가상 주소를 가져옵니다.|  
|[ComputePointer 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-computepointer-method.md)|사용되지 않습니다. 지정 된 코드 섹션에 대 한 버퍼를 결정합니다.|  
|[EmitString 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-emitstring-method.md)|사용되지 않습니다. 코드 베이스에 지정된 된 문자열을 내보냅니다.|  
|[GenerateCeeFile 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-generateceefile-method.md)|사용되지 않습니다. 이에 현재 로드 된 코드 베이스를 포함 하는 코드 베이스 파일이 생성 `ICeeGen`합니다.|  
|[GenerateCeeMemoryImage 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-generateceememoryimage-method.md)|사용되지 않습니다. 코드 베이스에 대 한 메모리에 이미지를 생성합니다.|  
|[GetIlSection 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-getilsection-method.md)|사용되지 않습니다. 지정된 된 핸들에서 참조 기본 중간 언어 코드의 섹션을 가져옵니다.|  
|[GetIMapTokenIface 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-getimaptokeniface-method.md)|사용되지 않습니다. 지정한 토큰이 참조 되는 인터페이스를 가져옵니다.|  
|[GetMethodBuffer 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-getmethodbuffer-method.md)|사용되지 않습니다. 지정된 된 상대 가상 주소에서 메서드에 대 한 적절 한 크기의 버퍼를 가져옵니다.|  
|[GetSectionBlock 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-getsectionblock-method.md)|사용되지 않습니다. 코드 베이스의 섹션에서는 블록을 가져옵니다.|  
|[GetSectionCreate 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-getsectioncreate-method.md)|사용되지 않습니다. 생성 하 고 지정한 이름 및 플래그 값을 사용 하 여 코드 섹션을 가져옵니다.|  
|[GetSectionDataLen 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-getsectiondatalen-method.md)|사용되지 않습니다. 지정된 된 섹션의 길이 가져옵니다.|  
|[GetString 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-getstring-method.md)|사용되지 않습니다. 지정된 된 상대 가상 주소에 저장 된 문자열을 가져옵니다.|  
|[GetStringSection 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-getstringsection-method.md)|사용되지 않습니다. 지정된 된 핸들에서 참조 하는 코드 섹션의 문자열 표현을 가져옵니다.|  
|[TruncateSection 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-truncatesection-method.md)|사용되지 않습니다. 지정 된 코드 섹션을 지정 된 길이로 자릅니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 인터페이스](../../../../docs/framework/unmanaged-api/metadata/metadata-interfaces.md)
