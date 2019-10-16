---
title: 내 첫 번째 클레임 인식 WCF 서비스 구축
ms.date: 03/30/2017
ms.assetid: e0e6d091-9a97-4888-8f2c-cbcee42d90ee
author: BrucePerlerMS
ms.openlocfilehash: 330d785721cb434f74ec746310a71bfd39fefd0b
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045546"
---
# <a name="building-my-first-claims-aware-wcf-service"></a>내 첫 번째 클레임 인식 WCF 서비스 구축
## <a name="applies-to"></a>적용 대상  
  
- WIF(Windows Identity Foundation)  
  
- WCF(Windows Communication Foundation)  
  
## <a name="overview"></a>개요  
 이 항목에서는 WIF를 사용하여 클레임 인식 WCF 서비스를 빌드하는 시나리오에 대해 간략하게 설명합니다. 일반적으로 클레임 인식 웹 서비스 시나리오에는 웹 서비스, 최종 사용자 및 STS(보안 토큰 서비스)와 같은 세 가지 참가 요소가 있습니다. 다음 그림은 이 시나리오를 보여줍니다.  
  
 ![WIF 기본 클레임 인식 WCF 서비스 구성 요소를 보여 주는 다이어그램입니다.](./media/building-my-first-claims-aware-wcf-service/windows-identify-foundation-basic-claims-aware-windows-communication-foundation-service.gif)  
  
1. WCF 서비스 클라이언트(에이전트라고도 함)는 WIF를 사용하여 STS에 자격 증명을 보내고, 성공적으로 인증되면 STS가 에이전트에 토큰을 발급합니다.  
  
2. 에이전트가 STS에서 발급한 토큰을 WCF 서비스에 보냅니다.  
  
3. 클레임 인식 WCF 서비스는 STS 및 발급되는 토큰을 신뢰하도록 구성됩니다. 클레임 인식 WCF 서비스에서는 WIF를 사용하여 토큰의 유효성을 검사하고 구문 분석합니다. 개발자가 인증 구현과 같이 애플리케이션의 요구에 맞는 적절한 WIF API 및 형식(예: **ClaimsPrincipal**)을 사용합니다.  
  
 .NET 4.5부터 WIF가 .NET Framework 패키지의 일부로 제공됩니다. WIF 클래스를 프레임워크에서 직접 사용할 수 있도록 하면 .NET에 클레임 기반 ID를 더욱 심층적으로 통합하여 클레임을 더욱 쉽게 사용하도록 할 수 있습니다. WIF 4.5를 사용하면 클레임 인식 웹 응용 프로그램 개발을 시작하기 위해 대역 외 구성 요소를 설치할 필요가 없습니다. 현재 WIF 클래스가 다양한 어셈블리에 분산되어 있으며, 주요 클래스는 System.Security.Claims, System.IdentityModel 및 System.IdentityModel.Services입니다.  
  
 STS는 성공적으로 인증되면 토큰을 발급하는 서비스입니다. Microsoft는 다음과 같은 두 가지 업계 표준 STS를 제공합니다.  
  
- [Active Directory Federation Services (AD FS) 2.0](https://go.microsoft.com/fwlink/?LinkID=247516)
  
- [Windows Azure Access Control Service (ACS)](https://docs.microsoft.com/previous-versions/azure/azure-services/hh147631(v=azure.100))
  
 ADFS 2.0은 Windows Server R2에 속하며, 온-프레미스 시나리오의 STS로 사용할 수 있습니다. Azure Active Directory Access Control(Access Control Service 또는 ACS라고도 함)는 Microsoft Azure의 일부로 제공되는 클라우드 서비스입니다. 테스트 또는 교육용으로 클레임 인식 응용 프로그램을 작성하기 위해 다른 STS를 사용할 수도 있습니다. 예를 들어 온라인에서 무료로 제공 되는 [Visual Studio 용 id 및 액세스 도구에](https://go.microsoft.com/fwlink/?LinkID=245849) 포함 된 로컬 개발 STS를 사용할 수 있습니다.  
  
 WIF를 사용 하 여 첫 번째 클레임 인식 WCF 서비스를 빌드하려면 [방법: WCF 웹 서비스 응용 프로그램](how-to-enable-wif-for-a-wcf-web-service-application.md)에 대해 WIF를 사용 하도록 설정 합니다.
  
## <a name="see-also"></a>참고자료

- [WIF 시작](getting-started-with-wif.md)
