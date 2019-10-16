---
title: WCF 구성 스키마
ms.date: 03/30/2017
ms.assetid: c282aeb5-91f0-4522-8e2f-704c1ef3651f
ms.openlocfilehash: 37330b571553bb5e8f17ffad85faafbcaf19d217
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70041282"
---
# <a name="wcf-configuration-schema"></a>WCF 구성 스키마
WCF (Windows Communication Foundation) 구성 요소를 사용 하 여 WCF 서비스와 클라이언트 응용 프로그램을 구성할 수 있습니다. [구성 편집기 도구(SvcConfigEditor.exe)](../../../wcf/configuration-editor-tool-svcconfigeditor-exe.md)를 사용하여 클라이언트 및 서비스에 대한 구성 파일을 만들고 수정할 수 있습니다. 구성 파일은 XML 형식이므로 텍스트 편집기를 사용하여 구성 파일을 수동으로 편집하려면 XML에 익숙해야 합니다. 그렇지 않으면 찾을 수 없는 XML 요소 태그나 특성과 같은 문제가 발생할 수 있습니다. XML 요소 태그 및 속성이 대소문자를 구분하기 때문입니다.  
  
 WCF 구성 시스템은 <xref:System.Configuration> 네임 스페이스를 기반으로 합니다. 따라서 애플리케이션 및 구성의 보안을 향상시키기 위해 구성 잠금, 암호화 및 병합과 같은 <xref:System.Configuration> 네임스페이스에서 제공하는 표준 기능을 모두 사용할 수 있습니다. 이러한 개념에 대한 자세한 내용은 다음 항목을 참조하세요.  
  
 [구성 정보 암호화](https://go.microsoft.com/fwlink/?LinkId=95337)  
  
 [구성 설정 잠금](https://go.microsoft.com/fwlink/?LinkId=95338)  
  
 이 섹션에서는 각 구성 항목의 가능한 모든 값 및 이 값이 다른 WCF 구성 요소와 상호 작용하는 방법에 대해 설명합니다. 다음 맵은 WCF 구성 스키마를 보여 줍니다.  
  
 ![WCF 구성 스키마를 보여 주는 다이어그램입니다.](./media/index/windows-communication-foundation-configuration-schema.gif)  
  
> [!CAUTION]
> 잠재적 보안 위협을 방지 하기 위해 적절 한 ACL (Access Control 목록)을 사용 하 여 응용 프로그램 구성 파일 (app.config)의 WCF 구성 섹션을 보호 해야 합니다.  예를 들어, 적절한 사용자만이 애플리케이션 바인딩의 보안 설정 또는 서비스에 대한 구성 파일의 서비스 모델 섹션에 액세스하거나 이를 수정할 수 있도록 해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [\<system.serviceModel>](system-servicemodel.md)  
 `ServiceModel` 요소에 대해 설명합니다.  
  
 [\<system.serviceModel.activation>](system-servicemodel-activation.md)  
 SMSvcHost.exe 도구를 구성합니다.  
  
 [\<system.runtime.serialization>](system-runtime-serialization.md)  
 <xref:System.Runtime.Serialization.DataContractSerializer>와 같은 serializer를 사용하는 경우 옵션 설정의 최상위 요소입니다.  
  
## <a name="related-sections"></a>관련 단원  
 [Windows Communication Foundation 응용 프로그램 구성](../../../wcf/configuring-services.md)  
 WCF 서비스 및 클라이언트를 구성 하는 방법을 설명 합니다.
