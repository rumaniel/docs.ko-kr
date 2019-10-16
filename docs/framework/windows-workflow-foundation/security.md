---
title: 보안
ms.date: 03/30/2017
ms.assetid: 737ec121-bfc5-4b75-a504-2d53c2c8af39
ms.openlocfilehash: f47b75fa1fd345869f560326861ebc31e6b5e1a9
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045309"
---
# <a name="security"></a>보안
SQL 워크플로 인스턴스 저장소에서는 다음과 같은 데이터베이스 보안 역할을 사용하여 지속성 데이터베이스의 인스턴스 상태 정보에 대한 액세스에 보안을 설정합니다.  
  
- **System.Activities.DurableInstancing.InstanceStoreUsers**. 이 역할에는 공용 뷰에 대한 읽기 및 쓰기 액세스 권한과 인스턴스 생성, 로드 및 저장과 관련된 저장 프로시저에 대한 실행 권한이 있습니다.  
  
- **System.Activities.DurableInstancing.InstanceStoreObservers**. 이 역할에는 공용 뷰에 대한 읽기 전용 액세스 권한이 있습니다.  
  
- **System.Activities.DurableInstancing.WorkflowActivationUsers**. 이 역할은 인스턴스 활성화 프로세스에 포함되는 저장 프로시저에 대한 실행 권한이 있습니다. 인스턴스 활성화에 대 한 자세한 내용은 [인스턴스 활성화](instance-activation.md)를 참조 하십시오. 일반 호스트 (Windows Server AppFabric의 호스팅 기능에 대 한 워크플로 관리 서비스)가 실행 되는 사용자 계정은이 데이터베이스 역할에 추가 되어야 합니다.  
  
 Windows Server 응용 프로그램 패브릭을 사용 하는 지 속성 저장소의 보안에 대 한 자세한 내용은 [App fabric의 지 속성 저장소에 대 한 보안 구성](https://go.microsoft.com/fwlink/?LinkId=201208) 을 참조 하세요.  
  
> [!CAUTION]
> 인스턴스 저장소에 있는 고유 인스턴스 데이터에 대한 액세스 권한을 가진 클라이언트는 동일한 인스턴스 저장소에 있는 모든 다른 인스턴스에 대한 액세스 권한이 있습니다. 인스턴스 저장소는 인스턴스 수준의 보안 권한 지정을 지원하지 않습니다. 다른 저장소에 대한 액세스 권한을 갖도록 하려면 별도의 인스턴스 저장소를 만들고 다른 그룹/사용자를 매핑해야 합니다.
