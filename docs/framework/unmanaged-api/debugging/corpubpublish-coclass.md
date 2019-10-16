---
title: CorpubPublish Coclass
ms.date: 03/30/2017
api_name:
- CorpubPublish Coclass
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorpubPublish
helpviewer_keywords:
- CorpubPublish coclass [.NET Framework debugging]
ms.assetid: 191015da-f54a-4bac-a28a-1de7ab3c3428
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7d1ca8ea9d00de8a07c67977cf108c50268802e6
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67739352"
---
# <a name="corpubpublish-coclass"></a>CorpubPublish Coclass
애플리케이션 도메인 및 프로세스에 대한 정보를 게시하기 위한 인터페이스를 제공합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
coclass CorpubPublish {  
    [default] interface ICorPublish;  
    interface           ICorPublishProcess;  
    interface           ICorPublishAppDomain;  
    interface           ICorPublishProcessEnum;  
    interface           ICorPublishAppDomainEnum;  
};  
```  
  
## <a name="interfaces"></a>인터페이스  
  
|인터페이스|설명|  
|---------------|-----------------|  
|[ICorPublish 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icorpublish-interface.md)|해당 프로세스의 프로세스 및 응용 프로그램 도메인에 대 한 정보를 게시 하기 위한 메서드를 제공 합니다.|  
|[ICorPublishAppDomain 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icorpublishappdomain-interface.md)|를 나타내며 응용 프로그램 도메인을 프로세스에 대 한 정보를 제공 합니다.|  
|[ICorPublishAppDomainEnum 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icorpublishappdomainenum-interface.md)|프로세스 내에서 현재 존재 하는 응용 프로그램 도메인의 컬렉션을 이동 하는 메서드를 제공 합니다.|  
|[ICorPublishProcess 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icorpublishprocess-interface.md)|컴퓨터에서 실행 되는 프로세스를 나타냅니다.|  
|[ICorPublishProcessEnum 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icorpublishprocessenum-interface.md)|컴퓨터에서 실행 중인 프로세스의 컬렉션을 이동 하는 메서드를 제공 합니다.|  
  
## <a name="remarks"></a>설명  
 일반적인 게시 시나리오는 응용 프로그램 도메인 내의 컴퓨터에서 실행 되는 관리 되는 코드를 디버그 하려는 개발자가 포함 됩니다. 호스팅 환경 프로세스 내에서 둘 이상의 응용 프로그램 도메인을 실행할 수 있습니다. 개발자의 모든 컴퓨터에서 실행 되는 프로세스를 나열 하는 그래픽 사용자 인터페이스 또는 다른 수단을 사용 하 고 특정 프로세스를 선택 하려고 합니다. 관리 코드를 실행 하는 프로세스 내의 응용 프로그램 도메인의 모든 목록에 포함 되어야 합니다. 그런 다음 개발자는 특정 응용 프로그램 도메인을 식별 하 고 해당 도메인에 디버거를 연결할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorPub.idl  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET framework 버전:**  [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
