---
title: WCF 서비스 호스트 자동 시작 제어
ms.date: 03/30/2017
f1_keywords:
- WcfOptions
ms.assetid: 6abe5d34-519b-4cef-8f02-3c0a7f125585
ms.openlocfilehash: 806d85df2a7fff63704db755400b81cc2dc5c37b
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64652084"
---
# <a name="controlling-auto-launching-of-wcf-service-host"></a>WCF 서비스 호스트 자동 시작 제어
여러 프로젝트가 포함 된 동일한 Visual Studio 솔루션의 다른 프로젝트를 디버깅할 때 WCF 서비스 라이브러리 프로젝트의 경우 Windows Communication Foundation (WCF) 서비스 호스트 (WcfSvcHost.exe)의 자동 시작 기능을 제어할 수 있습니다.  
  
 이렇게 하려면에서 WCF 서비스 프로젝트를 마우스 오른쪽 단추로 **솔루션 탐색기**, 선택 **속성**, 클릭 **WCF 옵션** 탭 합니다. 합니다 **WCF 서비스 호스트 시작 동일한 솔루션의 다른 프로젝트를 디버깅할 때** 확인란은 기본적으로 사용 됩니다. 동일한 솔루션의 다른 프로젝트를 디버깅할 때이 특정 프로젝트에 대 한 WCF 서비스 호스트가 시작 되지 않도록 상자를 지울 수 있습니다.  
  
 이 동작은 F5 키를 사용한 디버깅이나 이 프로젝트의 서비스 참조 추가 기능에는 영향을 주지 않습니다.  
  
 이 옵션은 다음 프로젝트에 사용할 수 있습니다.  
  
- WCF 서비스 라이브러리 프로젝트입니다.  
  
- 순차 워크플로 서비스 라이브러리 프로젝트  
  
- 상태 시스템 워크플로 서비스 라이브러리 프로젝트  
  
- 배포 서비스 라이브러리 프로젝트  
  
## <a name="see-also"></a>참고자료

- [WCF 서비스 호스트(WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)
