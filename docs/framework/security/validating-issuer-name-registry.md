---
title: 발급자 이름 레지스트리 유효성 검사
ms.date: 03/30/2017
ms.assetid: c4644dd1-dead-48ff-abeb-7bffae69a6ac
ms.openlocfilehash: dc7da9d3dc4ab696d8c27d8e12583b8d06e747fe
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045306"
---
# <a name="validating-issuer-name-registry"></a>발급자 이름 레지스트리 유효성 검사
Windows Identity Foundation의 VINR(Validating Issuer Name Registry)을 사용하면 다중 테넌트 애플리케이션에서 들어오는 토큰이 신뢰할 수 있는 테넌트 및 ID 공급자에 의해 발급되었는지 확인할 수 있습니다. 이 기능은 Microsoft Azure Active Directory에서 발급한 모든 토큰이 동일한 인증서를 사용하여 서명되므로 Microsoft Azure AD를 사용하는 다중 테넌트 애플리케이션에 특히 유용합니다. 동일한 인증서를 사용함에 따라 동일한 지문을 보유하는 여러 테넌트의 요청을 구분하기 위해 애플리케이션이 유효성 검사 논리를 수행하려면 각 테넌트에 대한 발급자 이름을 유지해야 합니다. VINR은 이러한 기능을 제공하며, 이를 통해 사용자가 사용자 지정 유효성 검사 논리를 추가하거나 발급자 레지스트리 데이터를 구성 파일 이외의 위치에 저장할 수 있습니다. 확장은 애플리케이션의 WIF 파이프라인에 추가하거나 독립적으로 사용할 수 없습니다.  
  
 VINR은 NuGet 패키지로 사용할 수 있습니다. 자세한 내용은 [발급자 이름 레지스트리 유효성 검사 패키지 다운로드](downloading-the-validating-issuer-name-registry-package.md)를 참조하세요.  
  
## <a name="scenarios"></a>시나리오  
 VINR을 통해 다음과 같은 주요 시나리오를 사용할 수 있습니다.  
  
- **다중 테 넌 트 응용 프로그램에서 토큰의 유효성을 검사 합니다**. 이 시나리오에서 Litware 라는 회사는 Windows Azure AD와 같은 id 공급자를 사용 하는 다중 테 넌 트 응용 프로그램을 개발 했습니다. 이 응용 프로그램은 두 고객을 제공 합니다. Contoso와 Fabrikam. Fabrikam의 사용자가 Litware의 애플리케이션을 인증하는 경우 Microsoft Azure AD에서 생성되는 토큰은 표준 인증서를 통해 서명되며 요청은 Fabrikam에 의해 발급됩니다. 애플리케이션은 발급자 이름과 토큰이 모두 유효한지 확인해야 하며, Microsoft Azure AD의 동일한 인증서를 사용하여 서명되는 Contoso의 요청을 구분해야 합니다. VINR을 통해 Litware의 애플리케이션에서 Contoso 및 Fabrikam과 같은 여러 테넌트의 요청을 쉽게 구분하고 유효성을 검사할 수 있습니다.  
  
## <a name="features"></a>기능  
 VINR의 특징은 다음과 같습니다.  
  
- **다중 테 넌 트 응용 프로그램에 대 한 발급자 이름 및 토큰 유효성 검사**: 발급자 이름 (테 넌 트) 및 토큰이 id 공급자의 유효한 인증서를 사용 하 여 서명 되었는지 여부를 확인 하 여 들어오는 토큰의 유효성을 검사 합니다.  
  
- **사용자 지정 유효성 검사 논리 및 데이터 저장소에 대 한 확장성**: 사용자 고유의 유효성 검사 논리를 삽입 하 고 기본 구성 파일 이외의 데이터 저장소를 지정 하는 확장성을 제공 합니다.
