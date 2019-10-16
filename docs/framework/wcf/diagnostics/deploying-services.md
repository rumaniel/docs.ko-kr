---
title: 서비스 배포
ms.date: 03/30/2017
ms.assetid: ac361bfb-017d-4da9-a2d7-fc0fb72d65bb
ms.openlocfilehash: 684b781c568518cfb321d8021e4f7062e855e6aa
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798135"
---
# <a name="deploying-services"></a>서비스 배포
이 항목에서는 런타임 환경에 WCF (Windows Communication Foundation) 응용 프로그램을 배포 하는 방법에 대해 설명 합니다.  
  
## <a name="choosing-the-hosting-environment-for-your-application"></a>애플리케이션의 호스팅 환경 선택  
 WCF 서비스는 관리 코드를 지 원하는 모든 Windows 프로세스에서 실행 되도록 설계 되었습니다. 활성화할 서비스는 서비스를 만들고 컨텍스트와 수명을 제어하는 런타임 환경에 호스팅해야 합니다. 호스팅 옵션은 가장 간단한 콘솔 애플리케이션에서 Windows 서비스, IIS(Internet Information Services), 또는 WAS(Windows Activation Service)에서 관리하는 작업자 프로세스 등의 서버 환경까지 다양합니다. WCF 응용 프로그램에 대 한 다양 한 호스팅 옵션을 검토 하려면 [호스팅 서비스](../hosting-services.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [호스팅](../feature-details/hosting.md)
- [서비스 호스팅](../hosting-services.md)
