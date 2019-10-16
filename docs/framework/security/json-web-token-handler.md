---
title: JSON 웹 토큰 처리기
ms.date: 03/30/2017
ms.assetid: 9968f12e-e05d-4e6a-9b65-6896c0e31ab1
ms.openlocfilehash: 3dc76f3de714fd91d397cc240d02a1a8605fe18b
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045325"
---
# <a name="json-web-token-handler"></a>JSON 웹 토큰 처리기
Windows Identity Foundation의 JSON 웹 토큰 처리기 확장을 사용하면 애플리케이션에서 JWT(JSON 웹 토큰)를 만들고 유효성을 검사할 수 있습니다. JWT 토큰 처리기는 다른 내장 보안 토큰 처리기와 같이 WIF 파이프라인에서 실행하도록 구성할 수 있습니다. 그러나 독립적으로 사용하여 경량형 애플리케이션에서 토큰의 유효성 검사를 수행할 수도 있습니다. JWT 토큰 처리기는 Microsoft Azure Active Directory 인증과 같이 OAuth 2.0 전달자 토큰 체계를 사용하는 경우 특히 유용합니다.  
  
 JWT 토큰 처리기는 NuGet 패키지로 사용할 수 있습니다. 자세한 내용은 [JSON Web Token 처리기 패키지 다운로드](downloading-the-json-web-token-handler-package.md)를 참조하세요.  
  
## <a name="scenarios"></a>시나리오  
 JWT 토큰 처리기에서는 다음과 같은 주요 시나리오를 사용할 수 있습니다.  
  
- **서버 응용 프로그램에서 JWT 토큰의 유효성을 검사**합니다. 이 시나리오에서 Litware 라는 회사에는 WIF를 사용 하 여 웹 로그온 요청을 처리 하는 서버 응용 프로그램이 있습니다. Litware를 사용하면 애플리케이션이 인증에 JWT 토큰을 사용할 수 있습니다. 애플리케이션이 JWT 토큰 처리기로 업데이트된 다음 애플리케이션 구성이 WIF 파이프라인에서 JWT 토큰 처리기를 추가하도록 업데이트됩니다. 업데이트되고 새 요청이 WIF 파이프라인을 시작하면 JWT 토큰이 새 처리기를 사용하여 유효성 검사되고 인증이 성공적으로 완료됩니다.  
  
- **REST 웹 서비스에서 JWT 토큰의 유효성을 검사**합니다. 이 시나리오에서 Litware 라는 회사는 Windows Azure Active Directory로 보호 되는 REST 웹 서비스를 포함 합니다. 웹 서비스에 대한 요청은 Microsoft Azure AD의 인증을 받아야 하며, 성공적으로 인증되면 JWT 토큰이 발급됩니다. Litware에는 웹 서비스에 액세스해야 하는 클라이언트 애플리케이션이 있습니다. 클라이언트가 웹 서비스에 대한 요청을 만들고 Microsoft Azure AD의 JWT 토큰을 제공합니다. 그런 다음 웹 서비스에서 JWT 토큰 처리기를 사용하여 해당 토큰의 유효성을 검사합니다. JWT 토큰 처리기가 토큰의 유효성을 검사하면 원하는 리소스가 웹 서비스에 의해 클라이언트로 반환됩니다.  
  
## <a name="features"></a>기능  
 JWT 토큰 처리기의 특징은 다음과 같습니다.  
  
- **JWT 토큰의 유효성을 검사 합니다**. JWT 토큰은 응용 프로그램의 WIF 파이프라인의 일부 또는 WIF에 독립적으로 호출 되는 토큰 처리기의 유효성 검사 논리를 통해 쉽게 유효성을 검사할 수 있습니다.  
  
- **JWT 토큰을 만듭니다**. JWT 토큰 처리기를 사용 하 여 다운스트림 서비스에서 권한 부여에 대 한 JWT 토큰을 만들 수 있습니다.
