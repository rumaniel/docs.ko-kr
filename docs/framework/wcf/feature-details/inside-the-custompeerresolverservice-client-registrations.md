---
title: 'CustomPeerResolverService 내: 클라이언트 등록'
ms.date: 03/30/2017
ms.assetid: 40236953-a916-4236-84a6-928859e1331a
ms.openlocfilehash: 3d1e1c6493da54bc3ae0e74a33985da59382ea52
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64619774"
---
# <a name="inside-the-custompeerresolverservice-client-registrations"></a>CustomPeerResolverService 내: 클라이언트 등록
메시의 각 노드는 `Register` 함수를 통해 해당 엔드포인트 정보를 확인자 서비스에 게시합니다. 확인자 서비스는 이 정보를 등록 레코드로 저장합니다. 이 레코드에는 노드의 고유 식별자(RegistrationID) 및 엔드포인트 정보(PeerNodeAddress)가 포함됩니다.  
  
## <a name="stale-records-and-expiration-time"></a>잘못된 레코드 및 만료 시간  
 노드가 메시를 벗어날 때 `Unregister` 함수를 호출하여 등록 엔트리가 확인자 서비스에 의해 제거되는 것이 이상적이지만 `Unregister`를 호출하기 전에 노드가 종료되거나 액세스 불가능한 상태가 되어 잘못된 등록 레코드가 발생하는 경우도 있습니다.  
  
 확인자 서비스의 잘못된 레코드로 인해 연결에 실패할 수 있습니다. 메시에 연결하려는 노드가 확인자 서비스로부터 잘못된 연결 정보를 받으면 메시에 참가하는 데 시간이 더 오래 걸릴 수 있습니다. 잘못된 레코드는 메모리도 많이 차지합니다. 효율적인 정리 프로세스를 수행하지 않으면 등록 항목을 저장하는 데 사용되는 캐시가 언젠가는 오버플로되어 확인자 서비스에서 충돌을 발생시킬 수 있습니다.  
  
 <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService>는 각 레코드를 만료 시간(DateTime)으로 표시하고 이 정보를 레코드의 일부로 저장합니다. 이 서비스는 만료 시간을 사용하여 잘못된 레코드를 식별합니다. 사용자 지정 구현도 이와 유사하게 작동합니다.  
  
## <a name="refreshinterval-and-cleanupinterval"></a>RefreshInterval 및 CleanupInterval  
 `RefreshInterval`의 <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService> 속성은 서비스의 등록 조회 테이블에 등록 레코드가 유효한 상태로 남아 있는 시간을 정의합니다. 지정된 레코드에 대해 이 속성에 제공된 시간이 지나면 해당 레코드가 잘못된 상태가 되며 삭제되도록 표시됩니다.  
  
 `CleanupInterval`의 <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService> 속성은 잘못된 등록 레코드를 검색하여 삭제하는 빈도를 서비스에 알려 줍니다. `CleanupInterval`은 서비스에 설정된 `RefreshInterval`보다 크거나 같은 시간으로 설정되어야 합니다.  
  
 사용자의 확인자 서비스를 구현하려면 유지 관리 함수를 작성하여 잘못된 등록 레코드를 제거해야 합니다. 다음과 같은 여러 가지 방법으로 이 작업을 수행할 수 있습니다.  
  
- **정기적인 유지 관리**: 정기적으로 이동 하 고 이전 레코드를 삭제 하 여 데이터 저장소를 통해 이동 하도록 타이머를 설정 합니다. <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService>는 이 접근 방식을 사용합니다.  
  
- **수동 삭제**: 적극적으로 정기적으로 오래 된 레코드에 대 한 검색을 하는 대신 식별할 수 있으며 서비스에서 이미 다른 함수를 수행할 때 오래 된 레코드를 삭제할 수 있습니다. 이렇게 하면 확인자 클라이언트가 보낸 요청에 대한 응답 시간이 지연될 수 있지만 타이머를 사용하지 않아도 되므로 `Unregister`를 호출하지 않고 벗어날 것으로 예상되는 노드가 적을 경우 보다 효율적일 수 있습니다.  
  
## <a name="registrationlifetime-and-refresh"></a>RegistrationLifetime 및 Refresh  
 확인자 서비스에 노드가 등록되면 서비스로부터 <xref:System.ServiceModel.PeerResolvers.RegisterResponseInfo> 개체를 받게 됩니다. 이 개체에는 등록이 만료되어 확인자 서비스에 의해 제거되기 전까지 남은 시간을 노드에 알려 주는 `RegistrationLifetime` 속성이 있습니다. 예를 들어, `RegistrationLifetime`이 2분인 경우 노드에서 2분 안에 `Refresh`를 호출해야 레코드가 최신 상태로 유지되어 삭제되지 않습니다. `Refresh` 요청을 받을 경우 확인자 서비스는 레코드를 조회하여 만료 시간을 다시 설정합니다. Refresh는 <xref:System.ServiceModel.PeerResolvers.RefreshResponseInfo> 속성이 지정된 `RegistrationLifetime` 개체를 반환합니다.  
  
## <a name="see-also"></a>참고자료

- [피어 확인자](../../../../docs/framework/wcf/feature-details/peer-resolvers.md)
